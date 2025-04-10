# Ability Foundry Bluetooth Buddy Button Project

## Included Files
This repository contains everything you need to build your own Buddy Button:

- `/Buddy Button Instructions.md` — You are reading it now.
- `/assets/buddy_button.ino` — Arduino sketch for controlling the button’s behavior
- `/assets/SLDPRTs/` — SolidWorks files for the top, bottom, and base components (`bb-top.SLDPRT`, `bb-bottom.SLDPRT`, `bb-base.SLDPRT`)
- `/assets/STLs/` — Exported STL versions for easy 3D printing
- `/Parts List.txt` — Links and descriptions for all recommended components

## Table of Contents
- [Overview](#overview)
- [Hardware Components](#hardware-components)
- [Mechanical Design](#mechanical-design)
- [Electronics Setup](#electronics-setup)
- [Code Explanation](#code-explanation)
- [How to Upload the Code](#how-to-upload-the-code)
- [Usage](#usage)
- [Future Improvements](#future-improvements)
- [References](#references)

---

## Overview
The **Buddy Button** is a customizable, accessible Bluetooth-enabled button designed for users with motor disabilities or for use in maker projects. It combines a tactile, 3D-printed enclosure with internal electronics capable of sending **wireless HID signals** (like keypresses) to a phone, tablet, or computer. Key features include:

- A **mechanical spring-loaded design** that gives responsive feedback.
- A **NeoPixel RGB LED** that indicates status (e.g., charging, pairing, low battery).
- **Bluetooth HID support** using the Adafruit Feather nRF52 Bluefruit LE, allowing the button to act like a wireless keyboard or mouse.
- **Rechargeable power** using a small **LiPo battery** (150–500mAh).
- **Modular customization** options such as different button tops, textures, and spring sensitivities.

### Example Use Cases
- Assistive tech for users needing a larger or more responsive external button.
- DIY projects where Bluetooth control is needed via a tactile input.
- Classroom demos for HID/Bluetooth hardware projects.

### Key Parts Used
- [**Adafruit Feather nRF52 Bluefruit LE**](https://www.adafruit.com/product/3406) — BLE microcontroller with HID support  
- [**LiPo Batteries - 150mAh**](http://www.adafruit.com/product/1317) and [500mAh**](https://www.adafruit.com/product/1578) — rechargeable power sources  
- [**RGB Smart LED (NeoPixel)**](https://www.adafruit.com/product/1260) — status indication  
- [**Spring (McMaster #9657K289)**](https://www.mcmaster.com/9657k289) — provides resistance and travel in button press  
- [**Feather Header Kit**](http://www.adafruit.com/product/2886) and [**Stacking Headers**](http://www.adafruit.com/product/2830) — to mount components cleanly inside the case

This modular design allows for experimentation and refinement across mechanical and electronic domains. The current iteration is Version 5, which uses a twist-to-lock mechanism and a fully embedded rechargeable system .

---

## Hardware Components
| Item | Description | Qty | Cost |
|------|-------------|-----|------|
| [Adafruit Feather nRF52 Bluefruit LE](https://www.adafruit.com/product/3406) | BLE HID microcontroller | 1 | $24.95 |
| [Feather Header Kit](http://www.adafruit.com/product/2886) | 12-pin and 16-pin male headers | 1 | $0.95 |
| [Feather Stacking Headers](http://www.adafruit.com/product/2830) | Female headers for stacking | 1 | $1.25 |
| [LiPo Battery - 3.7v 150mAh](http://www.adafruit.com/product/1317) | Rechargeable battery | 1 | $5.95 |
| [LiPo Battery - 3.7v 500mAh](https://www.adafruit.com/product/1578) | Alternative for longer runtime | 1 | $7.95 |
| [RGB Smart LED](https://www.adafruit.com/product/1260) | Status indicator light | 1 | $6.50 |
| [Spring (McMaster #9657K289)](https://www.mcmaster.com/9657k289) | Tactile feedback mechanism | 1 | $1.00 |
| 3D Printed Housing | Top and bottom shell | 1 | ~$2.00 (varies) |

Total estimated cost per unit: **$48.55**

---

## Mechanical Design

The mechanical design consists of:

- **Top Half**: Moves vertically when pressed. Contains a groove and locking tabs to allow travel and retention.
- **Bottom Half**: Holds the electronics and spring. Designed with cutouts for lock tabs and spring supports.

STL files for 3D printing are located in `/assets/STLs`. Original SolidWorks files are in `/assets/SLDPRTs`.

### Design Iterations
- **Version 3**: Reduced wall thickness to 1.5mm, improved space economy.
- **Version 4**: Added a twist-lock mechanism; adjusted tolerances for tighter fits.
- **Version 5**: Refined locking system, added a track-based twist-to-lock system with 2mm travel.

Wall thickness and spring support dimensions were iteratively refined for structural integrity without excess bulk. Design feedback was gathered by testing spring rigidity and assembly friction (see design notes in `/Parts List.txt` and source files).

---

## Electronics Setup

1. **Microcontroller**: Adafruit Feather nRF52
2. **Power**: LiPo battery connected to JST port (built-in charging circuit used)
3. **LED**: NeoPixel on pin D6, powered by 3.3V and grounded
4. **Battery Monitoring**: Analog pin A7 reads battery voltage through a voltage divider
5. **Button Input**: Momentary switch connects to a digital input pin

---

## Code Explanation

**File**: `/assets/buddy_button.ino`

### Battery Voltage Reading
```cpp
#define VBAT_PIN          (A7)
#define VBAT_MV_PER_LSB   (0.73242188F)
#define VBAT_DIVIDER      (0.71275837F)
#define VBAT_DIVIDER_COMP (1.403F)
```
These constants allow the analog input to read and compute the real battery voltage.

### BLE HID Setup
```cpp
BLEUart bleuart;
BLEHidAdafruit blehid;
BLEDis bledis;
```
These initialize the HID services for the device to act like a Bluetooth keyboard/mouse.

### LED Setup
```cpp
Adafruit_NeoPixel strip = Adafruit_NeoPixel(60, PIN, NEO_GRB + NEO_KHZ800);
```
This sets up the NeoPixel strip (or single LED). Adjust number as needed.

### Loop Logic
In `loop()`, it checks BLE connections, reads the button state, updates LED colors, and triggers HID actions.

---

## How to Upload the Code

1. Install the **Arduino IDE**.
2. Add **Adafruit nRF52** boards via the Board Manager.
3. Install required libraries:
   - Adafruit Bluefruit nRF52
   - Adafruit NeoPixel
4. Connect the Feather to USB and select it under **Tools > Port**.
5. Open `/assets/buddy_button.ino` and click **Upload**.

---

## Usage

1. **Power On**: Plug in a LiPo battery or USB.
2. **Bluetooth Pairing**: Look for `Bluefruit52` on your phone/tablet/computer and pair.
3. **HID Activation**: Press the button to send key presses or other actions (customize in code).
4. **LED Status**: NeoPixel changes color based on charge/pairing/state.

---

## Future Improvements

- Slimmer housing with even smaller battery
- Software configuration to change actions
- Stronger or softer springs depending on user feedback
- Optional wired version for simpler setups
- Improved app integration for iOS/Android

---

## References

- [Adafruit Feather nRF52 Guide](https://learn.adafruit.com/bluefruit-nrf52-feather-learning-guide/downloads)
- [NeoPixel LED Downloads](https://learn.adafruit.com/flora-rgb-smart-pixels/downloads)
