Trkey: Custom Micropad Configurator Project
Trkey is a comprehensive open-source solution designed to empower users with full control over their 3x3 micropad keyboards. This project integrates a user-friendly web-based configurator with custom firmware for ESP32-C3 microcontrollers, providing an end-to-end customization experience.
Project Overview
The Trkey project allows you to:
 * Design your micropad's keymap through an intuitive drag-and-drop web interface.
 * Generate custom shortcuts with the help of an integrated AI.
 * Manage macros for complex key sequences.
 * Test your key presses in real-time.
 * Export your configuration as a QMK-compatible JSON file.
 * Directly upload the configuration to your XIAO ESP32C3 via USB (using the Web Serial API).
 * Flash the provided firmware to your ESP32-C3, enabling it to act as a keyboard over both USB and Bluetooth.
Key Features
Web Application (Software)
 * Visual Keymap Configuration: Drag-and-drop interface for assigning shortcuts to a 3x3 virtual keyboard.
 * Layer Management: Support for configuring multiple keymap layers.
 * Extensive Shortcut Library: Pre-defined common shortcuts for Windows, macOS, Linux, Android, and iPad.
 * AI-Powered Shortcut Generation: Generate custom shortcut ideas based on natural language prompts.
 * Macro Editor: Create, edit, and delete custom key sequence macros.
 * Real-time Key Tester: Diagnose key presses by displaying key codes and values.
 * Profile Management: Save and load configurations to/from local browser storage.
 * QMK JSON Integration: Export configurations as QMK-compatible JSON; import JSON directly.
 * Direct Device Upload: Flash configurations to compatible microcontrollers via Web Serial API.
 * Responsive Design: Optimized for seamless use across various devices, from iPads to laptops.
Micropad Firmware (XIAO ESP32C3)
 * Dual Connectivity: Functions as a keyboard via both USB HID and Bluetooth Low Energy (BLE) HID.
 * 3x3 Key Matrix Scanning: Efficiently reads inputs from a 3-row by 3-column key matrix.
 * XIAO ESP32C3 Optimized: Configured for specific GPIO pins (1-6) on the XIAO ESP32C3.
 * Basic Debouncing: Includes a simple debouncing mechanism for reliable key detection.
 * Serial Debugging: Provides serial output for development and troubleshooting.
Compatibility
Trkey Web Application
The web application's user interface and core features are broadly compatible with modern web browsers. The "Upload to Device" feature, however, specifically requires the Web Serial API.
 * Windows (Desktop): Fully supported with Google Chrome or Microsoft Edge.
 * macOS (Desktop): Fully supported with Google Chrome or Microsoft Edge.
 * Linux (Desktop): Fully supported with Google Chrome or Microsoft Edge.
 * Android Tablets: UI is responsive; "Upload to Device" supported with Google Chrome (requires USB OTG and serial port access).
 * iPad/iOS Devices: UI is responsive; Web Serial API is NOT supported by Safari or other browsers on iOS/iPadOS. Direct device upload is not possible.
Trkey Micropad Firmware (XIAO ESP32C3)
Once flashed, the micropad acts as a standard HID keyboard, ensuring broad compatibility.
 * Windows (Desktop), macOS (Desktop), Linux (Desktop): Fully compatible as both USB HID and Bluetooth LE HID keyboards.
 * Android Tablets: Fully compatible as USB HID (via OTG) and Bluetooth LE HID keyboards.
 * iPad/iOS Devices: Fully compatible as USB HID (via adapter) and Bluetooth LE HID keyboards.
Firmware Upload Process: The firmware itself is uploaded using the Arduino IDE, which is supported on Windows, macOS, and Linux.
Getting Started
 * Hardware Setup: Connect your 3x3 key matrix to your XIAO ESP32C3 (Rows: GPIO1, GPIO2, GPIO3; Columns: GPIO4, GPIO5, GPIO6).
 * Firmware Flash:
   * Install Arduino IDE and ESP32 board definitions.
   * Install BleKeyboard and USBComposite libraries.
   * Open the firmware sketch (XIAO_ESP32C3_Micropad_Firmware.ino), select XIAO ESP32C3 board, and upload.
 * Web App Access: Open the web application's index.html file in a compatible web browser (Chrome/Edge recommended).
 * Configure: Use the web app's intuitive interface to design your keymap, create macros, and generate AI shortcuts.
 * Deploy: Export your configuration as JSON or use the "Upload to Device" feature to flash it directly to your micropad.
Technologies Used
 * Web Application: React, Tailwind CSS, Google Gemini API, Web Serial API.
 * Firmware: Arduino IDE, ESP32 Arduino Core, BleKeyboard library, USBHIDKeyboard library.
