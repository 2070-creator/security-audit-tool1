name: Build Windows Portable EXE

on:
  workflow_dispatch:
  push:
    branches: [ main, master ]

jobs:
  build-windows-exe:
    runs-on: windows-latest

    steps:
      - name: Checkout Source Code
        uses: actions/checkout@v4

      - name: Setup Node.js Environment
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      - name: Install Project Dependencies
        run: npm ci || npm install

      - name: Build Web Frontend (React + Vite)
        run: npm run build

      - name: Install Electron Build Tools
        run: npm install --save-dev electron electron-builder

      - name: Package Windows Portable EXE (Single Executable)
        run: npx electron-builder --win portable --x64

      - name: Upload EXE Binary Artifact
        uses: actions/upload-artifact@v4
        with:
          name: 제어망_PC_보안점검도구_Windows_x64_EXE
          path: dist_electron/*.exe
          if-no-files-found: error
