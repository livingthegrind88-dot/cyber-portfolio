# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-01
**Device:** ESP32 CYD (Cheap Yellow Display)
**Target firmware:** ESP32 Marauder v1.4.3 (CYD2USB, no-GPS build)
**Assessment role:** WiFi discovery / deauthentication testing / beacon & probe-request analysis
**Operator:** K. Solem (livingthegrind88)
**Date:** 2026-08-17
**Host platform:** Linux (HP Z6 G4, kernel 7.0.0-28-generic)
**Flash method:** `esptool` v5.3.1 — direct USB serial write

---

## Objective

Deploy a self-contained WiFi assessment unit with on-device display output for
network discovery, deauthentication testing, and beacon/probe-request analysis.

## Hardware

- **Board:** ESP32 CYD (Cheap Yellow Display), integrated 2.8" TFT
- **Chip (confirmed by esptool):** ESP32-D0WD-V3 (revision v3.1) — classic ESP32, dual-core 240MHz
- **USB-serial bridge:** CH340 (`1a86:7523`)
- **Flash size:** 4MB
- **MAC:** 44:1d:64:f3:eb:c4
- **Serial enumeration:** `/dev/ttyUSB0` — the CH340 bridge is supported in-kernel, so the board presented as `ttyUSB0` with no driver work required.

## Environment Setup (one-time, this session)

```bash
# esptool installed to user site-packages
pip install esptool --break-system-packages     # -> esptool v5.3.1

# grant serial access without sudo (added user to dialout group)
sudo usermod -a -G dialout crash
newgrp dialout
```

## Firmware Source

```bash
# Marauder application image (Fr4nkFletcher CYD build, v1.4.3)
wget https://github.com/Fr4nkFletcher/ESP32-Marauder-Cheap-Yellow-Display/releases/download/v1.4.3/esp32_marauder_v1_4_3_20250416_cyd2usb_nogps.bin
# bootloader + partition table (Adafruit WebSerial ESPTool static resources)
wget .../CYD/esp32_marauder.ino.bootloader.bin
wget .../CYD/esp32_marauder.ino.partitions.bin
```

## Method

Browser-based web flashers did not reliably detect the boards on this host;
firmware was written directly with `esptool`. Marauder ships as three images
(bootloader, partitions, application).

```bash
esptool.py --port /dev/ttyUSB0 --baud 921600 write_flash \
  0x1000  esp32_marauder.ino.bootloader.bin \
  0x8000  esp32_marauder.ino.partitions.bin \
  0x10000 esp32_marauder_v1_4_3_20250416_cyd2usb_nogps.bin
```

**Confirmed values (from session log):**
- Port: `/dev/ttyUSB0`   ·   Baud: `921600`   ·   esptool v5.3.1
- Offsets: bootloader `0x1000`, partitions `0x8000`, application `0x10000`
- Firmware: Marauder v1.4.3 `cyd2usb_nogps` (dated 2025-04-16)

## Issues Encountered

- Web flasher did not reliably detect the board → direct `esptool` serial write used.

## Verification

- All three images written and **hash-verified** (`Hash of data verified.` on each).
- Application (1,550,192 bytes) wrote successfully at `0x10000`.
- Device **auto-rebooted directly into the Marauder firmware** (hard reset via RTS);
  Marauder UI confirmed operational on the integrated display.

## Status

✅ **Operational**

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal-lab use only.*
