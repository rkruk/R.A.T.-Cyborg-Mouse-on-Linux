# Cyborg R.A.T. Mouse on Linux

<div align="center">
  <img width="260" height="161" src="./images/rat-logo.png" alt="Cyborg R.A.T. Logo">
  
  **Xorg Server Configuration & Setup for Cyborg R.A.T. Series**
  
  [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
  [![Issues](https://img.shields.io/github/issues/rkruk/R.A.T.-Cyborg-Mouse-on-Linux)](https://github.com/rkruk/R.A.T.-Cyborg-Mouse-on-Linux/issues)
</div>

## Table of Contents

- [Cyborg R.A.T. Mouse on Linux](#cyborg-rat-mouse-on-linux)
  - [Table of Contents](#table-of-contents)
  - [Problem Description](#problem-description)
    - [Root Cause](#root-cause)
  - [Quick Fix](#quick-fix)
  - [Detailed Setup](#detailed-setup)
    - [Step 1: Identify Your Mouse](#step-1-identify-your-mouse)
    - [Step 2: Test Mouse Buttons](#step-2-test-mouse-buttons)
    - [Step 3: Configure Xorg](#step-3-configure-xorg)
    - [Step 4: Apply Changes](#step-4-apply-changes)
  - [Kernel Driver Method](#kernel-driver-method)
    - [Prerequisites](#prerequisites)
    - [Build Steps](#build-steps)
  - [Supported Systems](#supported-systems)
  - [Mouse Technical Details](#mouse-technical-details)
  - [Contributing](#contributing)
  - [License](#license)

## Problem Description

After connecting a Cyborg R.A.T. mouse, it appears to work but exhibits the following issues:

- **Unresponsive buttons** - Cannot open/close windows or use context menus
- **Dragging issues** - Unable to drag windows or select text properly  
- **General unresponsiveness** - Mouse feels laggy and difficult to use

### Root Cause

These problems are caused by conflicts between the R.A.T. mouse's "Mode" button (profile changer) and the Xorg server's input handling.

## Quick Fix

The simplest solution is to disable the problematic "Mode" buttons in Xorg configuration:

1. **Create the configuration file:**
   ```bash
   sudo nano /etc/X11/xorg.conf.d/10-evdev.conf
   ```

2. **Add the configuration** (see [`10-evdev.conf`](./10-evdev.conf) for the complete file)

3. **Restart your X session** or reboot

> **Note:** Using a separate configuration file ensures your settings survive Xorg updates.

## Detailed Setup

### Step 1: Identify Your Mouse

First, find your mouse in the system:

```bash
xinput list
```

Look for output similar to:
```
Virtual core pointer                          id=2    [master pointer  (3)]
  ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
  ↳ Saitek Cyborg R.A.T.9 Wireless Mouse      id=10   [slave  pointer  (2)]
```

Note the ID number (in this example: `id=10`).

### Step 2: Test Mouse Buttons

Test each button to identify their numbers:

```bash
xinput --test 10  # Replace 10 with your mouse ID
```

Press each button and note the numbers. Example output:
- **Left button:** 1
- **Right button:** 3  
- **Wheel click:** 2
- **Wheel up:** 4
- **Wheel down:** 5
- **Back button:** 8
- **Forward button:** 9
- **Sniper button:** 12
- **Horizontal wheel left:** 11
- **Horizontal wheel right:** 10
- **Mode buttons:** 11, 12, 13 ⚠️ *These need to be disabled*

### Step 3: Configure Xorg

Create `/etc/X11/xorg.conf.d/10-evdev.conf` with your button mapping:

```bash
sudo nano /etc/X11/xorg.conf.d/10-evdev.conf
```

Add configuration based on your button test results. See the example [`10-evdev.conf`](./10-evdev.conf) file.

**Key settings:**
- `Option "Buttons" "17"` - Maximum button number from your test
- `Option "ButtonMapping" "1 2 3 4 5 0 0 8 9 7 6 12 0 0 0 16 17"` - Button mapping with mode buttons disabled (set to 0)

### Step 4: Apply Changes

Restart your X session or reboot your system.

## Kernel Driver Method

> **Advanced Users Only** - Requires kernel compilation experience

Recent Linux kernels include dedicated MadCatz/Saitek mouse drivers that can eliminate the need for Xorg configuration.

### Prerequisites
- Kernel sources
- Build tools: `gcc`, `make`, `ctags`, `ncurses-devel`

### Build Steps

1. **Access kernel configuration:**
   ```bash
   cd /usr/src/linux
   sudo make menuconfig
   ```

2. **Navigate to mouse drivers:**
   ```
   Device Drivers → Input device support → Mice
   ```

3. **Enable the following drivers:**
   - `HID Multitouch panels` 
   - `Mouse interface` 
   - `Synaptics I2C Touchpad support`

4. **Compile and install:**
   ```bash
   sudo make -j$(nproc) && sudo make modules_install
   sudo make install
   ```

**Warning:** Kernel compilation can make your system unbootable if misconfigured. Consult your distribution's documentation for specific instructions.

## Supported Systems

**Tested Linux Distributions:**
- Gentoo (testing profile)
- Funtoo (current profile) 
- Arch Linux (current)
- Ubuntu (14.04 - 18.04+)

**Compatibility:**
- **Kernels:** 2.6+ to current (kernel-agnostic solution)
- **Xorg/evdev:** All versions to current

## Mouse Technical Details

**Cyborg R.A.T. Series Specifications:**
- **Connectivity:** 2.4GHz Wireless (R.A.T.9) or Wired (R.A.T.3, R.A.T.7)
- **DPI Range:** 25-6400 DPI (25 DPI increments)
- **Tracking Speed:** Up to 6 meters per second
- **Button Layout:**
  - 2 main buttons (left/right)
  - 4 custom DPI settings  
  - 6 programmable buttons
  - 3 Cyborg modes
  - **Total:** 8+ functional buttons

**Cross-Model Compatibility:**
Settings are transferable between MadCatz and Saitek R.A.T. models.

> **Note:** This solution works for many multi-button mice beyond just the R.A.T. series.

## Contributing

Contributions are welcome! This configuration helps with many multi-button mice beyond just the R.A.T. series.

**How to contribute:**
1. Fork the repository
2. Test with your mouse model
3. Submit documentation improvements
4. Report issues with specific hardware

## License

This project is licensed under the GPL v3 License - see the [LICENSE](LICENSE) file for details.

---

**Disclaimer:** This is an independent community project and is not affiliated with MadCatz or Saitek.
