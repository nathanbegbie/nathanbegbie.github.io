Title: Searching Files that are part of a Pull Request
Date: 2021-11-09 14:40
Category: Data Science

> In this article, I'll combine a couple of helpful command line tools together. If you're not familiar with these tools, I have included the necessary links to help you get started. This is also specific to a unix environment - apologies to Windows users.

Being able to use some command line tools can give us superpowers when it comes to quickly finding relevant material.
Today I wanted to search only the files that had been changed within a particular pull request.
If you're using the web tool, you can simply open the pull request `/files` tab and `cmd/ctrl + f` to find the code you're looking for.
However, if you want to do this from the command line, it gets a bit more complicated.

-   Git does not inherently 'know' what a pull request is, it's something that Github manages
-   There doesn't seem to be an easy way to convert a branch name to a pull request number
-   Shell commands. They get messy.

I'll slowly build up and explain the command that I eventually ended up with.

## Get a Pull Request ID from a branch name

Firstly, we're on a specific branch. To get the name of that branch we run:

```shell
> git branch --show-current
reconfigure-styles
```

Then we need to link the branch name to the pull request.
To get this information, we use the [`gh command line tool`](https://cli.github.com/) from Github.

```shell
> gh pr list
```

This will launch an interactive shell that you will need to hit `q` to exit.
It looks something like this:

```shell
#1  Ensure Blog Publishes Correctly                         ensure-blog-publishes-correctly
#5  Reconfigure styles of Blog                              reconfigure-styles
```

If you want the output to appear directly on the command line, we can pipe the results of the `cat` command like so:

```shell
> gh pr list | cat
1  Ensure Blog Publishes Correctly                         ensure-blog-publishes-correctly
5  Reconfigure styles of Blog                              reconfigure-styles
```

Great! So how do combine these bits of information together?
We can use grep to filter the results using the current branch name:

```shell
> gh pr list | grep $(git branch --show-current)
5  Reconfigure styles of Blog                              reconfigure-styles
```

Woohoo! But when we use `gh` it expects that we use _just_ the PR number.
To get this, we reach for the handy tool `awk`.
`awk` is great for working with tabular data.
It allows us to concisely request a specific column of data with `awk '{print $NUMBER_OF_COLUMN_WE_WANT}'`.
In this case, we want the first column.

```shell
> gh pr list | grep $(git branch --show-current) | awk '{print $1}'
5
```

## Getting File Names from a Pull Request Number

So now we have the current PR number from the branch we currently have checked out.
Next, we want to get all of the files that were changed within a particular PR.
In this case, we can use `gh` in combination with a tool called `jq` to get all of the file names.
I found [this answer on StackOverflow](https://stackoverflow.com/a/68682405/3623641) immensely helpful and will attempt to break down what it suggests:

```shell
> gh pr view 5 --json files --jq '.files.[].path'
```

`gh pr view 2615` just gives us details about the pull request in the command line.
But here we want to be more specific about the information we want back.
So we request a JSON response with details about the `files` in the pull request.
Hence the `--json files`.
(I also pipe to `cat` here to avoid the interactive shell)

```shell
> gh pr view 5 --json files | cat
{
  "files": [
    {
      "path": "styles/index.css",
      "additions": 110,
      "deletions": 0
    },
    {
      "path": "docs/style_guide.md",
      "additions": 22,
      "deletions": 5
    },
    {
      "path": "README.md",
      "additions": 1,
      "deletions": 0
    },
    {
      "path": "index.html",
      "additions": 55,
      "deletions": 3
    }
  ]
}
```

Finally, because we don't want to deal with a whole JSON blob we use the [`jq`](https://stedolan.github.io/jq/) flag which reference [a very nifty tool](https://stedolan.github.io/jq/tutorial/) that helps us get information from JSON with very concise expressions.
So by adding `--jq '.files.[].path'` we can extract all the paths in each JSON blob.

This leaves us with:

```shell
> gh pr view 5 --json files --jq '.files.[].path'
styles/index.css
docs/style_guide.md
README.md
index.html
```

We can then pipe these file names in to a tool like grep.
But we need to combine our first two commands together.
There are a few ways that we can do this, but I've chosen this way becaue I find that variable names help future me understand what the heck I was trying to do.
To be completely honest, there may be a better/safer/more performant way - I'm sure someone can send me an angry email correcting me.

```shell
> PR_NUMBER=$(gh pr list | grep $(git branch --show-current) | awk '{print $1}') && \
    gh pr view $PR_NUMBER --json files --jq '.files.[].path' | cat
styles/index.css
docs/style_guide.md
README.md
index.html
```

## Actually searching

We're almost there!
Finally, we will embed the file names within the git grep command.
We can pass each file name to `grep` using `xargs`:

```shell
> PR_NUMBER=$(gh pr list | grep $(git branch --show-current) | awk '{print $1}') && \
    gh pr view $PR_NUMBER --json files --jq '.files.[].path' | xargs grep #00FF00
styles/index.css:      background-color: #00FF00;
styles/index.css:      color: #00FF00;
styles/index.css:      background-color: #00FF00;
styles/index.css:      <tagname style="color:#00FF00;">
```

And there we have it!

## Some Final Thoughts

I hope that this has deomnstrated how we can combine a couple of simple tools together to quickly accomplish what we want.
There are some caveats though.
This script is not robust to failure and follows what we call the 'happy path'.
This means that if I'm in the wrong directory, or in a branch that doesn't have a pull request associated with it, the code breaks and I won't be explicitly told where or why.
That's okay, because I don't expect anyone else to use this code in a production setting.
If there were some more complicated logic flows, you might want to use a scripting language other than bash.
This comes with tradeoffs though so think it through - would you trade off the 'it should run in most shells' for 'it clearly communciates why something is wrong'?

Remeber, command line tools are really nifty and useful to combine, so use liberally to solve your specific use case.
Just do not expect that everyone will understand or love your weird and wonderful code concoctions as much as you do. 😉
