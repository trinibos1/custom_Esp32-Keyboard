
Trkey Micropad Firmware for XIAO ESP32C3
This repository contains Arduino-based firmware for a 3x3 key matrix micropad using the Seeed Studio XIAO ESP32C3. The firmware supports both USB and Bluetooth Low Energy (BLE) HID, allowing the device to function as a wireless or wired keyboard.

✨ Features
3×3 Key Matrix Scanning
Supports 9 momentary switches arranged in a 3-row by 3-column matrix.

Dual HID Connectivity (USB + BLE)
Sends keypresses over USB or BLE, letting your micropad function as a keyboard on PCs, tablets, or phones.

XIAO ESP32C3 Optimized
Tailored for GPIO pin capabilities and constraints of the Seeed Studio XIAO ESP32C3 board.

Basic Debouncing
Simple delay() used for debouncing. Easily replaceable with advanced software debouncing if needed.

Serial Debugging
Outputs useful logs via Serial Monitor for development and testing.

🛠️ Hardware Requirements
Microcontroller: Seeed Studio XIAO ESP32C3

Key Matrix: 3×3 grid of momentary push buttons

Wiring Setup:

Function	XIAO ESP32C3 GPIO
Row 1	GPIO1
Row 2	GPIO2
Row 3	GPIO3
Column 1	GPIO4
Column 2	GPIO5
Column 3	GPIO6

Note: Rows should be configured as INPUT_PULLUP. When a button is pressed, it should pull the row pin LOW.

💻 Software Requirements
Arduino Setup
Install the Arduino IDE
Download from arduino.cc

Add ESP32 Board Support

Go to File > Preferences

Add this URL to Additional Board Manager URLs:

bash
Copy
Edit
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
Then go to Tools > Board > Boards Manager, search for "esp32", and install it.

Required Libraries
Install these via Sketch > Include Library > Manage Libraries...:

BleKeyboard by T-vK

USBComposite (usually included with ESP32 Arduino core)

🚀 Getting Started
Open the Sketch
Load XIAO_ESP32C3_Micropad_Firmware.ino in the Arduino IDE.

Select Board
Go to Tools > Board > ESP32 Arduino > Seeed XIAO ESP32C3.

Select Port
Connect the XIAO ESP32C3 via USB-C and select the correct COM port.

Upload the Firmware
Click the "Upload" (→) button in the toolbar.

Monitor Output
Use Tools > Serial Monitor at 115200 baud to view debug output.

⚙️ How It Works
Matrix Scanning
The firmware activates each column (sets it LOW one at a time), and reads each row's state.

Button Detection
If a button is pressed, it pulls a row pin LOW while its column is active.

State Change Tracking
It compares the current state to the previous state (lastButtonState[][]) to detect presses/releases.

HID Output
Key events are sent over both BLE and USB using .press() and .release() commands.

Keymap
By default, keys '1' through '9' are mapped in the grid. You can customize this.

🧩 Customization
Device Name (Bluetooth)
Change the #define BLE_KEYBOARD_NAME at the top of the sketch.

Key Mapping
Modify the KEYMAP[][] array to send your preferred characters or HID keycodes (e.g., KEY_F1, KEY_MEDIA_VOLUME_UP).

Debouncing
For better performance, replace delay(10) with a software debouncing library like Bounce2.

🔌 Future Integration: Trkey Web App
This firmware is designed for future compatibility with the Trkey web app, where users can dynamically remap keys and manage settings through a GUI interface.
