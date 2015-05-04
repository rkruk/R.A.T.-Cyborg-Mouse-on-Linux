***

Linux Xorg/evdev setups for multi buttons devices like "CYBORG R.A.T." Mouse (16 actions for all buttons).
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

Those settings has been tested on Funtoo/Gentoo/Arch and Ubuntu Linux machines with the latest Xorg. This workaround works with kernel 2.6 and with the latest kernel 3.. & 4.. > current. (nothing has changed - evdev still can't work with this class of devices *and it is May 2015.. :/ ).

-Gentoo with current profile (~amd64);
-Funtoo with current profile (~amd64);
-Arch (64bit);
-Ubuntu (tested from 14.04 to 15.04 (and 15.10 too).

====================================================================

**TECH STUFF:**

Gentoo profile ~ current
Funtoo standard profile

Kernel line is: 
*Linux from 2.6 all versions > to current* (nobody care about older stuff - right?)

====================================================================

Mouse settings are working with all current kernel versions and mods ( tested with: pf, ck). You can use this setups for any kernel mod (pf-kernel, ck-kernel, etc..) -in most cases it should just works.

====================================================================

**MOUSE TECHNICAL DETAILS:**

-Mouse with Very Low Latency 2.4Ghz Wireless or Cable Versions (v.3 and v.7);

-6400 DPI (track approx up to 6 meters per second);

-Buttons-

-2 regular left and right mouse buttons

-4 Custom DPI Settings

-6 Programmable Buttons

-3 Cyborg Modes

-A total of: 8 buttons.

==============================================================

All settings are fully customizable and transferable between different mouse models (non MadCatz too - probably).

(I believe that the problem with 'setting up' pro-mouses (pro - I mean mouse with more then 2 or 3 buttons) in the linux environment is wider than MadCatz R.A.T.s mouses) and these settings could be be used with other mice makers/models/vendors.

Set up:
It is only the correct number of buttons to setup correctly - to work with other mouse makers/models/vendors.

==============================================================
