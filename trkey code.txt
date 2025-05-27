import React, { useState, useEffect, useCallback } from "react";

// --- START OF PRESETS DATA ---
const presets = {
  "BASIC": [
    { combo: "M", description: "Move" },
    { combo: "V", description: "Via" },
    { combo: "R", description: "Rotate" },
    { combo: "Del", description: "Delete" },
    { combo: "Ctrl+Z", description: "Undo" },
    { combo: "Ctrl+Y", "description": "Redo" },
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
    { combo: "T", description: "Text" },
    { combo: "Ctrl+C", description: "Copy" },
    { combo: "Ctrl+V", description: "Paste" },
    { combo: "Ctrl+Z", description: "Undo" },
    { combo: "Ctrl+X", description: "Cut" },
    { combo: "Ctrl+S", description: "Save" },
    { combo: "Ctrl+Shift+G", description: "Ungroup" },
    { combo: "Alt+Shift+B", description: "Bring to Back" },
    { combo: "Ctrl+D", description: "Duplicate" },
    { combo: "Ctrl+Alt+K", description: "Lock" },
    { combo: "Ctrl+P", description: "Command Palette" },
    { combo: "Ctrl+Shift+P", description: "Show All Commands" },
    { combo: "Ctrl+F", description: "Find" },
    { combo: "Alt+Shift+F", description: "Format Document" },
  ],
  "WINDOWS_SHORTCUTS": [
    { combo: "Win+D", description: "Show Desktop" },
    { combo: "Win+E", description: "Open File Explorer" },
    { combo: "Win+L", description: "Lock Screen" },
    { combo: "Win+Tab", description: "Task View" },
    { combo: "Alt+F4", description: "Close App/Shutdown" },
    { combo: "Ctrl+Shift+Esc", description: "Open Task Manager" },
    { combo: "Win+PrintScreen", description: "Screenshot to File" },
    { combo: "Win+.", description: "Emoji Panel" },
    { combo: "Win+Shift+S", description: "Snip & Sketch" },
  ],
  "MACOS_SHORTCUTS": [
    { combo: "Cmd+Space", description: "Spotlight Search" },
    { combo: "Cmd+C", description: "Copy" },
    { combo: "Cmd+V", description: "Paste" },
    { combo: "Cmd+Z", description: "Undo" },
    { combo: "Cmd+X", description: "Cut" },
    { combo: "Cmd+S", description: "Save" },
    { combo: "Cmd+Q", description: "Quit App" },
    { combo: "Cmd+W", description: "Close Window" },
    { combo: "Cmd+Tab", description: "Switch Apps" },
    { combo: "Cmd+Shift+3", description: "Screenshot Full" },
    { combo: "Cmd+Shift+4", description: "Screenshot Selection" },
  ],
  "LINUX_SHORTCUTS": [
    { combo: "Ctrl+Alt+T", description: "Open Terminal" },
    { combo: "Alt+Tab", description: "Switch Windows" },
    { combo: "Ctrl+Alt+Del", description: "Logout/Shutdown Menu" },
    { combo: "Super+D", description: "Show Desktop" }, // 'Super' typically is the Windows/Meta key
    { combo: "Super+L", description: "Lock Screen" },
    { combo: "Ctrl+Shift+N", description: "New Folder" },
    { combo: "F2", description: "Rename File" },
    { combo: "PrintScreen", description: "Screenshot" },
    { combo: "ls", description: "List directory contents" },
    { combo: "cd", description: "Change directory" },
    { combo: "pwd", description: "Print working directory" },
    { combo: "mkdir", description: "Make directory" },
    { combo: "rm", description: "Remove file/directory" },
    { combo: "cp", description: "Copy file" },
    { combo: "mv", description: "Move file" },
    { combo: "sudo", description: "Run command as superuser" },
    { combo: "man", description: "Manual pages" },
    { combo: "top", description: "Show running processes" },
    { combo: "ps", description: "List processes" },
    { combo: "kill", description: "Terminate process" },
    { combo: "grep", description: "Search text" },
    { combo: "chmod", description: "Change permissions" },
    { combo: "chown", description: "Change ownership" },
    { combo: "nano", description: "Text editor" },
    { combo: "vim", description: "Vi Improved editor" },
    { combo: "df", description: "Disk usage" },
    { combo: "du", description: "Directory usage" },
    { combo: "tar", description: "Archive files" },
    { combo: "zip/unzip", description: "Compress/Extract" },
    { combo: "ssh", description: "Remote access" },
    { combo: "scp", description: "Secure copy" },
    { combo: "wget", description: "Download files" },
    { combo: "curl", description: "Transfer data" },
    { combo: "alias", description: "Create shortcut command" },
    { combo: "history", description: "Show command history" },
    { combo: "clear", description: "Clear terminal" },
    { combo: "reboot", description: "Restart system" },
    { combo: "shutdown", description: "Shutdown system" },
    { combo: "uptime", description: "Show system uptime" },
  ],
  "ANDROID_SHORTCUTS": [
    { combo: "RecentApps", description: "Show Recent Apps" },
    { combo: "Home", description: "Go Home" },
    { combo: "Back", description: "Go Back" },
    { combo: "VolumeUp", description: "Volume Up" },
    { combo: "VolumeDown", description: "Volume Down" },
    { combo: "Power", description: "Power Button" },
    { combo: "Search", description: "Open Search" },
    { combo: "Camera", description: "Open Camera" },
  ],
  "IPAD_SHORTCUTS": [
    { combo: "Cmd+Space", description: "Search/Spotlight" },
    { combo: "Cmd+H", description: "Go Home" },
    { combo: "Cmd+Tab", description: "Switch Apps" },
    { combo: "Cmd+Shift+3", description: "Screenshot Full" },
    { combo: "Cmd+Shift+4", description: "Screenshot Selection" },
    { combo: "Globe+C", description: "Copy (Contextual)" }, // Globe key is common on iPad keyboards
    { combo: "Globe+V", description: "Paste (Contextual)" },
    { combo: "Globe+Z", description: "Undo (Contextual)" },
  ],
  "MINECRAFT_SHORTCUTS": [
    { combo: "W", description: "Move forward" },
    { combo: "A", description: "Move left" },
    { combo: "S", description: "Move backward" },
    { combo: "D", description: "Move right" },
    { combo: "Space", description: "Jump" },
    { combo: "Shift", description: "Sneak" },
    { combo: "Ctrl", description: "Sprint" },
    { combo: "E", description: "Open inventory" },
    { combo: "Q", description: "Drop selected item" },
    { combo: "T", description: "Open chat" },
    { combo: "F3+D", description: "Clear chat" },
    { combo: "F5", description: "Change camera" },
    { combo: "F8", description: "Smooth camera" },
    { combo: "Tab", description: "Player list" },
    { combo: "Esc", description: "Menu" },
    { combo: "Middle Click", description: "Pick block (Creative)" },
    { combo: "Double Space", description: "Fly toggle (Creative)" },
    { combo: "Ctrl+Middle Click", description: "Copy block with NBT" },
    { combo: "Shift+Left Click", description: "Destroy instantly (Creative)" },
    { combo: "Shift+Right Click", description: "Edit command block (Creative)" },
    { combo: "Shift+Click", description: "Move stack (Inventory)" },
    { combo: "Ctrl+Q", description: "Drop stack" },
    { combo: "Ctrl+Click", description: "Select same items" },
    { combo: "Double Click", description: "Grab all of that item" },
    { combo: "Mouse wheel", description: "Scroll hotbar" },
    { combo: "Number+Hover", description: "Move item to hotbar" },
    { combo: "F3+N", description: "Switch gamemode" },
    { combo: "Alt+F4", description: "Rage quit" },
    { combo: "F3+C", description: "Force crash" },
    { combo: "F3+A", description: "Reload chunks" },
    { combo: "Shift+Click", description: "Craft all (in recipe book)" },
  ],
  "WAR_THUNDER_SHORTCUTS": [
    { combo: "W/S", description: "Throttle up/down" },
    { combo: "A/D", description: "Rudder left/right" },
    { combo: "Q/E", description: "Roll left/right" },
    { combo: "Shift", description: "Afterburner" },
    { combo: "Ctrl", description: "Air brake" },
    { combo: "G", description: "Landing gear" },
    { combo: "F", description: "Flaps" },
    { combo: "V", description: "View mode" },
    { combo: "C", description: "Free camera" },
    { combo: "X", description: "Look left" },
    { combo: "Z", description: "Look right" },
    { combo: "Y", description: "Look back" },
    { combo: "B", description: "Bomb view" },
    { combo: "N", description: "Navigation lights" },
    { combo: "J", description: "Bail out" },
    { combo: "M", description: "Map" },
    { combo: "Tab", description: "Scoreboard" },
    { combo: "T", description: "Target" },
    { combo: "R", description: "Radar" },
    { combo: "H", description: "Head tracking" },
    { combo: "Space", description: "Fire main guns" },
    { combo: "Alt", description: "Fire secondary" },
    { combo: "Ctrl+Space", description: "Drop bomb" },
    { combo: "Shift+Space", description: "Fire rocket" },
    { combo: "Mouse 2", description: "Zoom" },
    { combo: "Mouse 1", description: "Fire guns" },
    { combo: "Mouse 3", description: "Track enemy" },
    { combo: "F1", description: "Help" },
    { combo: "F2", description: "Toggle cockpit" },
    { combo: "F3", description: "Chase camera" },
    { combo: "W/A/S/D", description: "Drive (Tank)" },
    { combo: "Shift", description: "Speed boost" },
    { combo: "V", description: "Binocular view" },
    { combo: "U", description: "Repair" },
    { combo: "O", description: "Toggle optics" },
    { combo: "K", description: "Thermal/IR" },
    { combo: "L", description: "Headlights" },
    { combo: "R", description: "Rangefinder" },
    { combo: "C", description: "Commander cam" },
    { combo: "X", description: "Machine gun" },
    { combo: "Esc", description: "Menu" },
    { combo: "Enter", description: "Chat" },
    { combo: "Backspace", description: "Leave vehicle" },
    { combo: "Home", description: "Reset view" },
    { combo: "Del", description: "Zoom out" },
    { combo: "Ins", description: "Zoom in" },
    { combo: "Alt+F10", description: "Save replay" },
    { combo: "Alt+PrintScreen", description: "Screenshot" },
    { combo: "Ctrl+Y", description: "Chat channel" },
    { combo: "Ctrl+G", description: "Gunner view" },
  ],
  "ROBLOX_STUDIO_SHORTCUTS": [
    { combo: "Ctrl+S", description: "Save" },
    { combo: "Ctrl+Shift+S", description: "Save As" },
    { combo: "Ctrl+N", description: "New place" },
    { combo: "Ctrl+O", description: "Open place" },
    { combo: "Ctrl+Z", description: "Undo" },
    { combo: "Ctrl+Y", description: "Redo" },
    { combo: "Ctrl+C/V/X", description: "Copy/Paste/Cut" },
    { combo: "Ctrl+D", description: "Duplicate" },
    { combo: "Ctrl+G", description: "Group" },
    { combo: "Ctrl+U", description: "Ungroup" },
    { combo: "Ctrl+P", description: "Publish" },
    { combo: "F", description: "Focus selection" },
    { combo: "Shift+F", description: "Follow camera" },
    { combo: "Alt+Click", description: "Select parent" },
    { combo: "Ctrl+Click", description: "Multi-select" },
    { combo: "Ctrl+Shift+H", description: "View explorer" },
    { combo: "Ctrl+Shift+X", description: "Properties" },
    { combo: "Ctrl+Shift+C", description: "Output" },
    { combo: "Ctrl+Shift+D", description: "Asset manager" },
    { combo: "Ctrl+Shift+E", description: "Toolbox" },
    { combo: "W/A/S/D", description: "Camera move" },
    { combo: "E/Q", description: "Move up/down" },
    { combo: "T", description: "Rotate" },
    { combo: "R", description: "Resize" },
    { combo: "G", description: "Move" },
    { combo: "Ctrl+T", description: "Anchor" },
    { combo: "Ctrl+L", description: "Lock" },
    { combo: "Ctrl+B", description: "Break joints" },
    { combo: "Ctrl+J", description: "Join surfaces" },
    { combo: "Ctrl+M", description: "Material" },
    { combo: "Ctrl+Shift+M", description: "Model" },
    { combo: "Shift+Drag", description: "Constrain" },
    { combo: "Arrow Keys", description: "Nudge" },
    { combo: "Ctrl+P", description: "Quick publish" },
    { combo: "Alt+Shift+E", description: "Export" },
    { combo: "Ctrl+S", description: "Save" },
  ],
  "ENLISTED_SHORTCUTS": [
    { combo: "W/A/S/D", description: "Move" },
    { combo: "Space", description: "Jump" },
    { combo: "Shift", description: "Sprint" },
    { combo: "Ctrl", description: "Crouch" },
    { combo: "Z", description: "Prone" },
    { combo: "X", description: "Lean left" },
    { combo: "C", description: "Lean right" },
    { combo: "F", description: "Interact" },
    { combo: "R", description: "Reload" },
    { combo: "G", description: "Grenade" },
    { combo: "T", description: "Pick weapon" },
    { combo: "V", description: "Melee" },
    { combo: "B", description: "Fire mode" },
    { combo: "Q/E", description: "Switch soldier" },
    { combo: "Tab", description: "Scoreboard" },
    { combo: "M", description: "Map" },
    { combo: "N", description: "Night vision" },
    { combo: "Y", description: "Orders" },
    { combo: "L", description: "Flashlight" },
    { combo: "Esc", description: "Menu" },
    { combo: "Click", description: "Fire" },
    { combo: "Right Click", description: "Aim" },
    { combo: "Scroll", description: "Change weapon" },
    { combo: "1-3", description: "Weapons" },
    { combo: "H", description: "Help" },
    { combo: "Alt", description: "Free look" },
    { combo: "Ctrl+Shift", description: "Walk" },
    { combo: "F1", description: "Camera" },
    { combo: "Alt+M", description: "Minimap" },
    { combo: "Ctrl+R", description: "Reload prone" },
    { combo: "Ctrl+F1", description: "Switch class" },
    { combo: "Alt+V", description: "Change view" },
    { combo: "Middle Mouse", description: "Ping" },
    { combo: "Hold T", description: "Mark enemy" },
    { combo: "Hold Shift", description: "Sprint long" },
    { combo: "Hold F", description: "Plant/diffuse" },
    { combo: "Ctrl+Number", description: "Squad command" },
    { combo: "Shift+1-4", description: "Formations" },
    { combo: "K", description: "Kill feed" },
    { combo: "U", description: "Medkit" },
    { combo: "1", description: "Inventory" },
    { combo: "Backspace", description: "Suicide" },
    { combo: "Del", description: "Respawn" },
    { combo: "F3", description: "Record" },
    { combo: "F12", description: "Screenshot" },
    { combo: "Tilde", description: "Console" },
    { combo: "Ctrl+Alt+Delete", description: "Force quit" },
  ],
  "CODING_IDE_SHORTCUTS": [
    { combo: "Ctrl+P", description: "Quick open file" },
    { combo: "Ctrl+Shift+P", description: "Command palette" },
    { combo: "Ctrl+`", description: "Terminal toggle" },
    { combo: "Ctrl+B", description: "Sidebar toggle" },
    { combo: "Ctrl+J", description: "Panel toggle" },
    { combo: "Ctrl+Shift+E", description: "Explorer" },
    { combo: "Ctrl+Shift+F", description: "Search in files" },
    { combo: "Ctrl+Shift+G", description: "Git" },
    { combo: "Ctrl+Shift+D", description: "Debug" },
    { combo: "Ctrl+Shift+X", description: "Extensions" },
    { combo: "Ctrl+Space", description: "Trigger suggestion" },
    { combo: "Ctrl+/-", description: "Comment line" },
    { combo: "Alt+Up/Down", description: "Move line" },
    { combo: "Shift+Alt+Down", description: "Copy line down" },
    { combo: "Ctrl+Shift+K", description: "Delete line" },
    { combo: "Ctrl+D", description: "Select next occurrence" },
    { combo: "Ctrl+L", description: "Select line" },
    { combo: "Ctrl+Enter", description: "Insert line below" },
    { combo: "Ctrl+Shift+Enter", description: "Insert line above" },
    { combo: "Ctrl+Shift+-", description: "Jump to bracket" },
    { combo: "Ctrl+Tab", description: "Next editor" },
    { combo: "Ctrl+Shift+Tab", description: "Previous editor" },
    { combo: "Ctrl+W", description: "Close editor" },
  ],
  "KICAD_SHORTCUTS": [
    { combo: "Ctrl+N", description: "New project" },
    { combo: "Ctrl+O", description: "Open project" },
    { combo: "Ctrl+S", description: "Save" },
    { combo: "Ctrl+Z", description: "Undo" },
    { combo: "Ctrl+Y", description: "Redo" },
    { combo: "Ctrl+C/V/X", description: "Copy/Paste/Cut" },
    { combo: "Del", description: "Delete" },
    { combo: "R", description: "Rotate" },
    { combo: "M", description: "Move" },
    { combo: "E", description: "Edit properties" },
    { combo: "W", description: "Wire" },
    { combo: "P", description: "Place component" },
    { combo: "Shift+Space", description: "Cycle units" },
    { combo: "Page Up/Down", description: "Zoom in/out" },
    { combo: "Ctrl+Scroll", description: "Zoom" },
    { combo: "F1/F2/F3/F4", description: "Pan directions" },
    { combo: "Space", description: "Reset origin" },
    { combo: "Alt+1-5", description: "Layer view" },
    { combo: "Ctrl+B", description: "Rebuild ratsnest" },
    { combo: "Ctrl+H", description: "Highlight net" },
  ],
  "FUSION_360_SHORTCUTS": [
    { combo: "S", description: "Toolbox" },
    { combo: "L", description: "Line" },
    { combo: "R", description: "Rectangle" },
    { combo: "C", description: "Circle" },
    { combo: "D", description: "Dimension" },
    { combo: "T", description: "Text" },
    { combo: "M", description: "Move" },
    { combo: "Q", description: "Press/Pull" },
    { combo: "E", description: "Extrude" },
    { combo: "F", description: "Fillet" },
    { combo: "Shift+S", description: "Sketch shortcuts" },
    { combo: "Ctrl+Z/Y", description: "Undo/Redo" },
    { combo: "Ctrl+C/V", description: "Copy/Paste" },
    { combo: "Delete", description: "Remove" },
    { combo: "B", description: "Emboss" },
    { combo: "J", description: "Joint" },
    { combo: "H", description: "Hole" },
    { combo: "G", description: "Grid settings" },
    { combo: "Tab", description: "Switch input" },
    { combo: "Alt+Drag", description: "Orbit" },
    { combo: "Shift+Scroll", description: "Pan" },
    { combo: "Scroll", description: "Zoom" },
    { combo: "Home", description: "View cube" },
    { combo: "F6", description: "Home view" },
    { combo: "F7", description: "Slice" },
    { combo: "Ctrl+1/2/3", description: "Orthographic views" },
    { combo: "Ctrl+Shift+E", description: "Export" },
    { combo: "Ctrl+S", description: "Save" },
  ],
  "CANVA_SHORTCUTS": [
    { combo: "Ctrl+C/V/X", description: "Copy/Paste/Cut" },
    { combo: "Ctrl+Z/Y", description: "Undo/Redo" },
    { combo: "Ctrl+A", description: "Select all" },
    { combo: "Delete", description: "Remove" },
    { combo: "Ctrl+G/U", description: "Group/Ungroup" },
    { combo: "Ctrl+D", description: "Duplicate" },
    { combo: "Shift+Arrow", description: "Nudge" },
    { combo: "Alt+Drag", description: "Duplicate while dragging" },
    { combo: "T", description: "Add text" },
    { combo: "R", description: "Add rectangle" },
    { combo: "L", description: "Add line" },
    { combo: "C", description: "Add circle" },
    { combo: "B", description: "Bold" },
    { combo: "I", description: "Italic" }, // Corrected from '1' to 'I' based on common Canva shortcuts
    { combo: "U", description: "Underline" },
    { combo: "Ctrl+K", description: "Link" },
    { combo: "Ctrl+Shift+K", description: "Unlink" },
    { combo: "Ctrl+E", description: "Align center" },
    { combo: "Ctrl+L/R", description: "Align left/right" },
    { combo: "Ctrl+Shift+M", description: "Comment" },
    { combo: "Alt+[/]", description: "Layer back/front" },
    { combo: "Ctrl+P", description: "Print" },
    { combo: "Ctrl+S", description: "Save" },
    { combo: "Ctrl+Shift+S", description: "Save As" },
    { combo: "Ctrl+Shift+D", description: "Download" },
  ],
  // The "MACRO" category will be dynamically populated based on the 'macros' state
  // "MEDIA", "LAYERS", "SPECIAL", "QMK LIGHTING" remain static presets
  "MEDIA": [
    { combo: "KC_MPRV", description: "Prev Track" },
    { combo: "KC_MNXT", description: "Next Track" },
    { combo: "KC_MPLY", description: "Play/Pause" },
    { combo: "KC_MUTE", description: "Mute" },
    { combo: "KC_VOLU", description: "Volume Up" },
    { combo: "KC_VOLD", description: "Volume Down" },
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
// --- END OF PRESETS DATA ---

// Helper function to create an empty 3x3 grid for a keymap layer
const createEmptyGrid = () => Array(3).fill().map(() => Array(3).fill({ tap: null, hold: null }));

// --- START OF KeyComponent DEFINITION ---
const KeyComponent = React.memo(({
  keyData,
  isMacro, // Prop from App.js to indicate if this key represents a macro
  isShortcut, // Prop from App.js to indicate if this key represents a custom/AI shortcut
  onClick,
  onDoubleClick,
  customBgColor,
  customStyles
}) => {
  const { combo, description } = keyData;

  let mainText = '';
  let subText = '';

  // Determine main and sub text based on available data
  if (description) {
    mainText = description;
    if (combo && combo !== description) {
      subText = combo;
    }
  } else if (combo) {
    mainText = combo;
  } else {
    mainText = 'Empty';
  }

  // Append type indicators to subText if applicable
  if (isMacro) {
    subText = subText ? `${subText} (Macro)` : '(Macro)';
  } else if (isShortcut) {
    subText = subText ? `${subText} (Custom)` : '(Custom)';
  }


  // Base Tailwind classes for all key components
  const keyClass = `
    relative
    w-16 h-16 sm:w-20 sm:h-20 md:w-24 md:h-24 lg:w-28 lg:h-28
    flex items-center justify-center
    font-bold rounded-lg
    border-b-4 border-r-2 border-red-700
    active:border-b-0
    transition-all duration-100 ease-in-out
    transform active:translate-y-1 active:translate-x-0.5
    shadow-lg
    cursor-pointer
    select-none
    overflow-hidden
    p-1
  `;

  // Determine background color and text color based on type (macro, shortcut, or default red) or custom color
  let colorClass = '';
  let mainTextColorClass = ''; // For mainText
  let subTextColorClass = ''; // For subText

  if (customBgColor) {
    colorClass = `bg-[${customBgColor}]`;
    mainTextColorClass = 'text-white';
    subTextColorClass = 'text-zinc-400 opacity-80';
  } else if (isMacro) {
    colorClass = 'bg-purple-600 hover:bg-purple-700';
    mainTextColorClass = 'text-white';
    subTextColorClass = 'text-purple-200 opacity-80';
  } else if (isShortcut) {
    colorClass = 'bg-blue-600 hover:bg-blue-700';
    mainTextColorClass = 'text-white';
    subTextColorClass = 'text-blue-200 opacity-80';
  } else {
    // Default red keys
    colorClass = 'bg-red-500 hover:bg-red-600';
    mainTextColorClass = 'text-black'; // Main text is black as requested
    subTextColorClass = 'text-zinc-700 opacity-80'; // Subtext is a darker gray for contrast on red
  }

  return (
    <div
      className={`${keyClass} ${colorClass} ${customStyles || ''}`}
      onClick={onClick}
      onDoubleClick={onDoubleClick}
      style={customBgColor ? { backgroundColor: customBgColor } : {}}
    >
      <div className="text-center break-words leading-tight">
        <span className={`block text-base font-bold ${mainTextColorClass}`}>{mainText}</span>
        {subText && <span className={`block text-xs mt-0.5 ${subTextColorClass}`}>{subText}</span>}
      </div>
    </div>
  );
});
// --- END OF KeyComponent DEFINITION ---

// --- START OF Modal DEFINITION ---
const Modal = ({ show, title, message, onClose, customButtons }) => {
  if (!show) {
    return null;
  }

  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div className="bg-zinc-800 p-6 rounded-lg shadow-xl max-w-md w-full border border-red-500">
        <h2 className="text-xl font-bold text-red-300 mb-4">{title}</h2>
        <p className="text-white mb-6">{message}</p>
        <div className="flex justify-end space-x-2">
          {customButtons ? (
            customButtons.map((button, index) => (
              <button
                key={index}
                onClick={button.onClick}
                className={`${button.className || 'bg-red-600 hover:bg-red-700'} text-white font-bold py-2 px-4 rounded-lg`}
              >
                {button.label}
              </button>
            ))
          ) : (
            <button
              onClick={onClose}
              className="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg"
            >
              Close
            </button>
          )}
        </div>
      </div>
    </div>
  );
};
// --- END OF Modal DEFINITION ---

// --- START OF MacroFormModal DEFINITION ---
const MacroFormModal = ({ show, onClose, onSave, macro }) => {
  const [name, setName] = useState('');
  const [description, setDescription] = useState('');
  const [sequence, setSequence] = useState(''); // Renamed from 'steps' to 'sequence' for clarity
  const [error, setError] = useState('');

  useEffect(() => {
    if (show && macro) {
      setName(macro.name || '');
      setDescription(macro.description || '');
      setSequence(macro.sequence || ''); // Use 'sequence'
      setError('');
    } else if (show && !macro) {
      setName('');
      setDescription('');
      setSequence('');
      setError('');
    }
  }, [show, macro]);

  const handleSave = () => {
    if (!name.trim()) {
      setError('Macro name cannot be empty.');
      return;
    }
    if (!sequence.trim()) {
      setError('Macro sequence cannot be empty.');
      return;
    }
    setError('');
    // Pass 'sequence' instead of 'steps'
    onSave({ id: macro ? macro.id : Date.now(), name, description, sequence });
    onClose();
  };

  if (!show) {
    return null;
  }

  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div className="bg-zinc-800 p-6 rounded-lg shadow-xl max-w-md w-full border border-red-500">
        <h2 className="text-xl font-bold text-red-300 mb-4">{macro ? 'Edit Macro' : 'Create New Macro'}</h2>

        {error && <p className="text-red-500 text-sm mb-4">{error}</p>}

        <div className="mb-4">
          <label htmlFor="macroName" className="block text-white text-sm font-bold mb-2">Macro Name:</label>
          <input
            type="text"
            id="macroName"
            className="shadow appearance-none border border-zinc-700 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline bg-zinc-900"
            value={name}
            onChange={(e) => setName(e.target.value)}
            placeholder="e.g., Delete Line"
          />
        </div>
        <div className="mb-4">
          <label htmlFor="macroDescription" className="block text-white text-sm font-bold mb-2">Description (optional):</label>
          <input
            type="text"
            id="macroDescription"
            className="shadow appearance-none border border-zinc-700 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline bg-zinc-900"
            value={description}
            onChange={(e) => setDescription(e.target.value)}
            placeholder="e.g., Deletes current line, copies to clipboard"
          />
        </div>
        <div className="mb-6">
          <label htmlFor="macroSequence" className="block text-white text-sm font-bold mb-2">Macro Sequence (e.g., Hello World!{`{Enter}`}, Ctrl+S{`{Delay 100}`}{`{Ctrl+P}`}):</label>
          <textarea
            id="macroSequence"
            className="shadow appearance-none border border-zinc-700 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline bg-zinc-900 h-24 resize-y"
            value={sequence}
            onChange={(e) => setSequence(e.target.value)}
            placeholder="e.g., Ctrl+C,Ctrl+V,Enter"
          />
        </div>

        <div className="flex justify-end space-x-2">
          <button
            onClick={onClose}
            className="bg-zinc-600 hover:bg-zinc-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            Cancel
          </button>
          <button
            onClick={handleSave}
            className="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            {macro ? 'Save Changes' : 'Create Macro'}
          </button>
        </div>
      </div>
    </div>
  );
};
// --- END OF MacroFormModal DEFINITION ---

// --- START OF ConfirmationModal DEFINITION ---
const ConfirmationModal = ({ show, onClose, onConfirm, message }) => {
  if (!show) {
    return null;
  }

  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div className="bg-zinc-800 p-6 rounded-lg shadow-xl max-w-md w-full border border-red-500">
        <h2 className="text-xl font-bold text-red-300 mb-4">Confirm Action</h2>
        <p className="text-white mb-6">{message}</p>
        <div className="flex justify-end space-x-2">
          <button
            onClick={onClose}
            className="bg-zinc-600 hover:bg-zinc-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            Cancel
          </button>
          <button
            onClick={onConfirm}
            className="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            Confirm
          </button>
        </div>
      </div>
    </div>
  );
};
// --- END OF ConfirmationModal DEFINITION ---

// --- START OF AddShortcutModal DEFINITION ---
const AddShortcutModal = ({ show, onClose, onSave }) => {
  const [combo, setCombo] = useState('');
  const [description, setDescription] = useState('');
  const [error, setError] = useState('');

  useEffect(() => {
    if (show) {
      setCombo('');
      setDescription('');
      setError('');
    }
  }, [show]);

  const handleSave = () => {
    if (!combo.trim()) {
      setError('Shortcut combination cannot be empty.');
      return;
    }
    if (!description.trim()) {
      setError('Description cannot be empty.');
      return;
    }
    setError('');
    // Ensure the new shortcut is marked as a custom shortcut
    onSave({ id: Date.now(), combo, description, isCustomShortcut: true });
    onClose();
  };

  if (!show) {
    return null;
  }

  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div className="bg-zinc-800 p-6 rounded-lg shadow-xl max-w-md w-full border border-red-500">
        <h2 className="text-xl font-bold text-red-300 mb-4">Add New Shortcut</h2>

        {error && <p className="text-red-500 text-sm mb-4">{error}</p>}

        <div className="mb-4">
          <label htmlFor="shortcutCombo" className="block text-white text-sm font-bold mb-2">Shortcut Combo (e.g., Ctrl+C):</label>
          <input
            type="text"
            id="shortcutCombo"
            className="shadow appearance-none border border-zinc-700 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline bg-zinc-900"
            value={combo}
            onChange={(e) => setCombo(e.target.value)}
            placeholder="e.g., Alt+Shift+F"
          />
        </div>
        <div className="mb-6">
          <label htmlFor="shortcutDescription" className="block text-white text-sm font-bold mb-2">Description (e.g., Format Document):</label>
          <input
            type="text"
            id="shortcutDescription"
            className="shadow appearance-none border border-zinc-700 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline bg-zinc-900"
            value={description}
            onChange={(e) => setDescription(e.target.value)}
            placeholder="e.g., Open quick search"
          />
        </div>

        <div className="flex justify-end space-x-2">
          <button
            onClick={onClose}
            className="bg-zinc-600 hover:bg-zinc-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            Cancel
          </button>
          <button
            type="submit"
            onClick={handleSave}
            className="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg"
          >
            Add Shortcut
          </button>
        </div>
      </div>
    </div>
  );
};
// --- END OF AddShortcutModal DEFINITION ---


// Main App component
export default function App() {
  // State for the keymap, organized by layer (e.g., '0', '1', etc.)
  const [keymap, setKeymap] = useState({ '0': createEmptyGrid() });
  // State for the currently active layer being edited
  const [activeLayer, setActiveLayer] = useState('0');

  // State for the pool of available shortcuts, initialized from presets
  const [shortcutPool, setShortcutPool] = useState(Object.fromEntries(Object.entries(presets).map(([k, v]) => [k, [...v]])));
  // State for controlling the general info/error modal
  const [showModal, setShowModal] = useState(false);
  // Content for the general info/error modal
  const [modalContent, setModalContent] = useState({ title: "", message: "" });
  // State to track the shortcut being dragged for visual feedback
  const [draggedShortcut, setDraggedShortcut] = useState(null);
  // State for sidebar navigation tab
  const [activeTab, setActiveTab] = useState('keymap');
  // State for JSON input in the settings tab
  const [jsonInput, setJsonInput] = useState('');

  // State for Key Tester tab: stores currently pressed keys
  const [pressedKeys, setPressedKeys] = useState([]);

  // State for Macros: list of defined macros
  const [macros, setMacros] = useState([]);
  // Counter for assigning unique IDs to new macros
  const [nextMacroId, setNextMacroId] = useState(1);
  // State for showing the macro form modal (add/edit)
  const [showMacroFormModal, setShowMacroFormModal] = useState(false);
  // State for the macro currently being edited
  const [editingMacro, setEditingMacro] = useState(null);
  // State for showing the macro deletion confirmation modal
  const [showConfirmationModal, setShowConfirmationModal] = useState(false);
  // ID of the macro to be deleted
  const [macroToDeleteId, setMacroToDeleteId] = useState(null);

  // State for AI Shortcut Generator prompt and loading status
  const [aiPrompt, setAiPrompt] = useState('');
  const [isGeneratingAiShortcuts, setIsGeneratingAiShortcuts] = useState(false);

  // State for AI Macro Generator prompt and loading status
  const [aiMacroPrompt, setAiMacroPrompt] = useState('');
  const [isGeneratingAiMacros, setIsGeneratingAiMacros] = useState(false);

  // State for currently selected shortcut category in the pool display
  const [selectedShortcutCategory, setSelectedShortcutCategory] = useState('BASIC');

  // State for showing the Add Shortcut Modal
  const [showAddShortcutModal, setShowAddShortcutModal] = useState(false);

  // State for Web Serial API connection (for device communication)
  const [connectedPort, setConnectedPort] = useState(null);


  // Effect to inject custom scrollbar styles into the document head
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
    // Cleanup function to remove the style when the component unmounts
    return () => {
      document.head.removeChild(style);
    };
  }, []); // Empty dependency array means this runs once on mount

  // Effect to load user profile from local storage on component mount
  useEffect(() => {
    loadProfile();
  }, []); // Empty dependency array means this runs once on mount

  // Effect for Key Tester functionality: attaches/removes keyboard event listeners
  useEffect(() => {
    if (activeTab === 'keytester') {
      // Handler for keydown events
      const handleKeyDown = (e) => {
        e.preventDefault(); // Prevent default browser actions (e.g., scrolling with spacebar)
        setPressedKeys(prev => {
          const newKey = { key: e.key, code: e.code, timestamp: Date.now() };
          // Add key to list only if it's not already recorded as pressed (to avoid duplicates on hold)
          if (!prev.some(k => k.code === e.code && k.type === 'down')) {
            return [...prev, { ...newKey, type: 'down' }];
          }
          return prev;
        });
      };

      // Handler for keyup events
      const handleKeyUp = (e) => {
        e.preventDefault(); // Prevent default browser actions
        // Remove released key from the list of pressed keys
        setPressedKeys(prev => prev.filter(k => k.code !== e.code));
      };

      // Add event listeners when Key Tester tab is active
      window.addEventListener('keydown', handleKeyDown);
      window.addEventListener('keyup', handleKeyUp);

      // Cleanup function to remove event listeners when component unmounts or tab changes
      return () => {
        window.removeEventListener('keydown', handleKeyDown);
        window.removeEventListener('keyup', handleKeyUp);
      };
    } else {
      // Clear any pressed keys if switching away from the Key Tester tab
      setPressedKeys([]);
    }
  }, [activeTab]); // Reruns when activeTab changes

  // Effect to dynamically update the "MACRO" category in shortcutPool based on the 'macros' state
  useEffect(() => {
    setShortcutPool(prevPool => ({
      ...prevPool,
      "MACRO": macros.map(m => ({
        combo: `MACRO_${m.id}`, // Unique combo for the macro
        description: m.name,    // Display the macro's user-defined name
        isMacro: true           // Flag to identify it as a macro for KeyComponent
      }))
    }));
  }, [macros]); // This effect runs whenever the 'macros' state changes


  // Helper to check if the current active layer's keymap is entirely empty
  const isKeymapEmpty = keymap[activeLayer] && keymap[activeLayer].flat().every(cell => cell.tap === null && cell.hold === null);


  // Handles dropping a draggable item onto a keymap cell
  const handleDrop = (e, row, col) => {
    e.preventDefault(); // Prevent default browser handling of the drop
    const data = e.dataTransfer.getData("text/plain"); // Get data transferred during drag

    setKeymap(prevKeymap => {
      // Create a mutable copy of the active layer's keymap, or an empty grid if it doesn't exist
      const updatedLayer = [...(prevKeymap[activeLayer] || createEmptyGrid())];
      try {
        const droppedItem = JSON.parse(data); // Attempt to parse the dropped data as JSON

        if (droppedItem.isKeymapCell) {
          // If the dropped item originated from another keymap cell (reordering)
          const sourceRow = droppedItem.sourceRow;
          const sourceCol = droppedItem.sourceCol;

          // Swap the contents of the source and target cells
          const tempCell = updatedLayer[row][col];
          updatedLayer[row][col] = droppedItem.cell;
          updatedLayer[sourceRow][sourceCol] = tempCell;
        } else {
          // If the dropped item is a shortcut from the pool (assigning)
          let assignedShortcut = { ...droppedItem }; // Create a copy to modify

          // If it's from the "AI GENERATED" category or was explicitly marked as custom (from AddShortcutModal)
          // ensure it retains its custom shortcut flag.
          if (selectedShortcutCategory === "AI GENERATED" || assignedShortcut.isCustomShortcut) {
            assignedShortcut.isCustomShortcut = true;
          }
          // If it's from the "MACRO" category, it already has isMacro: true from the useEffect that populates shortcutPool
          // So no need to explicitly set isMacro here again, just ensure it's copied.

          updatedLayer[row][col] = { tap: assignedShortcut, hold: null }; // Assign the augmented shortcut
        }
        // Return the updated keymap state
        return { ...prevKeymap, [activeLayer]: updatedLayer };
      } catch (error) {
        // Fallback if JSON parsing fails (e.g., plain text was dragged)
        console.error("Failed to parse dropped data:", error);
        // Treat as a generic custom shortcut if parsing fails
        updatedLayer[row][col] = { tap: { combo: data, description: data, isCustomShortcut: true }, hold: null };
        return { ...prevKeymap, [activeLayer]: updatedLayer };
      }
    });
    setDraggedShortcut(null); // Clear the dragged shortcut state after drop
  };

  // Handles starting a drag operation from a keymap cell (for reordering)
  const handleKeymapDragStart = (e, cell, row, col) => {
    // Store the entire cell object and its original position as JSON
    const dragData = JSON.stringify({ isKeymapCell: true, cell: cell, sourceRow: row, sourceCol: col });
    e.dataTransfer.setData("text/plain", dragData);
  };

  // Handles starting a drag operation from a shortcut pool item
  const handleShortcutDragStart = (e, shortcut) => {
    // Store the entire shortcut object (combo and description) as JSON
    e.dataTransfer.setData("text/plain", JSON.stringify(shortcut));
    setDraggedShortcut(shortcut); // Store the shortcut being dragged for visual feedback
  };

  // Handles drag end event for visual feedback (clears the dragged item state)
  const handleDragEnd = () => {
    setDraggedShortcut(null);
  };

  // Saves the current keymap and macros to browser's local storage
  const saveProfile = () => {
    const profileData = {
      keymap: keymap,
      macros: macros
    };
    localStorage.setItem("trkey_profile", JSON.stringify(profileData));
    setModalContent({
      title: "Profile Saved",
      message: "Your current keymap and macros have been saved to your browser's local storage."
    });
    setShowModal(true);
  };

  // Loads a saved profile from browser's local storage
  const loadProfile = () => {
    const saved = localStorage.getItem("trkey_profile");
    if (saved) {
      const profileData = JSON.parse(saved);
      // Ensure keymap has at least layer '0' and all layers are valid 3x3 grids
      const loadedKeymap = profileData.keymap || { '0': createEmptyGrid() };
      for (const layer in loadedKeymap) {
          if (!Array.isArray(loadedKeymap[layer]) || loadedKeymap[layer].length !== 3 || loadedKeymap[layer][0].length !== 3) {
              loadedKeymap[layer] = createEmptyGrid();
          }
      }
      setKeymap(loadedKeymap);
      setMacros(profileData.macros || []); // Load macros, default to empty array if none
      setModalContent({
        title: "Profile Loaded",
        message: "Profile loaded successfully from browser storage."
      });
    } else {
      setModalContent({
        title: "No Profile Found",
        message: "No saved profile found in browser storage."
      });
    }
    setShowModal(true);
  };

  // Updates a shortcut within a specific category in the shortcut pool
  const updatePreset = (app, index, newShortcut) => {
    setShortcutPool(prevPool => {
      const newPool = { ...prevPool };
      // Ensure the category exists before attempting to update
      if (!newPool[app]) {
          newPool[app] = [];
      }
      newPool[app][index] = newShortcut; // Update the shortcut at the specified index
      return newPool;
    });
  };

  // Exports the current keymap and macros as a JSON file
  const exportKeymap = () => {
    const exportedLayers = {}; // Layers will be an object of arrays
    for (const layerNum in keymap) {
        const flatLayer = [];
        // Iterate through the 3x3 grid row by row, then column by column
        for (let r = 0; r < 3; r++) {
            for (let c = 0; c < 3; c++) {
                const cell = keymap[layerNum][r][c];
                // Get the combo string, or "KC_NO" if empty
                flatLayer.push(cell.tap ? cell.tap.combo : "KC_NO");
            }
        }
        exportedLayers[layerNum] = flatLayer;
    }

    const exportedMacros = {}; // Macros will be an object
    macros.forEach(macro => {
        // Ensure macro name is valid for a key (uppercase, no spaces, no special chars)
        const macroKey = `MACRO_${macro.name.toUpperCase().replace(/\s/g, '_').replace(/[^A-Z0-9_]/g, '')}`;
        // The sequence is stored as a single-element array containing the string
        exportedMacros[macroKey] = [macro.sequence];
    });

    const fullMap = {
      layers: exportedLayers, // Include all configured layers
      macros: exportedMacros, // Include macros in the new object format
      combos: [], // Add an empty combos array as requested
      // layer_toggle_button is omitted as it doesn't map directly to current UI
    };
    // Create a Blob containing the JSON data
    const blob = new Blob([JSON.stringify(fullMap, null, 2)], { type: "application/json" });
    // Create a URL for the Blob
    const url = URL.createObjectURL(blob);
    // Create a temporary anchor element to trigger the download
    const a = document.createElement("a");
    a.href = url;
    a.download = "trkey_config.json"; // Suggested filename
    document.body.appendChild(a);
    a.click(); // Programmatically click the anchor to start download
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    // Show a success modal
    setModalContent({
      title: "Export Successful",
      message: "Configuration exported as trkey_config.json."
    });
    setShowModal(true);
  };

  // Connects to a serial device using Web Serial API
  const connectToDevice = async () => {
    try {
      // Request permission to access a serial port
      const port = await navigator.serial.requestPort();
      setConnectedPort(port); // Store the connected port in state
      setModalContent({
        title: "Device Connected",
        message: "Micropad connected successfully. You can now upload your keymap."
      });
    } catch (err) {
      // Handle connection errors
      setModalContent({
        title: "Connection Failed",
        message: "Failed to connect to device: " + err.message
      });
      setConnectedPort(null); // Clear connected port on failure
    } finally {
      setShowModal(true); // Always show a modal with connection status
    }
  };

  // Disconnects from the currently connected serial device
  const disconnectDevice = async () => {
    if (connectedPort) {
      try {
        await connectedPort.close(); // Close the serial port
        setConnectedPort(null); // Clear connected port from state
        setModalContent({
          title: "Disconnected",
          message: "Micropad disconnected successfully."
        });
      } catch (err) {
        // Handle disconnection errors
        setModalContent({
          title: "Disconnection Failed",
          message: "Failed to disconnect: " + err.message
        });
      } finally {
        setShowModal(true); // Always show a modal with disconnection status
      }
    }
  };

  // Uploads the current keymap configuration to the connected serial device
  const uploadKeymapToConnectedDevice = async () => {
    if (!connectedPort) {
      // If no device is connected, inform the user
      setModalContent({
        title: "No Device Connected",
        message: "Please connect to your micropad first."
      });
      setShowModal(true);
      return;
    }

    try {
      // Open the port if it's not already open. Baud rate must match device firmware.
      if (connectedPort.readable === null && connectedPort.writable === null) {
        await connectedPort.open({ baudRate: 500000 }); // Common baud rate for ESP32
      }

      // Get a writer to send data to the device
      const writer = connectedPort.writable.getWriter();

      // Prepare the keymap data for export (similar to exportKeymap function)
      const exportedLayers = {};
      for (const layerNum in keymap) {
        const flatLayer = [];
        for (let r = 0; r < 3; r++) {
            for (let c = 0; c < 3; c++) {
                const cell = keymap[layerNum][r][c];
                flatLayer.push(cell.tap ? cell.tap.combo : "KC_NO");
            }
        }
        exportedLayers[layerNum] = flatLayer;
      }

      const exportedMacros = {};
      macros.forEach(macro => {
          const macroKey = `MACRO_${macro.name.toUpperCase().replace(/\s/g, '_').replace(/[^A-Z0-9_]/g, '')}`;
          exportedMacros[macroKey] = [macro.sequence];
      });

      const fullMap = {
        layers: exportedLayers,
        macros: exportedMacros,
        combos: [],
      };
      const json = JSON.stringify(fullMap); // Convert the full map to a JSON string
      const encoder = new TextEncoder(); // Create a TextEncoder to convert string to bytes
      await writer.write(encoder.encode(json)); // Write the JSON bytes to the serial port
      writer.releaseLock(); // Release the writer lock

      // Show success modal
      setModalContent({
        title: "Upload Successful",
        message: "Configuration uploaded successfully! The device should restart with the new keymap."
      });
    } catch (err) {
      // Handle upload errors
      setModalContent({
        title: "Upload Failed",
        message: "Failed to upload: " + err.message + ". Please ensure the device is ready to receive data (e.g., in programming mode or awaiting input)."
      });
    } finally {
      setShowModal(true); // Always show a modal with upload status
    }
  };

  // Loads keymap and macros from a JSON string pasted into a text area
  const loadJsonFromTextArea = () => {
    try {
      const parsedJson = JSON.parse(jsonInput);
      let loadedMacros = []; // Declare loadedMacros here to be accessible for layers

      // 1. Load Macros first, as layers might refer to them
      if (parsedJson.macros && typeof parsedJson.macros === 'object') {
        let currentMacroId = 1;
        for (const macroKey in parsedJson.macros) {
          const sequenceArray = parsedJson.macros[macroKey];
          if (Array.isArray(sequenceArray) && sequenceArray.length > 0) {
            const sequence = sequenceArray[0]; // Take the first element as the sequence string
            // Convert MACRO_KEY to a readable name (e.g., "MACRO_HELLO_WORLD" -> "Hello World")
            let name = macroKey.replace(/^MACRO_/, '').replace(/_/g, ' ').toLowerCase();
            name = name.split(' ').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ');

            loadedMacros.push({ id: currentMacroId++, name: name, sequence: sequence });
          }
        }
        setMacros(loadedMacros);
        setNextMacroId(currentMacroId);
      } else {
        setMacros([]);
        setNextMacroId(1);
      }

      // 2. Then load Layers
      if (parsedJson.layers && typeof parsedJson.layers === 'object') {
        const newKeymap = {};
        for (const layerNum in parsedJson.layers) {
          const flatLayer = parsedJson.layers[layerNum];
          const gridLayer = createEmptyGrid(); // Start with an empty 3x3 grid
          if (Array.isArray(flatLayer) && flatLayer.length === 9) { // Expect exactly 9 elements for 3x3
            for (let i = 0; i < 9; i++) {
              const row = Math.floor(i / 3);
              const col = i % 3;
              const comboString = flatLayer[i];

              if (comboString && comboString !== "KC_NO") { // Ignore "KC_NO" or empty strings
                let tapObj = { combo: comboString, description: comboString };

                // Check if it's a macro reference
                if (comboString.startsWith('MACRO_')) {
                  // Reconstruct the expected macro name from the combo string for lookup
                  const macroNameForLookup = comboString.replace(/^MACRO_/, '').replace(/_/g, ' ').toLowerCase().split(' ').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ');
                  const correspondingMacro = loadedMacros.find(m => m.name === macroNameForLookup);

                  if (correspondingMacro) {
                    tapObj.description = correspondingMacro.name;
                    tapObj.isMacro = true;
                  } else {
                    // If macro not found, just display its raw combo and mark as custom
                    tapObj.description = macroNameForLookup; // Still try to show a readable name
                    tapObj.isCustomShortcut = true; // Treat as custom if macro reference is broken
                  }
                } else {
                  // Check if it's a known preset or custom shortcut
                  const foundPreset = Object.values(presets).flat().find(p => p.combo === comboString);
                  if (foundPreset) {
                    tapObj.description = foundPreset.description;
                  } else {
                    tapObj.isCustomShortcut = true;
                  }
                }
                gridLayer[row][col] = { tap: tapObj, hold: null };
              }
            }
          } else {
            console.warn(`Layer ${layerNum} in JSON is malformed (expected 9 elements) and was reset to empty.`);
          }
          newKeymap[String(layerNum)] = gridLayer; // Store with string key for consistency
        }

        // Ensure layer '0' always exists in the new keymap
        if (!newKeymap['0']) {
            newKeymap['0'] = createEmptyGrid();
        }
        setKeymap(newKeymap);
        setActiveLayer('0'); // Reset active layer to 0 after loading
      } else {
        // If 'layers' property is missing or invalid in the JSON, reset keymap
        setKeymap({ '0': createEmptyGrid() });
        setActiveLayer('0');
      }

      // Handle combos (for now, just acknowledge their presence if they exist)
      if (parsedJson.combos && Array.isArray(parsedJson.combos)) {
          console.log("Combos found in JSON, but not currently used by UI:", parsedJson.combos);
          // If you later add UI for combos, you would set a state here
      }

      setModalContent({
        title: "JSON Loaded",
        message: "Configuration loaded from text area successfully."
      });
    } catch (error) {
      // Handle any JSON parsing errors
      setModalContent({
        title: "JSON Parsing Error",
        message: "Failed to parse JSON: " + error.message
      });
    } finally {
      setShowModal(true); // Always show a modal with the result
    }
  };

  // Macro functions:

  // Opens the MacroFormModal to add a new macro
  const handleAddMacro = () => {
    setEditingMacro(null); // Clear any existing macro data for a new entry
    setShowMacroFormModal(true);
  };

  // Opens the MacroFormModal to edit an existing macro
  const handleEditMacro = (macro) => {
    setEditingMacro(macro); // Set the macro to be edited
    setShowMacroFormModal(true);
  };

  // Saves a new or updated macro to the macros list
  const handleSaveMacro = (newMacro) => {
    if (newMacro.id) {
      // If macro has an ID, it's an existing macro being edited
      setMacros(prev => prev.map(m => m.id === newMacro.id ? newMacro : m));
    } else {
      // If no ID, it's a new macro
      setMacros(prev => [...prev, { ...newMacro, id: nextMacroId }]);
      setNextMacroId(prev => prev + 1); // Increment ID for the next new macro
    }
    setShowMacroFormModal(false); // Close the modal
  };

  // Initiates the macro deletion process by showing a confirmation modal
  const handleDeleteMacro = (id) => {
    setMacroToDeleteId(id); // Store the ID of the macro to be deleted
    setShowConfirmationModal(true);
  };

  // Confirms and performs the macro deletion
  const confirmDeleteMacro = () => {
    setMacros(prev => prev.filter(m => m.id !== macroToDeleteId)); // Filter out the macro to delete
    setShowConfirmationModal(false); // Close confirmation modal
    setMacroToDeleteId(null); // Clear the ID
  };

  // Function to open the Add Shortcut Modal
  const handleAddShortcut = () => {
    setShowAddShortcutModal(true);
  };

  // Function to save a new shortcut from the Add Shortcut Modal to the current category
  const handleSaveNewShortcut = (newShortcut) => {
    setShortcutPool(prevPool => {
      const newPool = { ...prevPool };
      // Ensure the currently selected category exists before adding
      if (!newPool[selectedShortcutCategory]) {
        newPool[selectedShortcutCategory] = [];
      }
      newPool[selectedShortcutCategory].push(newShortcut); // Add the new shortcut
      return newPool;
    });
    setShowAddShortcutModal(false); // Close the modal after saving
  };

  // Generates new shortcuts using AI based on user prompt
  const generateAiShortcuts = async () => {
    setIsGeneratingAiShortcuts(true); // Set loading state
    try {
      const chatHistory = [];
      // Construct the prompt for the AI model
      const promptText = `Generate a JSON array of 5-10 common keyboard shortcuts based on the following request: "${aiPrompt}". Each object in the array should have two properties: "combo" (the actual key combination, e.g., "Ctrl+C", "Win+D", "KC_MPLY") and "description" (a brief explanation of what the shortcut does, e.g., "Copy selected text", "Show desktop", "Play/Pause media"). Ensure the output is valid JSON and only contains the array.`;

      chatHistory.push({ role: "user", parts: [{ text: promptText }] });
      const payload = {
        contents: chatHistory,
        generationConfig: {
          responseMimeType: "application/json", // Request JSON output
          responseSchema: { // Define the expected JSON schema
            type: "ARRAY",
            items: {
              type: "OBJECT",
              properties: {
                "combo": { "type": "STRING" },
                "description": { "type": "STRING" }
              },
              "propertyOrdering": ["combo", "description"]
            }
          }
        }
      };

      const apiKey = ""; // API key will be provided by Canvas at runtime
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

      // Make the API call to Gemini
      const response = await fetch(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const result = await response.json(); // Parse the JSON response from the API

      // Check for valid response structure
      if (result.candidates && result.candidates.length > 0 &&
          result.candidates[0].content && result.candidates[0].content.parts &&
          result.candidates[0].content.parts.length > 0) {
        const jsonString = result.candidates[0].content.parts[0].text;
        const generatedShortcuts = JSON.parse(jsonString); // Parse the generated JSON string

        if (Array.isArray(generatedShortcuts)) {
          // Add generated shortcuts to a new "AI GENERATED" category in the shortcut pool
          setShortcutPool(prev => ({
            ...prev,
            "AI GENERATED": generatedShortcuts.filter(s => s.combo && s.description).map(s => ({...s, isCustomShortcut: true})) // Mark as custom
          }));
          setSelectedShortcutCategory("AI GENERATED"); // Automatically switch to the new category
          setModalContent({
            title: "AI Shortcuts Generated",
            message: "New shortcuts added to 'AI GENERATED' category in the shortcut pool."
          });
        } else {
          throw new Error("AI response was not a valid array of shortcuts.");
        }
      } else {
        throw new Error("No valid response from AI for shortcuts.");
      }
    } catch (error) {
      console.error("AI Generation Error:", error);
      setModalContent({
        title: "AI Generation Failed",
        message: "Could not generate shortcuts. Please try again or refine your prompt. Error: " + error.message
      });
    } finally {
      setIsGeneratingAiShortcuts(false); // Reset loading state
      setShowModal(true); // Show modal with status
    }
  };

  // Generates new macros using AI based on user prompt
  const generateAiMacros = async () => {
    setIsGeneratingAiMacros(true); // Set loading state
    try {
      const chatHistory = [];
      // Construct the prompt for the AI model
      const promptText = `Generate a JSON array of 1-3 simple macros based on the following request: "${aiMacroPrompt}". Each object in the array should have two properties: "name" (a short descriptive name for the macro) and "sequence" (the key sequence for the macro, e.g., "Hello World!{Enter}", "Ctrl+S{Delay 100}Ctrl+P"). Use common key names like {Enter}, {Tab}, {Space}, {Escape}, {Backspace}, {Delete} for special keys. Ensure the output is valid JSON and only contains the array.`;

      chatHistory.push({ role: "user", parts: [{ text: promptText }] });
      const payload = {
        contents: chatHistory,
        generationConfig: {
          responseMimeType: "application/json", // Request JSON output
          responseSchema: { // Define the expected JSON schema
            type: "ARRAY",
            items: {
              type: "OBJECT",
              properties: {
                "name": { "type": "STRING" },
                "sequence": { "type": "STRING" }
              },
              "propertyOrdering": ["name", "sequence"]
            }
          }
        }
      };

      const apiKey = ""; // API key will be provided by Canvas at runtime
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

      // Make the API call to Gemini
      const response = await fetch(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const result = await response.json(); // Parse the JSON response from the API

      // Check for valid response structure
      if (result.candidates && result.candidates.length > 0 &&
          result.candidates[0].content && result.candidates[0].content.parts &&
          result.candidates[0].content.parts.length > 0) {
        const jsonString = result.candidates[0].content.parts[0].text;
        const generatedMacros = JSON.parse(jsonString); // Parse the generated JSON string

        if (Array.isArray(generatedMacros)) {
          setMacros(prev => {
            let currentId = nextMacroId;
            // Map generated macros to include unique IDs and add them to the existing list
            const newMacros = generatedMacros.map(m => ({
              id: currentId++,
              name: m.name,
              sequence: m.sequence
            }));
            setNextMacroId(currentId); // Update the next available macro ID
            return [...prev, ...newMacros.filter(m => m.name && m.sequence)]; // Filter out malformed entries
          });
          setModalContent({
            title: "AI Macros Generated",
            message: "New macros added to your list."
          });
        } else {
          throw new Error("AI response was not a valid array of macros.");
        }
      } else {
        throw new Error("No valid response from AI for macros.");
      }
    } catch (error) {
      console.error("AI Macro Generation Error:", error);
      setModalContent({
        title: "AI Macro Generation Failed",
        message: "Could not generate macros. Please try again or refine your prompt. Error: " + error.message
      });
    } finally {
      setIsGeneratingAiMacros(false); // Reset loading state
      setShowModal(true); // Show modal with status
    }
  };


  // --- START OF COMPONENT RENDERING ---
  return (
    <div className="min-h-screen bg-zinc-800 text-white flex flex-col lg:flex-row font-inter">
      {/* Sidebar Navigation */}
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
              <a href="#" onClick={() => setActiveTab('save-load')} className={`flex items-center ${activeTab === 'save-load' ? 'text-red-300' : 'text-zinc-400'} hover:text-white transition-colors duration-200`}>
                <svg className="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 20 20"><path d="M5 4a2 1 0 012-2h6a2 1 0 012 2v14l-5-2.5L5 18V4z"></path></svg>
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

      {/* Main Content Area */}
      <div className="flex-grow p-4 lg:p-8 bg-zinc-800 flex flex-col">
        {/* Top Bar - Simplified for device info */}
        <div className="flex justify-end items-center mb-4 pb-4 border-b border-zinc-700">
          <div className="text-zinc-500 text-sm sm:text-base">
            <span className="mr-1 sm:mr-2">1UP60HSE</span>
          </div>
        </div>

        {/* Conditional rendering based on activeTab */}
        {activeTab === 'keymap' && (
          <>
            {/* Keymap Section */}
            <div className="mb-6 lg:mb-10">
              <h2 className="text-xl font-bold text-red-300 mb-4">KEYMAP</h2>
              <div className="flex space-x-2 mb-6">
                {/* Layer selection buttons */}
                {['0', '1', '2', '3'].map(layer => (
                  <button
                    key={layer}
                    onClick={() => setActiveLayer(layer)}
                    className={`px-3 py-1 sm:px-4 sm:py-2 rounded-md font-semibold text-sm sm:text-lg transition-colors duration-200 ${activeLayer === layer ? 'bg-red-600 text-white' : 'bg-zinc-700 text-zinc-300 hover:bg-zinc-600'}`}
                  >
                    {layer}
                  </button>
                ))}
              </div>

              {/* Micropad Grid Display */}
              {keymap[activeLayer] && keymap[activeLayer].length > 0 ? (
                <div className="bg-zinc-900 p-4 sm:p-6 rounded-lg shadow-inner border border-zinc-700 w-fit mx-auto">
                  <div className="grid grid-cols-3 gap-2">
                    {keymap[activeLayer].map((row, rIdx) =>
                      row.map((cell, cIdx) => (
                        <KeyComponent // Render each key using the KeyComponent
                          key={`${rIdx}-${cIdx}`}
                          keyData={cell.tap || {}} // Pass tap data to KeyComponent
                          isMacro={cell.tap && cell.tap.isMacro} // Pass isMacro flag
                          isShortcut={cell.tap && cell.tap.isCustomShortcut} // Pass isCustomShortcut flag
                          // Drag and drop props for reordering and assigning
                          draggable
                          onDragStart={(e) => handleKeymapDragStart(e, cell, rIdx, cIdx)}
                          onDrop={(e) => handleDrop(e, rIdx, cIdx)}
                          onDragOver={(e) => e.preventDefault()} // Allow drop
                          onDragEnd={handleDragEnd}
                          // Tailwind classes for styling and hover effects (removed bg-zinc-700 and text-white)
                          className={`
                            w-20 h-20 sm:w-24 sm:h-24 rounded-md shadow-md border border-zinc-600
                            flex flex-col justify-center items-center cursor-grab active:cursor-grabbing
                            relative overflow-hidden
                            transform transition-all duration-200
                            ${draggedShortcut ? 'border-dashed border-red-300' : 'hover:bg-red-600 hover:scale-105'}
                          `}
                        />
                      ))
                    )}
                  </div>
                </div>
              ) : (
                // Message when the current layer's keymap is empty
                <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 h-48 flex items-center justify-center text-zinc-400 text-lg text-center">
                  No keymap configured for Layer {activeLayer}. Drag shortcuts from the pool below to configure this layer.
                </div>
              )}
            </div>

            {/* Shortcut Pool Section */}
            <div className="mt-6 lg:mt-10 w-full">
              <h2 className="text-xl text-red-400 font-bold mb-4">SHORTCUTS</h2>
              {/* Category Selection Buttons */}
              <div className="flex flex-wrap gap-2 mb-4 p-2 bg-zinc-900 rounded-lg border border-zinc-700 overflow-x-auto custom-scrollbar">
                {Object.keys(shortcutPool).map(category => (
                  <button
                    key={category}
                    onClick={() => setSelectedShortcutCategory(category)}
                    className={`
                      px-4 py-2 rounded-md font-semibold text-sm
                      ${selectedShortcutCategory === category ? 'bg-red-600 text-white' : 'bg-zinc-700 text-zinc-300 hover:bg-zinc-600'}
                      transition-colors duration-200 flex-shrink-0
                    `}
                  >
                    {category.replace(/_/g, ' ')} {/* Display category name nicely */}
                  </button>
                ))}
              </div>

              {/* Display Area for Selected Category's Shortcuts */}
              <div className="bg-zinc-900 p-4 rounded-xl shadow-xl border border-red-600">
                <h3 className="text-lg font-semibold mb-3 text-red-300 border-b border-red-500 pb-2">
                  {selectedShortcutCategory.replace(/_/g, ' ')} Shortcuts
                </h3>
                <div className="grid grid-cols-auto-fit-minmax gap-2" style={{ gridTemplateColumns: 'repeat(auto-fit, minmax(80px, 1fr))' }}>
                  {shortcutPool[selectedShortcutCategory] && shortcutPool[selectedShortcutCategory].map((s, i) => (
                    <div
                      key={`${selectedShortcutCategory}-${i}`}
                      draggable
                      onDragStart={(e) => handleShortcutDragStart(e, s)}
                      onDragEnd={handleDragEnd}
                      className="
                        w-full h-20 bg-zinc-700 text-white rounded-md shadow-md cursor-grab
                        hover:bg-red-500 hover:scale-105 transition-all duration-200
                        flex flex-col items-center justify-center text-center text-sm font-medium
                        relative overflow-hidden
                      "
                    >
                      <span className="relative z-10 px-1">{s.description || s.combo}</span>
                      {/* Hidden input for editing shortcut combo directly */}
                      <input
                        type="text"
                        value={s.combo}
                        onChange={(e) => updatePreset(selectedShortcutCategory, i, { ...s, combo: e.target.value, description: s.description || e.target.value })}
                        onClick={(e) => e.stopPropagation()} // Prevent drag start when clicking input
                        className="absolute inset-0 w-full h-full bg-transparent text-transparent border-none focus:outline-none cursor-text opacity-0"
                        style={{ zIndex: 10 }} // Ensure input is clickable
                      />
                    </div>
                  ))}
                  {/* Button to add a new custom shortcut to the current category */}
                  <button
                    onClick={handleAddShortcut}
                    className="
                      w-full h-20 bg-zinc-800 hover:bg-zinc-700 text-white text-sm py-2 rounded-md transition-colors duration-200
                      flex items-center justify-center shadow-md border border-zinc-600 hover:border-red-500
                    "
                  >
                    + Add Shortcut
                  </button>
                </div>
              </div>

              {/* AI Shortcut Generator Section */}
              <div className="mt-8 bg-zinc-900 p-4 rounded-xl shadow-xl border border-blue-600">
                <h3 className="text-lg font-semibold mb-3 text-blue-300 border-b border-blue-500 pb-2">AI-POWERED SHORTCUT GENERATOR</h3>
                <p className="text-sm text-zinc-400 mb-3">Describe the shortcuts you need (e.g., "common shortcuts for web browsing in macOS", "media controls for Windows").</p>
                <textarea
                  className="w-full h-24 bg-zinc-800 text-white p-3 rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-blue-500 font-mono text-sm"
                  placeholder="e.g., shortcuts for navigating documents in Linux"
                  value={aiPrompt}
                  onChange={(e) => setAiPrompt(e.target.value)}
                ></textarea>
                <button
                  onClick={generateAiShortcuts}
                  disabled={isGeneratingAiShortcuts}
                  className="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white text-lg py-2 rounded-lg transition-colors duration-200 shadow-lg disabled:opacity-50 disabled:cursor-not-allowed"
                >
                  {isGeneratingAiShortcuts ? "Generating..." : "Generate with AI"}
                </button>
              </div>
            </div>
          </>
        )}

        {/* Macros Tab Content */}
        {activeTab === 'macros' && (
          <div className="w-full max-w-4xl mx-auto">
            <h2 className="text-xl font-bold text-red-300 mb-4">MACROS</h2>
            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 mb-6">
              <button
                onClick={handleAddMacro}
                className="bg-red-600 hover:bg-red-700 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-75 mb-4"
              >
                + Add New Macro
              </button>
              {macros.length === 0 ? (
                <p className="text-zinc-400">No macros defined yet. Add a new macro or use the AI generator below.</p>
              ) : (
                <div className="space-y-4">
                  {macros.map(macro => (
                    <div key={macro.id} className="bg-zinc-800 p-4 rounded-md border border-zinc-700 flex flex-col sm:flex-row justify-between items-start sm:items-center">
                      <div className="mb-2 sm:mb-0">
                        <h4 className="font-semibold text-lg text-red-200">{macro.name}</h4>
                        <p className="text-sm text-zinc-300 break-all">{macro.sequence}</p>
                      </div>
                      <div className="flex space-x-2">
                        <button onClick={() => handleEditMacro(macro)} className="bg-blue-600 hover:bg-blue-700 text-white px-3 py-1 rounded-md text-sm">Edit</button>
                        <button onClick={() => handleDeleteMacro(macro.id)} className="bg-red-600 hover:bg-red-700 text-white px-3 py-1 rounded-md text-sm">Delete</button>
                      </div>
                    </div>
                  ))}
                </div>
              )}
            </div>

            {/* AI Macro Generator Section */}
            <div className="mt-8 bg-zinc-900 p-4 rounded-xl shadow-xl border border-blue-600">
              <h3 className="text-lg font-semibold mb-3 text-blue-300 border-b border-blue-500 pb-2">AI-POWERED MACRO GENERATOR</h3>
              <p className="text-sm text-zinc-400 mb-3">Describe the macros you need (e.g., "macro for opening calculator", "email signature macro").</p>
              <textarea
                className="w-full h-24 bg-zinc-800 text-white p-3 rounded-md border border-zinc-600 focus:outline-none focus:ring-2 focus:ring-blue-500 font-mono text-sm"
                placeholder="e.g., macro for inserting current date"
                value={aiMacroPrompt}
                onChange={(e) => setAiMacroPrompt(e.target.value)}
              ></textarea>
              <button
                onClick={generateAiMacros}
                disabled={isGeneratingAiMacros}
                className="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white text-lg py-2 rounded-lg transition-colors duration-200 shadow-lg disabled:opacity-50 disabled:cursor-not-allowed"
              >
                {isGeneratingAiMacros ? "Generating..." : "Generate with AI"}
              </button>
            </div>
          </div>
        )}

        {/* Key Tester Tab Content */}
        {activeTab === 'keytester' && (
          <div className="w-full max-w-4xl mx-auto">
            <h2 className="text-xl font-bold text-red-300 mb-4">KEY TESTER</h2>
            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 h-64 overflow-y-auto custom-scrollbar">
              <p className="text-zinc-400 mb-4">Press any key on your physical keyboard to see its key code and key value.</p>
              {pressedKeys.length === 0 ? (
                <p className="text-zinc-500">No keys pressed yet...</p>
              ) : (
                <ul className="space-y-2">
                  {pressedKeys.map((keyInfo, index) => (
                    <li key={index} className="bg-zinc-700 p-2 rounded-md font-mono text-sm">
                      <span className="text-red-300">Key:</span> {keyInfo.key} | <span className="text-blue-300">Code:</span> {keyInfo.code}
                    </li>
                  ))}
                </ul>
              )}
            </div>
          </div>
        )}

        {/* Save/Load Profile Tab Content */}
        {activeTab === 'save-load' && (
          <div className="flex flex-col items-center justify-center h-full text-zinc-400 text-2xl w-full max-w-4xl mx-auto">
            <h2 className="text-xl font-bold text-red-300 mb-4">SAVE / LOAD Profile</h2>
            <div className="bg-zinc-900 p-6 rounded-lg shadow-inner border border-zinc-700 w-full flex flex-wrap justify-center gap-4 mt-8">
              <button onClick={saveProfile} className="bg-zinc-700 hover:bg-zinc-600 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-zinc-500 focus:ring-opacity-75">
                Save Profile
              </button>
              <button onClick={loadProfile} className="bg-zinc-700 hover:bg-zinc-600 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-zinc-500 focus:ring-opacity-75">
                Load Profile
              </button>
            </div>
          </div>
        )}

        {/* Settings Tab Content */}
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
                {!connectedPort ? (
                  <button onClick={connectToDevice} className="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-75">
                    Connect to Micropad
                  </button>
                ) : (
                  <>
                    <button onClick={uploadKeymapToConnectedDevice} className="bg-white text-black hover:bg-zinc-200 px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-white focus:ring-opacity-75">
                      Upload Keymap to Device
                    </button>
                    <button onClick={disconnectDevice} className="bg-zinc-700 hover:bg-zinc-600 text-white px-6 py-3 rounded-full shadow-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-zinc-500 focus:ring-opacity-75">
                      Disconnect Micropad
                    </button>
                  </>
                )}
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
              {/* This JSON.stringify renders the current keymap state as formatted JSON */}
              {JSON.stringify({
                layers: Object.keys(keymap).map(layerNum => {
                  const flatLayer = [];
                  for (let r = 0; r < 3; r++) {
                      for (let c = 0; c < 3; c++) {
                          const cell = keymap[layerNum][r][c];
                          flatLayer.push(cell.tap ? cell.tap.combo : "KC_NO");
                      }
                  }
                  return flatLayer;
                }),
                macros: Object.fromEntries(
                  macros.map(macro => [
                    `MACRO_${macro.name.toUpperCase().replace(/\s/g, '_').replace(/[^A-Z0-9_]/g, '')}`,
                    [macro.sequence]
                  ])
                ),
                combos: [] // Always show empty combos in preview for now
              }, null, 2)}
            </pre>
          </div>
        )}
      </div>

      {/* Modals (these components are defined within this App.js file) */}
      {/* General Info/Error Modal */}
      <Modal
        show={showModal}
        title={modalContent.title}
        message={modalContent.message}
        onClose={() => setShowModal(false)}
        customButtons={modalContent.customButtons} // Pass custom buttons if needed
      />

      {/* Macro Form Modal for adding/editing macros */}
      <MacroFormModal
        show={showMacroFormModal}
        onClose={() => setShowMacroFormModal(false)}
        onSave={handleSaveMacro}
        macro={editingMacro} // Pass the macro object if editing
      />

      {/* Confirmation Modal for deleting macros */}
      <ConfirmationModal
        show={showConfirmationModal}
        onClose={() => setShowConfirmationModal(false)}
        onConfirm={confirmDeleteMacro}
        message="Are you sure you want to delete this macro? This action cannot be undone."
      />

      {/* Add Shortcut Modal for adding custom shortcuts */}
      <AddShortcutModal
        show={showAddShortcutModal}
        onClose={() => setShowAddShortcutModal(false)}
        onSave={handleSaveNewShortcut}
      />
    </div>
  );
}
