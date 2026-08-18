# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-01
**Device:** ESP32 CYD (Cheap Yellow Display)
**Target firmware:** Marauder (CYD build)
**Assessment role:** WiFi discovery / deauthentication testing / beacon & probe-request analysis
**Operator:** K. Solem (livingthegrind88)
**Date:** <VERIFY: YYYY-MM-DD>
**Host platform:** Linux (esptool flashing station)
**Flash method:** `esptool` — direct USB serial write

---

## Objective

Deploy a self-contained WiFi assessment unit with on-device display output for network discovery, deauthentication testing, and beacon/probe-request analysis.

## Hardware

- **Board:** ESP32 CYD (Cheap Yellow Display)
- **Chip:** Classic ESP32 (integrated TFT display)
- **Flash offset (chip-dependent):** 0x1000 (typical for classic ESP32)

## Method

Browser-based web flashers failed to enumerate this board as a connected serial
device on the host, so firmware was written directly with `esptool` over USB
serial.

```bash
# 1. Confirm the board is present on USB (vendor:product ID)
lsusb

# 2. Identify the serial PORT path esptool needs
ls /dev/ttyUSB* /dev/ttyACM* 2>/dev/null
#    (or: dmesg | tail  immediately after plugging the board in)

# 3. (Recommended) confirm chip + link before writing
esptool --port <PORT> chip_id

# 4. Write firmware
esptool --port <PORT> --baud <BAUD> write_flash 0x1000 <marauder_cyd.bin>

# 5. Power-cycle (unplug/replug) and verify boot
```

**Values to confirm from `history | grep esptool`:**
- `<PORT>` — **VERIFY** `/dev/ttyUSB0` vs `/dev/ttyACM0`
- `<BAUD>` — **VERIFY** `115200` vs `460800`
- offset — **VERIFY** `0x1000 (typical for classic ESP32)`
- `<marauder_cyd.bin>` — **VERIFY** exact firmware image filename / version

## Issues Encountered

- Web-based Marauder flasher did not detect the board as a connected serial device on this host.
- Resolved by switching to a direct `esptool` serial write.

## Verification

- After the write completed, the device **auto-rebooted directly into the Marauder firmware** with no manual reset required.
- Marauder UI confirmed operational on the integrated display.

## Status

✅ **Operational**

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal lab use only.*
