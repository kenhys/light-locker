# light-locker

light-locker is a simple locker (forked from gnome-screensaver) that aims to have simple, sane, secure defaults and be well integrated with the desktop while not carrying any desktop-specific dependencies.

It relies on lightdm for locking and unlocking your session via UPower or logind/systemd.


## Requirements

To use light-locker with systemd, you need at least lightdm 1.7.0.

light-locker doesn't work with lightdm version 1.7.5-1.7.9

## Usage

After installing light-locker, it will auto start along your session and you will be able to lock your session with "light-locker-command -l".

This will redirect you to VT8 (assuming that your open session was on VT7 and is now kept safe by light-locker) and present LightDM's greeter for unlocking your session again.
On suspend/resume light-locker will lock the active session and redirect to the LightDM's greeter for unlocking the session again.

There is no support for gnome-settings-daemon in order to keep things slim, so you might have to add a custom keyboard-shortcut for this to work.

light-locker will automatically lock the session shortly after the X11 screen saver kicks in. The timeout can be set with --lock-after-screensaver. With xset the X11 screen saver can be adjusted.

Use --late-locking to avoid some of the negative effects of VT switching. This will lock the session on the deactivation of X11 screen saver instead of activation.

light-locker will automatically lock the session on suspend/resume. To disable this behaviour with --no-lock-on-suspend.
With --lock-on-lid light-locker will automatically lock the lid close.

With logind sessions can have an idle hint. This is used to perform some action after a timeout. Use --idle-hint to let light-locker set the idle hint, in case nothing else does.


## Building

light-locker different configurable dependencies and some of these require the development files to be installed.
Most of these configurations will be enabled automatically when their dependencies are available.
Here is a list of the different dependencies and their configuration flags:

  --with-systemd: This adds the support for systemd logind. This option requires the development files to be installed.

  --with-upower: This adds the support for UPower.

  --with-mit-ext: This enables the lock-after-screensaver feature. This options requires the X11 Screen Saver extension development files to be installed.

  --with-dpms-ext: This adds the support for DPMS. This is used to turn on the display on screen saver deactivation.

Many of the light-locker features can be disabled/enabled and configured at build time. Here is a list of these configuration flag:

  --enable-late-locking: Enables --late-locking and --no-late-locking. Default enabled with --no-late-locking. This requires mit-ext.

  --enable-lock-on-suspend: Enables --lock-on-suspend and --no-lock-on-suspend. Default enabled with --lock-on-suspend. This requires either systemd or upower.

  --enable-lock-on-lid: Enables --lock-on-lid and --no-lock-on-lid. Default enabled with --no-lock-on-suspend. This requires upower.

## Users

Known users of light-locker are:

  * elementary OS
  * XFCE
