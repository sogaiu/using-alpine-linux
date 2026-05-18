# Gripes

A collection of gripes that came up while going through and
interacting with Alpine Linux materials and system.

Relatively minor things perhaps :)

* The wiki was unavailable at one point while working on these pages.
  Some of the pages were available via archive.org though.

* Within the fine "user handbook", the table of contents on the left
  side seems to have content that is confusing.

  A specific example of this can be observed when one clicks on
  "Working With Alpine".  instead of seeing "Working With Alpine" as
  the title of the content on the right, one sees "Post Installation
  Recommendations"...and it does not appear that one can find "Post
  Installation Recommendations" within the table of contents on the
  left.

  Source for the handbook is in asciidoc at:

    https://gitlab.alpinelinux.org/alpine/docs/user-handbook

  Possibly relevant commit:

    https://gitlab.alpinelinux.org/alpine/docs/user-handbook/-/commit/28580c07c671ea64ab549aff0549e745dd71bd29

* Some of the apk subcommands seem confusing in the sense that it is
  not obvious in some cases which one might be relevant for the task
  at hand.  To be fair, this seems to be a common issue on other
  distributions that have similar sorts of commands.  It could be that
  with an appropriate perspective (that doesn't involve having to know
  a lot of the implementation details) things make sense but atm it
  doesn't feel that way :)

* Despite its name (and man page first line description), rc-update
  can show enabled services.  i.e. it's not just add and remove stuff.

* rc-service, rc-update (and friends?) have man pages with
  synopsises(?) that don't make it clear which items are parameters,
  e.g. in:

    rc-update [-s, --stack] add service [runlevel ...]

  This may be something specific to alpine's stuff as apk's man page
  seems similar.

  In many other man pages, angle brackets are used around things that
  are not meant as literal text (e.g. see git's man page).

  Presumably "service" is not literal text, while "add" is.

* Use of tabs for indentation in setup-* scripts - too easy for
  apparent line lengths to get long and result in wrapping of text and
  consequently unnecessarily harder to read content.

