# Rescue

Sometimes something goes wrong and one's system will no longer boot up
to a functioning Alpine system.

For example, when upgrading from 3.23.4 to 3.24, the [upgrade
notes](https://www.alpinelinux.org/posts/Alpine-3.24.0-released.html#upgrade_notes)
mentioned that:

> GRUB users must run `grub-install <device>` or `grub-install
> <efi-options>` after upgrading to ensure the new GRUB version is
> properly installed to disk.

but this was problematic for a couple of reasons:

1. `<efi-options>` is rather non-specific
2. Even though `<efi-options>` might be guessed from examining the
source to the `setup-disk` script, that didn't seem to be sufficient
in the end anyway [1].

In any case, the `grub-install` invocation that was tried was:

```
grub-install \
  --target=x86_64-efi \
  --efi-directory=/boot/efi \
  --bootloader-id=alpine \
  --boot-directory=/boot \
  --no-nvram
```

Upon rebooting, was greeted by a screen with message:

```
error: symbol `grub_memcpy' not found.
Entering rescue mode...
grub rescue>
```

In these kinds of cases, it can be helpful to boot from "resuce
media", chroot, and perform some fixes.  Needless to say, doing some
research first into whatever symptoms are exhibited might be a good
idea.

The installation media for Alpine seems to be sufficient for the case
mentioned above.  See
[here](https://wiki.alpinelinux.org/wiki/Rescue_disk) for more info on
"rescue disk".

## From Zero to Chroot

To get to a situation where investigation or fixing might be
possible, the following series of steps might be taken:

* Boot with installation media
* Mount appropriate filesystems
* Chroot

The following is an example series of steps adapted from the Alpine
Wiki's [Chroot](https://wiki.alpinelinux.org/wiki/Chroot) page.

```
mount /dev/nvme0n1p3 /mnt

mkdir -p /mnt/boot/efi
mount /dev/nvme0n1p1 /mnt/boot/efi

cd /mnt

# XXX: the various -o bits might not be needed in many cases?
mount --bind /dev ./dev
mount -t devpts devpts ./dev/pts -o nosuid,noexec
mount -t sysfs sys ./sys -o nosuid,nodev,noexec,ro
mount -t proc proc ./proc -o nosuid,nodev,noexec
mount -t tmpfs tmp ./tmp -o mode=1777,nosuid,nodev,strictatime
mount -t tmpfs run ./run -o mode=0755,nosuid,nodev
# XXX: haven't needed shm so far

# XXX: wiki page was much more involved...
chroot /mnt /bin/sh
```

## Network

Sometimes we might want access to the network.  The following steps
are an example of what has worked in some cases.  Depending on one's
setup, details may need to be adjusted.

```
/etc/init.d/wpa_supplicant start
/etc/init.d/networking start
```

## Investigation and/or Fixing

For the case mentioned above about `grub_memcpy`, the problem appeared
to be that there was a mismatch between the `.efi` bootloader file and
the grub `.mod` (module) files.  This can happen if an appropriate
version of grub has not been installed / copied into place.

Initially, this seemed peculiar because `grub-install` had been
executed precisely to update the bootloader file and its friends.  It
turned out that the actual boot process was not using
`/boot/efi/EFI/alpine/grubx64.efi`, but rather
`/boot/efi/EFI/boot/bootx64.efi`.  The `grub-install` invocation
updated the former, but did not do anything about the latter [2].

What turned out to work in this case was to copy the content of the
former path to the latter [3].

```
cp /boot/efi/EFI/alpine/grubx64.efi \
   /boot/efi/EFI/boot/bootx64.efi
```

and reboot.

It may be that some people would prefer to exit the chroot and unmount
things cleanly before rebooting.

---

[1] To be honest, the instructions were vague and perhaps a case could
be made that they were a bit off as there was no mention of what one
might have to do apart from execute `grub-install`.  At least for one
case, the fix was to copy a file into a particular location and there
was no mention of this.  It might be that this is specific to the
machine in question...not sure really :)

[2] Comparing the file sizes and last modification dates of the two
paths seemed to be consistent with this idea, though subsequently
another installation and upgrade were performed while examining file
changes and confirmation was obtained that way.

[3] Adjusting the boot entry order seemed like it ought to work but an
attempt at doing so resulted in the same kind of `grub_memcpy` error
message.

