Title: Stop Teaching People Git
Date: 2025-01-12 22:30
Category: Data Science

A lot of people use Git. I'm not really sure how this happened, but it seems as though, as soon as we wanted to start *really* coding, someone, perhaps a teacher, colleague or YouTuber, told us that we needed to use Git to get our code places. So we did. Somehow, we're suddenly all fumbling around with the command line and blundering our way through these weird commands, until we're *just* good enough to do what needs to be done. As always, this has been captured with excellent wit by [XKCD](https://xkcd.com/1597/).

So why stop teaching people Git? That was clickbait. Thank you for reading the first paragraph. I want more people using Git, not fewer. But I really do think that Git:

* Has a pretty poor user experience
* Is really hard to teach when the starting point is the command line and some really bizarre commands

I also think that if you want people to use Git, don't start by teaching them the tool itself. Instead, I've found it far more effective to first teach them to collaborate, using the GitHub web UI. It's an approach that I've found quite effective in introducing Git to people. It really simplifies and streamlines things by:

* Teaching them that what they're really doing is collaborating
* Avoiding dumping too many things on them at once like the command line

One of the hardest things to sell with Git is *why* it's important. Because if your user is fairly new to coding, they'll be asking themselves why this experience isn't more like a Google doc, where updates are shared instantaneously. You need to sell them on the concepts quickly, get a little bit of buy-in and hopefully make it fun. Then hit them with the 'okay so now we need to start doing this on *your* computer' and they'll at least have a smidgen of an idea of why that might be important. This should fortify them for the inevitable slip-ups on the command line and the realization that in Git, there is no undo button, there is only wailing and gnashing of teeth.

## Brief Outline for Introducing Folks to Version Control

1. Make a new organisation on Github. Call it whatever you want, just make it low-risk should something go wrong.

2. Ask everyone to make an account on Github. If they already have an account on Github, you can also get them to add their work email address to Github.

3. Invite everyone to your new organisation.

4. Create a new repository, explain to them that this is akin to a project. In this case, we're not going to worry about code - remember that your users might be new to coding, or that unless your group is coding in only one language, then you risk introducing more complication than you need in your explanation. Everyone understands a text file though, or at least, that there is some sort of dumbed down version of a word document out there. Tell them that you're all collaborating on a book which you'll start off describing in the readme.txt file in your repository.

5. Using the concepts of a Commit, make a change to the readme within Github. It's super easy to do - click the edit file on the right hand side of the readme. Then create the change, message and commit directly to the master branch, all on Github. Then show everyone the 2 commits and how the change you made is highlighted in green.

6. Have everyone browse to the repository and click the "Edit" button on the README file themselves. Get them to add a line about what kind of book they think this should be. This introduces the concept of multiple people working on the same file.

7. When they try to commit their changes, some will likely get an error because someone else made a change first. This is perfect - it naturally introduces the concept of conflicts and why we need version control. Then walk them through "resolving a conflict" by just editing the file to reflect what consolidating those 2 viewpoints should look like.

8. Create a simple "Chapter 1" file in the repository. Show them how to create a new file using the "Add file" button. This introduces the concept that repositories can contain multiple files, all with their own history.

9. Introduce branches by having everyone create their own branch, make changes, and then see that these don't affect anyone else.

10. Show them Pull Requests by having one person create a pull request in the GitHub UI and then requesting the review of someone else. WAlk them through the review and finally, merging. Do it again with someone else's branch to demonstrate the process of dealing with new changes.

11. Then leave it there. You've introduced enough core concepts that need digesting, but you've demonstrated the high level process.

Only after they're comfortable with these concepts and can see the value in version control, introduce the idea of working on these files locally - and there are already a ton of tutorials that take folks through that process. But now you've hooked them on the why - and possibly made conflicts a bit less terrifying.
