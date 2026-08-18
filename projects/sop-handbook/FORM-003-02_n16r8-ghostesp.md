# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-02
**Device:** ESP32 N16R8 (+ expansion board)
**Target firmware:** GhostESP v2.1.1 (GhostESP-Revival, esp32s3-generic build)
**Assessment role:** WiFi penetration node (scanning / access-point testing)
**Operator:** K. Solem (livingthegrind88)
**Date:** 2026-08-17
**Host platform:** Linux (HP Z6 G4, kernel 7.0.0-28-generic)
**Flash method:** `esptool` v5.3.1 — direct USB serial write

---

## Objective

Deploy a WiFi penetration node leveraging the ESP32-S3's additional RAM and flash
headroom for scanning and access-point testing.

## Hardware

- **Board:** ESP32 N16R8 (16 MB flash / 8 MB PSRAM) + expansion board
- **Chip (confirmed by esptool):** ESP32-S3 (QFN56) revision v0.2 — dual-core 240MHz, BT 5 (LE)
- **USB-serial bridge:** CH9102 / CH343-class (`1a86:55d3`) — **required an out-of-tree driver (see below).**
- **MAC:** 1c:db:d4:ae:d9:c4
- **Serial enumeration:** `/dev/ttyACM0` (after driver fix)

## Blocker & Resolution — CH341/CH9102 driver

This board did **not** enumerate as a usable serial port out of the box on kernel
7.0.0-28. The `1a86:55d3` bridge was being claimed by the generic `cdc_acm`
path / not producing a stable device node, and the stock in-tree `ch341` driver
did not bind it. A manual `new_id` bind attempt did not resolve it.

**Fix:** compiled and installed the vendor out-of-tree driver
(WCHSoftGroup `ch341ser_linux`) against the running kernel headers:

```bash
sudo apt install build-essential linux-headers-$(uname -r) -y
git clone https://github.com/WCHSoftGroup/ch341ser_linux.git ~/ch341ser
cd ~/ch341ser/driver && make && sudo make install
sudo rmmod ch341 && sudo modprobe ch341
```

After reloading the driver the board presented reliably as `/dev/ttyACM0`.
Full narrative: see `../../writeups/writeup_ch341-driver-fix.md`.

## Firmware Source

```bash
# NOTE: the 'latest/esp32s3.zip' asset URL 404'd; the correct v2.1.1 asset
# is 'esp32s3-generic.zip'.
wget https://github.com/GhostESP-Revival/GhostESP/releases/download/v2.1.1/esp32s3-generic.zip
unzip esp32s3-generic.zip          # -> bootloader.bin, firmware.bin, merged.bin, partitions.bin
```

## Method

GhostESP ships a single pre-merged image (`merged.bin`) written at offset `0x0`.

```bash
# confirm chip/link first
esptool --port /dev/ttyACM0 --chip esp32s3 chip-id

# write the merged image
esptool --port /dev/ttyACM0 --baud 921600 --chip esp32s3 write-flash 0x0 merged.bin
```

**Confirmed values (from session log):**
- Port: `/dev/ttyACM0`   ·   Baud: `921600`   ·   esptool v5.3.1
- Single merged image at offset `0x0`
- Firmware: GhostESP **v2.1.1**, `esp32s3-generic` build

## Issues Encountered

1. Web flasher did not enumerate the board.
2. CH9102 bridge required a compiled out-of-tree driver before any serial access (resolved above).
3. GhostESP `latest/esp32s3.zip` download URL returned 404; correct asset was `esp32s3-generic.zip` under the v2.1.1 tag.

## Verification

- Merged image (3,173,648 bytes) written and **hash-verified**.
- Board hard-reset via RTS pin on completion.
- Device broadcasts its **`GhostNet` SSID**; associated to it and reached the device's management interface.

## Status

✅ **Operational**

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal-lab use only.*
