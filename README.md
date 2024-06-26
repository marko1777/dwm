#My edits for dwm usind dwm-distrotube as base

The original README.md for distrotube as follows:

#+TITLE: dwm-distrotube

* Table of Contents :toc:
- [[#about-dwm][About DWM]]
  - [[#the-patches-i-added-to-this-build-include][The patches I added to this build include:]]
  - [[#the-dependencies-for-dwm-distrotube-include][The dependencies for dwm-distrotube include:]]
- [[#installing-dwm-distrotube-on-arch-linux][Installing dwm-distrotube on Arch Linux]]
- [[#installing-dwm-distrotube-on-other-linux-distributions][Installing dwm-distrotube on other Linux distributions]]
- [[#my-keybindings][My Keybindings]]
  - [[#main-keybindings][Main keybindings]]
  - [[#layout-controls][Layout controls]]
  - [[#application-controls][Application controls]]
  - [[#doom-emacs][Doom emacs]]
- [[#running-dwm][Running dwm]]
- [[#configuring-dwm-distrotube][Configuring dwm-distrotube]]
- [[#adding-an-autostart-file][Adding an autostart file]]

* About DWM
#+CAPTION: dmenu-distrotube
#+ATTR_HTML: :alt dmenu-distrotube :title dmenu-distrotube :align left
[[https://gitlab.com/dwt1/dotfiles/raw/master/.screenshots/dotfiles04-thumb.png]]

Dwm is an extremely fast, small, and dynamic window manager for X. Dwm is created by the good folks at [[https://suckless.org][suckless.org]].  This is my personal build of dwm.  I used a number of patches in this build to make dwm more "sensible" rather than "suckless."

** The patches I added to this build include:
+ alpha (for transparency)
+ attachaside (new clients appear in the stack rather than as the master)
+ cyclelayouts (cycles through the available layouts)
+ gridmode (adding a grid layout)
+ restartsig (allows dwm to be restarted with a keybinding)
+ rotatestack (moves a window through the stack, in either direction)
+ statuspadding (horizontal and vertical padding in the status bar are now configurable options)
+ uselessgap (adding gaps when more than one window)

** The dependencies for dwm-distrotube include:
+ libxft
+ ttf-hack
+ ttf-joypixels
+ st
+ dmenu
+ tabbed

Also, you will need to add the following from the AUR:
+ nerd-fonts-complete (optional)
+ https://aur.archlinux.org/packages/libxft-bgra/ (needed for colored fonts and emojis)

Also, if you are building this on an Ubuntu-based system, you need to install libx11-dev and xorg-dev.

* Installing dwm-distrotube on Arch Linux
All you need to do is download the PKGBUILD from this repository.  Then run the following command:

=makepkg -cf=

This will create a file that ends in .pkg.tar.zst (for example, dwm-distrotube-git-6.2-1-x86_64.pkg.tar.zst).  Then run:

=sudo pacman -U *.pkg.tar.zst=

Alternatively, you could also install dwm-distrotube from my own personal [[https://gitlab.com/dwt1/dtos][dtos repository]].  To do so, add the following to the end of /etc/pacman.conf :

#+begin_example
[dtos-core-repo]
SigLevel = Optional DatabaseOptional
Server = https://gitlab.com/dwt1/$repo/-/raw/main/$arch
#+end_example

Then, sync the repositories and update your system with:
=sudo pacman -Syyu=

And, then:
=sudo pacman -S dwm-distrotube=

=NOTE:= Installing dwm-distrotube conflicts with the standard dwm package.  If you already have dwm installed, you will be asked if you want to remove dwm and install dwm-distrotube instead.

* Installing dwm-distrotube on other Linux distributions
Download the source code from this repository or use a git clone:

#+begin_example
git clone https://gitlab.com/dwt1/dwm-distrotube.git
cd dwm-distrotube
sudo make clean install
#+end_example

=NOTE:= Installing dwm-distrotube will overwrite your existing dwm installation.

* My Keybindings
The MODKEY is set to the Super key (aka the Windows key).  I try to keep the keybindings consistent with all of my window managers, but if you several of my window manager configs, there may be some discrepancies between them.

** Main keybindings

| Keybinding              | Action                                                       |
|-------------------------+--------------------------------------------------------------|
| MODKEY + RETURN         | opens terminal (alacritty but can be easily changed)         |
| MODKEY + SHIFT + RETURN | opens run launcher (dmenu but can be changed)                |
| MODKEY + SHIFT + c      | closes window with focus                                     |
| MODKEY + SHIFT + r      | restarts dwm                                                 |
| MODKEY + SHIFT + q      | quits dwm                                                    |
| MODKEY + b              | hides the bar                                                |
| MODKEY + 1-9            | switch focus to workspace (1-9)                              |
| MODKEY + SHIFT + 1-9    | send focused window to workspace (1-9)                       |
| MODKEY + j              | focus stack +1 (switches focus between windows in the stack) |
| MODKEY + k              | focus stack -1 (switches focus between windows in the stack) |
| MODKEY + SHIFT + j      | rotate stack +1 (rotates the windows in the stack)           |
| MODKEY + SHIFT + k      | rotate stack -1 (rotates the windows in the stack)           |
| MODKEY + h              | setmfact -0.05 (expands size of window)                      |
| MODKEY + l              | setmfact +0.05 (shrinks size of window)                      |
| MODKEY + .              | focusmon +1 (switches focus next monitors)                   |
| MODKEY + ,              | focusmon -1 (switches focus to prev monitors)                |

** Layout controls

| Keybinding             | Action                  |
|------------------------+-------------------------|
| MODKEY + d             | row layout              |
| MODKEY + i             | column layout           |
| MODKEY + TAB           | cycle layout (-1)       |
| MODKEY + SHIFT + TAB   | cycle layout (+1)       |
| MODKEY + SPACE         | change layout           |
| MODKEY + SHIFT + SPACE | toggle floating windows |
| MODKEY + t             | layout 1                |
| MODKEY + f             | layout 2                |
| MODKEY + m             | layout 3                |
| MODKEY + g             | layout 4                |

** Application controls

| Keybinding       | Action                                                                       |
|------------------+------------------------------------------------------------------------------|
| MODKEY + ALT + b | open Brave browser                                                           |
| MODKEY + ALT + s | tabbed -r 2 surf -pe x '.surf/html/homepage.html'                            |
| MODKEY + ALT + m | open [mailspring](https://github.com/Foundry376/Mailspring)                  |
| MODKEY + ALT + f | open [pcmanfm (PaCMANFileManager)](https://wiki.archlinux.org/title/PCManFM) |

** Doom emacs

| Keybinding   | Action                                                 |
|--------------+--------------------------------------------------------|
| CTRL + e + e | emacsclient -c -a 'emacs'`                            |
| CTRL + e + d | emacsclient -c -a 'emacs' --eval '(dired nil)'        |
| CTRL + e + m | emacsclient -c -a 'emacs' --eval '(mu4e)'             |
| CTRL + e + b | emacsclient -c -a 'emacs' --eval '(ibuffer)'          |
| CTRL + e + n | emacsclient -c -a 'emacs' --eval '(elfeed)'           |
| CTRL + e + s | emacsclient -c -a 'emacs' --eval '(eshell)'           |
| CTRL + e + v | emacsclient -c -a 'emacs' --eval '(+vterm/here nil)'  |

* Running dwm
If you do not use a login manager (such as lightdm) then you can add the following line to your .xinitrc to start dwm using startx:

=exec dwm=

If you use a login manager (like lightdm), make sure that you have a file called dwm.desktop in your /usr/share/xsessions/ directory.  It should look something like this:

#+begin_example
[Desktop Entry]
Encoding=UTF-8
Name=Dwm
Comment=Dynamic window manager
Exec=dwm
Icon=dwm
Type=XSession
#+end_example

* Configuring dwm-distrotube

If you installed dwm-distrotube with pacman, then the source code can be found in /opt/dwm-distrotube.  If you downloaded the source and built dwm-distrotube yourself, then the source is in the directory that you downloaded.  The configuration of dwm-distrotube is done by editing the config.def.h and (re)compiling the source code.

=sudo make install=
	
* Adding an autostart file
dwm-distrotube has been patched in such a way that it looks for an autostart file at: $HOME/.dwm/autostart.sh

You will need to create this file and the directory that it is located.  An example autostart.sh is included below:

#+begin_example
#! /bin/bash
picom &
nitrogen --restore &
dwmblocks &
#+end_example

The example autostart.sh above launches the compton compositor, sets the wallpaper with nitrogen and launches dwmblocks to add some widgets to our dwm panel.  Obviously, you would need to install compton and nitrogen to use those programs in your autostart.  And you would need to install [dwmblocks](https://gitlab.com/dwt1/dwmblocks-distrotube) to use it.  To use my dwmblocks, you also need to download the scripts found [here](https://gitlab.com/dwt1/dotfiles/-/tree/master/.local/bin).
