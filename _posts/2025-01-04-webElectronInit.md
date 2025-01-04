---
title: "[Web] 일렉트론 환경구축"

sidebar:
  nav: "dev"
---

<br/>

# 1. Electron-Vite 프로젝트 생성

> 설치 참고 : [https://electron-vite.org/guide/](https://electron-vite.org/guide/)
> {: .notice--info}

```bash
$ npm create @quick-start/electron@latest
$ npm install
$ npm run dev
```

- 생성된 폴더 내에서 `npm run dev` 명령어를 실행하면 실시간 미리보기가 가능하다.
- `npm run preview` 명령어를 실행하면 build된 결과를 preview로 볼 수 있다.
- `npm run build:win` 명령어를 실행하면 윈도우용 빌드를 진행한다.

<br/>

# 2. Tailwind CSS 라이브러리 설치

## (1) 라이브러리 설치

> 설치 참고 : [https://tailwindcss.com/docs/guides/vite](https://tailwindcss.com/docs/guides/vite)
> {: .notice--info}

프로젝트 폴더 안에서 아래 명령어를 실행한다.

```bash
$ npm install -D tailwindcss postcss autoprefixer
$ npx tailwindcss init -p
```

## (2) `postcss.config.js` 파일을 `postcss.config.cjs` 으로 확장자 변경

## (3) `tailwind.config.cjs` 파일 수정

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/renderer/index.html",
    "./src/renderer/src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## (4) `src/renderer/src/assets` 내의 다른 파일들 모두 삭제

## (5) `src/renderer/src/assets/index.css` 파일 생성

```css
body {
  margin: 0;
  display: flex;
  justify-content: center;
  min-height: 100vh;
  @apply text-[#404040];
  @apply font-['NanumSquareRound-B'];
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}

@tailwind base;
@tailwind components;
@tailwind utilities;

@font-face {
  font-family: "NanumSquareNeo-B";
  src: url("./fonts/NanumSquareNeo/NanumSquareNeoTTF-cBd.woff");
}

@font-face {
  font-family: "NanumSquareNeo-EB";
  src: url("./fonts/NanumSquareNeo/NanumSquareNeoTTF-dEb.woff");
}

@font-face {
  font-family: "NanumSquareNeo-HB";
  src: url("./fonts/NanumSquareNeo/NanumSquareNeoTTF-eHv.woff");
}

@font-face {
  font-family: "NanumSquareNeo-L";
  src: url("./fonts/NanumSquareNeo/NanumSquareNeoTTF-aLt.woff");
}

@font-face {
  font-family: "NanumSquareNeo-R";
  src: url("./fonts/NanumSquareNeo/NanumSquareNeoTTF-bRg.woff");
}

@font-face {
  font-family: "NanumSquareRound-B";
  src: url("./fonts/NanumSquareRound/NanumSquareRoundOTFB.otf");
}

@font-face {
  font-family: "NanumSquareRound-EB";
  src: url("./fonts/NanumSquareRound/NanumSquareRoundOTFEB.otf");
}

@font-face {
  font-family: "NanumSquareRound-L";
  src: url("./fonts/NanumSquareRound/NanumSquareRoundOTFL.otf");
}

@font-face {
  font-family: "NanumSquareRound-R";
  src: url("./fonts/NanumSquareRound/NanumSquareRoundOTFR.otf");
}
```

## (6) `src/renderer/src/assets/fonts` 폴더에 폰트 파일 넣기

<br/>

# 3. Redux toolkit 설치

## (1) 라이브러리 설치

```bash
$ npm install @reduxjs/toolkit react-redux
```

## (2) `src\renderer\src\redux\index.jsx` 파일 생성

```javascript
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({
  reducer: {},
});

export default store;
```

## (3) `src\renderer\src\main.jsx` 수정

```javascript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

import "@assets/index.css";
import { Provider } from "react-redux";
import store from "@redux";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

<br/>

# 4. `electron-store` 라이브러리 설치

## (1) 라이브러리 설치

```bash
$ npm install electron-store
```

<br/>

# 5. `package.json` 파일 수정

아래 내용을 추가한다.

```javascript
{
	"type": "module",
}
```

<br/>

# 6. `src\renderer\src\App.jsx` 파일 수정

```javascript
import Test from "@components/Test";

function App() {
  return (
    <>
      <Test />
    </>
  );
}

export default App;
```

<br/>

# 7. `src\renderer\src\components\Test.jsx` 파일 생성

```javascript
function Test() {
  return (
    <>
      <h1>Test</h1>
    </>
  );
}

export default Test;
```

<br/>

# 8. `src\renderer\index.html` 파일 수정

`{프로젝트 이름}` 부분은 적절히 수정한다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>{프로젝트 이름}</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP -->
    <meta
      http-equiv="Content-Security-Policy"
      content="default-src 'self' http://localhost:* ws://127.0.0.1:*; script-src 'self'; style-src 'self' 'unsafe-inline'"
    />
  </head>

  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

<br/>

# 9. `src\main\index.js` 파일 수정

```javascript
import { app, shell, BrowserWindow, dialog, ipcMain } from "electron";
import { join } from "path";
import { electronApp, optimizer, is } from "@electron-toolkit/utils";
import icon from "../../resources/icon.png?asset";

import Store from "electron-store";

function createWindow() {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 1280,
    height: 720,
    minWidth: 1280,
    minHeight: 720,
    show: false,
    autoHideMenuBar: true,
    ...(process.platform === "linux" ? { icon } : {}),
    webPreferences: {
      preload: join(__dirname, "../preload/index.js"),
      sandbox: false,
    },
  });
  mainWindow.removeMenu();

  mainWindow.on("ready-to-show", () => {
    mainWindow.show();
  });

  mainWindow.webContents.setWindowOpenHandler((details) => {
    shell.openExternal(details.url);
    return { action: "deny" };
  });

  // HMR for renderer base on electron-vite cli.
  // Load the remote URL for development or the local html file for production.
  if (is.dev && process.env["ELECTRON_RENDERER_URL"]) {
    mainWindow.loadURL(process.env["ELECTRON_RENDERER_URL"]);
  } else {
    mainWindow.loadFile(join(__dirname, "../renderer/index.html"));
  }
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.whenReady().then(() => {
  // Set app user model id for windows
  electronApp.setAppUserModelId("com.electron");

  // Default open or close DevTools by F12 in development
  // and ignore CommandOrControl + R in production.
  // see https://github.com/alex8088/electron-toolkit/tree/master/packages/utils
  app.on("browser-window-created", (_, window) => {
    optimizer.watchWindowShortcuts(window);
  });

  ipcMain.handle("message", async (event, type, title, message) => {
    return dialog.showMessageBox(BrowserWindow.fromWebContents(event.sender), {
      message: message,
      type: type,
      title: title,
    });
  });

  ipcMain.handle("openDir", async (event, defalut_path) => {
    return dialog
      .showOpenDialog(BrowserWindow.fromWebContents(event.sender), {
        defaultPath: defalut_path,
        properties: ["openDirectory"],
      })
      .then(({ canceled, filePaths }) => {
        if (canceled) return;
        return filePaths[0];
      });
  });

  ipcMain.handle("openFile", async (event, filters) => {
    return dialog
      .showOpenDialog(BrowserWindow.fromWebContents(event.sender), {
        filters: filters,
      })
      .then(({ canceled, filePaths }) => {
        if (canceled) return;
        return filePaths[0];
      });
  });

  ipcMain.handle("saveFile", async (event, filters) => {
    return dialog
      .showSaveDialog(BrowserWindow.fromWebContents(event.sender), {
        filters: filters,
      })
      .then(({ canceled, filePath }) => {
        if (canceled) return;
        return filePath;
      });
  });

  ipcMain.handle("setStore", (_, key, value) => {
    const store = new Store();
    store.set(key, value);
    return;
  });

  ipcMain.handle("getStore", (_, key) => {
    const store = new Store();
    return store.get(key);
  });

  createWindow();

  app.on("activate", function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (BrowserWindow.getAllWindows().length === 0) createWindow();
  });
});

// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on("window-all-closed", () => {
  if (process.platform !== "darwin") {
    app.quit();
  }
});

// In this file you can include the rest of your app"s specific main process
// code. You can also put them in separate files and require them here.
```

<br/>

# 10. `src\preload\index.js` 파일 수정

```javascript
import { contextBridge, ipcRenderer } from "electron";
import { electronAPI } from "@electron-toolkit/preload";

// Custom APIs for renderer
const api = {};

// Use `contextBridge` APIs to expose Electron APIs to
// renderer only if context isolation is enabled, otherwise
// just add to the DOM global.
if (process.contextIsolated) {
  try {
    contextBridge.exposeInMainWorld("electron", electronAPI);
    contextBridge.exposeInMainWorld("api", api);
  } catch (error) {
    console.error(error);
  }
} else {
  window.electron = electronAPI;
  window.api = api;
}

contextBridge.exposeInMainWorld("electronAPI", {
  message: (type, title, message) =>
    ipcRenderer.invoke("message", type, title, message),
  openDir: (defalut_path) => ipcRenderer.invoke("openDir", defalut_path),
  openFile: (filters) => ipcRenderer.invoke("openFile", filters),
  saveFile: (filters) => ipcRenderer.invoke("saveFile", filters),
  setStore: (key, value) => ipcRenderer.invoke("setStore", key, value),
  getStore: (key) => ipcRenderer.invoke("getStore", key),
});
```

<br/>

# 11. `.eslintrc.cjs` 파일 수정

```css
module.exports = {
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    '@electron-toolkit',
    '@electron-toolkit/eslint-config-prettier'
  ],
  rules: {
    'prettier/prettier': [
      'error',
      {
        endOfLine: 'auto'
      }
    ],
    'react/no-unknown-property': [
      'error',
      {
        ignore: [
          'intensity',
          'args',
          'position',
          'rotation',
          'attach',
          'array',
          'count',
          'itemSize',
          'object',
          'enableRotate',
          'frustumCulled',
          'transparent'
        ]
      }
    ]
  }
}
```

<br/>

# 12. `.gitignore` 파일 수정

```
node_modules
dist
out
.DS_Store
*.log*

.vscode
```

<br/>

# 13. `electron-builder.yml` 파일 수정

`{프로젝트 이름}` 부분은 적절히 수정한다.

```yaml
appId: com.electron.app
productName: { 프로젝트 이름 }
directories:
  buildResources: build
files:
  - "!**/.vscode/*"
  - "!src/*"
  - "!electron.vite.config.{js,ts,mjs,cjs}"
  - "!{.eslintignore,.eslintrc.cjs,.prettierignore,.prettierrc.yaml,dev-app-update.yml,CHANGELOG.md,README.md}"
  - "!{.env,.env.*,.npmrc,pnpm-lock.yaml}"
asarUnpack:
  - resources/**
win:
  executableName: { 프로젝트 이름 }
nsis:
  artifactName: ${name}-${version}-setup.${ext}
  shortcutName: ${productName}
  uninstallDisplayName: ${productName}
  createDesktopShortcut: always
  oneClick: false
  allowToChangeInstallationDirectory: true
mac:
  entitlementsInherit: build/entitlements.mac.plist
  extendInfo:
    - NSCameraUsageDescription: Application requests access to the device's camera.
    - NSMicrophoneUsageDescription: Application requests access to the device's microphone.
    - NSDocumentsFolderUsageDescription: Application requests access to the user's Documents folder.
    - NSDownloadsFolderUsageDescription: Application requests access to the user's Downloads folder.
  notarize: false
dmg:
  artifactName: ${name}-${version}.${ext}
linux:
  target:
    - AppImage
    - snap
    - deb
  maintainer: electronjs.org
  category: Utility
appImage:
  artifactName: ${name}-${version}.${ext}
npmRebuild: false
publish:
  provider: generic
  url: https://example.com/auto-updates
```

<br/>

# 14. `electron.vite.config.mjs` 파일 수정

```javascript
import { resolve } from "path";
import { defineConfig, externalizeDepsPlugin } from "electron-vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  main: {
    plugins: [externalizeDepsPlugin()],
  },
  preload: {
    plugins: [externalizeDepsPlugin()],
  },
  renderer: {
    resolve: {
      alias: {
        "@renderer": resolve("src/renderer/src"),
        "@assets": resolve("src/renderer/src/assets"),
        "@components": resolve("src/renderer/src/components"),
        "@utils": resolve("src/renderer/src/utils"),
        "@redux": resolve("src/renderer/src/redux"),
      },
    },
    plugins: [react()],
  },
});
```

<br/>
