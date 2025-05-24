
Trkey Micropad Configurator
This is a web-based configurator for Trkey micropads, designed to allow users to easily define and manage keymaps for their custom 3x3 micropads using an intuitive interface.

🚀 Features
Intuitive Keymap Configuration:

Visual Grid: A clear 3x3 grid visually represents your micropad, making it easy to see your layout at a glance.

Drag-and-Drop Assignment: Effortlessly assign key actions by dragging shortcuts from the comprehensive pool directly onto any keycap in the grid.

Tap and Hold Actions: Configure distinct actions for both a quick "tap" and a prolonged "hold" on each key, maximizing functionality.

Human-Readable Descriptions: Keycaps display descriptive labels (e.g., "Copy", "Volume Up") making your layout easy to understand.

Multi-Layer Support:

Design and switch between multiple layers (e.g., Layer 0 for basic functions, Layer 1 for media controls) to expand your micropad's capabilities beyond its physical keys.

Comprehensive Shortcut Pool:

Organized Categories: Shortcuts are neatly categorized (e.g., Basic, Media, Macro, Layers, Special, QMK Lighting, Windows/macOS/Linux shortcuts, application-specific shortcuts like Minecraft, Fusion 360, Canva, etc.) for quick access.

Customizable Shortcuts: Easily edit the key combination or description of any shortcut within the pool to tailor it to your needs.

Add New Shortcuts: Create entirely new key combinations and add them to your preferred category in the shortcut pool.

AI-Powered Shortcut Generation:

Leverage AI to generate relevant shortcut suggestions based on your natural language prompts (e.g., "common shortcuts for web browsing," "media controls for Windows"). Generated shortcuts are added to a dedicated "AI GENERATED" category.

Advanced Macro Management:

Create Custom Macros: Define complex sequences of key presses and delays as custom macros.

Edit & Delete: Full control to modify or remove your created macros.

Peripheral Controls (Potentiometer Support):

Configure external controls like potentiometers, assigning functions such as volume control, scrolling, or custom QMK keycodes to them. This allows for rotary encoder or dial integration.

Real-time Key Tester:

A dedicated "Key Tester" tab allows you to press keys on your physical keyboard and instantly see their corresponding key values and codes, which is invaluable for debugging and verifying key presses.

Profile Management:

Save Profiles: Store your entire keymap configuration (including layers, macros, and peripheral settings) directly in your browser's local storage for easy recall.

Load Profiles: Quickly load previously saved configurations.

QMK JSON Integration:

Export Keymap JSON: Generate a complete QMK-compatible JSON file of your configured keymap, ready for flashing to your microcontroller.

Direct Device Upload: Connect directly to your ESP32-C3 (or other compatible) micropad via Web Serial API and upload your keymap configuration without needing external flashing tools.

Import JSON: Paste existing QMK keymap JSON directly into the configurator to load and visualize layouts from other sources.

User-Friendly Interface:

Sleek Design: Features a modern, dark theme with rounded corners and subtle gradients for an engaging visual experience.

Responsive Layout: Adapts seamlessly to different screen sizes, from mobile devices to large desktops.

Clear Navigation: An intuitive sidebar allows for easy switching between different configuration sections.

Custom Modals: Provides custom modal dialogs for notifications, confirmations, and input, enhancing the user experience.

🛠️ Technologies Used
React: A JavaScript library for building user interfaces.

Tailwind CSS: A utility-first CSS framework for rapid UI development.

Web Serial API: For direct communication with serial devices (e.g., microcontrollers).

Google Gemini API: For AI-powered shortcut generation.

NPM (Node Package Manager): For managing project dependencies.

GitHub Pages: For static website hosting.

gh-pages: A utility for deploying React applications to GitHub Pages.

💻 Getting Started (Local Development)
To get a local copy up and running, follow these simple steps.

Prerequisites
Node.js (LTS version recommended)

npm (comes with Node.js) or Yarn

Installation
Clone the repository (or ensure you have the project files in your local directory):

# If starting from scratch with a new project name:
npx create-react-app trkey-configurator
cd trkey-configurator

# If you already have your files, ensure you are in the project root:
cd /path/to/your/trkey-configurator-project

Install project dependencies:

npm install
# or
yarn install

Install gh-pages for deployment:

npm install --save-dev gh-pages
# or
yarn add --dev gh-pages

Project Structure
Ensure your core files are in their expected locations:

public/index.html: The main HTML file where the React app is mounted.

src/App.js: Your primary React component (Trkey Configurator UI).

src/index.js: The React entry point (renders App.js).

src/index.css: Your main CSS file (can be empty if only using Tailwind CDN).

src/reportWebVitals.js: (Optional) For web performance metrics.

Running the Application
To start the development server:

npm start
# or
yarn start

This will typically open the application in your browser at http://localhost:3000.

🚀 Deployment to GitHub Pages
This project is configured for easy deployment to GitHub Pages using the gh-pages package.

Configure package.json:
Open your package.json file and ensure you have the following lines. Remember to replace YOUR_USERNAME and YOUR_REPO_NAME with your actual GitHub details.

{
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


Run the deploy script:

npm run deploy
# or
yarn deploy


This command will build your application for production and push the build output to a gh-pages branch in your GitHub repository.

Enable GitHub Pages:

Go to your GitHub repository in your web browser.

Navigate to Settings > Pages.

Under "Branch", select gh-pages as the source and click Save.

Your site should then be published at the URL specified in your homepage field (e.g., https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/). Allow a few minutes for deployment.

⌨️ Keymap JSON Structure
The configurator aims to generate JSON data in a structure similar to this, which can then be used by microcontroller firmware:

{
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


Contributing
Feel free to open issues or submit pull requests if you have suggestions or improvements!

License
Tim
=======
# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
>>>>>>> 0be5c40 (Initial commit for Trkey React app)
