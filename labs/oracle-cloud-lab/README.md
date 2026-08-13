# Lab — Oracle Cloud Free Tier Lab

## Architecture
Oracle Cloud Free Tier VM (Ampere ARM, 4 OCPU / 24GB RAM — permanently free tier)
running two services:

- **WireGuard VPN server** — private self-hosted tunnel between lab machines and
  the cloud VM. Traffic exits through Oracle's IP. No third-party logs.
- **DIY CTF server** — a deliberately vulnerable SSH environment modeled after
  OverTheWire Bandit. Accessible privately over the WireGuard tunnel.

## Purpose
Build and document a dual-purpose cloud infrastructure project that demonstrates
cloud provisioning, VPN configuration, network segmentation, Linux server
administration, and security design — all on the Oracle Cloud permanent free tier
at zero cost.

## Status
Planned. Provisioning begins Week 3–4 of the program.

## Skills demonstrated
Cloud infrastructure, WireGuard VPN, network segmentation, SSH hardening, Linux
server administration, CTF/wargame design, documentation.

## Links
- [FORM-003](../projects/sop-handbook/FORM-003-pentest-hardware.md) — engagement documentation
- [FORM-001](../projects/sop-handbook/FORM-001-writeup.md) — build log entries
