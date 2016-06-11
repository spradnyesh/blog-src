{:title "passwordless login in lightdm"
 :layout :post
 :tags  ["lightdm" "passwordless" "login" "linux" "stumpwm"]
 :toc true}

i've mentioned before [here](/posts/2014-01-17-stumpwm.html), [here](/posts/2014-01-16-kill-that-rat.html), [here](/posts/2014-01-18-vimperator.html) and [here](/posts/2014-01-19-vimperator-part-2.html) that i prefer using the keyboard than the mouse for increased productivity. i also use [lightdm](https://en.wikipedia.org/wiki/LightDM) as my [display manager](https://en.wikipedia.org/wiki/X_display_manager_\(program_type\)) from which i invoke [stumpwm](https://en.wikipedia.org/wiki/StumpWM).

since mostly i'm the only person using my desktop i like to be auto-logged-in into my system. i don't care much about security because i use [colemak](http://colemak.com/) as my keyboard layout and hence any person using my system won't be able to use it anyways ;)

it's really very easy to enable passwordless login in lightdm. simply uncomment "autologin-user" and put in your userid there, as below

> autologin-user=[userid]

that's it! although it's super simple, i'm keeping it here for my own future reference O:-)
