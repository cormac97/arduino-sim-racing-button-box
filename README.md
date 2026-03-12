# Sim Racing Button Box

A custom sim racing button box built around an Arduino Nano, with a 
self-designed enclosure created in Onshape and printed on a Bambu Lab A1.
Presents to Windows as a USB HID joystick — no drivers needed, works 
plug-and-play with iRacing and Assetto Corsa Rally.

## Hardware

- Arduino Nano
- 5 push buttons
- 9 two-way momentary switches (each counts as 2 inputs)
- 1 on/off toggle switch
- 3 rotary encoders (each direction = 1 button press = 6 virtual buttons)
- Custom enclosure: designed in Onshape, printed in PLA on Bambu Lab A1

## How It Works

All buttons are wired into a 6×5 matrix (25 button inputs total). The 3 
rotary encoders add 6 virtual buttons (clockwise and counter-clockwise 
each register as a separate button press), bringing the total to 31 
mappable inputs.

The Arduino uses the Keypad library to scan the matrix and the Joystick 
library to present the device to Windows as a USB HID joystick. No 
custom drivers are needed — the OS sees it as a standard game controller 
and it appears immediately in iRacing and Assetto Corsa for button mapping.

Rotary encoder direction is decoded using a state machine lookup table 
for reliable, debounce-free detection.

## Inputs Summary

| Input Type | Count | Button IDs |
|---|---|---|
| Push buttons & switches | 25 | 0–24 |
| Rotary encoder CCW | 3 | 25, 27, 29 |
| Rotary encoder CW | 3 | 26, 28, 30 |
| **Total** | **31** | |

## Libraries Required

- [Keypad](https://github.com/Chris--A/Keypad) by Mark Stanley & Alexander Brevig
- [Arduino Joystick Library](https://github.com/MHeironimus/ArduinoJoystickLibrary) 
  by Matthew Heironimus

Install both via Arduino IDE Library Manager before uploading.

## Uploading

1. Install both libraries above
2. Open `button_box.ino` in Arduino IDE
3. Set board to **Arduino Nano** and select the correct port
4. Upload

The device will appear in Windows as a joystick immediately on first 
connection. Open **Game Controllers** (joy.cpl) to verify all inputs.

## Enclosure

The enclosure was designed from scratch in Onshape to fit the specific 
layout of buttons and encoders. Printed in PLA on a Bambu Lab A1.

<!-- Add photo here once available -->

## What I Learned

First time designing a wiring matrix from scratch — working out the 
row/column layout to minimise wire runs and fit the physical button 
layout was the most involved part. Getting reliable rotary encoder 
detection without spurious inputs led me to the state machine approach, 
which was a good introduction to that pattern.

## Compatibility

Tested with iRacing and Assetto Corsa Rally. Should work with any 
sim that supports USB HID joystick input.
