# OpenLCB ESP32 28-Input Node

An OpenLCB (NMRAnet) node built on an ESP32 microcontroller, expanded to support a total of **28 configurable inputs**. It uses 14 direct pins on the ESP32 and an additional 14 inputs handled via an **MCP23017 I2C I/O expander**. Configuration and event generation are managed seamlessly through JMRI via the integrated Configuration Description Information (CDI) XML.

---

## Features

- **28 Total Inputs:**
  - **14 Direct ESP32 Pins** (Split into two groups of 7).
  - **14 MCP23017 Expander Pins** (7 on Port A, 7 on Port B, split into two groups of 7).
- **Safety Outputs:** MCP23017 Port A pin 7 and Port B pin 15 are configured as safe, static `LOW` outputs.
- **Structured CDI in JMRI:** Organized into 4 clean groups of 7 inputs each for intuitive configuration.
- **Flexible Input Types:** Supports Active High, Active Low, Pull-ups, and Toggle (falling edge) modes with programmable on/off delays.
- **Robust Debouncing:** Built-in 20ms polling loop with a 4-cycle debounce threshold.

---

## Hardware Pin Mapping

### 1. ESP32 Direct Inputs (14 Pins)
Defined in your `Boards.h` / `Config.h` setup (typically: `D4, D16, D17, D5, D18, D19, D13, D12, D14, D27, D26, D25, D33, D32`).
- **Group 1 (Inputs 0–6):** ESP32 Direct Inputs Part 1
- **Group 2 (Inputs 7–13):** ESP32 Direct Inputs Part 2

### 2. MCP23017 I2C Expander (Address: `0x20`)
- **Group 3 (Inputs 14–20):** MCP23017 Port A (Pins GPA0 through GPA6). 
  - *Note:* GPA7 (Pin 7) is configured as an output driven `LOW` for safety.
- **Group 4 (Inputs 21–27):** MCP23017 Port B (Pins GPB0 through GPB6). 
  - *Note:* GPB7 (Pin 15) is configured as an output driven `LOW` for safety.

---

## Dependencies

Make sure you have the following libraries installed in your Arduino IDE:
1. **OpenLCB Arduino Library** (including core headers like `OpenLCBHeader.h`)
2. **Wire Library** (Built-in for ESP32 I2C)
3. **MCP23017 Library** by Bertrand Lemasle (`<MCP23017.h>`)

---

## Configuration & Setup

1. **Hardware Connections:**
   - Connect the I2C bus: ESP32 **SDA (GPIO 21)** and **SCL (GPIO 22)** to the MCP23017 SDA and SCL pins.
   - Power the MCP23017 and tie address pins (A0, A1, A2) to GND to set address `0x20`.
2. **Upload Sketch:** Open the `.ino` sketch in the Arduino IDE, select your ESP32 board, and upload.
3. **JMRI Configuration:**
   - Open JMRI (e.g., DecoderPro).
   - Open the **CDI (Configuration Description Information)** for the node.
   - You will see the inputs cleanly separated into 4 groups of 7:
     - *ESP32 Direct Inputs (Group 1)*
     - *ESP32 Direct Inputs (Group 2)*
     - *MCP23017 Port A Inputs*
     - *MCP23017 Port B Inputs*
   - Assign input types, descriptions, and EventIDs as needed.
