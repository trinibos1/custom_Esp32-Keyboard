Trkey Micropad ConfiguratorThis is a web-based configurator for Trkey micropads, designed to allow users to easily define and manage keymaps for their custom 3x3 micropads using an intuitive interface.🚀 FeaturesIntuitive Keymap Configuration:Visual Grid: A clear 3x3 grid visually represents your micropad, making it easy to see your layout at a glance.Drag-and-Drop Assignment: Effortlessly assign key actions by dragging shortcuts from the comprehensive pool directly onto any keycap in the grid.Tap and Hold Actions: Configure distinct actions for both a quick "tap" and a prolonged "hold" on each key, maximizing functionality.Human-Readable Descriptions: Keycaps display descriptive labels (e.g., "Copy", "Volume Up") making your layout easy to understand.Multi-Layer Support:Design and switch between multiple layers (e.g., Layer 0 for basic functions, Layer 1 for media controls) to expand your micropad's capabilities beyond its physical keys.Comprehensive Shortcut Pool:Organized Categories: Shortcuts are neatly categorized (e.g., Basic, Media, Macro, Layers, Special, QMK Lighting, Windows/macOS/Linux shortcuts, application-specific shortcuts like Minecraft, Fusion 360, Canva, etc.) for quick access.Customizable Shortcuts: Easily edit the key combination or description of any shortcut within the pool to tailor it to your needs.Add New Shortcuts: Create entirely new key combinations and add them to your preferred category in the shortcut pool.AI-Powered Shortcut Generation:Leverage AI to generate relevant shortcut suggestions based on your natural language prompts (e.g., "common shortcuts for web browsing," "media controls for Windows"). Generated shortcuts are added to a dedicated "AI GENERATED" category.Advanced Macro Management:Create Custom Macros: Define complex sequences of key presses and delays as custom macros.Edit & Delete: Full control to modify or remove your created macros.Peripheral Controls (Potentiometer Support):Configure external controls like potentiometers, assigning functions such as volume control, scrolling, or custom QMK keycodes to them. This allows for rotary encoder or dial integration.Real-time Key Tester:A dedicated "Key Tester" tab allows you to press keys on your physical keyboard and instantly see their corresponding key values and codes, which is invaluable for debugging and verifying key presses.Profile Management:Save Profiles: Store your entire keymap configuration (including layers, macros, and peripheral settings) directly in your browser's local storage for easy recall.Load Profiles: Quickly load previously saved configurations.QMK JSON Integration:Export Keymap JSON: Generate a complete QMK-compatible JSON file of your configured keymap, ready for flashing to your microcontroller.Direct Device Upload: Connect directly to your ESP32-C3 (or other compatible) micropad via Web Serial API and upload your keymap configuration without needing external flashing tools.Import JSON: Paste existing QMK keymap JSON directly into the configurator to load and visualize layouts from other sources.User-Friendly Interface:Sleek Design: Features a modern, dark theme with rounded corners and subtle gradients for an engaging visual experience.Responsive Layout: Adapts seamlessly to different screen sizes, from mobile devices to large desktops.Clear Navigation: An intuitive sidebar allows for easy switching between different configuration sections.Custom Modals: Provides custom modal dialogs for notifications, confirmations, and input, enhancing the user experience.🛠️ Technologies UsedReact: A JavaScript library for building user interfaces.Tailwind CSS: A utility-first CSS framework for rapid UI development.Web Serial API: For direct communication with serial devices (e.g., microcontrollers).Google Gemini API: For AI-powered shortcut generation.NPM (Node Package Manager): For managing project dependencies.GitHub Pages: For static website hosting.gh-pages: A utility for deploying React applications to GitHub Pages.💻 Getting Started (Local Development)To get a local copy up and running, follow these simple steps.PrerequisitesNode.js (LTS version recommended)npm (comes with Node.js) or YarnInstallationClone the repository (or ensure you have the project files in your local directory):# If starting from scratch with a new project name:
npx create-react-app trkey-configurator
cd trkey-configurator

# If you already have your files, ensure you are in the project root:
cd /path/to/your/trkey-configurator-project
Install project dependencies:npm install
# or
yarn install
Install gh-pages for deployment:npm install --save-dev gh-pages
# or
yarn add --dev gh-pages
Project StructureEnsure your core files are in their expected locations:public/index.html: The main HTML file where the React app is mounted.src/App.js: Your primary React component (Trkey Configurator UI).src/index.js: The React entry point (renders App.js).src/index.css: Your main CSS file (can be empty if only using Tailwind CDN).src/reportWebVitals.js: (Optional) For web performance metrics.Running the ApplicationTo start the development server:npm start
# or
yarn start
This will typically open the application in your browser at http://localhost:3000.🚀 Deployment to GitHub PagesThis project is configured for easy deployment to GitHub Pages using the gh-pages package.Configure package.json:Open your package.json file and ensure you have the following lines. Remember to replace YOUR_USERNAME and YOUR_REPO_NAME with your actual GitHub details.{
  "name": "trkey-configurator",
  "version": "0.1.0",
  "private": true,
  "homepage": "https://YOUR_USERNAME.github.io/YOUR_REPO_NAME",
  "dependencies": {
    // ... (your existing dependencies)
  },
  "devDependencies": {
    "gh-pages": "^5.0.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  },
  // ... (rest of your package.json)
}

Run the deploy script:npm run deploy
# or
yarn deploy

This command will build your application for production and push the build output to a gh-pages branch in your GitHub repository.Enable GitHub Pages:Go to your GitHub repository in your web browser.Navigate to Settings > Pages.Under "Branch", select gh-pages as the source and click Save.Your site should then be published at the URL specified in your homepage field (e.g., https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/). Allow a few minutes for deployment.⌨️ Keymap JSON StructureThe configurator aims to generate JSON data in a structure similar to this, which can then be used by microcontroller firmware:{
  "layout": "3x3",
  "layers": {
    "0": [
      [
        { "tap": "KC_MPRV", "hold": null },
        { "tap": "KC_MNXT", "hold": null },
        { "tap": "KC_MPLY", "hold": null }
      ],
      [
        { "tap": "KC_MUTE", "hold": null },
        { "tap": "KC_VOLU", "hold": null },
        { "tap": "KC_VOLD", "hold": null }
      ],
      [
        { "tap": "Ctrl+C", "hold": null },
        { "tap": "Ctrl+V", "hold": null },
        { "tap": "Ctrl+D", "hold": null }
      ]
    ]
  }
}

ContributingFeel free to open issues or submit pull requests if you have suggestions or improvements!License Tim
