# Non-Packaged Libraries and Programs

There is a package for `stow`, so in a number of cases, this can be
used to build from source and manage the results accordingly.

So far, have had luck with:

* emacs-31.x
* zig-0.16.0

Might try to use with:

* janet

## Tor Browser

For whatever reason, Tor Browser doesn't appear to work as-is in
Alpine Linux (may be it's a glibc vs musl thing?).  The Alpine Wiki
had [a hint](https://wiki.alpinelinux.org/wiki/Tor#Installation) that
it might work via [flatpak](https://wiki.alpinelinux.org/wiki/Flatpak)
and that turned out to be correct in at least one case:

```
doas apk add flatpak

flatpak \
  remote-add \
  --user \
  --if-not-exists \
  flathub \
  https://dl.flathub.org/repo/flathub.flatpakrepo

# log out and back in -- restart may be unneeded

# find appropriate id
flatpak --user search "Tor Browser"

flatpak --user install org.torproject.torbrowser-launcher

# apparently appropriate "portal" bits are needed
doas apk add xdg-desktop-portal xdg-desktop-portal-gtk

# can launch via command line
flatpak run org.torproject.torbrowser-launcher
```

If you happen to be in the unfortunate situation where your ISP blocks
web access to torbrowser.org, the initial launching may fail.  Finding
a more friendly connection just for setup is a work-around for some
people.

An alternative approach might be to run tails via qemu.

## tree-sitter-module

For tree-sitter parser shared objects / libraries.

Already had these bits (also linked to from under `~/.emacs.d`), but FWIW:

```
cd ~/src
git clone https://github.com/casouri/tree-sitter-module
cd tree-sitter-module
bash batch.sh
```

## janet

To follow development of janet.

```
cd ~/src
git clone https://github.com/janet-lang/janet
cd janet
make clean && PREFIX=$HOME/.local make && PREFIX=$HOME/.local make install
```

