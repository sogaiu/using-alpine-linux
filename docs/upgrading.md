# Upgrading

## Preparation

1. The first thing to do is probably to read the release notes.  For
   3.24.0, they looked like
   [this](https://www.alpinelinux.org/posts/Alpine-3.24.0-released.html).

   There may be an "Upgrade Notes" section, so try to understand it if
   there is one.

2. Head over to the Wiki's [ Upgrading Alpine Linux to a new release
   branch](https://wiki.alpinelinux.org/wiki/Upgrading_Alpine_Linux_to_a_new_release_branch)
   page to get a reminder of the steps that are likely to be the same
   most of the time:

   * Update Repositories file
   * Updating package lists
   * Upgrading packages

   It's likely some new files that end in `.apk-new` will show up
   under `/etc` so be prepared to review these and do some studying.

3. It might help to jot down some notes of the expected overall
   process before starting.  Also, prepare to log what actually
   happens.

4. Consider backing up any relevant data before starting and do so if
   appropriate.

## Perform the Upgrade

0. Log out of graphical environment and log in on a virtual console.

1. Edit `/etc/apk/repositories` so it mentions the new version instead
   of the old (e.g. change all instances of `3.23` to `3.24`).

2. Update the package lists: `doas apk update`

3. Upgrade `apk-tools`: `doas apk add --upgrade apk-tools`

4. Upgrade installed packages: `doas apk upgrade --available`

5. Go through output by looking at the relevant portion of
   `/var/log/apk.log` making notes about changes, e.g.  it's likely
   there will be some new files under `/etc` ending in `.apk-new`.

6. Attend to what was noted in the last step.

7. Attend to anything mentioned in the "Upgrade Notes" section
   in the release announcment.

8. Recompile any software as needed (e.g. from-source builds of emacs
   managed with stow).

9. Try to cope with anything that didn't go well :)

