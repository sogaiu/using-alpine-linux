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

  * cat /var/log/apk.log

* list files for an installed package:

  * apk info -L &lt;name&gt;

* find installed package owning a file path:

  * apk info -W &lt;path&gt;

* search for package by substring of name or description:

  * apk search &lt;name&gt;
  * apk search -d &lt;description&gt;

* show installed packages:

  * apk info
  * apk query --install '*'

* view which services are enabled for particular runlevels:

  * rc-update show -v

* for upgrading to a new release(?):

    > When alpine has a new release, the repository path will
    > change. Assuming you are going forward in time (e.g from 3.12 to
    > 3.13), you can simply edit /etc/apk/repositories and run apk
    > upgrade --available.
