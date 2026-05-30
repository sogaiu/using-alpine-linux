# Post Installation Bits

## Basic Non-root User Preparation

* Get basic desktop environment files and directories into place
  (e.g. `~/.config`, etc.)

  * Graphical login as user (via original virtual console)

  * Log out

* Restore / bring in some desktop environment settings

  * Login as user at virtual console

  * Copy files from elsewhere on to internal storage (e.g. via USB)

  * Copy certain settings files into place, e.g.

    * cp xfce4-keyboard-shortcuts.xml \
         ~/.config/xfce4/xfconf/xfce-perchannel-xml/

    * cp world ~/

* Prepare some files, directories, and environment variables

  * If the `~/.local` directory doesn't exist, create it in
    preparation for per-user software installation.  Also create the
    `~/bin` directory for symlinking to files built from source that
    can be used "in-tree" (e.g. like emacs).

  * Ensure there is a `~/.profile` file that adds `$HOME/.local/bin`
    and `$HOME/bin` to `PATH`

## Install Packages

* Graphical login as user

* Install packages

  * Manual - `doas apk add ...`

  * Restore - edit `/etc/apk/world` and then `doas apk add`

* Ensure no network services started

  * doas netstat -tunlp

* Enable nftables (installation via `/etc/apk/world` above)

  * doas rc-service start
  * doas rc-update add nftables boot

* Log out once to get things like sound working

## Adjust User Things

* Graphical login as user

* Turn off lockscreen via `Settings > Xfce Screensaver > Lock Screen`

* Set "focus follows mouse" via `Settings > Window Manager > Focus`

* Turn off microphone via pavucontrol

* ...

