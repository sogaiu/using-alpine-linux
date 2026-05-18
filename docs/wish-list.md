# Wish List

Various things that seem like they might be "nice to have".

* ...be notified of updates via a status tray icon like on linux mint
  (or ubuntu or debian?)

* ...be notified if some network service starts listening on
  a port

## Turn and Keep Microphone Off

Need to verify if this is a problem on Alpine Linux.

## Disable IPV6

Not needed yet it seems as there seems to be [a request to add
configuration](https://gitlab.alpinelinux.org/alpine/alpine-conf/-/work_items/10448).
Disabling can be done via grub IIRC.

## Policy Checker

A "policy checker" to confirm that things like "microphone is off"
hold, no network services are running, etc. would be nice to have.

Better would be for this to run periodically and report on status?

Another good time to run might be after installation / updating of
packages.

