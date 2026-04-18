# From 7MB VRAM to Ventura Full Acceleration

## 从 7MB 显存到 Ventura 满血加速

A personal high-fidelity Hackintosh project built around an Intel Broadwell industrial mini PC.

This repository is not just an EFI dump.  
It is a reproducible engineering log of how a nearly broken Broadwell machine was pushed from:

- 7MB VRAM
- no graphics acceleration
- unstable Bluetooth
- incomplete Apple ecosystem support

to a practical macOS Ventura 13.7.8 system with:

- full graphics acceleration
- working audio
- working Wi-Fi
- working Bluetooth
- strong Apple ecosystem integration

---

## Project Philosophy / 项目理念

This project is built with three goals:

1. **Reproducibility / 可复刻**
2. **Clarity / 可解释**
3. **Style / 有质感**

It is meant to be both:
- a public technical archive
- and a private recovery manual for my future self

---

## Hardware / 硬件平台

- **CPU**: Intel Core i5-5200U
- **iGPU**: Intel HD Graphics 5500
- **Platform**: H81U industrial mini PC
- **RAM**: 8GB DDR3 1600MHz
- **Storage**: 128GB SATA SSD
- **Ethernet**: Dual Realtek RTL8111
- **Wi-Fi / Bluetooth**: Broadcom BCM94352HMB / DW1550
- **BIOS**: AMI Aptio Setup Utility

---

## Final System State / 最终系统状态

- **macOS**: Ventura 13.7.8
- **SMBIOS**: MacBookPro14,1
- **Graphics**: Intel HD 5500 fully accelerated
- **Reported VRAM**: 1536MB
- **Audio**: working
- **Wi-Fi**: working
- **Bluetooth**: working
- **Apple Ecosystem**: partially to strongly working

---

## What Works / 已实现功能

- [x] Boot
- [x] Graphics acceleration
- [x] Audio
- [x] Wi-Fi
- [x] Bluetooth
- [x] Handoff
- [x] Phone relay
- [x] iPhone hotspot relay
- [x] Wired continuity camera / microphone
- [x] iPhone to Mac AirDrop
- [x] Webpage handoff
- [x] Apple ecosystem partial integration

---

## Partial / Known Limitations / 部分可用与已知限制

- [~] Mac to iPhone AirDrop
- [~] Universal Clipboard
- [~] Wireless continuity camera behavior may be incomplete

---

## Core Breakthroughs / 核心突破点

### 1. Graphics Recovery / 图形加速恢复
The machine originally booted with only 7MB VRAM and no proper graphics acceleration.  
Ventura + OCLP root patch + BIOS graphics memory tuning finally restored full acceleration.

### 2. Broadcom Wireless Bring-up / 博通无线链路打通
Wi-Fi and Bluetooth were recovered through:
- proper Broadcom injector selection
- updated Broadcom kexts
- USB mapping correction
- required Bluetooth NVRAM variables

### 3. Apple Ecosystem Integration / 苹果生态接入
The machine is not merely "booting macOS".  
It is capable of:
- Handoff
- phone relay
- hotspot relay
- continuity camera (wired)
- AirDrop in practical use

---

## Documentation / 文档目录

- [Hardware](docs/hardware.md)
- [BIOS Settings](docs/bios-settings.md)
- [Install Log](docs/install-log.md)
- [Graphics Fix](docs/graphics-fix.md)
- [Wi-Fi, Bluetooth, Audio](docs/wifi-bluetooth-audio.md)
- [Apple Ecosystem](docs/apple-ecosystem.md)
- [Known Issues](docs/known-issues.md)
- [Recovery](docs/recovery.md)

---

## Warning / 警告

This repository contains a **sanitized** configuration for public reference only.

Do not copy the EFI blindly if your:
- motherboard
- BIOS
- USB topology
- Wi-Fi card
- display path

are different.

---

## Credits / 致谢

- OpenCore
- Dortania
- OpenCore Legacy Patcher
- Acidanthera
- the Hackintosh community

---

## Personal Note / 个人注记

This machine started as a weird industrial Broadwell box with broken graphics, unstable wireless, and almost no Apple-class experience.

Now it stands as a fully accelerated Ventura machine with real ecosystem features.

That is the whole point of this repository.
