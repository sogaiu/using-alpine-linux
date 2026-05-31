# Basic Setup

Alpine Linux provides a set of shell scripts for setup tasks.  Some of
these are used below.  See
[here](https://wiki.alpinelinux.org/wiki/Alpine_configuration_management_scripts)
for more details.

Depending on one's familiarity with various unixen, there might not be
much that is surprising for a `sys` type of installation (i.e. the
type that doesn't try to do things from RAM).

A few things worth noting might be:

* `doas` is used instead of `sudo`
* OpenRC is used instead of `systemd`

The former might be seen as just retraining muscle memory, while the
latter is significant from the perspective of investigating issues (as
well as attack surface area).

## Base Installation

* Prepare installation media:

  * Choose a release, see:

    https://alpinelinux.org/releases/

  * Download iso and checksum from:

    https://alpinelinux.org/downloads/

  * Verify using `sha256sum` or other appropriate tool

  * Place `.iso` on boot media (e.g. use Ventoy on USB drive)

* Perform basic installation steps:

  * Boot from obtained install media (e.g. via Ventoy)

  * Login as root (no password)

  * Get pre-prepared [answerfile](./answerfile.md) on to machine
    somehow, e.g via USB (hints: `fdisk -l`, `mount`, etc.)

  * Run and interact with setup script (e.g. wifi info, root password,
    etc.) [1]:

    * setup-alpine -f answerfile

  * If the wireless interface isn't detected (e.g. no option to choose
    `wlan0` or similar), check `dmesg` output to see if the hardware
    was appropriately detected and initialized.  It may be that
    additional firmware might need to be loaded.

    [This work
    item](https://gitlab.alpinelinux.org/alpine/alpine-conf/-/work_items/10646)
    has a work-around for the case of some Intel hardware:

    ```
    mkdir /root/upper /root/workdir
    mount -t overlay overlay -o lowerdir=/.modloop/,upperdir=/root/upper,workdir=/root/workdir /.modloop
    apk add linux-firmware-intel
    rmmod iwlwifi
    modprobe iwlwifi
    ```

    If your hardware is non-Intel, it might be worth trying a
    different `linux-firmware-*` package and adjusting the `rmmod` /
    `modprobe` bits.

  * Setup the disk (choose the appropriate storage device and "sys"):

    * setup-disk

  * Shutdown and remove media (may need manual poweroff)

    * halt

  * Boot and login as root (will have password this time)

## Perform Manual Adjustments

* Ensure non-root user has admin capabilities

  * Configure doas (doas likely installed during setup-alpine)

    * echo "permit persist :wheel" > /etc/doas.d/doas.conf

  * Verify non-root user is in wheel group

    * less /etc/group

* Ensure user has a password

  * passwd user

## Desktop Environment Installation

* Install desktop environment

  * setup-desktop xfce

* Restart

  * reboot

## Footnotes

[1] If `wlan0` does not show up as a candidate for wireless
connectivity, two work-arounds are: 1. use a wifi USB dongle, or
2. use a wired connection.  After the first reboot, wifi hardware may
be detected appropriately.  If a wired connection was used to
work-around the issue, it may be that running `setup-interfaces` on
its own (it's usually executed by `setup-alpine`) may help get things
going.  Haven't tried the wired work-around though so don't really
know.  See #10646 in the alpine-conf repository though for another
idea.

