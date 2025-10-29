# Interactive Computing without Notebook Hell

Remember when Jupyter notebooks promised [Literate Programming](https://en.wikipedia.org/wiki/Literate_programming) heaven?
After about 10 years of using notebook editing environments in various forms, I've moved back to using an editor and taken the good stuff with me.
No more JSON diff hellscapes for me.
The idea that we can colocate our ideas, code and outputs together, particularly for scientific computing, has enormous appeal.
However, as I and many others have noted, this sort of environment begins to grate against one's nerves after extended use.
I'll discuss a few that I've found frustrating and how I've moved to an environment that solves some of these issues (TLDR: just use your code editor if it's good enough).

*Who this is for*: Solo developers and researchers who prioritize editor experience and version control over notebook features. If you're on a data science team that heavily uses notebooks in a browser, this may not fit your workflow. Or read this anyway and be challenged.

## Challenges with Notebooks in the Browser

1. My fingers don't remember your setup - If you _just_ spend your time working in notebooks, you can very rapidly get to grips with the shortcuts and how to run your code etc.
However, if you code in any other language or on a codebase, you'll inevitably find yourself switching between environments and having to manage different ways of doing things.
If there's one thing coders and developers seem to care about more than the air they breathe, it's the editor they use and the editing experience they desire.
Moving away from that, or attempting to bring Jupyter and other editing environments in line with this approach seems foolhardy.
1. How you want me to use LLMs is not how I want to use LLMs - wanting to quickly get LLM-corrected code is what first set me down this path. Inital attempts to shoehorn LLMs in to the notebook environment were _horrific_. I just want to highlight code in a cell and have an LLM weigh in on it. Don't make me install another package, don't make me have LLM responses as cell output, don't give me a chat window on the side with no way to reference the code that I'm working on. In short, don't make me suffer.
1. Python has made Installing and managing packages complicated enough - managing and pinning dependencies with a notebook and the relevant kernel is obscured.
In particular, it introduces another thing that has to be managed.
As great tools like `uv` begin to lead us to a brighter tomorrow, then just using the one thing is a better approach overall. No thank you conda.
1. Sharing notebooks is a terrible user experience - you can use version control, but the mess of JSON means that actually reviewing those changes in a pull request is cursory at best. It's one of the things that I really like when using [RMarkdown](https://rmarkdown.rstudio.com/).
Again, using packages to provide better experiences tend to increase overall complexity and setup, rather than streamline the process.
1. The path to production is unclear - arguably, this is not what notebooks are inherently for and trying to shoehorn them for this purpose is perhaps not the best route in the first place. However, it is still a necessary process in order for those in data science teams to meaningfully contribute and add value to an organisation. Newer tools like [Marimo](https://marimo.io/) have reverted to having an underlying `.py` file.

## Solving Most of My Problems by Just Moving Back to the Editor

I'm not saying that I have the ultimate solution, but I have found myself moving to an environment that better fits my workflow.
Many editors, seeing the popularity of notebooks, have incorporated an interactive environment within them.
VS Code solved this by just shoving the whole Jupyter notebook environment in to the browser itself.
So while you don't have to switch between a browser and your editor, you still keep most the issues I encountered with using Jupyter notebooks.
Other editors (like NeoVim and [Zed](https://zed.dev/docs/repl)) simply exposed a REPL that can push the output back in to your editor, giving you an interactive computing environment alongside your code.
I've found this to be a much more comfortable solution to my workflows.
A developer's editor is the thing that they use most and are most comfortable with.
Keeping the experience of this sort of computing without ejecting them from it has been the pivotal part of improving my notebook experience.

My setup is as follows:

1. I use the Zed editor, which provides a [REPL](https://zed.dev/docs/repl) within a standard `.py` file - cells are denoted by `# %%` and you can run the cells in-line.
1. I use `uv` to manage the python version and virtual environment.
1. Wrap up the process of installation in an executable bash script - shared at the end of the article.
1. Leverage Zed's built-in A.I. features like [inline assistant](https://zed.dev/docs/ai/inline-assistant) for quick one-off fixes, the chat sidebar in order to not break out of my environment to switch to a different LLM driven chat. I've found this particularly useful when I'm running a self-hosted model.

## How This Makes Me Less Curmudgeonly

I've really appreciated this approach for the following reasons:

* I use the text editing experience I'm used to, with minimal mental overhead when accessing files, documents or just using the shortcuts that I already know.
* I can use the built-in A.I. features that Zed provides. Inline commenting, or the sidebar means that I'm able to reduce context switching and remain in a state of flow.
* Version control makes sense again - progress can be delineated in to diffs that make sense instead of enormous globs of JSON. Praise be.
* If I want to move from a more exploratory phase to a more production-ised version of my code, I can do so with relative ease - "breaking down" a file from an exploratory notebook to classes and methods, with unit tests to solidify the expected behaviour of my code.

## Drawbacks

It's not perfect.

My main gripe is that the REPL output in Zed is not directly interactive and limited in size.

1. If you want to copy the output you can only copy the entire output.
1. If you want to play around with the entire output, you have to open another tab.
1. Zed limits the size of the output to a much smaller output than you get in a Jupyter notebook.
1. Despite configuring the Jupyter environment in the editor config, I often have to manually refresh and select the relevant kernel.

However, these are small to medium nitpicks that don't break my workflow too often. I do hope that Zed improved this though.

## Conclusion (#WorksForMe)

I get that my solution is fairly individualistic.
It won't work for larger teams unless everyone agrees on an entirely new way of doing things, which is often more pain than just sticking with Notebooks.
But this is my current setup and it works for me.
It reduces friction from idea to executing code and conducting exploratory analysis.
If you're struggling with notebooks and a browser-based editing experience, give it a shot.

## Addendum

Below is the script that I currently use to setup a new project with all the bells and whistles ready to go.

In short, it achieves the following:

1. Set up the directory with uv and version control
1. Set up the virtual environment including iPython and some optional packages that I use often
1. Set up the relevant kernel
1. Set up the relevant config so that Zed references the correct computing environment

```sh
#!/bin/bash
set -e

# Usage example:
# slugify "Hello World! (Special Characters)"
# Output: hello_world_special_characters
slugify() {
    echo "$1" | \
        iconv -t ascii//TRANSLIT | \
        sed -E 's/[^a-zA-Z0-9]+/_/g' | \
        sed -E 's/^_+|_+$//g' | \
        tr '[:upper:]' '[:lower:]'
}


# zed "$DIRECTORY_NAME"

# Get the directory name from first argument
DIRECTORY_NAME="$1"

if [ -z "$DIRECTORY_NAME" ]; then
    echo "Usage: $0 <directory_name>" >&2
    exit 1
fi

# Get current directory
CURRENT_DIR="$(pwd)"
DEFAULT_PATH="${CURRENT_DIR}/${DIRECTORY_NAME}"

# Ask user about location
read -e -r -p "Create in current directory ($DEFAULT_PATH)? Press Enter to accept, or type a different path: " custom_path

# Use default if empty, otherwise use custom path
if [ -n "$custom_path" ]; then
    while [ ! -d "$custom_path" ]; do
        echo "Invalid path: $custom_path. Please enter an existing directory."
        read -r -p "Create in current directory ($DEFAULT_PATH)? Press Enter to accept, or type a different path: " custom_path
    done
fi

FINAL_PATH="${custom_path:+"${custom_path%/}/$DIRECTORY_NAME"}"
FINAL_PATH="${FINAL_PATH:-"$DEFAULT_PATH"}"

# Create directory
echo "Creating directory at: $FINAL_PATH"
if mkdir -p "$FINAL_PATH"; then
    (
        cd "$FINAL_PATH" || exit 1
        # Your commands here
        echo "Successfully created and moved to $FINAL_PATH"

        # Call uv init with the directory name
        uv init --vcs git --name "$DIRECTORY_NAME" .
        if [ $? -eq 0 ]; then
            echo "Directory '$DIRECTORY_NAME' initialized successfully."
        else
            echo "Failed to initialize directory '$DIRECTORY_NAME'."
        fi

        uv --project "$DIRECTORY_NAME" venv

        echo '[tool.pyright]
venvPath = "."
venv = ".venv"' >> "pyproject.toml"


        uv --project "$DIRECTORY_NAME" add ipykernel python-dotenv

        read -r -p "Do you want to install requests? (Y/n) " install_requests
        [[ $install_requests =~ ^[Yy]$ || $install_requests == "" ]] && {
            uv --project "$DIRECTORY_NAME" add requests
        }

        read -r -p "Do you want to install pandas? (Y/n) " install_pandas
        [[ $install_pandas =~ ^[Yy]$ || $install_pandas == "" ]] && {
            uv --project "$DIRECTORY_NAME" add pandas
        }

        KERNEL_NAME=$(slugify "$DIRECTORY_NAME")

        if uv --project "$DIRECTORY_NAME" run ipython kernel install --user --name "$KERNEL_NAME" --display-name "$DIRECTORY_NAME"; then
            echo "Kernel installed with name:'$KERNEL_NAME' and display name:'$DIRECTORY_NAME'"
        else
            echo "Failed to install Kernel with name:'$KERNEL_NAME' and display name:'$DIRECTORY_NAME'"
        fi

        # Set up local project settings for zed
        # Set the kernel you just created as the default for Python
        mkdir ".zed"
        echo '{
  "jupyter": {
    "kernel_selections": {
      "python": "'"$KERNEL_NAME"'"
    }
  }
}' > ".zed/settings.json"

        # set up a .gitignore file using Github's default
        curl https://raw.githubusercontent.com/github/gitignore/refs/heads/main/Python.gitignore > ".gitignore"

        # now we do some set up for our directory
        rm "hello.py" || true
        mkdir -p "analysis"

        echo '# %% Setup
import os
from dotenv import load_dotenv

load_dotenv()
TOKEN = os.getenv("TOKEN")' > "analysis/main.py"

        mkdir -p "data/raw"
        mkdir "data/processed"
        echo "TOKEN=\"\"" > ".env"

        # create a new workspace in zed
        zed --new "."
        # open in the relevant file
        zed "analysis/main.py:1:1"
    )
else
    echo "Failed to create directory: $FINAL_PATH" >&2
    exit 1
fi
```
