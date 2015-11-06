{:title "Vimperator: part - 2"
 :layout :post
 :tags  []
 :toc true}

Hello there. Welcome back! I hope you have already read my first post on vimperator [here](http://www.golb.in/vimperator-30.html), if not, I urge you to read that first and then come back here. Go on, I'll wait :)

Today I will show you some advanced, but even more awesome features of vimperator -- the tool that takes web browsing to another level! The first is "modes". If you have used the fantastic [vim](http://www.vim.org/) editor before, you will know what I am talking about; and you will feel very much at home with vimperator (in fact, I am sure you would have guessed that the name "vimperator" stems from "vim"). For those of you who have not used vim, worry not; that is why I am here, to help you out :)

Anyways, so vimperator has different modes of operation. The most commonly used are the "insert" and the "normal" modes. The "insert" mode is where the focus is inside some inputbox or textarea of a form (for example when you are filling up the username/password in a login form, or even when you are typing inside the search box on some website). In this mode your keyboard shortcuts like h, j, k, l, etc (see my previous post [here](http://www.golb.in/vimperator-30.html) for details) will NOT work. Instead whatever you type on the keyboard will get filled in the box.

As against this, the "normal" mode is where you really use the keyboard shortcuts to navigate on the page, or between tabs, etc. The easiest way to go from "normal" mode to "input" mode is

* either press "f", and select the number corresponding to the input box you want to type into
* or click with mouse inside the input box
* or press "gi" to go to the first (or last visited) input box

Similarly, to go from "input" mode to "normal" mode is

* either left-click your mouse anywhere on the page (except inside an input box)
* press the "Esc" key on your keyboard

The next feature, which is my favorite, that I am going to show you is "macros". Again, if you have used a real editor (vim and/or emacs), then you know what editor macros are. Basically they are a recorded set of commands that you can repeat with just 1 key press. Understanding macros can make your life super simple! So lets say you want to repeat a set of tasks a few number of times; for example, you want to register 10 accounts on a website that you are developing/testing. Also lets say, for the sake of this discussion, that the registration page is quite long (has say 20 fields). However, for the testing accounts you would want to only have the username to be different (something like "test1", "test2", "test3", and so on), and all other fields to be the same. Lets also assume filling 1 form takes about 2 minutes -- that is 20 minutes for 10 accounts. So how do we do the same task in like 2.5 mins; or maybe 20 accounts in 3 mins?

The first thing you do, obviously, is to open the page ;). Now, before you start filling the form, press 'qa'. The key 'q' will start the recording and save it in a buffer 'a'. You should now see the word 

> Recording

 in your status bar. Then you fill up the form content. After finishing, press the 'q' key again, and the whole sequence (including form content) will be saved into the 'a' buffer. You should now see a message in the status bar like:

> Recorded macro 'a'

Remember to NOT press the "submit" button of the form while the recording is still going on, because that will use the same username all the 10 (or 20) times, and will simply result in an error. After you have pressed 'q' for the second time (and completed the macro recording), you should press the submit button. Now that we have this macro recorded, we want to repeat it 10 times. For that all you need to do is to open the registration page, and press '@a'. The '@' key tells vimperator that we want to invoke a previously saved macro, and the 'a' tells the macro name. In fact this can be done in an even better way by saving the "page open" also inside the macro (using the "t &amp;lt;page-url&amp;gt;" command (see my previous post [here](http://www.golb.in/vimperator-30.html))); this is left as an excercise for the user ;)

The above was just 1 scenario where one can use macros. But once you know that you have this powerful tool at your disposal, the opportunities of using it are endless. I have even successfully used it for developer testing of web frontend (something similar to what selenium does).

Finally, let me show you some configurations that you can put in your ~/.vimperatorrc file, with the help of a snippet of my config file

```
set ds=yahoo

map &amp;lt;C-.&amp;gt; gt
map &amp;lt;C-,&amp;gt; gT
map &amp;lt;C-s&amp;gt; :sav

ia Pra Pradnyesh
ia Sa Sawant
ia sp spradnyesh
```

* "set ds=yahoo" sets Yahoo! as my default search engine. so if i say "t &amp;lt;some space separated text&amp;gt;", then this is not a URL, and instead, vimperator will search for this text on the Yahoo! search engine
* the "map" command maps a key combination to a particular command. For example, I personally find the "gt" and "gT" combos extremely unwieldy for changing tabs. So I have mapped the "control+." and "control+,", respectively, which are much more convenient for me. Similarly, "control+s" saves the page ;)
* the "ia" command expands the shortform into the longform when the first is entered into some form input box. For example when I press "Pra" into an input box, it automatically gets expanded into "Pradnyesh". Ain't that neat?

I sincerely hope that I have been able to show you what a great tool vimperator is and how it can turn web-browsing into a completely different ball game. I also hope that you have enjoyed reading this as much as I have writing it.

Finally, as always, do share your experiences and don't feel shy/afraid to ask for help :)

ps: I have tried similar plugins for the chrome browser, but they don't come anywhere near to what vimperator can do.
