Trkey: Custom Micropad Configurator Project
Trkey is a comprehensive open-source project designed to empower users to customize and control their 3x3 micropad keyboards. It consists of a web-based configurator application and a corresponding firmware for ESP32-C3 microcontrollers, working in tandem to provide a complete customization solution.

Features
End-to-End Customization: Configure your micropad using an intuitive web interface and flash the generated firmware to your device.

Customizable Keymap:

Visually configure your 3x3 micropad layout with a realistic keycap appearance.

Assign and reorder shortcuts using a drag-and-drop interface.

Displays clear, descriptive names for assigned functions (e.g., "Undo" for "Ctrl+Z").

Supports multiple layers for extended functionality.

Dynamically displays the micropad layout based on configuration status.

Extensive Shortcut Library:

Includes predefined categories of common keyboard shortcuts.

Allows for direct editing of existing shortcut definitions.

Enables creation and addition of new custom shortcuts.

Programmable Macros:

Create, edit, and delete custom macro sequences to automate complex tasks.

Real-time Key Testing:

A dedicated tool within the web app to test physical keyboard inputs, displaying key values and codes for diagnostic purposes.

Profile Management:

Save and load your complete micropad configurations (keymap, macros, etc.) to and from your browser's local storage.

Firmware Integration:

QMK JSON Export: Export your configured keymap as a QMK-compatible JSON file from the web app.

Direct Device Upload: Upload configurations directly to compatible microcontrollers (e.g., XIAO ESP32C3) via the Web Serial API from the web app.

JSON Import: Import existing QMK-style JSON keymap files into the web app by pasting them into a text area.

Dual Connectivity (USB & BLE HID): The firmware enables the micropad to function as a keyboard over both USB and Bluetooth Low Energy (BLE) HID.

Matrix Scanning: Firmware includes logic for scanning a 3x3 key matrix.

Intuitive Design:

Features a sleek, dark-themed, and responsive user interface for the web application.

Provides clear navigation across different configuration sections.

Utilizes custom modal dialogs for a seamless user experience.

Project Components
Trkey Web Application (React):

A front-end application built with React and Tailwind CSS.

Provides the graphical user interface for configuring the micropad.

Handles saving/loading profiles, managing shortcuts and macros, and interacting with the device for firmware upload/JSON import/export.

Trkey Micropad Firmware (Arduino for XIAO ESP32C3):

An Arduino sketch designed for the Seeed Studio XIAO ESP32C3 microcontroller.

Enables the physical micropad to act as a keyboard.

Supports both USB and Bluetooth HID communication.

Includes basic matrix scanning logic for a 3x3 key matrix.

Getting Started
To get this project up and running, you'll need to set up both the web application and flash the firmware to your XIAO ESP32C3.

1. Hardware Setup (XIAO ESP32C3 & Key Matrix)
Seeed Studio XIAO ESP32C3: Ensure you have your microcontroller board.

3x3 Key Matrix: Connect your custom keypad with 9 momentary buttons.

Wiring Connections:

Row Pins (Inputs with Pull-ups): Connect your 3 matrix row lines to XIAO ESP32C3 GPIO1, GPIO2, and GPIO3.

Column Pins (Outputs): Connect your 3 matrix column lines to XIAO ESP32C3 GPIO4, GPIO5, and GPIO6.

Ensure your buttons are wired to pull the row pin LOW when pressed (e.g., one side to a column, other side to a row, and the row configured as INPUT_PULLUP).

2. Firmware Setup (XIAO ESP32C3)
Arduino IDE: Download and install the latest version from arduino.cc.

ESP32 Boards Manager:

In Arduino IDE, go to File > Preferences.

In "Additional Boards Manager URLs", add: https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json

Go to Tools > Board > Boards Manager....

Search for "esp32" and install the esp32 by Espressif Systems package.

Libraries: Install the following libraries via the Arduino Library Manager (Sketch > Include Library > Manage Libraries...):

BleKeyboard by T-vK (Search for "BleKeyboard")

USBComposite (This is typically included with the ESP32 Arduino core. If you encounter issues, ensure your ESP32 board package is up to date.)

Open the Sketch: Open the XIAO_ESP32C3_Micropad_Firmware.ino file (located in the esp32-firmware directory of this project) in your Arduino IDE.

Select Board: Go to Tools > Board > ESP32 Arduino and select XIAO ESP32C3.

Select Port: Connect your XIAO ESP32C3 to your computer via a USB-C cable. Go to Tools > Port and select the appropriate serial port.

Upload: Click the "Upload" button in the Arduino IDE toolbar to compile and flash the firmware to your XIAO ESP32C3.

Monitor: Open the Serial Monitor (Tools > Serial Monitor) with a baud rate of 115200 to see debug messages and key press detections.

3. Web Application Setup (React App)
Clone the Repository: If you haven't already, clone this entire GitHub repository to your local machine:

git clone https://github.com/your-username/trkey-micropad-configurator.git
cd trkey-micropad-configurator

Navigate to Web App: Go into the web application directory:

cd trkey-webapp # (or whatever you named your web app folder)

Install Dependencies: If this were a full React project, you would typically run:

npm install # or yarn install

(Note: For this specific project as generated, the React code is provided as a single file. You might need to set up a basic React development environment (like Create React App) and place the Configurator.js file within its src directory, or simply open the index.html if it's a self-contained HTML file with embedded React.)

Access the Application:

If it's a self-contained HTML file, simply open index.html in a modern web browser (Chrome or Edge recommended for Web Serial API support).

If you've set up a React development environment, run npm start (or yarn start) and access the app in your browser, usually at http://localhost:3000.

How to Use the Web Application
Navigate: Use the sidebar on the left to switch between different configuration tabs:

KEYMAP: Configure your 3x3 micropad's key assignments.

MACROS: Define and manage custom key sequences.

SAVE + LOAD: Manage your saved configuration profiles.

SETTINGS: Access advanced JSON import/export and device upload options.

KEY TESTER: Test key presses from your physical keyboard.

Configure Your Keymap (KEYMAP tab):

If the micropad grid is empty, a message will guide you to drag shortcuts.

Assign Shortcuts: Drag a shortcut chip from the "SHORTCUTS" pool (below the keymap) and drop it onto any keycap in the 3x3 grid. The keycap will update to show the shortcut's description.

Reorder Keys: Drag and drop existing keycaps within the 3x3 grid to rearrange your layout.

Layers: Use the layer buttons (0, 1, 2, 3) to configure different functions for your keys across multiple layers.

Manage Shortcuts (KEYMAP tab - SHORTCUTS section):

Edit: Click on a shortcut chip to edit its key combination. The description will automatically update if not explicitly set.

Add New: Click "+ Add Shortcut" to create a new custom shortcut with a key combination and a descriptive name.

Manage Macros (MACROS tab):

Click "+ Add New Macro" to create a new macro, providing a name and its key/text sequence.

Use "Edit" and "Delete" buttons to modify or remove existing macros.

Save & Load Profiles (SAVE + LOAD tab):

Save Profile: Saves your current configuration to your browser's local storage.

Load Profile: Retrieves a previously saved configuration from local storage.

QMK JSON Configuration (SETTINGS tab):

Export Keymap JSON: Downloads your 3x3 keymap as a QMK-compatible JSON file.

Upload Keymap to Device: Attempts to upload the generated JSON configuration to your connected micropad via USB.

Load JSON from Text Area: Paste a QMK-style JSON string into the text area to import a keymap.

Test Keys (KEY TESTER tab):

Navigate to this tab and press keys on your physical keyboard to see their detected values.

How the Firmware Works
The ESP32 firmware continuously scans the 3x3 key matrix to detect button presses and releases:

Column Activation: It iterates through each column, setting one column pin LOW at a time while keeping the others HIGH.

Row Reading: For the currently active (LOW) column, it reads the digital state of each row pin.

Button Detection: If a button is pressed, it creates a connection between the active column (LOW) and its corresponding row, pulling the row pin LOW.

State Change Detection: The lastButtonState array stores the previous state of each button. When a change is detected (from unpressed to pressed, or vice-versa), the appropriate HID command is sent.

HID Output: Key press (.press()) and key release (.release()) commands are sent over both the BLE (Bluetooth Low Energy) and USB HID interfaces, allowing the micropad to function as a standard keyboard for any connected computer or device.

Keymap: The KEYMAP array in the firmware is currently hardcoded for demonstration. In a full integration, this would be dynamically updated by the web application.

Customization
Web App:

Modify the presets object in the React code to change the default shortcut pool.

Adjust Tailwind CSS classes for visual customization.

Firmware:

BLE_KEYBOARD_NAME: Change the Bluetooth name of your micropad.

KEYMAP: Modify the hardcoded KEYMAP array for different default key assignments (though dynamic loading from the web app is the intended final state).

Debouncing: For more robust debouncing, consider advanced algorithms.

Technologies Used
React: JavaScript library for building the web application's user interface.

Tailwind CSS: A utility-first CSS framework for styling the web application.

Web Serial API: Enables communication between the web application and the microcontroller.

Arduino IDE: Development environment for the ESP32 firmware.

ESP32 Arduino Core: Provides the necessary tools and libraries for programming ESP32 boards with Arduino.

BleKeyboard Library: Enables Bluetooth HID functionality on ESP32.

USBHIDKeyboard Library: Enables USB HID keyboard functionality on ESP32.
