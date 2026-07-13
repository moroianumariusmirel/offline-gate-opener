# Offline Gate Opener (Web Client)

This folder contains a standalone, fully offline web client designed to connect to and open your `WBT01` gate opener over Bluetooth Low Energy (BLE) using the browser's Web Bluetooth API.

It does not make any network requests or send any telemetry. All cryptography and GATT operations are executed entirely on your local phone/device.

---

## Prerequisites (Browser Support)
The Web Bluetooth API is supported by default in:
- **Android**: Google Chrome, Microsoft Edge, Opera, Samsung Internet.
- **Desktop (Windows/Mac/Linux/ChromeOS)**: Google Chrome, Microsoft Edge, Opera.
- **iOS (iPhone/iPad)**: Requires a Web Bluetooth browser app like **Bluefy** or **WebBLE** (since Safari blocks Web Bluetooth).

---

## Setting Up (Web Security Context)
For security reasons, web browsers only allow Web Bluetooth in **secure contexts**:
1. Accessed via `localhost` (e.g. `http://localhost:8000`).
2. Accessed via `https://` (e.g., hosted on a free HTTPS platform).

Here are the two easiest ways to use the app:

### Option A: Hosting on GitHub Pages (Recommended for Daily Phone Use)
Since Github Pages automatically hosts files securely under `https://` for free, you can access the gate controller directly from your phone's browser:
1. Create a free GitHub repository.
2. Upload `index.html` to it.
3. Go to **Settings** -> **Pages** in the repo, set the source branch to `main` (or `master`), and save.
4. Open the generated HTTPS URL on your phone's browser, fill in your credentials, and click **Connect**.
5. *Tip*: Tap "Add to Home Screen" in Chrome/Edge to save it as a standalone app!

### Option B: Local Server (For PCs / Laptops)
If you want to run it on your local computer:
1. Open a terminal in the folder containing `index.html`.
2. Start a local server:
   - **Using Python**:
     ```bash
     python3 -m http.server 8000
     ```
   - **Using Node (npx)**:
     ```bash
     npx http-server -p 8000
     ```
3. Open your browser and navigate to `http://localhost:8000`.

---

## How to Control the Gate
1. Tap **Connect**.
2. A browser dialog will scan for Bluetooth devices. Select your device (named `WBT01-XXXX`).
3. The app will:
   - Read the nonce challenge from the gate (`0000b001`).
   - Hash your passcode + PIN + nonce.
   - Write back the authenticated key to complete the handshake.
4. Once connected, tap **FULL OPEN**, **FULL CLOSE**, or **EMERGENCY STOP** to control the gate.
