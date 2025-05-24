<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Trkey - Micropad Keymap Configurator"
    />
    <title>Trkey Configurator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Add this to your src/index.css */

        @keyframes spin {
          0% { transform: rotate(0deg); }
          100% { transform: rotate(360deg); }
        }

        .spinner {
          border: 4px solid rgba(255, 255, 255, 0.3);
          border-top: 4px solid #fff;
          border-radius: 50%;
          width: 50px;
          height: 50px;
          animation: spin 1s linear infinite;
        }

        /* Animation for random micropad button clicks */
        @keyframes button-click-pulse {
          0% { transform: scale(1); background-color: #3f3f46; } /* zinc-700 */
          50% { transform: scale(1.05); background-color: #ef4444; } /* red-500 */
          100% { transform: scale(1); background-color: #3f3f46; }
        }

        .micropad-button-active {
          animation: button-click-pulse 0.4s ease-in-out forwards; /* Apply pulse animation */
        }


        /* Basic Tailwind reset (if not already handled by Create React App) */
        @tailwind base;
        @tailwind components;
        @tailwind utilities;

        /* You can add any global styles here */
        body {
          margin: 0;
          font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
            'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
            sans-serif;
          -webkit-font-smoothing: antialiased;
          -moz-osx-font-smoothing: grayscale;
        }

        code {
          font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
            monospace;
        }

        /* New styles for Keyboard Tester */
        .keyboard-layout-grid {
          display: flex;
          flex-direction: column;
          align-items: center;
          padding: 1rem;
          background-color: #27272a; /* zinc-800 */
          border-radius: 0.5rem;
        }

        .keyboard-row {
          display: flex;
          gap: 0.25rem; /* Equivalent to gap-1 in Tailwind */
          margin-bottom: 0.25rem; /* Equivalent to mb-1 in Tailwind */
          justify-content: center;
        }

        .key-cap {
          background-color: #3f3f46; /* zinc-700 */
          border: 1px solid #52525b; /* zinc-600 */
          border-radius: 0.25rem;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          font-weight: bold;
          color: #a1a1aa; /* zinc-400 */
          transition: background-color 0.1s ease-in-out, color 0.1s ease-in-out;
          flex-shrink: 0; /* Prevent keys from shrinking */
          white-space: pre-wrap; /* Allow labels to wrap if needed */
          text-align: center;
          padding: 0.25rem; /* Add some padding inside key caps */
          box-sizing: border-box; /* Include padding in width/height */
          min-width: 40px; /* Base width */
          min-height: 40px; /* Base height */
        }

        .key-cap .key-label {
          line-height: 1; /* Adjust line height for multiline labels */
        }

        .key-pressed {
          background-color: #ef4444; /* red-500 */
          color: #ffffff; /* white */
          box-shadow: 0 0 8px rgba(239, 68, 68, 0.7); /* Red glow */
        }

        /* Adjustments for specific key widths */
        .key-cap.w-24 { width: 6rem; /* 40px * 1.5 */ }
        .key-cap.w-32 { width: 8rem; /* 40px * 2 */ }
        .key-cap.w-40 { width: 10rem; /* 40px * 2.5 */ }
        .key-cap.w-48 { width: 12rem; /* 40px * 3 */ }
        .key-cap.w-56 { width: 14rem; /* 40px * 3.5 */ }
        .key-cap.w-64 { width: 16rem; /* 40px * 4 */ }
        .key-cap.w-80 { width: 20rem; /* 40px * 5 */ }
        .key-cap.w-100 { width: 25rem; /* 40px * 6.25 */ }
        /* Add more as needed based on your key width multiples */
    </style>
</head>
<body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>

    <script type="module">
        import React, { useState, useEffect, useCallback } from 'https://esm.sh/react@18.2.0';
        import ReactDOM from 'https://esm.sh/react-dom@18.2.0/client';

        // Restructured presets to include both combo and description
        const presets = {
          "BASIC": [
            { combo: "M", description: "Move" },
            { combo: "V", description: "Via" },
            { combo: "R", description: "Rotate" },
            { combo: "Del", description: "Delete" },
            { combo: "Ctrl+Z", description: "Undo" },
            { combo: "Ctrl+Y", description: "Redo" },
            { combo: "F1", description: "Help" },
            { combo: "F2", description: "Rename" },
            { combo: "F3", description: "Search" },
            { combo: "L", description: "Line" },
            { combo: "E", description: "Extrude" },
            { combo: "P", description: "Project" },
            { combo: "C", description: "Circle" },
            { combo: "Q", description: "Press/Pull" },
            { combo: "X", description: "Cut" },
            { combo: "S", description: "Sketch" },
            { combo: "T", "description": "Text" },
            { combo: "Ctrl+C", description: "Copy" },
            { combo: "Ctrl+V", description: "Paste" },
            { combo: "Ctrl+Z", description: "Undo" }, // Duplicate, but kept for consistency with original presets
            { combo: "Ctrl+X", description: "Cut" }, // Duplicate, but kept for consistency with original presets
            { combo: "Ctrl+S", description: "Save" }, // Duplicate, but kept for consistency with original presets
            { combo: "Ctrl+Shift+G", description: "Ungroup" },
            { combo: "Alt+Shift+B", description: "Bring to Back" },
            { combo: "Ctrl+D", description: "Duplicate" },
            { combo: "Ctrl+Alt+K", description: "Lock" },
            { combo: "Ctrl+P", description: "Command Palette" },
            { combo: "Ctrl+Shift+P", description: "Show All Commands" },
            { combo: "Ctrl+F", description: "Find" },
            { combo: "Alt+Shift+F", description: "Format Document" },
          ],
          "MEDIA": [
            { combo: "KC_MPRV", description: "Prev Track" },
            { combo: "KC_MNXT", description: "Next Track" },
            { combo: "KC_MPLY", description: "Play/Pause" },
            { combo: "KC_MUTE", description: "Mute" },
            { combo: "KC_VOLU", description: "Volume Up" },
            { combo: "KC_VOLD", description: "Volume Down" },
          ],
          "MACRO": [
            { combo: "MACRO_1", description: "Macro 1" },
            { combo: "MACRO_2", description: "Macro 2" },
            { combo: "MACRO_3", description: "Macro 3" },
          ],
          "LAYERS": [
            { combo: "TG(1)", description: "Toggle Layer 1" },
            { combo: "MO(1)", description: "Momentary Layer 1" },
            { combo: "TO(0)", description: "To Layer 0" },
          ],
          "SPECIAL": [
            { combo: "KC_PWR", description: "Power" },
            { combo: "KC_SLEP", description: "Sleep" },
            { combo: "KC_WAKE", description: "Wake" },
          ],
          "QMK LIGHTING": [
            { combo: "RGB_TOG", description: "RGB Toggle" },
            { combo: "RGB_MOD", description: "RGB Mode" },
            { combo: "RGB_HUI", description: "Hue Inc" },
            { combo: "RGB_HUD", description: "Hue Dec" },
            { combo: "RGB_SAI", description: "Sat Inc" },
            { combo: "RGB_SAD", description: "Sat Dec" },
            { combo: "RGB_VAI", description: "Val Inc" },
            { combo: "RGB_VAD", description: "Val Dec" },
          ]
        };

        // Initial grid where all cells are null, indicating an unconfigured state
        const initialGrid = Array(3).fill().map(() => Array(3).fill({ tap: null, hold: null }));

        // Modal component for displaying messages
        const Modal = ({ show, title, message, onClose }) => {
          if (!show) return null;

          return (
            <div className="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center p-4 z-50">
              <div className="bg-zinc-800 text-white p-6 rounded-lg shadow-xl max-w-sm w-full border-2 border-red-500">
                <h3 className="text-xl font-bold mb-4 text-red-400">{title}</h3>
                {message && <p className="mb-4">{message}</p>}
                <div className="flex justify-end">
                  <button
                    onClick={onClose}
                    className="bg-red-600 hover:bg-red-700 px-4 py-2 rounded-xl shadow-lg transition-colors duration-200"
                  >
                    OK
                  </button>
                </div>
              </div>
            </div>
          );
        };

        // Keyboard Layout Data (Simplified for a standard QWERTY layout)
        // This can be expanded for more complex layouts and key sizes
        const keyboardLayout = [
          // Row 1
          [
            { code: 'Escape', label: 'Esc', width: 1.5 },
            { code: 'F1', label: 'F1' }, { code: 'F2', label: 'F2' }, { code: 'F3', label: 'F3' }, { code: 'F4', label: 'F4' },
            { code: 'F5', label: 'F5' }, { code: 'F6', label: 'F6' }, { code: 'F7', label: 'F7' }, { code: 'F8', label: 'F8' },
            { code: 'F9', label: 'F9' }, { code: 'F10', label: 'F10' }, { code: 'F11', label: 'F11' }, { code: 'F12', label: 'F12' },
            { code: 'PrintScreen', label: 'Print' }, { code: 'ScrollLock', label: 'Scroll' }, { code: 'Pause', label: 'Pause' }
          ],
          // Row 2 (Number Row)
          [
            { code: 'Backquote', label: '`\n~' }, { code: 'Digit1', label: '1\n!' }, { code: 'Digit2', label: '2\n@' },
            { code: 'Digit3', label: '3\n#' }, { code: 'Digit4', label: '4\n$' }, { code: 'Digit5', label: '5\n%' },
            { code: 'Digit6', label: '6\n^' }, { code: 'Digit7', label: '7\n&' }, { code: 'Digit8', label: '8\n*' },
            { code: 'Digit9', label: '9\n(' }, { code: 'Digit0', label: '0\n)' }, { code: 'Minus', label: '-\n_' },
            { code: 'Equal', label: '=\n+' }, { code: 'Backspace', label: 'Backspace', width: 2.5 }
          ],
          // Row 3 (QWERTY Row)
          [
            { code: 'Tab', label: 'Tab', width: 1.75 }, { code: 'KeyQ', label: 'Q' }, { code: 'KeyW', label: 'W' },
            { code: 'KeyE', label: 'E' }, { code: 'KeyR', label: 'R' }, { code: 'KeyT', label: 'T' },
            { code: 'KeyY', label: 'Y' }, { code: 'KeyU', label: 'U' }, { code: 'KeyI', label: 'I' },
            { code: 'KeyO', label: 'O' }, { code: 'KeyP', label: 'P' }, { code: 'BracketLeft', label: '[\n{' },
            { code: 'BracketRight', label: ']\n}' }, { code: 'Backslash', label: '\\\n|', width: 1.5 }
          ],
          // Row 4 (ASDF Row)
          [
            { code: 'CapsLock', label: 'Caps Lock', width: 2.25 }, { code: 'KeyA', label: 'A' }, { code: 'KeyS', label: 'S' },
            { code: 'KeyD', label: 'D' }, { code: 'KeyF', label: 'F' }, { code: 'KeyG', label: 'G' },
            { code: 'KeyH', label: 'H' }, { code: 'KeyJ', label: 'J' }, { code: 'KeyK', label: 'K' },
            { code: 'KeyL', label: 'L' }, { code: 'Semicolon', label: ';\n:' }, { code: 'Quote', label: "'\n\"" },
            { code: 'Enter', label: 'Enter', width: 2.25 }
          ],
          // Row 5 (ZXC Row)
          [
            { code: 'ShiftLeft', label: 'Shift', width: 2.75 }, { code: 'KeyZ', label: 'Z' }, { code: 'KeyX', label: 'X' },
            { code: 'KeyC', label: 'C' }, { code: 'KeyV', label: 'V' }, { code: 'KeyB', label: 'B' },
            { code: 'KeyN', label: 'N' }, { code: 'KeyM', label: 'M' }, { code: 'Comma', label: ',\n<' },
            { code: 'Period', label: '.\n>' }, { code: 'Slash', label: '/\n?' }, { code: 'ShiftRight', label: 'Shift', width: 2.25 }
          ],
          // Row 6 (Bottom Row)
          [
            { code: 'ControlLeft', label: 'Ctrl', width: 1.5 }, { code: 'MetaLeft', label: 'Win', width: 1.25 },
            { code: 'AltLeft', label: 'Alt', width: 1.25 }, { code: 'Space', label: 'Space', width: 6.25 },
            { code: 'AltRight', label: 'Alt', width: 1.25 }, { code: 'MetaRight', label: 'Win', width: 1.25 },
            { code: 'ContextMenu', label: 'Menu' }, { code: 'ControlRight', label: 'Ctrl', width: 1.5 }
          ],
          // Numpad and Arrow Keys (simplified)
          [
            { code: 'Numpad7', label: '7', row: 'numpad', col: 1 }, { code: 'Numpad8', label: '8', row: 'numpad', col: 2 }, { code: 'Numpad9', label: '9', row: 'numpad', col: 3 },
            { code: 'NumpadSubtract', label: '-', row: 'numpad', col: 4 },
            { code: 'Home', label: 'Home', row: 'arrow', col: 1 }, { code: 'ArrowUp', label: '↑', row: 'arrow', col: 2 }, { code: 'PageUp', label: 'PgUp', row: 'arrow', col: 3 }
          ],
          [
            { code: 'Numpad4', label: '4', row: 'numpad', col: 1 }, { code: 'Numpad5', label: '5', row: 'numpad', col: 2 }, { code: 'Numpad6', label: '6', row: 'numpad', col: 3 },
            { code: 'NumpadAdd', label: '+', row: 'numpad', col: 4, height: 2 },
            { code: 'End', label: 'End', row: 'arrow', col: 1 }, { code: 'ArrowLeft', label: '←', row: 'arrow', col: 2 }, { code: 'ArrowRight', label: '→', row: 'arrow', col: 3 }
          ],
          [
            { code: 'Numpad1', label: '1', row: 'numpad', col: 1 }, { code: 'Numpad2', label: '2', row: 'numpad', col: 2 }, { code: 'Numpad3', label: '3', row: 'numpad', col: 3 },
            { code: 'NumpadEnter', label: 'Enter', row: 'numpad', col: 4, height: 2 },
            { code: 'PageDown', label: 'PgDn', row: 'arrow', col: 1 }, { code: 'ArrowDown', label: '↓', row: 'arrow', col: 2 }
          ],
          [
            { code: 'Numpad0', label: '0', row: 'numpad', col: 1, width: 2.5 },
            { code: 'NumpadDecimal', label: '.', row: 'numpad', col: 3 }
          ]
        ];


        function App() {
          const [keymap, setKeymap] = useState(initialGrid);
          const [shortcutPool, setShortcutPool] = useState(Object.fromEntries(Object.entries(presets).map(([k, v]) => [k, [...v]])));
          const [showModal, setShowModal] = useState(false);
          const [modalContent, setModalContent] = useState({ title: "", message: "" });
          const [draggedShortcut, setDraggedShortcut] = useState(null); // To store the shortcut being dragged from the pool
          const [activeTab, setActiveTab] = useState('keymap'); // State for sidebar navigation
          const [jsonInput, setJsonInput] = useState(''); // State for JSON input in settings

          // State for Key Tester
          const [pressedKeyCodes, setPressedKeyCodes] = useState(new Set()); // Use a Set for efficient lookup of pressed keys
          const [keyLog, setKeyLog] = useState([]); // For the list of pressed keys

          // State for Macros
          const [macros, setMacros] = useState([
            { id: 1, name: "Hello World", sequence: "Hello World!" },
            { id: 2, name: "Signature", sequence: "John Doe\nSoftware Engineer" },
          ]);
          const [nextMacroId, setNextMacroId] = useState(3);

          // State for Potentiometer configuration
          const [potentiometerConfig, setPotentiometerConfig] = useState({
            enabled: false,
            pin: 34, // Default analog pin for ESP32
            function: 'volume', // 'volume', 'scroll', 'custom'
            customAction: '' // For custom QMK keycode
          });

          // Connection states
          const [isConnected, setIsConnected] = useState(false);
          const [isConnecting, setIsConnecting] = useState(false);
          const [connectionError, setConnectionError] = useState(null);
          const [connectedPort, setConnectedPort] = useState(null); // To store the connected serial port

          // State for random button animation on waiting screen
          const [activeButtonIndex, setActiveButtonIndex] = useState(null);


          // This function will contain your Web Serial API connection logic
          const handleConnect = async () => {
            setIsConnecting(true);
            setConnectionError(null);

            try {
              // Request permission to access a serial port
              const port = await navigator.serial.requestPort();
              await port.open({ baudRate: 115200 }); // Open the port with a common baud rate

              // Set the connected port state
              setConnectedPort(port);
              setIsConnected(true);
              console.log('Connected to ESP32!');
              setModalContent({
                title: "Connection Successful",
                message: "Successfully connected to your Micropad!"
              });

              // You might want to set up a reader here to listen for data from the device
              // const reader = port.readable.getReader();
              // while (true) {
              //   const { value, done } = await reader.read();
              //   if (done) {
              //     reader.releaseLock();
              //     break;
              //   }
              //   // Process incoming data (e.g., device status, debug messages)
              //   console.log('Received from device:', new TextDecoder().decode(value));
              // }

            } catch (error) {
              console.error('Error during connection attempt:', error);
              setConnectionError(`Connection failed: ${error.message}. Please ensure the device is connected and drivers are installed.`);
              setIsConnected(false);
              setConnectedPort(null);
              setModalContent({
                title: "Connection Failed",
                message: `Failed to connect: ${error.message}. Please ensure your device is connected and try again.`
              });
            } finally {
              setIsConnecting(false);
              setShowModal(true);
            }
          };

          const handleDisconnect = async () => {
            if (connectedPort) {
              try {
                await connectedPort.close();
                setIsConnected(false);
                setConnectedPort(null);
                setModalContent({
                  title: "Disconnected",
                  message: "Micropad disconnected successfully."
                });
              } catch (error) {
                console.error('Error during disconnection:', error);
                setModalContent({
                  title: "Disconnection Failed",
                  message: `Failed to disconnect: ${error.message}`
                });
              } finally {
                setShowModal(true);
              }
            }
          };


          // Custom scrollbar for modal options (though options are removed from modal, keeping for general styling)
          useEffect(() => {
            const style = document.createElement('style');
            style.innerHTML = `
              .custom-scrollbar::-webkit-scrollbar {
                width: 8px;
              }
              .custom-scrollbar::-webkit-scrollbar-track {
                background: #3f3f46; /* zinc-700 */
                border-radius: 10px;
              }
              .custom-scrollbar::-webkit-scrollbar-thumb {
                background: #ef4444; /* red-500 */
                border-radius: 10px;
              }
              .custom-scrollbar::-webkit-scrollbar-thumb:hover {
                background: #dc2626; /* red-600 */
              }
            `;
            document.head.appendChild(style);
            return () => {
              document.head.removeChild(style);
            };
          }, []);

          // Load profile on component mount
          useEffect(() => {
            loadProfile();
          }, []);

          // Key Tester Event Listeners
          useEffect(() => {
            if (activeTab === 'keytester') { // Key tester is active always, connection is for device interaction
              const handleKeyDown = (e) => {
                // Only track if not already pressed to avoid duplicates on hold
                if (!pressedKeyCodes.has(e.code)) {
                  setPressedKeyCodes(prev => new Set(prev).add(e.code));
                  setKeyLog(prev => [{ key: e.key, code: e.code, type: 'down', timestamp: Date.now() }, ...prev].slice(0, 50)); // Keep last 50
                }
              };

              const handleKeyUp = (e) => {
                setPressedKeyCodes(prev => {
                  const newSet = new Set(prev);
                  newSet.delete(e.code);
                  return newSet;
                });
                setKeyLog(prev => [{ key: e.key, code: e.code, type: 'up', timestamp: Date.now() }, ...prev].slice(0, 50));
              };

              window.addEventListener('keydown', handleKeyDown);
              window.addEventListener('keyup', handleKeyUp);

              return () => {
                window.removeEventListener('keydown', handleKeyDown);
                window.removeEventListener('keyup', handleKeyUp);
              };
            } else {
              setPressedKeyCodes(new Set()); // Clear pressed keys when not in key tester tab
              setKeyLog([]); // Clear log when not in key tester tab
            }
          }, [activeTab, pressedKeyCodes]); // Include pressedKeyCodes in dependencies to react to changes


          // Effect for random button animation on waiting screen
          useEffect(() => {
            let intervalId;
            if (isConnecting) {
              intervalId = setInterval(() => {
                // Randomly select a button index (0-8 for a 3x3 grid)
                setActiveButtonIndex(Math.floor(Math.random() * 9));
              }, 200); // Change button every 200ms
            } else {
              setActiveButtonIndex(null); // Clear highlight when not connecting
            }

            return () => {
              if (intervalId) {
                clearInterval(intervalId);
              }
            };
          }, [isConnecting]);


          // Check if the keymap is empty (all cells are null)
          const isKeymapEmpty = keymap.flat().every(cell => cell.tap === null && cell.hold === null);

          // Handles dropping a draggable item onto a keymap cell
          const handleDrop = (e, row, col) => {
            e.preventDefault();
            const data = e.dataTransfer.getData("text/plain");

            const updatedKeymap = [...keymap];

            try {
              const droppedItem = JSON.parse(data);

              if (droppedItem.isKeymapCell) {
                // This is a keymap cell being dragged (reordering)
                const sourceRow = droppedItem.sourceRow;
                const sourceCol = droppedItem.sourceCol;

                // Swap the cells
                const tempCell = updatedKeymap[row][col];
                updatedKeymap[row][col] = droppedItem.cell;
                updatedKeymap[sourceRow][sourceCol] = tempCell;
              } else {
                // This is a shortcut from the pool being dragged (assigning)
                updatedKeymap[row][col] = { tap: droppedItem, hold: null }; // Store the full shortcut object
              }
              setKeymap(updatedKeymap);
            } catch (error) {
              console.error("Failed to parse dropped data:", error);
              // Fallback for plain text if JSON parsing fails (e.g., old drag data)
              updatedKeymap[row][col] = { tap: { combo: data, description: data }, hold: null };
              setKeymap(updatedKeymap);
            }
            setDraggedShortcut(null); // Clear the dragged shortcut after drop
          };

          // Handles starting a drag operation from a keymap cell
          const handleKeymapDragStart = (e, cell, row, col) => {
            // Store the entire cell object and its original position
            const dragData = JSON.stringify({ isKeymapCell: true, cell: cell, sourceRow: row, sourceCol: col });
            e.dataTransfer.setData("text/plain", dragData);
          };

          // Handles starting a drag operation from a shortcut pool item
          const handleShortcutDragStart = (e, shortcut) => {
            // Store the entire shortcut object (combo and description)
            e.dataTransfer.setData("text/plain", JSON.stringify(shortcut));
            setDraggedShortcut(shortcut); // Store the shortcut being dragged
          };

          // Handles drag end for visual feedback
          const handleDragEnd = () => {
            setDraggedShortcut(null); // Clear the dragged shortcut on drag end
          };

          const saveProfile = () => {
            const profileData = {
              keymap: keymap,
              potentiometerConfig: potentiometerConfig,
              macros: macros // Save macros as well
            };
            localStorage.setItem("trkey_profile", JSON.stringify(profileData));
            setModalContent({
              title: "Profile Saved",
              message: "Profile saved to browser storage."
            });
            setShowModal(true);
          };

          const loadProfile = () => {
            const saved = localStorage.getItem("trkey_profile");
            if (saved) {
              const profileData = JSON.parse(saved);
              setKeymap(profileData.keymap || initialGrid);
              setPotentiometerConfig(profileData.potentiometerConfig || { enabled: false, pin: 34, function: 'volume', customAction: '' });
              setMacros(profileData.macros || []);
              setModalContent({
                title: "Profile Loaded",
                message: "Profile loaded successfully."
              });
            } else {
              setModalContent({
                title: "No Profile Found",
                message: "No saved profile found."
              });
            }
            setShowModal(true);
          };

          // Update preset now takes app, index, and the new shortcut object {combo, description}
          const updatePreset = (app, index, newShortcut) => {
            const newPool = { ...shortcutPool };
            newPool[app][index] = newShortcut;
            setShortcutPool(newPool);
          };

          const exportKeymap = () => {
            const fullMap = {
              layout: "3x3",
              layers: {
                default: keymap.map(row => row.map(cell => ({
                  tap: cell.tap ? cell.tap.combo : "", // Export only the combo
                  hold: cell.hold ? cell.hold.combo : ""
                }))),
              },
              peripherals: {
                potentiometers: [
                  potentiometerConfig.enabled ? {
                    pin: potentiometerConfig.pin,
                    function: potentiometerConfig.function,
                    customAction: potentiometerConfig.customAction
                  } : null
                ].filter(Boolean) // Remove null if not enabled
              },
              macros: macros.map(m => ({ name: m.name, sequence: m.sequence }))
            };
            const blob = new Blob([JSON.stringify(fullMap, null, 2)], { type: "application/json" });
            const url = URL.createObjectURL(blob);
            const a = document.createElement("a");
            a.href = url;
            a.download = "trkey_config.json";
            a.click();
            setModalContent({
              title: "Export Successful",
              message: "Configuration exported as trkey_config.json."
            });
            setShowModal(true);
          };

          const uploadToDevice = async () => {
            if (!connectedPort) {
              setModalContent({
                title: "Upload Failed",
                message: "No device connected. Please connect to your Micropad first."
              });
              setShowModal(true);
              return;
            }

            try {
              const writer = connectedPort.writable.getWriter();
              const fullMap = {
                layout: "3x3",
                layers: {
                  default: keymap.map(row => row.map(cell => ({
                    tap: cell.tap ? cell.tap.combo : "", // Export only the combo
                    hold: cell.hold ? cell.hold.combo : ""
                  }))),
                },
                peripherals: {
                  potentiometers: [
                    potentiometerConfig.enabled ? {
                      pin: potentiometerConfig.pin,
                      function: potentiometerConfig.function,
                      customAction: potentiometerConfig.customAction
                    } : null
                  ].filter(Boolean)
                },
                macros: macros.map(m => ({ name: m.name, sequence: m.sequence }))
              };
              const json = JSON.stringify(fullMap);
              const encoder = new TextEncoder();
              await writer.write(encoder.encode(json));
              writer.releaseLock();
              // Keep port open for subsequent uploads if needed, user can disconnect manually
              setModalContent({
                title: "Upload Successful",
                message: "Configuration uploaded successfully!"
              });
            } catch (err) {
              setModalContent({
                title: "Upload Failed",
                message: "Failed to upload: " + err.message + ". Ensure the device is ready to receive data."
              });
            } finally {
              setShowModal(true);
            }
          };

          const loadJsonFromTextArea = () => {
            try {
              const parsedJson = JSON.parse(jsonInput);
              if (parsedJson.layers && parsedJson.layers.default) {
                const newKeymap = parsedJson.layers.default.map(row =>
                  row.map(combo => {
                    const foundPreset = Object.values(presets).flat().find(p => p.combo === combo);
                    return {
                      tap: combo ? { combo: combo, description: foundPreset ? foundPreset.description : combo } : null,
                      hold: null
                    };
                  })
                );
                const finalKeymap = Array(3).fill().map((_, rIdx) =>
                  Array(3).fill().map((_, cIdx) =>
                    newKeymap[rIdx] && newKeymap[rIdx][cIdx] ? newKeymap[rIdx][cIdx] : { tap: null, hold: null }
                  )
                );
                setKeymap(finalKeymap);

                // Load potentiometer config if present
                if (parsedJson.peripherals && parsedJson.peripherals.potentiometers && parsedJson.peripherals.potentiometers.length > 0) {
                  const loadedPot = parsedJson.peripherals.potentiometers[0];
                  setPotentiometerConfig({
                    enabled: true,
                    pin: loadedPot.pin || 34,
                    function: loadedPot.function || 'volume',
                    customAction: loadedPot.customAction || ''
                  });
                } else {
                    setPotentiometerConfig({ enabled: false, pin: 34, function: 'volume', customAction: '' });
                }

                // Load macros if present
                if (parsedJson.macros && Array.isArray(parsedJson.macros)) {
                    setMacros(parsedJson.macros.map((m, idx) => ({ id: idx + 1, name: m.name, sequence: m.sequence })));
                    setNextMacroId(parsedJson.macros.length + 1);
                } else {
                    setMacros([]);
                    setNextMacroId(1);
                }


                setModalContent({
                  title: "JSON Loaded",
                  message: "Configuration loaded from text area successfully."
                });
              } else {
                setModalContent({
                  title: "Invalid JSON",
                  message: "The pasted JSON does not contain a valid 'layers.default' structure."
                });
              }
            } catch (error) {
              setModalContent({
                title: "JSON Parsing Error",
                message: "Failed to parse JSON: " + error.message
              });
            } finally {
              setShowModal(true);
            }
          };

          // Macro functions
          const addMacro = () => {
            const name = prompt("Enter macro name:");
            if (!name) return;
            const sequence = prompt("Enter macro sequence (e.g., 'Hello World!'):");
            if (sequence) {
              setMacros(prev => [...prev, { id: nextMacroId, name, sequence }]);
              setNextMacroId(prev => prev + 1);
            }
          };

          const editMacro = (id) => {
            const macroToEdit = macros.find(m => m.id === id);
            if (!macroToEdit) return;

            const newName = prompt(`Edit name for "${macroToEdit.name}":`, macroToEdit.name);
            if (newName === null) return; // User cancelled

            const newSequence = prompt(`Edit sequence for "${macroToEdit.name}":`, macroToEdit.sequence);
            if (newSequence === null) return; // User cancelled

            setMacros(prev => prev.map(m =>
              m.id === id ? { ...m, name: newName, sequence: newSequence } : m
            ));
          };

          const deleteMacro = (id) => {
            if (window.confirm("Are you sure you want to delete this macro?")) {
              setMacros(prev => prev.filter(m => m.id !== id));
            }
          };


          return (
            <div className="min-h-screen bg-zinc-800 text-white flex font-inter">
              {/* Conditional rendering for the connection screen */}
              {!isConnected ? (
                <div className="flex flex-col items-center justify-center min-h-screen w-full bg-zinc-900 text-white font-inter p-4">
                  <h1 className="text-4xl font-bold mb-6 text-red-500 animate-pulse">Trkey Micropad Configurator</h1>
                  {connectionError && (
                    <p className="text-red-400 mb-4 text-center">{connectionError}</p>
                  )}
                  {!isConnecting ? (
                    <button
                      onClick={handleConnect}
                      className="px-8 py-4 bg-blue-600 hover:bg-blue-700 text-white text-xl font-semibold rounded-full shadow-lg transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-75"
                    >
                      Connect to Micropad
                    </button>
                  ) : (
                    <div className="flex flex-col items-center">
                      <div className="relative w-64 h-64 bg-zinc-800 p-4 rounded-lg shadow-inner border border-zinc-700 mb-8">
                        <div className="grid grid-cols-3 gap-2 w-full h-full">
                          {Array(9).fill().map((_, index) => (
                            <div
                              key={index}
                              className={`
                                w-full h-full bg-zinc-700 rounded-md shadow-md
                                flex items-center justify-center
                                transition-all duration-100 ease-in-out
                                ${activeButtonIndex === index ? 'micropad-button-active' : ''}
                              `}
                            ></div>
                          ))}
                        </div>
                      </div>
                      <p className="mt-4 text-2xl font-semibold text-zinc-300">Connecting to Micropad...</p>
                      <p className="text-md text-zinc-400 mt-2">Please ensure your ESP32 device is plugged in and ready.</p>
                    </div>
                  )}
                  <Modal
                    show={showModal}
                    title={modalContent.title}
                    message={modalContent.message}
                    onClose={() => setShowModal(false)}
                  />
                </div>
              ) : (
                // --- Main Configurator UI (rendered when connected) ---
                <div className="min-h-screen bg-zinc-800 text-white flex flex-col lg:flex-row font-inter">
                  {/* Sidebar */}
                  <div className="w-full lg:w-64 bg-zinc-900 p-6 flex flex-col border-b lg:border-b-0 lg:border-r border-zinc-700 shadow-xl">
                    <div className="text-2xl font-bold text-red-500 mb-8">Trkey</div>
                    <nav className="flex-grow">
                      <ul className="space-y-4">
                        <li>
                          <a href="#" onClick={() => setActiveTab('keymap')} className={`flex items-center ${activeTab === 'keymap' ? 'text-red-300' : 'text-zinc-400'} hover:text-red-500 font-semibold text-lg transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"></path></svg>
                            KEYMAP
                          </a>
                        </li>
                        <li>
                          <a href="#" onClick={() => setActiveTab('macros')} className={`flex items-center ${activeTab === 'macros' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M12 6.293V4a1 1 0 00-1-1H5a1 1 0 00-1 1v10a1 1 0 001 1h6a1 1 0 001-1v-2.293l1.707 1.707a1 1 0 001.414-1.414l-4-4a1 1 0 00-1.414 0l-4 4a1 1 0 001.414 1.414L10 10.414V12a1 1 0 001 1h2a1 1 0 001-1V8.293l1.707 1.707a1 1 0 001.414-1.414l-4-4z"></path></svg>
                            MACROS
                          </a>
                        </li>
                        <li>
                          <a href="#" onClick={() => setActiveTab('controls')} className={`flex items-center ${activeTab === 'controls' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M10 18a8 8 0 100-16 8 8 0 000 16zM7 9a1 1 0 100-2 1 1 0 000 2zm6-1a1 1 0 100-2 1 1 0 000 2zm-3 8a1 1 0 100-2 1 1 0 000 2z"></path></svg>
                            CONTROLS
                          </a>
                        </li>
                        <li>
                          <a href="#" onClick={() => setActiveTab('save-load')} className={`flex items-center ${activeTab === 'save-load' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M5 4a2 2 0 012-2h6a2 2 0 012 2v14l-5-2.5L5 18V4z"></path></svg>
                            SAVE + LOAD
                          </a>
                        </li>
                        <li>
                          <a href="#" onClick={() => setActiveTab('settings')} className={`flex items-center ${activeTab === 'settings' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M10 2a1 1 0 00-1 1v1a1 1 0 002 0V3a1 1 0 00-1-1zm4 4a1 1 0 011 1v1a1 1 0 01-2 0V7a1 1 0 011-1zM6 6a1 1 0 00-1 1v1a1 1 0 002 0V7a1 1 0 00-1-1zm0 8a1 1 0 00-1 1v1a1 1 0 002 0v-1a1 1 0 00-1-1zm8 0a1 1 0 00-1 1v1a1 1 0 002 0v-1a1 1 0 00-1-1zm-4 4a1 1 0 00-1 1v1a1 1 0 002 0v-1a1 1 0 00-1-1zM2 10a1 1 0 001 1h1a1 1 0 000-2H3a1 1 0 00-1 1zm14 0a1 1 0 001 1h1a1 1 0 000-2h-1a1 1 0 00-1 1zM7 10a3 3 0 116 0 3 3 0 01-6 0z"></path></svg>
                            SETTINGS
                          </a>
                        </li>
                        <li>
                          <a href="#" onClick={() => setActiveTab('keytester')} className={`flex items-center ${activeTab === 'keytester' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                            <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 00-1 1v10a1 1 0 001 1h12a1 1 0 001-1V5a1 1 0 00-1-1h-3.382l-.724-1.447A1 1 0 0011 2H9zM4 6h12v8H4V6z"></path></svg>
                            KEY TESTER
                          </a>
                        </li>
                      </ul>
                    </nav>
                    <div className="text-sm text-zinc-500 mt-auto">
                      <p>Version 1.0</p>
                      <p>Device: Micropad</p>
                    </div>
                  </div>

                  {/* Main Content */}
                  <div className="flex-grow p-8 bg-zinc-800 flex flex-col">
                    {/* Top Bar */}
                    <div className="flex justify-between items-center mb-8 pb-4 border-b border-zinc-700">
                      <div className="flex space-x-6">
                        <span className="text-lg font-semibold text-red-400">CONFIGURE</span>
                        <span className="text-lg text-zinc-400">KEY TESTER</span>
                        <span className="text-lg text-zinc-400">SETTINGS</span>
                      </div>
                      <div className="text-zinc-500">
                        <span className="mr-2">1UP60HSE</span>
                        {isConnected && (
                          <button
                            onClick={handleDisconnect}
                            className="ml-4 px-3 py-1 bg-red-600 hover:bg-red-700 text-white rounded-md text-sm transition duration-300"
                          >
                            Disconnect
                          </button>
                        )}
                      </div>
                    </div>

                    {activeTab === 'keymap' && (
                      <>
                        {/* Keymap Section */}
                        <div className="mb-10">
                          <h2 className="text-xl font-bold text-red-300 mb-4">KEYMAP</h2>
                          <div className="flex space-x-2 mb-6">
                            {['0', '1', '2', '3'].map(layer => (
                              <button
                                key={layer}
                                // Currently hardcoded to layer 0 for demonstration, but can be expanded
                                className={`px-4 py-2 rounded-md font-semibold text-lg transition-colors duration-200 ${layer === '0' ? 'bg-red-600 text-white' : 'bg-zinc-700 text-zinc-300 hover:bg-zinc-600'}`}
                              >
                                {layer}
                              </button>
                            ))}
                          </div>

                          {/* Conditional rendering of the micropad grid */}
                          {!isKeymapEmpty ? (
                            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 w-fit mx-auto">
                              <div className="grid grid-cols-3 gap-2">
                                {keymap.map((row, rIdx) =>
                                  row.map((cell, cIdx) => (
                                    <div
                                      key={`${rIdx}-${cIdx}`}
                                      draggable
                                      onDragStart={(e) => handleKeymapDragStart(e, cell, rIdx, cIdx)}
                                      onDrop={(e) => handleDrop(e, rIdx, cIdx)}
                                      onDragOver={(e) => e.preventDefault()}
                                      onDragEnd={handleDragEnd}
                                      // Visual feedback for drag over
                                      className={`
                                        w-24 h-24 bg-zinc-700 text-white rounded-md shadow-md border border-zinc-600
                                        flex flex-col justify-center items-center cursor-grab active:cursor-grabbing
                                        relative overflow-hidden
                                        transform transition-all duration-200
                                        ${draggedShortcut ? 'border-dashed border-red-300' : 'hover:bg-red-600 hover:scale-105'}
                                      `}
                                    >
                                      <div className="absolute inset-0 bg-gradient-to-br from-zinc-800 to-zinc-700 rounded-md"></div>
                                      <div className="relative z-10 text-sm font-bold text-red-200 drop-shadow-md text-center px-1">
                                        {cell.tap ? cell.tap.description || cell.tap.combo : ""}
                                      </div>
                                      {cell.hold && <div className="relative z-10 text-xs text-zinc-400 mt-1">/ {cell.hold.description || cell.hold.combo}</div>}
                                    </div>
                                  ))
                                )}
                              </div>
                            </div>
                          ) : (
                            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 h-48 flex items-center justify-center text-zinc-400 text-lg text-center">
                              No keymap loaded. Drag shortcuts from the pool below to configure your micropad, or load a saved profile from Settings.
                            </div>
                          )}
                        </div>

                        {/* Shortcut Pool */}
                        <div className="mt-10 w-full">
                          <h2 className="text-xl text-red-400 font-bold mb-4">SHORTCUTS</h2>
                          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                            {Object.entries(shortcutPool).map(([app, shortcuts]) => (
                              <div key={app} className="mb-4 bg-zinc-900 p-5 rounded-xl shadow-xl border border-red-600">
                                <h3 className="text-lg font-semibold mb-3 text-red-300 border-b border-red-500 pb-2">{app}</h3>
                                <div className="flex flex-wrap gap-2">
                                  {shortcuts.map((s, i) => (
                                    <div
                                      key={`${app}-${i}`}
                                      draggable
                                      onDragStart={(e) => handleShortcutDragStart(e, s)}
                                      onDragEnd={handleDragEnd}
                                      className="
                                        px-4 py-2 bg-zinc-700 text-white rounded-full shadow-md cursor-grab
                                        hover:bg-red-500 hover:scale-105 transition-all duration-200
                                        flex items-center justify-center text-sm font-medium
                                        relative
                                      "
                                    >
                                      {s.description || s.combo} {/* Display description */}
                                      {/* Input for editing shortcut */}
                                      <input
                                        type="text"
                                        value={s.combo} // Input value is the combo
                                        onChange={(e) => updatePreset(app, i, { ...s, combo: e.target.value, description: s.description || e.target.value })}
                                        onClick={(e) => e.stopPropagation()} // Prevent drag start on click
                                        className="absolute inset-0 w-full h-full bg-transparent text-transparent border-none focus:outline-none cursor-text opacity-0"
                                        style={{ zIndex: 10 }} // Ensure input is clickable
                                      />
                                    </div>
                                  ))}
                                </div>
                                {/* Add New Shortcut Button */}
                                <button
                                  onClick={() => {
                                    const combo = prompt(`Enter new key combination for ${app}:`);
                                    if (combo) {
                                      const description = prompt(`Enter description for ${combo}:`);
                                      updatePreset(app, shortcuts.length, { combo, description: description || combo });
                                    }
                                  }}
                                  className="mt-4 w-full bg-red-800 hover:bg-red-900 text-white text-sm py-2 rounded-lg transition-colors duration-200"
                                >
                                  + Add Shortcut
                                </button>
                              </div>
                            ))}
                          </div>
                        </div>
                      </>
                    )}

                    {activeTab === 'macros' && (
                      <div className="w-full max-w-4xl mx-auto">
                        <h2 className="text-xl font-bold text-red-300 mb-4">MACROS</h2>
                        <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 mb-6">
                          <button
                            onClick={addMacro}
                            className="bg-red-600 hover:bg-red-700 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-75 mb-4"
                          >
                            + Add New Macro
                          </button>
                          {macros.length === 0 ? (
                            <p className="text-zinc-400">No macros defined yet.</p>
                          ) : (
                            <div className="space-y-4">
                              {macros.map(macro => (
                                <div key={macro.id} className="bg-zinc-800 p-4 rounded-md border border-zinc-700 flex justify-between items-center">
                                  <div>
                                    <h4 className="font-semibold text-lg text-red-200">{macro.name}</h4>
                                    <p className="text-sm text-zinc-300 break-all">{macro.sequence}</p>
                                  </div>
                                  <div className="flex space-x-2">
                                    <button onClick={() => editMacro(macro.id)} className="bg-blue-600 hover:bg-blue-700 text-white px-3 py-1 rounded-md text-sm">Edit</button>
                                    <button onClick={() => deleteMacro(macro.id)} className="bg-red-600 hover:bg-red-700 text-white px-3 py-1 rounded-md text-sm">Delete</button>
                                  </div>
                                </div>
                              ))}
                            </div>
                          )}
                        </div>
                      </div>
                    )}

                    {activeTab === 'controls' && (
                        <div className="w-full max-w-4xl mx-auto">
                            <h2 className="text-xl font-bold text-red-300 mb-4">PERIPHERAL CONTROLS</h2>
                            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 mb-6">
                                <h3 className="text-lg font-semibold text-red-300 mb-4">Potentiometer 1 Configuration</h3>
                                <div className="flex items-center mb-4">
                                    <label htmlFor="pot-enabled" className="mr-3 text-zinc-300">Enable Potentiometer:</label>
                                    <input
                                        type="checkbox"
                                        id="pot-enabled"
                                        checked={potentiometerConfig.enabled}
                                        onChange={(e) => setPotentiometerConfig(prev => ({ ...prev, enabled: e.target.checked }))}
                                        className="form-checkbox h-5 w-5 text-red-600 rounded border-gray-300 focus:ring-red-500"
                                    />
                                </div>
                                {potentiometerConfig.enabled && (
                                    <>
                                        <div className="mb-4">
                                            <label htmlFor="pot-pin" className="block text-zinc-300 mb-2">Analog Pin:</label>
                                            <input
                                                type="number"
                                                id="pot-pin"
                                                value={potentiometerConfig.pin}
                                                onChange={(e) => setPotentiometerConfig(prev => ({ ...prev, pin: parseInt(e.target.value) || 0 }))}
                                                className="w-24 px-3 py-2 bg-zinc-800 text-white rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-red-500"
                                                min="0"
                                            />
                                        </div>
                                        <div className="mb-4">
                                            <label htmlFor="pot-function" className="block text-zinc-300 mb-2">Function:</label>
                                            <select
                                                id="pot-function"
                                                value={potentiometerConfig.function}
                                                onChange={(e) => setPotentiometerConfig(prev => ({ ...prev, function: e.target.value }))}
                                                className="w-full px-3 py-2 bg-zinc-800 text-white rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-red-500"
                                            >
                                                <option value="volume">Volume Control</option>
                                                <option value="scroll">Scroll</option>
                                                <option value="custom">Custom QMK Keycode</option>
                                            </select>
                                        </div>
                                        {potentiometerConfig.function === 'custom' && (
                                            <div className="mb-4">
                                                <label htmlFor="pot-custom-action" className="block text-zinc-300 mb-2">Custom QMK Keycode:</label>
                                                <input
                                                    type="text"
                                                    id="pot-custom-action"
                                                    value={potentiometerConfig.customAction}
                                                    onChange={(e) => setPotentiometerConfig(prev => ({ ...prev, customAction: e.target.value }))}
                                                    className="w-full px-3 py-2 bg-zinc-800 text-white rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-red-500"
                                                    placeholder="e.g., KC_MPLY or custom_macro_name"
                                                />
                                            </div>
                                        )}
                                    </>
                                )}
                            </div>
                        </div>
                    )}

                    {activeTab === 'keytester' && (
                      <div className="w-full max-w-7xl mx-auto">
                        <h2 className="text-xl font-bold text-red-300 mb-4">KEY TESTER</h2>
                        <p className="text-zinc-400 mb-4">Press any key on your physical keyboard. The corresponding virtual key will light up, and the event will be logged below.</p>

                        {/* Virtual Keyboard Display */}
                        <div className="bg-zinc-900 p-4 rounded-lg shadow-inner border border-zinc-700 mb-6 overflow-x-auto">
                          <div className="keyboard-layout-grid">
                            {keyboardLayout.map((row, rowIndex) => (
                              <div key={rowIndex} className="keyboard-row flex justify-center gap-1 mb-1">
                                {row.map((key, keyIndex) => (
                                  <div
                                    key={key.code}
                                    className={`
                                      key-cap
                                      ${pressedKeyCodes.has(key.code) ? 'key-pressed' : ''}
                                    `}
                                    style={{
                                      width: key.width ? `${key.width * 40}px` : '40px', // Base unit of 40px for a key
                                      height: key.height ? `${key.height * 40}px` : '40px',
                                    }}
                                  >
                                    <span className="key-label text-xs sm:text-sm">{key.label}</span>
                                  </div>
                                ))}
                              </div>
                            ))}
                          </div>
                        </div>

                        {/* Key Event Log */}
                        <h3 className="text-lg font-bold text-red-300 mb-3">Key Event Log</h3>
                        <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 h-64 overflow-y-auto custom-scrollbar">
                          {keyLog.length === 0 ? (
                            <p className="text-zinc-500">No key events logged yet...</p>
                          ) : (
                            <ul className="space-y-2">
                              {keyLog.map((logEntry, index) => (
                                <li key={index} className="bg-zinc-700 p-2 rounded-md font-mono text-sm flex justify-between items-center">
                                  <div>
                                    <span className={`font-bold ${logEntry.type === 'down' ? 'text-green-300' : 'text-red-300'}`}>
                                      {logEntry.type === 'down' ? 'DOWN' : 'UP'}:
                                    </span>
                                    <span className="ml-2 text-white">Key: "{logEntry.key}"</span>
                                    <span className="ml-4 text-blue-300">Code: "{logEntry.code}"</span>
                                  </div>
                                  <span className="text-zinc-400 text-xs">
                                    {new Date(logEntry.timestamp).toLocaleTimeString()}
                                  </span>
                                </li>
                              ))}
                            </ul>
                          )}
                        </div>
                      </div>
                    )}

                    {activeTab === 'save-load' && (
                      <div className="flex flex-col items-center justify-center h-full text-zinc-400 text-2xl">
                        <h2 className="text-xl font-bold text-red-300 mb-4">SAVE / LOAD Profile</h2>
                        <div className="flex flex-wrap justify-center gap-4 mt-8">
                          <button onClick={saveProfile} className="bg-zinc-700 hover:bg-zinc-600 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-zinc-500 focus:ring-opacity-75">
                            Save Profile
                          </button>
                          <button onClick={loadProfile} className="bg-zinc-700 hover:bg-zinc-600 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-zinc-500 focus:ring-opacity-75">
                            Load Profile
                          </button>
                        </div>
                      </div>
                    )}

                    {activeTab === 'settings' && (
                      <div className="flex flex-col items-center justify-center w-full text-zinc-400">
                        <h2 className="text-xl font-bold text-red-300 mb-4">SETTINGS</h2>

                        <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 w-full max-w-4xl mb-8">
                          <h3 className="text-lg font-semibold text-red-300 mb-4">QMK JSON Configuration</h3>
                          <p className="mb-4 text-sm">
                            You can export your current micropad keymap as JSON, upload it to your device, or load a keymap by pasting JSON below.
                            Note: This configurator supports a 3x3 micropad layout.
                          </p>
                          <div className="flex flex-wrap justify-center gap-4 mb-6">
                            <button onClick={exportKeymap} className="bg-red-600 hover:bg-red-700 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-75">
                              Export Keymap JSON
                            </button>
                            <button
                              onClick={uploadToDevice}
                              disabled={!isConnected} // Disable upload if not connected
                              className={`px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-opacity-75 ${isConnected ? 'bg-white text-black hover:bg-zinc-200 focus:ring-white' : 'bg-gray-500 text-gray-300 cursor-not-allowed'}`}
                            >
                              Upload Keymap to Device
                            </button>
                          </div>

                          <h4 className="text-md font-semibold text-red-300 mb-2">Load JSON from Text Area</h4>
                          <textarea
                            className="w-full h-40 bg-zinc-800 text-white p-4 rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-red-500 font-mono text-sm"
                            placeholder="Paste your QMK keymap JSON here..."
                            value={jsonInput}
                            onChange={(e) => setJsonInput(e.target.value)}
                          ></textarea>
                          <button
                            onClick={loadJsonFromTextArea}
                            className="mt-4 w-full bg-red-800 hover:bg-red-900 text-white text-lg py-3 rounded-full transition-colors duration-200 shadow-lg"
                          >
                            Load JSON
                          </button>
                        </div>

                        {/* Live JSON Preview */}
                        <h3 className="text-lg font-semibold text-red-300 mb-2">Current Keymap JSON Preview</h3>
                        <pre className="mt-2 text-sm bg-zinc-900 p-6 rounded-lg text-left w-full max-w-4xl overflow-x-auto border border-red-500 font-mono shadow-inner">
                          {JSON.stringify({
                            layout: "3x3",
                            layers: { default: keymap.map(row => row.map(cell => ({
                              tap: cell.tap ? cell.tap.combo : "",
                              hold: cell.hold ? cell.hold.combo : ""
                            })))}
                          }, null, 2)}
                        </pre>
                      </div>
                    )}
                  </div>

                  <Modal
                    show={showModal}
                    title={modalContent.title}
                    message={modalContent.message}
                    onClose={() => setShowModal(false)}
                  />
                </div>
              )}
            </div>
          );
        }

        ReactDOM.createRoot(document.getElementById('root')).render(<App />);
    </script>
</body>
</html>
