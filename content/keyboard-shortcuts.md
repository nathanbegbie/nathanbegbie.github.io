Title: Stop Teaching People Git
Date: 2025-04-28 11:00
Category: Complaining With Authority

I used to love the idea of keyboard shortcuts in applications.
Now I'm not so sure.

These reflections began after a forgetful moment, I recently found myself without my mouse.
I also use a laptop stand to combat my gradual evolution morphing of my spine in to a C.
Thus my trackpad is elevated up and away from my hands.
So faced with my trackpad now being super awkward to use, I was faced with a choice.
I could briefly put my laptop down on the desk and use it like pretty much everyone else.
Or, _or_ I could simply stop using a mouse and like the ultra-elite hack3rs of yore, use my keyboard for everything.
I would move through the digital realms with absolute speed and precision.

Here's the problem with this approach.
It sucks.
When you try and tack on a keyboard-only approach for _everything_, you become acutely aware of just how much we rely on a mouse as the default tool for intuitively interacting with a myriad of things.
The thing is there.
I move the mouse to the thing.
I click.
Interaction.

But the keyboard is different.
It requires knowledge ahead of time about how what you do on the keyboard in order to interact with an interface.

And this is _much_ harder to get right, both from a design perspective and what you, as a user, are required to do.
Now at the risk of sounding like a twat, this experience has given me a slim insight in to what it might feel like to have some sort of restriction when interacting with interfaces built for the majority, and other interactions as an afterthought, or add-on.
I'm (probably) not mentioning this in order to up my creds, but instead, just to just mention an appreciation.
Folks who think about accessibility and properly give interfaces a think, benefit the rest of us.
So on the off chance that someone who does this work actually reads this - thanks.

Have you tried switching between Jupyter notebooks and Elixir livebooks?
Good luck.
There are other ways that you can

Here's a rule of thumb I think I could possibly profer to the universe in exchange for letting me whine about my tiny problems for 200 words.
(I retain the right to update this if upon relfection this feels less wise in 2 weeks time.)

If you're not going to be in the top 5 most used applications for a user, then you probably shouldn't bother coming up with keyboard shortcuts.
If you have a slim margin of power users who pester you for a keyboard interface (_sideye at the Vim community_), maybe make that optional.

### Keyboard shortcuts that make sense to support

`cmd - F`: Let me search. (Once those search options come up, let me use my fucking keyboard to interact with the results). However, if you're a developer, then messing with cmd-f means that you override the built-in functionality to find text anywhere on the page, which is provided by the browser. So if you're not working in-browser, I think
`cmd - enter/return`: we're in slightly shakier ground here - in some cases this puts you on a newline, and in other cases is submit. Please folks, let's sort this out and just do the same thing?
`shift - enter`: same as above.
`cmd - k`: you can do lots of things. But then this often clashes with the code editor convention of `cmd+shift+p`
...

### Machine Keyboard conventions:

For my sins, I have been a mac user for the past 13 years.
In that time, the ways to navigate text have become second nature.
Part of the reason for this is that this _always_ works.

`cmd - ←`: Go to the start of the line
`cmd - →`: Go to the end of the line
`cmd - ↑`: Go to the top of the page
`cmd - ↓`: Go to the bottom of the page

I think my main gripe here is that when you're thinking about power users, and you start to design for them, if the "speedsups" for them start to bleed over to your average user, then you've gone too far and you need to dial it back.
Please remember that _if you are the designer of the thing, then you are not the average or median user_.


I think it's probably also worth thinking about how long a user would spend in your interface, not in total, but the duration of times that a user spends in your application.
In other words, if I'm constantly dropping in your app and then spiriting myself away again to do something else, then the

Scrolling. Please. Just give me a way to scroll with my keyboard.

This is perhaps one reason why I am levitating away from native apps and instead back to web-apps of various apps.
Browser apps like vimium give me a consistent way to navigate around various interfaces.
Default apps vary wildly in their consistency with navigating with a keyboard.


You might be thinking, but ArtificiallyInteligent, you just don't have the right _setup_.
And you might be right, _if_ you're not taking in to account the time it takes to get used to that setup.
I have not switched to vim for that very reason, but it is the one convention that seems to have made it's way to other tools, so if I do end up going deeper down the rabbit hole, this is the most likely path.

## Keyboard interactions that I just want to whinge about
In the Spotify app, when you want to search for a song (and that's the only thing that you'd want _can_ do in the search bar) - then you don't go cmd+f, you have to do cmd+k
In apps like Slack and Linear, this activates the command bar, where you  can do a number of actions.
However, because the _only_ thing you're doing is searching, why would you let them do anything else?
