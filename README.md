# Electron Starter Template with React

A ready-to-use starter for building cross-platform desktop apps with **Electron** and **React** (Create React App).

Includes hot reload in development, a secure preload bridge, and production packaging for macOS, Windows, and Linux via `electron-builder`.

## Features

- React 18 + Create React App
- Electron main process with DevTools in development
- Preload script using `contextBridge` for safe renderer access
- Hot reload via `electronmon` + CRA
- One-command packaging for macOS (DMG), Windows (NSIS), and Linux (DEB)
- Navigation hardening in the main process

## Tech stack

| Layer | Tools |
| --- | --- |
| UI | React 18, Create React App |
| Desktop | Electron 32 |
| Dev tooling | concurrently, wait-on, electronmon, cross-env |
| Packaging | electron-builder |

## Prerequisites

- [Node.js](https://nodejs.org/) 18+ (LTS recommended)
- npm (comes with Node.js)

## Getting started

```bash
# Clone the repository
git clone https://github.com/<your-username>/Electron-starter-template-with-ReactJS.git
cd Electron-starter-template-with-ReactJS

# Install dependencies
npm install

# Run the Electron app in development
npm run electron:start
```

This starts the React dev server, waits until it is ready, then opens Electron with live reload.

To run the React UI in a browser only (no Electron window):

```bash
npm start
```

## Available scripts

| Script | Description |
| --- | --- |
| `npm start` | Start the CRA development server at `http://localhost:3000` |
| `npm test` | Run tests in watch mode |
| `npm run build` | Build the React app into the `build/` folder |
| `npm run electron:start` | Start Electron + React with hot reload |
| `npm run electron:package:mac` | Package a macOS `.dmg` |
| `npm run electron:package:win` | Package a Windows NSIS installer |
| `npm run electron:package:linux` | Package a Linux `.deb` |

> Packaging scripts expect a production React build. Run `npm run build` first, or ensure your packaging flow builds the app before calling `electron-builder`.

## Project structure

```text
.
├── public/
│   ├── electron.js   # Electron main process
│   ├── preload.js    # Preload / contextBridge bridge
│   └── index.html    # CRA HTML template
├── src/
│   ├── App.js        # Root React component
│   └── index.js      # React entry point
├── package.json      # Scripts, Electron, and electron-builder config
└── README.md
```

### How it fits together

1. **`public/electron.js`** — creates the `BrowserWindow`, loads `localhost:3000` in development or the built `index.html` in production, and applies basic navigation guards.
2. **`public/preload.js`** — exposes a small, controlled API to the renderer (example: `window.versions`).
3. **`src/`** — standard React app; edit UI here as you would in any CRA project.

## Packaging for distribution

1. Build the React app:

   ```bash
   npm run build
   ```

2. Package for your target OS:

   ```bash
   npm run electron:package:mac     # → dist/*.dmg
   npm run electron:package:win     # → dist/*.exe installer
   npm run electron:package:linux   # → dist/*.deb
   ```

Artifacts are written to the `dist/` directory.

### Customize the packaged app

Edit the `build` section in [`package.json`](./package.json):

```json
"build": {
  "appId": "com.electron.myapp",
  "productName": "My Electron App",
  ...
}
```

Also update `name`, `author`, and `description` at the top of `package.json` to match your project.

## Customization tips

- **App window** — adjust size and options in `createWindow()` inside `public/electron.js`.
- **Renderer bridge** — expose only what you need from `public/preload.js` via `contextBridge`.
- **Allowed navigation** — update `allowedNavigationDestinations` in `public/electron.js` before shipping.
- **Icons** — place build icons under `public/` (used as `buildResources` by electron-builder).

## License

This project is open source. Add a `LICENSE` file (for example MIT) before publishing if you want to clarify usage terms.
