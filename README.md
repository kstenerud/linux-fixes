Linux Fixes
===========

My personal collection of fixes and workarounds for various Linux issues.


Ignore lid closed
-----------------

The "lid closed" switch is handled via `/etc/systemd/logind.conf`. You'll want this:

    HandleLidSwitch=ignore



Manually suspend
----------------

This fixes various charging issues (where the OS gets stuck in low power charging mode).

    sudo systemctl suspend



Fix "A suspend operation is already in progress"
------------------------------------------------

    killall systemd-sleep

You may need to reset your window manager as well.

    xfwm4 --replace



Fix inconsistent scrolling direction
------------------------------------

Scroll direction becomes a problem because there are different settings that only affect certain kinds of programs.

To set it for absolutely everything:

* Reset all other scroll direction settings to default.

* Find the xinput id of your device: `xinput list`

* Find the scroll setting (assuming id 10): `xinput list-props 10 |grep Scroll`

You'll see either `VertScrollDelta` (change the sign to negative) or `Australian Scrolling` (change from 0 to 1).

* Edit your xorg config file: `sudo vi /usr/share/X11/xorg.conf.d/50-touchpad-cmt-cave.conf`

* Add the option to your config

        Option          "Australian Scrolling" "1"

* Reboot: `sudo reboot`
