# Writeup — Compiling a CH341/CH9102 Serial Driver to Bring Up an ESP32-S3

**Session:** N16R8 (ESP32-S3) bring-up for GhostESP flash
**Date:** 2026-08-17
**Host:** HP Z6 G4 · Ubuntu · kernel 7.0.0-28-generic
**Related artifact:** FORM-003-02 (N16R8 → GhostESP)

---

## The problem

Flashing GhostESP onto the ESP32-S3 (N16R8) required a working serial connection
to the board. It wouldn't cooperate. The board's USB-serial bridge — a WCH
CH9102/CH343-class chip, USB ID `1a86:55d3` — did not come up as a usable
`/dev/ttyUSB*` device. `esptool` had nothing to connect to.

This was the same class of blocker that pushed the whole toolkit off web
flashers and onto `esptool` in the first place: the convenience layer assumes the
OS already sees the board. Here the OS didn't see it in a usable form at all, so
the fix had to happen a layer lower — at the kernel driver.

## Diagnosis

Confirmed the board was physically present and identified the bridge chip:

```bash
lsusb        # -> Bus... ID 1a86:55d3 QinHeng Electronics ...
ls /dev/ttyUSB*    # -> No such file or directory
```

Present on USB, but no serial node. Checked what the kernel was doing with it:

```bash
sudo dmesg | grep -i "55d3\|ch9102\|ch341\|ttyUSB" | tail -20
```

The kernel logged the `1a86:55d3` device arriving but the in-tree `ch341` driver
did not bind it to a `ttyUSB` port — on this kernel the `55d3` variant fell
through to the generic `cdc_acm` path / produced no stable working node for
flashing. The stock driver simply didn't recognize this specific WCH variant.

## What didn't work

Tried forcing the existing `ch341` driver to claim the device by injecting its
USB ID:

```bash
echo "1a86 55d3" | sudo tee /sys/bus/usb-serial/drivers/ch341-uart/new_id
ls /dev/ttyUSB*    # still nothing
```

The `new_id` bind is the quick trick for "driver exists but doesn't list this
ID." It didn't help here, which pointed at the real issue: the in-tree driver on
this kernel didn't have working support for the `55d3` variant at all — not just
a missing ID entry. Also confirmed there was no `ch9102`/`ch342` module to fall
back on:

```bash
sudo modprobe ch9102     # FATAL: Module not found
```

## The fix — compile the vendor driver

The manufacturer (WCH / WCHSoftGroup) publishes an out-of-tree driver with proper
support for the newer bridge variants. Built and installed it against the running
kernel's headers:

```bash
sudo apt install build-essential linux-headers-$(uname -r) -y
git clone https://github.com/WCHSoftGroup/ch341ser_linux.git ~/ch341ser

# the makefile is in the driver/ subdirectory, not the repo root
cd ~/ch341ser/driver && make && sudo make install
```

The module compiled (with the expected benign warnings about compiler/pahole
version differences from the kernel build), producing `ch341.ko`. Then reloaded
it to replace the running module:

```bash
sudo rmmod ch341
sudo modprobe ch341
sudo dmesg | tail -10
```

`dmesg` now showed the vendor driver active (`V1.9 On 2025.12`) and the board
came up as a working port:

```bash
ls /dev/ttyACM*    # -> /dev/ttyACM0
```

With a real device node, `esptool` connected and identified the chip, and the
GhostESP flash proceeded normally (see FORM-003-02):

```bash
sudo chmod a+rw /dev/ttyACM0
esptool --port /dev/ttyACM0 --chip esp32s3 chip-id   # -> Connected to ESP32-S3
```

## Takeaways

The reusable lesson is the escalation ladder for "the OS doesn't see my board."
It goes: confirm presence with `lsusb`, check what the kernel did with it via
`dmesg`, try the cheap `new_id` bind, and — when that fails because the in-tree
driver genuinely lacks support — drop to compiling the vendor's out-of-tree
driver against your own kernel headers. Each rung is a layer deeper than the
last, and knowing they exist is the difference between "the board is dead" and
"the driver doesn't support this chip variant yet, so I'll build one that does."

Compiling a kernel module to bring up hardware is ordinary systems work, but it's
the kind that only happens when the easy path fails — and the easy path failing
is exactly what produced a real result worth documenting here. The board that
caused the most trouble generated the most useful writeup.

---

*Documented under the CrashStack SOP handbook. For authorized security testing
and personal-lab use only.*
