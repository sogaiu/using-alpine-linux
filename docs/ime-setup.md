# Input Method Editor Configuration

Alpine Linux has packages for both ibus and fcitx.  At the moment
there are some notes for ibus.

## Initial Setup

Choosing `Settings -> IBus Preferences` may lead to a dialog box
about starting ibus.  Answer in the affirmative and note the
information about:

```
 export GTK_IM_MODULE=ibus
 export XMODIFIERS=@im=ibus
 export QT_IM_MODULE=ibus
 ```

Adding this to `~/.profile` seems to be ok.

Logging out and back in seems like it helps get things working.

## Add Various Japanese, Korean, etc. IMEs

### Japanese

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Input Method" tab

* Click the "Add" button on the right side

* From the resulting dialog, choose "Japanese"

* Select the "Anthy" item

* Click on the "Add" button

* Not sure how to configure it so that the default input mode is
  Hiragana.

### Korean

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Input Method" tab

* Click the "Add" button on the right side

* From the resulting dialog, choose "..." and then scroll to "Korean"

* Select the "Korean (Hangul)" item (or similar)

* Click on the "Add" button

* It should be possible to choose "Start in Hangul Mode" or similar
  via configuration.

## English

Having an English IME may be handy for switching among different IMEs.
That may allow one to dispense with each individual IME's method of
providing "Latin" / "Roman" input.

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Input Method" tab

* Click the "Add" button on the right side

* From the resulting dialog, choose "English"

* Select one of the "English (...)" items

* Click on the "Add" button

## Disable Unwanted Key Bindings

Some of the default key bindings may interfere with other settings.
Disabling is one way to reduce confusion and/or unwanted feature
activation.

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Emoji" tab

* Click on the "..." button to the right of "Emoji annotation"
  and "Unicode code point" (one at a time)

* Delete existing key bindings

* Click the "OK" button

May need to repeat some of the operations above to delete remaining
key bindings as after deleting one, remaining ones may for some reason
not be accessible.

