***

Linux Xorg server configuration & setup for multi buttons mouses like Mad Catz "CYBORG R.A.T."
------------------------------------------------------------------------

----------
**Problem:**

After being plugged, the mouse seems to work, but with some issues :
-Unable to click button;
-Unable to drag open windows (apps) or move between them;
-Mouse - in general is unresponsive.

**Reason:** 

The problems are caused by an interaction between R.A.T Mode button (the profile changer) and the Xorg server. 

**Workaround:** 

The Profile Changer button must be disabled in Xorg. In the terminal as a root modify xorg.conf or create separate file evdev.conf (check 'evdev location' example).

**Tested on:**

Those settings has been tested on Funtoo/Gentoo/Arch and Ubuntu Linux machines with the latest Xorg. This workaround works with kernel line from 2.6 to the latest kernel 3.. & 4.. > current. 

(nothing has changed - evdev still can't work with this class of devices - and it is May 2015.. :/ ).

* Gentoo testing profile (~ current);

* Funtoo - current profile (~ standard);

* Arch (current);

* Ubuntu (tested from 14.04 to 15.04 (and 15.10 too).

Kernel versions: 

From 2.6 -> all versions -> to current

====================================================================

These settings are compatible with all kernel versions and mods ( tested with: pf, ck on Arch Linux). You can use this setup for any Linux Distribution - and in most cases it should just works as it is kernel, distro agnostic setup.

====================================================================

**MOUSE TECHNICAL DETAILS:**

-Mouse with Very Low Latency 2.4Ghz Wireless (v.9) or Cable Versions (v.3 and v.7);

-6400 DPI (track approx up to 6 meters per second);

-Buttons:

* 2 regular left and right mouse buttons

* 4 Custom DPI Settings

* 6 Programmable Buttons

* 3 'Cyborg Modes'

* A total of: 8 buttons.

==============================================================

All settings are fully customizable and transferable between different mouse models (non MadCatz (Saitek) too - probably?).

I believe that the problem with 'setting up' multi button mouses ( I mean mouses with more then 2 or 3 buttons) in the linux environment is wider than MadCatz R.A.T.) and this instruction could be be used with other mice makers/models/vendors.

==============================================================
