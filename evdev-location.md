**Mouse config file location:**

Linux is flexible, every distribution settings vary.

The /etc/X11/xorg.conf.d/ directory stores Xorg configuration. You are free to add configuration files there, 
and by convention their names start with XX- (two digits and a hyphen, so that for example 10 is read before 20). 
These files are parsed by the Xorg upon startup and are treated like part of the traditional /etc/X11/xorg.conf 
configuration file. Xorg server essentially treats the collection of all configuration files as one big file.

It could be:

/etc/X11/xorg.conf.d/10-evdev.conf 

or:

/etc/X11/xorg.conf.d/20-evdev.conf

etc..

It can be even inserted inside xorg.conf as a "Input Class" section (/etc/X11/xorg.conf) - but there is 
a risk involved: any potential xorg update will overwrite that settings.
