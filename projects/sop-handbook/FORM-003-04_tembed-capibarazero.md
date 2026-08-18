# FORM-003 — Pentest Hardware / Tool Usage Log

**Artifact ID:** FORM-003-04
**Device:** LilyGO T-Embed CC1101 Plus
**Target firmware:** CapibaraZero 0.5.2 (lilygo_t_embed_cc1101 build)
**Assessment role:** Handheld sub-GHz / NFC-RFID / IR multitool (capture, replay, access-control assessment)
**Operator:** K. Solem (livingthegrind88)
**Date:** 2026-08-17
**Host platform:** Linux (HP Z6 G4)
**Flash method:** `esptool` v5.3.1 — direct USB serial write

---

## Objective

Deploy a handheld multi-radio assessment tool for sub-GHz signal capture/replay,
NFC/RFID (13.56 MHz) access-control assessment, and IR capture/replay.

## Hardware

- **Board:** LilyGO T-Embed CC1101 Plus
- **Chip (confirmed by esptool):** ESP32-S3 (QFN56) revision v0.2 — dual-core 240MHz, BT 5 (LE)
- **Memory:** 8MB embedded PSRAM, 16MB flash (auto-detected)
- **MAC:** 90:70:69:36:8f:c0
- **Radios:** CC1101 sub-GHz · nRF24 · PN532 NFC/RFID · IR · BLE
- **Serial enumeration:** `/dev/ttyACM0` — the ESP32-S3 has native USB-Serial/JTAG (no UART bridge), so it presents as a `ttyACM` device rather than `ttyUSB`.

## Method

Browser-based web flashers failed to enumerate the board on the host, so firmware
was written directly with `esptool` over USB serial. The CapibaraZero release
ships as four images (bootloader, partitions, boot_app0, firmware).

Device permissions were set for the serial port before flashing, and chip
identity was confirmed before the write:

```bash
# Grant read/write on the port
sudo chmod a+rw /dev/ttyACM0

# Confirm chip + link before writing
esptool --port /dev/ttyACM0 --chip esp32s3 chip-id

# Write the four CapibaraZero images
esptool --port /dev/ttyACM0 --chip esp32s3 --baud 460800 \
  --before default-reset --after hard-reset write-flash -z \
  --flash-mode dio --flash-freq 80m --flash-size detect \
  0x0000  bootloader.bin \
  0x8000  partitions.bin \
  0xe000  boot_app0.bin \
  0x10000 firmware.bin
```

**Confirmed values (from session log):**
- Port: `/dev/ttyACM0`
- Baud: `460800`
- Flash mode / freq: `dio` / `80m`
- Offsets: bootloader `0x0`, partitions `0x8000`, boot_app0 `0xe000`, firmware `0x10000`
- Firmware version: CapibaraZero 0.5.2
- esptool: v5.3.1

## Firmware Compatibility Note

CapibaraZero is the correct target for this hardware. Flipper Zero firmware is
**not** compatible — the T-Embed is ESP32-S3 based, whereas Flipper Zero targets
the STM32WB55.

## Issues Encountered

- Web flasher did not enumerate the board on this host → direct `esptool` serial write used.
- Port required a permissions grant (`chmod a+rw /dev/ttyACM0`) before esptool could open it.

## Verification

- All four images written and **hash-verified** (`Hash of data verified.` on each).
- Firmware (1,986,128 bytes) wrote successfully at `0x10000`.
- Board hard-reset via RTS pin on completion.
- Device **rebooted into CapibaraZero**; firmware loaded correctly, **all
  on-device menus render and navigate**, display operational.

## Status

✅ **Operational**

---

*Documented under the CrashStack SOP handbook, FORM-003 (Pentest Hardware / Tool
Usage). For authorized security testing and personal-lab use only.*
