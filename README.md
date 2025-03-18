# Expo and NativeWind Setup Guide

## Step 1: Create and Start Expo Project
```sh
npx create-expo-app@latest
npx expo start
```

## Step 2: Install Required Dependencies
```sh
npm install nativewind tailwindcss react-native-reanimated react-native-safe-area-context
npx tailwindcss init
```

## Step 3: Configure TailwindCSS
Edit `tailwind.config.js`:
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./app/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## Step 4: Create a Global CSS File
Create `global.css` inside the `./app` directory and add:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Step 5: Configure Babel
Edit `babel.config.js`:
```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ],
  };
};
```

## Step 6: Modify Metro Config
Run:
```sh
npx expo customize metro.config.js
```
Replace the contents of `metro.config.js` with:
```js
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require('nativewind/metro');

const config = getDefaultConfig(__dirname);

module.exports = withNativeWind(config, { input: './app/global.css' });
```

## Step 7: Import Global CSS
Import the global CSS file in `_layout.tsx`:
```js
import './global.css';
```

## Step 8: Start the Expo Project with Cache Clear
```sh
npx expo start --clear
```

