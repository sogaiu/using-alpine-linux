# Troubles

* sound does not appear to work after resuming if attempted via
  dbus(?) - at least via gui suspend button in xfce.
  
  doas zzz doesn't appear to have the issue.  turns out that just
  writes a string to /sys/power/state...it looks like a request for
  suspending, if done through `xfce4-session-logout --suspend`,
  results in a dbus request and somehow whatever happens as a result
  is not the same as what `zzz` does.

  it turns out that there is a setting in elogind that seems
  inappropriate (at least for the machine being tested on).  changing
  the existing default setting of `SuspendMode` to blank / empty
  (i.e. `SuspendMode=`), seems to fix things.  this setting has a
  non-blank default value and it can be overridden by changing at
  setting in a file that lives under `/etc/elogind/sleep.conf.d/`.

  the following comment seemed in line with this:

  https://github.com/elogind/elogind/issues/232#issuecomment-1137599958

  it looks like in more recent versions, the SuspendMode setting was
  removed from the configuration file mentioned above.  not sure if
  that fixes things for the case being tested though...

  tracking this down was work because of all of the indirection.

  suspend background info:

    https://github.com/elogind/elogind/issues/180

* maximum battery charge level setting

  kernel's lg-laptop driver doesn't properly detect one of the
  machines properly.  patching the detection was sufficient
  to get things working.
  
  created a custom kernel based on the main/linux-lts aports
  package.
  
