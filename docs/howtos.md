# Howtos

* Single user mode can be entered by adding the following to the
  kernel command line (the line that starts "linux") at startup
  (e.g. get at grub menu via shift for bios or esc for uefi then 'e'
  to edit boot entry info):

    single

* Packages can be searched for at:

    https://pkgs.alpinelinux.org/packages

* Find package containing particular file name:

    https://pkgs.alpinelinux.org/contents

* See log of apk transactions:

  * `cat /var/log/apk.log`

* List files for an installed package:

  * `apk info -L <name>`

* Find installed package owning a file path:

  * `apk info -W <path>`

* Search for package by substring of name or description:

  * `apk search <name>`
  * `apk search -d <description>`

* Show installed packages:

  * `apk info`
  * `apk query --install '*'`

* View which services are enabled for particular runlevels:

  * `rc-update show -v`

* Persist certain system settings across reboots:

  * Create / put an executable script in `/etc/local.d/` with a
    name that ends with `.start`.  make the content such that
    it causes something to be set, e.g.

      ```
      #! /bin/sh

      echo 80 > /sys/class/power_supply/BAT0/charge_control_end_threshold
      ```

  * Enable the local service:

    * `doas rc-update add local`

* Disable ipv6 via grub:

  * Edit `/etc/default/grub` so that `GRUB_CMDLINE_LINUX_DEFAULT` has
    `ipv6.disable=1` as part of its value.  Do similarly for
    `GRUB_CMDLINE_LINUX` as well for a more comprehensive arrangement.

  * Update `/boot/grub/grub.cfg` (and backup old `.cfg`) via
    `update-grub` script:

    * `doas update-grub`

