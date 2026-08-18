# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-04
**Device:** LilyGO T-Embed CC1101 Plus
**Target firmware:** CapibaraZero
**Assessment role:** Handheld sub-GHz / NFC-RFID / IR multitool (capture, replay, access-control assessment)
**Operator:** K. Solem (livingthegrind88)
**Date:** <VERIFY: YYYY-MM-DD>
**Host platform:** Linux (esptool flashing station)
**Flash method:** `esptool` — direct USB serial write

---

## Objective

Deploy a handheld multi-radio assessment tool for sub-GHz signal capture/replay, NFC/RFID (13.56 MHz) access-control assessment, and IR capture/replay.

## Hardware

- **Board:** LilyGO T-Embed CC1101 Plus
- **Chip:** ESP32-S3 · CC1101 sub-GHz + nRF24 + PN532 NFC/RFID + IR + BLE · 1.9" ST7789V IPS
- **Flash offset (chip-dependent):** 0x0 (typical for ESP32-S3)

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
esptool --port <PORT> --baud <BAUD> write_flash 0x0 <capibarazero.bin>

# 5. Power-cycle (unplug/replug) and verify boot
```

**Values to confirm from `history | grep esptool`:**
- `<PORT>` — **VERIFY** `/dev/ttyUSB0` vs `/dev/ttyACM0`
- `<BAUD>` — **VERIFY** `115200` vs `460800`
- offset — **VERIFY** `0x0 (typical for ESP32-S3)`
- `<capibarazero.bin>` — **VERIFY** exact firmware image filename / version

## Issues Encountered

- Web flasher did not enumerate the board on this host.
- Resolved with a direct `esptool` serial write.

## Verification

- Device **rebooted into CapibaraZero** after the write.
- Firmware loaded correctly; **all on-device menus render and navigate**; display operational.

## Status

✅ **Operational**

> **Firmware compatibility note:** CapibaraZero is the correct target for this hardware. Flipper Zero firmware is **not** compatible — the T-Embed is ESP32-S3 based, whereas Flipper Zero targets the STM32WB55.

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal lab use only.*
