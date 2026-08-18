# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-02
**Device:** ESP32 N16R8 (+ expansion board)
**Target firmware:** GhostESP
**Assessment role:** WiFi penetration node (scanning / access-point testing)
**Operator:** K. Solem (livingthegrind88)
**Date:** <VERIFY: YYYY-MM-DD>
**Host platform:** Linux (esptool flashing station)
**Flash method:** `esptool` — direct USB serial write

---

## Objective

Deploy a WiFi penetration node leveraging the ESP32-S3's additional RAM and flash headroom for scanning and access-point testing.

## Hardware

- **Board:** ESP32 N16R8 (+ expansion board)
- **Chip:** ESP32-S3 · 16 MB flash / 8 MB PSRAM
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
esptool --port <PORT> --baud <BAUD> write_flash 0x0 <ghostesp_n16r8.bin>

# 5. Power-cycle (unplug/replug) and verify boot
```

**Values to confirm from `history | grep esptool`:**
- `<PORT>` — **VERIFY** `/dev/ttyUSB0` vs `/dev/ttyACM0`
- `<BAUD>` — **VERIFY** `115200` vs `460800`
- offset — **VERIFY** `0x0 (typical for ESP32-S3)`
- `<ghostesp_n16r8.bin>` — **VERIFY** exact firmware image filename / version

## Issues Encountered

- Web flasher did not enumerate the board on this host.
- Resolved with a direct `esptool` serial write.

## Verification

- Board **booted cleanly after power-cycle** (unplug/replug).
- Confirmed the device broadcasts its **`GhostNet` SSID**; associated to it and reached the device's management interface.

## Status

✅ **Operational**

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal lab use only.*
