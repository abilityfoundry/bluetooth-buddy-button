# 🟢 Buddy Button

**Open-Source Accessibility. One Click at a Time.**

The Buddy Button is an open-source Bluetooth-enabled switch designed for accessibility. Built to be 3D printed and easily assembled, this device enables users with limited mobility to interact with computers, tablets, or phones using a single press.

Created by [**Ability Foundry**](https://github.com/abilityfoundry), this project is part of our mission to build inclusive, impactful, and low-cost assistive technology tools for everyday use.

---

## 📸 3D Renders

Visual previews of the Buddy Button housing and how it fits together:

| Bottom View | Top View | Assembly View |
|-------------|----------|----------------|
| <img src="https://github.com/abilityfoundry/bluetooth-buddy-button/blob/main/assets/images/01-bottom.png" height="200"/> | <img src="https://github.com/abilityfoundry/bluetooth-buddy-button/blob/main/assets/images/02-top.png" height="200"/> | <img src="https://github.com/abilityfoundry/bluetooth-buddy-button/blob/main/assets/images/03-assembled.png" height="200"/> |

- **Bottom View**: Shows the internal mounting features for components.
- **Top View**: Displays the enclosure’s inner surface and guiding features.
- **Assembly View**: Illustrates how the top and bottom parts align during assembly.

---

## 🎯 What It Does

- 🖱️ Sends **wireless Bluetooth HID signals** (like keypresses)  
- 🔋 Runs on a **rechargeable LiPo battery**  
- 🌈 Uses a **NeoPixel RGB LED** for visual status  
- 🧩 Built to be **modular and customizable** (shape, color, sensitivity)  
- 🛠️ Easy to assemble using **3D-printed parts** and off-the-shelf components  

---

## 🧱 What's in This Repo

- `Buddy Button Instructions.md` – Complete build instructions  
- `/assets/buddy_button.ino` – Arduino code  
- `/assets/STLs/` – 3D-printable STL files  
- `/assets/SLDPRTs/` – Editable SolidWorks CAD files  

---

## 🛠️ Requirements

- Adafruit Feather nRF52 Bluefruit LE  
- 150–500mAh LiPo Battery  
- RGB NeoPixel  
- Spring (McMaster #9657K289)  
- Momentary switch  
- Basic soldering + 3D printer  

Full list with prices and links is in the [Hardware Components](https://github.com/abilityfoundry/bluetooth-buddy-button/blob/main/Buddy-Button-Instructions.md) section of the instructions.

---

## 🚀 Get Started

1. Print the button housing from the STL files  
2. Order components (linked in the guide)  
3. Flash the Arduino code to the Feather  
4. Assemble, pair via Bluetooth, and press to interact

---

## 🤝 Contribute

Have ideas for improving the design? Want to help make assistive tech more accessible and affordable? We welcome contributions! Open an issue or submit a pull request.

---

**Ability Foundry**  
> Building technology for a more inclusive future.  
> https://github.com/abilityfoundry
