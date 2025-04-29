# 📡 TP-Link AC600 Bluetooth Setup on Jetson Nano

This guide helps you get the **TP-Link AC600** Bluetooth adapter (based on the Realtek RTL8821AU chipset) working on a **Jetson Nano**, using the proper Realtek firmware.

---

### ✅ Tested On

- **Device:** Jetson Nano (Developer Kit)
- **OS:** Ubuntu-based (JetPack 4.6.1)
- **Bluetooth Chipset:** Realtek RTL8821AU (used in TP-Link AC600)

---

### ⚠️ Warning

This guide replaces system firmware files. Proceed with caution and only if you're facing Bluetooth issues with your AC600 adapter.

---

### 📥 Steps

1. **Remove old firmware (if any):**
   ```bash
   sudo rm -r /lib/firmware/rtl_bt
   ```

2. **Recreate the firmware directory:**
   ```bash
   sudo mkdir -p /lib/firmware/rtl_bt
   ```

3. **Download and install Realtek Bluetooth firmware:**
   ```bash
   sudo wget https://github.com/Realtek-OpenSource/android_hardware_realtek/raw/rtk1395/bt/rtkbt/Firmware/BT/rtl8821a_fw -O /lib/firmware/rtl_bt/rtl8821a_fw.bin
   sudo wget https://github.com/Realtek-OpenSource/android_hardware_realtek/raw/rtk1395/bt/rtkbt/Firmware/BT/rtl8821a_config -O /lib/firmware/rtl_bt/rtl8821a_config.bin
   ```

4. **Set appropriate permissions:**
   ```bash
   sudo chmod 644 /lib/firmware/rtl_bt/rtl8821a_*
   ```

5. **Verify the files:**
   ```bash
   ls -l /lib/firmware/rtl_bt/rtl8821a_*
   ```

6. **Reload Bluetooth modules:**
   ```bash
   sudo rmmod btusb
   sudo modprobe btusb
   sudo systemctl restart bluetooth
   ```

7. **Reconnect your AC600 adapter:**
   - Physically **unplug and replug** the AC600 USB dongle.

8. **Still not working? Try a reboot:**
   ```bash
   sudo reboot
   ```

---

### 🧪 Troubleshooting

- Run `dmesg | grep -i bluetooth` to check for Bluetooth logs.
- Use `bluetoothctl` to check adapter status and pair devices.

---

### 🧾 License

This repository and guide are released under the [MIT License](LICENSE).
