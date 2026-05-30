# Using Alpine Linux

Notes on setting up and using Alpine Linux.

The content was originally spread across some gists and a text file,
but it became unwieldy to work with so I decided to rearrange it in
the form of an ordinary git repository.

## Background

### Why Consider Something Other than Linux Mint?

Linux Mint was mostly good (and still may be), but:

* Linux Mint has not transitioned to being Debian-based yet (hopefully
  the LMDE effort will come to fruition).  Ubuntu is fundamentally a
  problematic entity for some folks.  Debian is far preferrable.

* Since Linux Mint is based on Ubuntu mostly, it uses systemd, which
  apart from its [controversial
  history](https://en.wikipedia.org/wiki/Systemd#History) (and [track
  record](https://www.theregister.com/software/2017/06/29/dont-panic-but-linuxs-systemd-can-be-pwned-via-an-evil-dns-query/374328))
  really does seem bloated and opaque.  Those are not points in its
  favor when one has to look after and into things from a system
  administrative perspective.

* Certain network services keep getting re-enabled (e.g. cups and
  related).  That a network service one has explicitly gotten rid of
  returns without much warning is disturbing.

* Microphone keeps getting turned on and it seems rather difficult to
  keep disabled without disabling audio entirely.  This is a major
  privacy concern for at least two reasons.  First, the potential
  leakage of conversations is pretty bad.  Second, that such important
  settings are difficult to make persistent (and they keep reverting)
  is not a good sign (what else might there be going on...or feels
  symptomatic of lack of proper prioritization to certain types of
  things).

* Reserved space here to be filled in when I remember other reasons :)

### Why Consider Alpine Linux?

* Seems simpler than many other distributions (in the Rich Hickey
  sense).

* System administrative burden seems less than many other
  distributions.  Understanding the system seems feasible and
  investigation cost seems lower.

* Not systemd-based.  As noted earlier, systemd-based things seem more
  bloated and opaque.

* Has more up-to-date packages than Linux Mint.

* A typical installation has far less stuff that one did not ask for
  than Linux Mint (or Ubuntu).  Since updating to cope with the
  increasing number of discovered vulnerabilities is getting worse, it
  probably is less work to keep an Alpine Linux system up-to-date.
  Also, the less complicated system may be easier for the maintainers
  to keep in better shape, but this may also depend on the available
  resources.

## Requirements

* Pretty good ability to be aware of security-related issues in a
  timely manner but also being able to respond appropriately.

* Pretty good ability to cope with something when the system behaves
  in an unexpected manner.  Depends on user knowledge of course, but
  it should be reasonably practical for a user to acquire the needed
  background.

* Relatively straight-forward and short setup process.

* Has recent enough versions of gnucash (with ability to interface via
  python [1]) and libreoffice.

* Convenient enough use of removable media via USB because this is a
  frequent need.

## Unaddressed Items

This lives on the top page to increase the chances things get attended
to :)



## Some Details

Currently, there are the following sections:

### Setting Things Up

* [Setup](docs/setup.md)
  * [Answerfile](docs/answerfile.md)
* [Post-Installation Bits](docs/post-installation-bits.md)
  * [Data Transfer](docs/data-transfer.md)
  * [IME Setup](docs/ime-setup.md)
  * [Non-Packaged Libraries and
  Programs](docs/non-packaged-libraries-and-programs.md)

### Maintenance and Reference

* [Howtos](docs/howtos.md)
* [Shell Stuff](docs/shell-stuff.md)
* [References](docs/references.md)

### Misc

* [Wish List](docs/wish-list.md)
* [Gripes](docs/gripes.md)

### Footnotes

[1] The `py3-gnucash` package exists for Alpine separately from the
`gnucash` package.

