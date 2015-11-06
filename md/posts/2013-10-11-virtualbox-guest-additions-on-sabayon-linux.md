{:title "Virtualbox guest-additions on Sabayon linux"
 :layout :post
 :tags  []
 :toc true}

First, things keep changing continuously in the Linux world. Secondly, configurations differ, ergo YMMV ;)

With that out of the way, lets attack the main issue. Thing is, i spent a total of 6 hours trying to get virtualbox guest additions to work my Sabayon Linux guest on a WindoZZZe-7 host :((

Unfortunately the [Sabayon wiki](https://wiki.sabayon.org/index.php?title%4DHOWTO:_Install_VirtualBox) does not help much for when Sabayon is installed as a guest

I got all sorts of errors right from guest addition features like full-screen and shared folder mounting not working to xorg crash without much helpful error logs. Also, simply installing virtualbox, pulls a new kernel, which makes things even more difficult. Anyways, long story short, i was able to solve all these problems by following the steps below. Do note down your kernel and virtualbox version numbers as they might vary with the ones given below

```
$ equo install sys-kernel/sabayon-sources-3.11.2 sys-kernel/linux-sabayon-3.11.2 x11-drivers/xf86-video-virtualbox-4.2.18#3.11.2-sabayon app-emulation/virtualbox-modules-4.2.18#3.11.2-sabayon app-emulation/virtualbox-guest-additions-4.2.18#3.11.2-sabayon
$ kernel-switcher switch linux-server-3.11.2
add "modules="vboxdrv vboxnetflt vboxnetadp vboxsf"" in /etc/conf.d/modules
add user to vboxusers and vboxguest groups
add virtualbox-guest-additions to default runlevel
$ eselect opengl set ati
```

Do *not* do the following. Basically don"t use vboxvideo driver, instead use an empty xorg.conf file and things should just work fine

```
$ cp /usr/share/doc/virtualbox-guest-additions-4.2.18/xorg.conf.vbox /etc/X11/xorg.conf
$ eselect opengl set xorg-x11
append "vboxvideo" to /etc/conf.d/modules (in step-3 above)
```

Even after doing all above, i"m still facing some issues. I"d be grateful if someone could kindly tell me the solution, or even tell me a better/correct-er way of getting things to work:

```
shared folders work weirdly: i cannot view/enter contents of shared-folder. however, i have a soft-link to a file inside a shared folder, and i am able to read/write from/to the file without any problem. weird, huh???
clipboard sharing does not work
```
