# M5StickC Plus2 + 433 MHz (XY-MK-5V RX + FS1000A TX) with Bruce
## Pin assignment: TX = GPIO25, RX = GPIO26

This setup uses **Bruce**’s built-in **RF** tab/menu. You’ll wire the modules to the ESP32 GPIOs and then set the pins inside Bruce:
- **RF TX Pin = GPIO25**
- **RF RX Pin = GPIO26**

Bruce RF menu reference: https://github.com/BruceDevices/firmware/wiki/RF

---

## 1) Hardware

- M5Stack **M5StickC Plus2 (ESP32)**

 ![IMG_7792](https://github.com/user-attachments/assets/d1fcc52d-9726-43db-9bda-8e3f6fd4c575)

- **XY-MK-5V** 433 MHz receiver (ASK/OOK)

![IMG_7789](https://github.com/user-attachments/assets/56337e56-3088-44e0-908b-31ee0d595c4e)

- **FS1000A** 433 MHz transmitter (ASK/OOK)

![IMG_7791](https://github.com/user-attachments/assets/afad11bd-2ea5-41a2-bc68-7a08bf63b70c)

- (Recommended) antennas: **~17.3 cm wire** for RX and TX

---

## 2) Wiring

### A) Receiver (XY-MK-5V) → M5StickC Plus2  (RX = GPIO26)

**Power**
- XY-MK-5V **VCC** → **5V**
- XY-MK-5V **GND** → **GND**

**DATA**
- XY-MK-5V **DATA** → **GPIO26** (RF RX pin)

#### RX level protection (recommended)
Because XY-MK-5V is usually powered at **5V** and ESP32 GPIO is **3.3V-only**, protect the GPIO input:

- XY-MK-5V **DATA** → **10kΩ** → ESP32 **GPIO26**
- ESP32 **GPIO26** → **20kΩ** → **GND**

> If your XY-MK-5V board has 2 DATA pins, either one usually works.

---

### B) Transmitter (FS1000A) → M5StickC Plus2  (TX = GPIO25)

**Power**
- FS1000A **VCC** → **5V** (better range)
- FS1000A **GND** → **GND**

**DATA**
- FS1000A **DATA** → **GPIO25** (RF TX pin)

---

## 3) Antenna (mandatory in practice)

Add a simple wire antenna:
- Length: **~17.3 cm**
- Connect to the **ANT** pad (or the antenna/coil input point) on each module.

Without antennas, capture/tx can look like it doesn’t work.

---

## 4) Install Bruce on M5StickC Plus2

Get the correct build from Bruce releases and flash it (M5Burner or esptool workflow depends on the release packaging):
- Releases: https://github.com/BruceDevices/firmware/releases

If using M5Burner, you can also restore stock firmware later:
- M5StickC Plus2 restore guide: https://docs.m5stack.com/en/guide/restore_factory/m5stickc_plus2

---

## 5) Configure inside Bruce (RF tab)

1. Open **RF** menu/tab
2. Set:
   - **RF TX Pin = 25**
   - **RF RX Pin = 26**
3. Choose the appropriate module profile (cheap ASK/OOK single-pin modules are typically grouped with FS1000A-style TX/RX).
4. Use RF functions (capture / view / transmit / replay depending on your Bruce build).

Bruce RF menu reference: https://github.com/BruceDevices/firmware/wiki/RF

---
If you tell me which physical connector/breakout you’re using on the StickC Plus2 (Grove header, hat, custom breakout), I can write an exact “wire-to-physical-pin” mapping as well.
