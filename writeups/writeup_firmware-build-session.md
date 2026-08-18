# Writeup — Building the Wireless/RF Assessment Toolkit

**Session:** Four-device firmware deployment
**Date:** <VERIFY: YYYY-MM-DD>
**Related artifacts:** FORM-003-01 through FORM-003-04

---

## What this session was

In one sitting I flashed four devices into a working wireless and RF assessment
toolkit: an ESP32 CYD running Marauder, an ESP32 N16R8 running GhostESP, an
ESP32 WROOM as a second WiFi penetration node, and a LilyGO T-Embed CC1101 Plus
running CapibaraZero. Individually each is a single board with new firmware.
Together they cover WiFi discovery and deauthentication, a second externally-
antenna'd WiFi node for wider coverage, and a handheld multitool spanning
sub-GHz, NFC/RFID, and infrared. That spread — several RF domains, coordinated —
is the point. It's the difference between owning a gadget and having a toolkit.

## The problem that actually defined the session

None of the browser-based web flashers would see the boards. Every one of the
four failed the same way: the board powered up, the host clearly had it on USB,
but the web flasher never presented it as a connected serial device. That could
have stopped the session. Instead it became the session's real work.

The fix was to stop relying on the abstraction the web flasher provides and go to
the layer underneath it — write the firmware directly with `esptool` over USB
serial. That meant confirming each board was present with `lsusb`, finding the
serial port the OS had assigned it, and issuing the write myself: port, baud
rate, flash offset, image. Four times. Once the method was proven on the first
board, the same procedure carried the other three, adjusting only the offset for
the ESP32-S3 boards versus the classic ESP32s.

## What I took away from it

The lesson I'd keep is small and practical: **identify the device first.** I
learned the port-identification step partway through rather than at the start,
and doing it up front — `lsusb` to confirm the board is there, then the
`/dev/tty*` path the tool actually needs — removes the guesswork that causes
failed write attempts. That's now the first step in my documented procedure, not
a mid-process correction.

The larger takeaway is about what to do when the easy path fails. The web flasher
not working wasn't the end of flashing — it was a signal to drop down a layer to
the tool the web flasher is itself a wrapper around. Knowing that `esptool` sits
underneath the friendly button, and being willing to use it directly, is the
difference between "the tool is broken, I'm stuck" and "the convenience layer
failed, I'll do it manually." That transfers well beyond flashing firmware.

There was also a hardware-literacy decision worth noting. The T-Embed can't run
Flipper Zero firmware — it's ESP32-S3 based, and Flipper targets a different
chip entirely (STM32WB55). Picking CapibaraZero wasn't following a default; it
was matching firmware to architecture on purpose. Same logic applied to the flash
offsets differing between the classic ESP32 and S3 boards. Getting those right is
the part that separates "flashed it" from "understood what I flashed."

## Where it leaves the toolkit

All four devices are operational and verified — each one confirmed by its own
expected behavior, not just a successful write: the CYD auto-booting into
Marauder, the N16R8 broadcasting its GhostNet control network, the WROOM
presenting its management AP, the T-Embed loading every CapibaraZero menu. Each
is documented as its own FORM-003 artifact with the exact procedure, the issues
hit, and how I verified it, so the work is reproducible rather than remembered.

The immediate next step is closing the placeholders — the exact port, baud, and
offset values pulled from shell history — so the logs are fully reproducible, and
recording the firmware image versions per device. After that these four become
the wireless/RF layer of the larger field platform: nodes that feed the pipeline
rather than four separate gadgets on a bench.

---

*Documented under the CrashStack SOP handbook. For authorized security testing
and personal-lab use only.*
