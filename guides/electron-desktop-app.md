# Electron desktop app recipe

Scope: web-shell desktop app + local/remote data toggle (devartslab-admin model).

## Tools

1. Xcode Command Line Tools: `xcode-select --install`
2. Node.js (mise), pnpm (fleet policy for devartslab repos)
3. npm packages: `electron`, `electron-builder`, `electron-store`, `electron-updater`, `electron-is-dev`, `concurrently`, `wait-on`
4. Built-ins: `iconutil`, `codesign`, `hdiutil`, `xattr`, `xcrun notarytool`, `xcrun stapler`
5. Optional: Apple Developer ID cert, keychain profile for notarization

## 1. Scaffold

1. `cd devartslab-admin`
2. `pnpm add electron-store && pnpm add -D electron electron-builder electron-is-dev concurrently wait-on`
3. Create `electron/main.cjs`:

   ```js
   const { app, BrowserWindow, ipcMain, net } = require("electron");
   const Store = require("electron-store");
   const isDev = !app.isPackaged;
   const store = new Store({ defaults: { dataSource: "local" } });

   const sources = {
     local: "http://localhost:8787",
     remote: process.env.REMOTE_API || "https://api.example.com",
   };

   ipcMain.handle("admin:data", async (_e, path, opts) => {
     const base = sources[store.get("dataSource")];
     const res = await net.fetch(base + path, opts); // no CORS, secrets stay in main
     return res.json();
   });
   ipcMain.handle("settings:get", (_e, k) => store.get(k));
   ipcMain.handle("settings:set", (_e, k, v) => store.set(k, v));

   app.whenReady().then(() => {
     const win = new BrowserWindow({
       width: 1440,
       height: 900,
       webPreferences: {
         preload: `${__dirname}/preload.cjs`,
         contextIsolation: true,
         nodeIntegration: false,
         sandbox: false,
       },
     });
     isDev ? win.loadURL("http://localhost:5173") : win.loadFile("dist/index.html");
   });
   app.on("window-all-closed", () => app.quit());
   ```

4. Create `electron/preload.cjs`:
   ```js
   const { contextBridge, ipcRenderer } = require("electron");
   contextBridge.exposeInMainWorld("admin", {
     data: (path, opts) => ipcRenderer.invoke("admin:data", path, opts),
     getSetting: (k) => ipcRenderer.invoke("settings:get", k),
     setSetting: (k, v) => ipcRenderer.invoke("settings:set", k, v),
   });
   ```
5. `vite.config.ts`: set `base: "./"` so `loadFile` resolves assets
6. Router: `createHashHistory()` (TanStack Router) — `file://` breaks history routing
7. `package.json`:
   - `"main": "electron/main.cjs"`
   - `"scripts": { "dev:electron": "concurrently \"vite\" \"wait-on tcp:5173 && electron .\"", "dist": "pnpm build && electron-builder --mac" }`
   - `"build": { "appId": "com.devartslab.admin", "productName": "DevArtsLab Admin", "files": ["electron/**/*", "dist/**/*"], "mac": { "target": "dmg", "category": "public.app-category.developer-tools" } }`

## 2. Data-source toggle (local | remote)

1. Toggle component: `admin.setSetting("dataSource", "local" | "remote")`
2. IPC layer reads `store.get("dataSource")` per call — no renderer restart needed
3. Local source options: `net.fetch` to localhost service, `better-sqlite3`, `fs`, `child_process` (spawn local tooling) — all inside `ipcMain.handle`
4. Remote secrets: load in main via `process.env` / vault env file; never reach renderer
5. Alt to `file://`: `protocol.registerSchemesAsPrivileged` + `protocol.handle("app://")` — gives a real origin, cleaner auth/cookie semantics
6. Broadcast source changes: `win.webContents.send("source:changed", v)` so renderer can refetch

## 3. Dev workflow

1. `pnpm dev:electron` — vite HMR in the Electron window
2. DevTools auto-open in dev: `win.webContents.openDevTools({ mode: "detach" })`
3. Test packaged path locally: `pnpm build && electron .` after `pnpm dist`

## 4. Package

1. Icon: `mkdir icon.iconset`, add `icon_16x16.png` … `icon_512x512@2x.png`, `iconutil -c icns icon.iconset`, move to `build/icon.icns`
2. `pnpm dist` → `dist-electron/mac/DevArtsLab Admin.app` + `dist-electron/DevArtsLab Admin-<ver>-arm64.dmg` (add `--x64` or `--universal` for other arch targets)
3. First launch auto-creates `~/Library/Application Support/DevArtsLab Admin` (Cookies, IndexedDB, Local Storage, Session Storage, SingletonLock — standard Chromium profile layout)
4. Unsigned local use: `xattr -cr "dist-electron/mac/DevArtsLab Admin.app"`

## 5. Distribution extras

1. Signed: `"identity": "Developer ID Application: Name (TEAMID)"` under `mac`
2. Notarize: `xcrun notarytool submit dist-electron/*.dmg --keychain-profile <profile> --wait`, then `xcrun stapler staple`
3. Camera/mic (proctoring-style, if needed): `build.mac.extendInfo` = `NSCameraUsageDescription` / `NSMicrophoneUsageDescription`; entitlements file with `com.apple.security.device.camera` / `audio-input`; set `build.mac.entitlements` + `entitlementsInherit`
4. Deep links: `build.protocols = [{ "name": "devartslab", "schemes": ["devartslab"] }]`; dev-mode `app.setAsDefaultProtocolClient("devartslab")`; handle `app.on("open-url")` on macOS
5. Auto-updates: `electron-updater` — `autoUpdater.checkForUpdatesAndNotify()` in main, `build.publish` config (GitHub Releases / generic host)
6. Single instance: `app.requestSingleInstanceLock()` (SingletonLock files appear regardless; explicit lock adds the `second-instance` event for deep-link routing)
7. Default entitlements injected by electron-builder: `allow-jit`, `allow-unsigned-executable-memory`, `disable-library-validation` — no action
8. No certs on the build machine: `CSC_IDENTITY_AUTO_DISCOVERY=false pnpm dist`
