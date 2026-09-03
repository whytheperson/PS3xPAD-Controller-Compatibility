# PS3xPAD Controller Compatibility for PS3 HEN

Community-maintained compatibility notes and configurations for using modern controllers on **PlayStation 3** with **PS3xPAD**.

The goal of this repository is to document controllers that have been **tested on real hardware**, including their USB IDs, connection mode, PS3xPAD configuration, and in-game results.

---

## Confirmed controller

### GameSir T4 Nova Lite

The **GameSir T4 Nova Lite** has now been confirmed working on a PS3 running HEN using PS3xPAD.

| Item | Status |
|---|---|
| PS3 HEN boots normally with PS3xPAD | ✅ Confirmed |
| Wired USB / XInput | ✅ Working |
| Original 2.4 GHz dongle | ✅ Working |
| Works inside PS3 games | ✅ Confirmed |
| Face buttons | ✅ Working |
| Analog sticks | ✅ Working |
| D-pad | ✅ Working |
| Shoulder buttons / triggers | ✅ Working |
| PS / Home button | 🧪 Not fully documented yet |
| Rumble | 🧪 Not fully documented yet |

---

## GameSir T4 Nova Lite USB modes

The controller exposes different USB IDs depending on the selected input mode.

### Green mode — XInput

This is the recommended mode for PS3xPAD.

```text
VID: 3537
PID: 1040
```

Windows identifies the controller as:

```text
Xbox 360 Controller for Windows
```

PS3xPAD configuration:

```text
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

This mode has been confirmed working in PS3 games.

---

### Yellow mode — HID / DInput

```text
VID: 3537
PID: 1041
```

Windows exposes this mode as a generic HID game controller.

The PS3 can receive input from the controller in this mode without proper translation, but the button mapping is incorrect.

For PS3xPAD, use the **green XInput mode** instead.

---

## Confirmed DInput button numbering

Using `joy.cpl` on Windows in the yellow/HID mode:

```text
A      = Button 1
B      = Button 2
X      = Button 4
Y      = Button 5

LB     = Button 7
RB     = Button 8
LT     = Button 9
RT     = Button 10

Select = Button 11
Start  = Button 12

L3     = Button 14
R3     = Button 15
```

These values describe the Windows HID/DInput report. They are not PS3 button numbers.

---

# Installation on PS3 HEN

## Required files

Place the PS3xPAD files in:

```text
/dev_hdd0/plugins/ps3xpad/
```

Example:

```text
/dev_hdd0/plugins/
├── webftp_server.sprx
└── ps3xpad/
    ├── xpad_vsh.sprx
    ├── xpad_game.sprx
    ├── xpad_devices.txt
    ├── xpad_settings.txt
    └── xpad_remap.txt
```

---

## xpad_devices.txt

For the GameSir T4 Nova Lite:

```text
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

Save it as:

```text
/dev_hdd0/plugins/ps3xpad/xpad_devices.txt
```

---

## boot_plugins.txt

Edit:

```text
/dev_hdd0/boot_plugins.txt
```

Keep any existing plugin entries such as webMAN.

Example:

```text
/dev_hdd0/plugins/webftp_server.sprx
/dev_hdd0/plugins/ps3xpad/xpad_vsh.sprx
```

If you previously tested another PS3xPAD build and still have:

```text
/dev_hdd0/plugins/xpad.sprx
```

remove that line before loading the v0.8-style plugin.

Do not load two different PS3xPAD VSH plugins at the same time.

---

## First boot

1. Shut the PS3 down completely.
2. Power it back on.
3. Enable HEN.
4. Wait for the XMB to finish loading.
5. Connect the controller.
6. Put the GameSir T4 Nova Lite in **green / XInput mode**.

The tested console successfully booted and enabled HEN normally with this setup.

---

# Confirmed working connections

## USB cable

Confirmed working.

Use:

```text
Green LED
XInput
VID:PID = 3537:1040
```

---

## Original 2.4 GHz dongle

Confirmed working in PS3 games.

The controller has been tested successfully while playing through the original wireless dongle.

> The dongle's own USB VID/PID has not yet been separately documented in this repository, so do not assume it is identical to the wired XInput ID until independently verified.

---

# Expected button mapping

In XInput mode, PS3xPAD translates the controller as expected:

```text
GameSir     PS3
----------------
A        -> Cross
B        -> Circle
X        -> Square
Y        -> Triangle

LB       -> L1
RB       -> R1
LT       -> L2
RT       -> R2

Left stick  -> Left stick
Right stick -> Right stick
D-pad       -> D-pad
Start       -> Start
Select      -> Select
```

The main controls have been confirmed working in games.

---

# PS3xPAD alpha001: LDD table issue

A newer PS3xPAD alpha build was also tested.

The plugin loaded successfully:

```text
XPAD Loaded!
```

and correctly parsed the custom device entry.

However, the debug log showed:

```text
LDD table full
```

The PS3 USB LDD registration table became full after many built-in device IDs were registered.

As a result, a custom device can be valid in `xpad_devices.txt` and still fail to register if it is processed too late.

## Suggested improvement

For future PS3xPAD builds, custom devices should be registered before lower-priority built-in IDs.

Conceptually:

```c
register_custom_devices();
register_high_priority_builtin_devices();
register_low_priority_builtin_devices();
```

The GameSir T4 Nova Lite could also be added directly to the built-in XInput device list:

```c
{0x3537, 0x1040, "GameSir T4 Nova Lite"}
```

---

# Other controllers

PS3xPAD can work with more than just the GameSir T4 Nova Lite.

The best candidates are controllers that Windows identifies as an Xbox/XInput-compatible device.

For example, if Windows shows:

```text
Xbox 360 Controller for Windows
```

and the device has:

```text
VID_1234
PID_5678
```

a possible PS3xPAD entry is:

```text
0x1234, 0x5678, Controller Name, XTYPE_XBOX360
```

This is not guaranteed, but it is a good first test for XInput-compatible hardware.

---

## Generic HID / DInput controllers

A controller that appears only as:

```text
HID-compliant game controller
```

may use a manufacturer-specific HID report.

In that case, adding only VID/PID may not be enough.

This is exactly why the GameSir T4 Nova Lite works much better in:

```text
3537:1040
XInput
```

than in:

```text
3537:1041
HID / DInput
```

---

# Find VID/PID on Windows

Connect the controller in the mode you want to test.

Open PowerShell:

```powershell
Get-PnpDevice -PresentOnly |
Where-Object {$_.InstanceId -match 'VID_.*PID_'} |
Where-Object {$_.FriendlyName -match 'Controller|Gamepad|HID|Xbox|GameSir'} |
Format-List FriendlyName,InstanceId
```

Look for:

```text
VID_XXXX&PID_YYYY
```

For the GameSir T4 Nova Lite in XInput mode:

```text
USB\VID_3537&PID_1040&MI_00
```

---

# Test DInput buttons on Windows

Run:

```text
joy.cpl
```

Open the controller properties and press each physical button.

This is useful for documenting raw HID/DInput behavior.

---

# Compatibility status

## GameSir T4 Nova Lite

```text
USB wired XInput:
✅ Working

Original 2.4 GHz dongle:
✅ Working

PS3 games:
✅ Working

PS3 HEN boot:
✅ Working

VID:PID wired XInput:
3537:1040

VID:PID HID/DInput:
3537:1041
```

### Still worth documenting

```text
PS/Home behavior
Rumble behavior
Dongle VID/PID
Compatibility across additional PS3 games
Compatibility on CFW
```

---

# Contributing

If you test another controller, open an Issue and include:

```text
Controller:
Manufacturer:
Connection:
Mode / LED:

VID:
PID:
Windows FriendlyName:

PS3 model:
Firmware:
HEN / CFW:
PS3xPAD version:

xpad_devices.txt entry:

Works in XMB?
Works in games?
Analog sticks?
D-pad?
Face buttons?
L1/R1?
L2/R2?
PS/Home?
Rumble?
```

Please only mark a controller as **confirmed compatible** after testing it on real PS3 hardware.

---

# Credits

PS3xPAD belongs to its original developers and contributors.

This repository documents community compatibility tests, configurations, troubleshooting, and hardware findings for modern controllers on PlayStation 3.
