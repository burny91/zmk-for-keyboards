# Sofle Choc Split Keyboard (ZMK Firmware)

Custom ZMK firmware configuration for the **Sofle Choc Split Keyboard** powered by **nice!nano v2** controllers, featuring integrated OLED status displays, WS2812B/SK6812 RGB underglow/backlight strips, and dual rotary encoders.

## 🚀 Features & Configuration

### ⌨️ Layout & Ergonomics

* **German QWERTZ Layout:** Keymap optimized for standard German OS language settings, providing direct access to `ß`, `Ü`, `Ö`, `Ä`.
* **Dual-Shift Configuration:** Dedicated `Left Shift` and `Right Shift` keys on the base layer for effortless touch typing.
* **Ergonomic Thumb Clusters:** Quick access to `Space`, `Enter`, `Backspace`, `Delete`, and layer toggles (`LOWER` & `RAISE`).
* **Inverted Rotary Encoders:**
  * **Left Encoder:** Volume control (`Volume Down` / `Volume Up`).
  * **Right Encoder:** Navigation (`Page Down` / `Page Up`).

### 🔋 Power Management (Logitech MX Keys Mini Style)

* **30-Second Idle Timeout:** RGB lighting automatically dims/turns off after 30 seconds of inactivity to save battery.
* **5-Minute Deep Sleep:** Controllers and OLED displays enter deep standby after 5 minutes of inactivity.
* **Smart Wake-Up:** The first keypress simultaneously wakes up the controller, OLED screens, and RGB lighting.
* **Windows Battery Reporting:** Optimized GATT subscription configuration (`CONFIG_BT_GATT_ENFORCE_SUBSCRIPTION=y`) for accurate battery level reporting in Windows.

### 💡 Lighting & Displays

* **Logitech MX Keys Light Effect:** Static, clean white lighting (0% saturation) instead of dynamic rainbow effects.
* **Power-Efficient Brightness:** Starts at 40% default brightness and is capped at 60% maximum brightness.
* **OLED Status Screens:** Displays current Bluetooth profile (1–5), connection status (BLE/USB), and real-time battery status in percentage (`%`).

---

## 🛠️ GitHub Actions: Building & Downloading Firmware

Any changes pushed to your `sofle.conf` or `sofle.keymap` files will trigger an automatic build via GitHub Actions.

### Automated Builds

1. Commit and push your local config changes:
   ```bash
   git add config/sofle.conf config/sofle.keymap
   git commit -m "Update keymap and power management"
   git push origin main
   ```
2. Navigate to the **Actions** tab in your GitHub repository.
3. Select the latest workflow run. The build is complete once both `sofle_left` and `sofle_right` display a green checkmark.

### Manual Build Trigger

1. Go to **Actions** $\rightarrow$ Select **Build Firmware** on the left menu.
2. Click **Run workflow** $\rightarrow$ Choose the `main` branch and click **Run workflow**.

### Downloading Firmware Files (`.uf2`)

1. Open the details of the successful workflow run.
2. Scroll down to the **Artifacts** section at the bottom of the page.
3. Download the `firmware.zip` archive.
4. Extract the zip file. You will get two firmware binaries:
   * `sofle_left-nice_nano_v2-zmk.uf2` (Left half / Central)
   * `sofle_right-nice_nano_v2-zmk.uf2` (Right half / Peripheral)

---

## ⚡ Flashing the Keyboard

To flash new `.uf2` binaries onto the nice!nano v2 controllers, put each half into **bootloader mode**.

### Rules & Sequence

1. **Left First, Right Second:** Always flash the **left half (Central)** first, followed by the **right half (Peripheral)**.
2. **Single USB Cable Connection:** Only connect the specific keyboard half you are currently flashing via USB-C to your PC.

### Step-by-Step Flashing Procedure

#### 1. Flashing the Left Half (Central):

1. Connect the **left keyboard half** to your PC using a USB-C cable.
2. Put the nice!nano controller into bootloader mode:
   * **Double-click** the physical reset button on the left PCB.
   * *Keyboard shortcut alternative:* Switch to the **RAISE** layer and press the reset key.
3. A new virtual storage drive named **`NICENANO`** will appear on your computer.
4. Drag and drop `sofle_left-nice_nano_v2-zmk.uf2` onto the `NICENANO` drive.
5. The drive will automatically unmount once flashing completes.

#### 2. Flashing the Right Half (Peripheral):

1. Disconnect the USB cable from the left half and plug it into the **right keyboard half**.
2. Put the right controller into bootloader mode by **double-clicking** its physical reset button.
3. Drag and drop `sofle_right-nice_nano_v2-zmk.uf2` onto the `NICENANO` drive.
4. The drive will unmount automatically, and your keyboard is fully updated!

---

## 📶 Re-pairing Bluetooth (Windows Fix)

If the battery percentage or connection status does not update properly in Windows after flashing new firmware:

1. Open Windows **Settings** $\rightarrow$ **Bluetooth & Devices**.
2. Remove the existing **Sofle_Choc** device from the list.
3. On the left half of the keyboard, switch to Bluetooth Profile 1 (`RAISE` Layer $\rightarrow$ `BT1`).
4. Click **Add Device** in Windows Bluetooth settings and re-pair the keyboard.
