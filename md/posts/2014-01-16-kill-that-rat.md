{:title "Kill that rat!"
 :layout :post
 :tags  []
 :toc true}

I have been using [Linux](http://www.linux.org/) for atleast the last 9 years, trying out different distributions like [RedHat](http://www.redhat.com/), [Fedora](http://fedoraproject.org/), [Debian](http://www.debian.org/), [Ubuntu](http://www.ubuntu.com/), [Gentoo](http://www.gentoo.org/) and finally settling down on [Sabayon](http://www.sabayon.org/) (for the last 2 years). Similarly, on the desktop manager side, I have used [KDE](http://kde.org/) for a long long time, but have been using [Stumpwm](http://www.nongnu.org/stumpwm/) for the last 3+ years. On the browser front, I use the awesome [vimperator](http://www.vimperator.org/) plugin for [firefox](http://www.mozilla.org/en-US/).

You might think, and correctly at that, "what is this guy talking about? what has all this to do with a rat, or even with productivity (if you read the description of this article on one of the Golbin! index pages)". Well, let me start with the following definition:

> mouse, n: A device for pointing at the xterm in which you want to type. --A.S.R.

If you don't get the above, I am basically talking about the PC "mouse". I feel that the mouse is only there to slow you down. Based on my personal experience, I can say very confidently that the less mouse I use, the faster I work. Agreed, that it takes a bit of practice, and maybe making some (initially difficult) choices too, but in the long term you will be a completely different person. Notice, that I don't say "a more productive person", but a "completely different person". That is because, using the keyboard changes you in more than 1 ways.

Of course your typing speed will increase, which will make regular things (coding, typing emails, blogging, etc) faster. This alone will help you think faster, because our system throughput is limited by the I/O (typing). Even though we are capable of thinking faster, we end up thinking slowly because our typing puts pauses to our thinking, breaking the flow.

Also, more importantly, your choice of tools/systems will change too. For example, I use the following tools/systems:

Linux: I am a software developer, and strongly believe that every software developer should use a Linux desktop to:

* learn something more than clicking "next, next, next, finish" :p
* getting hands dirty on the terminal. That itself will teach you so many tools (find, grep, etc) and techniques (regular expressions, bash scripting, etc) to make you a better developer
* huge number choice of desktop managers (among other things)

**Stumpwm**: I always liked KDE better than [Gnome](http://www.gnome.org/), simply because KDE allowed a _lot_ more keyboard customization than gnome (about 5-9 years ago). But in my search for a mouseless [DWM](http://en.wikipedia.org/wiki/Desktop_Window_Manager) (desktop window manager), I stumbled upon [Ratpoison](http://www.nongnu.org/ratpoison/), [wmii](http://en.wikipedia.org/wiki/Wmii) and Stumpwm. At that time, one of my colleagues was using wmii and showed it to me and I was impressed. However, since Stumpwm is written in common-lisp, and I was trying to learn it at that time, I tried using it, and have never looked back. Stumpwm is a [tiling window manager](http://en.wikipedia.org/wiki/Tiling_window_manager) (unlike KDE, gnome, etc which are [stacking window managers](http://en.wikipedia.org/wiki/Stacking_window_manager)). It allows me to have absolute control of where and how to place my windows, and all that without touching the mouse. But the feature I like the most in Stumpwm is to be able to bind keyboard shortcuts to applications (switch to a certain app, or start it if it's not already running and then switch to it). Agreed that recently KDE (and other DWMs) support this functionality, but they did not about 4+ years ago. And, just using this feature made me so much more productive, and gave me a adrenaline rush that I have never bothered looking at DWM advancements since; I have achieved DWM nirvana ;)

**Vim and Emacs**: I had been a (pure) [vim](http://www.vim.org/) guy for almost 5 years, when I switched to Emacs. The move was motivated largely because of common-lisp ([emacs](http://www.gnu.org/software/emacs/) + [slime](http://common-lisp.net/project/slime/) is the best way to code in common-lisp) and the uber awesome [org-mode](http://orgmode.org/) (which I use for note taking, reminders, organization, planning and almost everything). To some people, these might be simply editors, but people who use them know that they will change the way you think and do things. If you are a developer, you should definitely use them!

**Vimperator**: Being a web developer, browser is my "the" tool. I tend to use both [Chrome](http://www.google.com/chrome/) ([chromium](http://www.chromium.org/)) and firefox during development. But for development I simply cannot do without the firefox+vimperator setup because browsing is such an easy (nay, great!) experience. Not only do i not need to move my hands (from the keyboard) to open links (in same or background tabs), but I can even do cool stuff like record a macro and play it back over and over again. This makes automated testing super easy!

As Eric Raymond said in "How to Become a Hacker"

> Lisp is worth learning for the profound enlightenment experience you will have when you finally get it; that experience will make you a better programmer for the rest of your days, even if you never actually use Lisp itself a lot.

Similarly, going mouse-less is an enlightening way to learn something that will open the door to a wonderful new world. And if you will believe me, let me tell you, the grass is certainly greener on this side of the wall :)
