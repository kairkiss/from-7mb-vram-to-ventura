# Hardware / 硬件平台

## Machine Identity / 机器身份

This project is built on a compact industrial Broadwell machine rather than a native Apple device.

It behaves closer to a custom mini desktop than to a laptop, even though the final SMBIOS was tuned toward a MacBookPro profile for Ventura compatibility.

---

## Core Hardware / 核心硬件

- **CPU**: Intel Core i5-5200U
- **iGPU**: Intel HD Graphics 5500
- **Platform**: H81U industrial mini PC
- **RAM**: 8GB DDR3 1600MHz
- **Storage**: 128GB SATA SSD

---

## Networking / 网络

- **Ethernet**: Dual Realtek RTL8111
- **Wi-Fi / Bluetooth**: Broadcom BCM94352HMB / DW1550

---

## Notes / 备注

This hardware is far from ideal for macOS by default.

The final result depended on:
- OpenCore
- OCLP
- Broadcom tuning
- BIOS graphics memory tuning
- USB mapping correction
- Bluetooth NVRAM fixes
