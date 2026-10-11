# Ziggo Archer C7 v2 Firmware Archive

This repository contains the untouched, factory-original stock firmware for the **TP-Link Archer C7 v2 (Ziggo Extra Wifi-punt)** version **2.1.4**. 

This binary is highly valuable for restoring ("unbricking") devices that were misflashed, downgrading firmware, or for reverse-engineering the specific software optimizations used by the Dutch ISP Ziggo.

## 💾 Firmware Details
* **Device:** TP-Link Archer C7 v2 (Modified by Ziggo)
* **Filename:** `Ziggo_AccessPoint_FW_2.1.4.bin`
* **Firmware Version:** 2.1.4
* **Extraction Method:** Hardware dump via serial interface using an FTDI USB-to-TTL Serial Cable (3.3V).
* **Modification Status:** **100% Stock & Untouched**. The raw dump was cleanly cut to the exact firmware length without any modifications to the data blocks.

### 🔒 Integrity & Verification
The internal TP-Link header validation checks out perfectly. The bootloader (`U-Boot`), recovery tools, and the original web interface will recognize this as a valid, untampered image.

* **Header MD5Sum1:** `2e 4c 6d da de e1 27 ed 78 8d 57 81 8e 2a f1 37` (Status: **OK** - Matches natively without edits)
* **File SHA-256:** `890b2d5404d75d731a7681fb5c153ca075df2a3d46a1946e746648db73adcd15`

---

## 💻 Method 1: Flashing via Web Interface

Because the header checksum matches perfectly, you can flash this firmware directly through the router's standard management page. 

1. Connect your computer to the router via an ethernet cable or Wi-Fi.
2. Open your web browser and log into the router's web interface (typically `192.168.1.1` or `192.168.0.1`, depending on your current setup).
3. Navigate to the **Firmware Upgrade** section (usually under *System Tools*).
4. Click **Browse** / **Choose File** and select `Ziggo_AccessPoint_FW_2.1.4.bin`.
5. Click **Upgrade** and wait for the process to complete. **Do not turn off the router during this process.**

---

## 🛠️ Method 2: Recovery / Flashing Guide (TFTP Method)

If your Ziggo Access Point is bricked (e.g., power light blinking or boot loop) and the web interface is inaccessible, you can use the built-in hardware recovery mode.

### Prerequisites
1. An ethernet cable connecting your computer directly to one of the **LAN ports** of the router.
2. A TFTP Server utility installed on your PC (e.g., [**Tftpd32/Tftpd64**](https://github.com/PJO2/tftpd64/releases/) for Windows, or `tftpd` for Linux).

### Step-by-Step Instructions
1. **Rename the file:** Rename `Ziggo_AccessPoint_FW_2.1.4.bin` to exactly `ArcherC7v2_tp_recovery.bin`.
2. **Configure your Network Adapter:** 
   * Change your computer's static IP address to `192.168.0.66`
   * Set the Subnet Mask to `255.255.255.0`
3. **Setup the TFTP Server:** 
   * Place the renamed `ArcherC7v2_tp_recovery.bin` file into the root directory of your TFTP server application.
   * Start the TFTP server and ensure it is listening on the `192.168.0.66` interface.
4. **Trigger Recovery Mode:**
   * Turn off the Archer C7 using the power button.
   * Press and **hold the WPS/Reset button** on the back of the router.
   * While holding the button, turn the power back on.
   * Keep holding the button for about 6–8 seconds until the WPS/System LED changes behavior (usually blinks rapidly), then release it.
5. **Flash Process:** The router will automatically request the file from your TFTP server, flash it, and reboot. **Do not power off the device during this process.**

---

## ⚠️ Disclaimer
*This firmware is shared strictly for educational, archival, and hardware-rescue purposes. All intellectual property belongs to their respective owners (TP-Link / VodafoneZiggo).*
