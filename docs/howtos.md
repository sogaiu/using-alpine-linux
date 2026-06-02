# Howtos

* single user mode can be entered by adding the following to the
  kernel command line (the line that starts "linux") at startup
  (e.g. get at grub menu via shift for bios or esc for uefi then 'e'
  to edit boot entry info):

    single

* packages can be searched for at:

    https://pkgs.alpinelinux.org/packages

* find package containing particular file name:

    https://pkgs.alpinelinux.org/contents

* see log of apk transactions:

  * `cat /var/log/apk.log`

* list files for an installed package:

  * `apk info -L <name>`

* find installed package owning a file path:

  * `apk info -W <path>`

* search for package by substring of name or description:

  * `apk search <name>`
  * `apk search -d <description>`

* show installed packages:

  * `apk info`
  * `apk query --install '*'`

* view which services are enabled for particular runlevels:

  * `rc-update show -v`

* persist certain system settings across reboots:

  * create / put an executable script in `/etc/local.d/` with a
    name that ends with `.start`.  make the content such that
    it causes something to be set, e.g.

      ```
      #! /bin/sh

      echo 80 > /sys/class/power_supply/BAT0/charge_control_end_threshold
      ```

  * enable the local service:

    * `rc-update add local`

* upgrade to a new release:

    > When alpine has a new release, the repository path will
    > change. Assuming you are going forward in time (e.g from 3.12 to
    > 3.13), you can simply edit /etc/apk/repositories and run apk
    > upgrade --available.

