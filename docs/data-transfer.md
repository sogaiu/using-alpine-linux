# Data Transfer

## Identifying What Needs Copying

Without reviewing, classifying, and pruning what one has on a regular
basis, the amount one may have to do this for at once (say in the
event of an emergency or when moving to a new machine) keeps growing.
Perhaps this is one of the reasons that storage companies were able to
remain in business for so long...

## Questions

Permission info on files and directories complicate backing things up
(and restoring) across different platforms.  Is it possible to mostly
keep one's data "permission-less"?

Also, dot files and directories being "hidden" and spawning like
there's no tomorrow makes being clear about what to backup a fair bit
of work.  How can this be avoided or mitigated?

## From Where?

When using a physical machine, the network or a storage device
(internal SDD, external USB, etc.) are some obvious sources from which
to obtain data.

When using a virtual machine, say via qemu, a shared directory can
be arranged for and then mounted from within the guest:

```
mkdir -p shared
sudo mount -t 9p -o trans=virtio,version=9p2000.L host0 shared
```

For this to work though the qemu invocation probably needs to contain
something like:

```
-virtfs local,path=shared,mount_tag=host0,security_model=mapped,id=host0
```

## Plain Copying

Things copied over (`cp -a` may be good) so far:

* `~/.config/nvim` and `~/.local/share/nvim`
* `~/src`
* `~/.emacs.d`
* `~/.ssh`
* `~/.gitconfig`

## Slightly Involved Copying

Need to do while not logged in (or `xfconfd` not running...)
* `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-keyboard-shortcuts.xml` - for keyboard shortcuts

