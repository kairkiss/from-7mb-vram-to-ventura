# Install Log / 安装与排障实录

## Overview / 总览

This document records the actual path of this machine from a barely usable Hackintosh state to a stable and accelerated macOS Ventura 13.7.8 system.

It is not written as a generic tutorial.  
It is a real troubleshooting log focused on what actually mattered, what failed, and what finally worked.

---

## Starting Point / 起点状态

The machine did not begin as a polished Hackintosh.

Its early state was defined by several severe limitations:

- bootable, but not truly usable
- graphics acceleration missing
- Intel HD 5500 reported only **7MB VRAM**
- Wi-Fi unstable or unavailable
- Bluetooth detected in an incomplete state
- Apple ecosystem features mostly broken or absent

At this stage, the system was closer to a diagnostic shell than to a finished macOS machine.

---

## Phase 1 — Reaching a Bootable Base / 建立可启动基础

The first goal was not elegance.  
It was simply to get the machine into a reliably bootable macOS environment.

This stage required:

- a working OpenCore base
- a compatible SMBIOS direction
- basic input support
- basic storage and boot stability

At this point, the machine could enter macOS, but the experience was still far from complete.

---

## Phase 2 — The Graphics Crisis / 图形危机

The most dramatic early failure was graphics.

### Symptom / 症状
The system reported:

- Intel HD Graphics 5500
- **VRAM: 7MB**
- no real acceleration
- UI effects incomplete
- poor visual fluidity

### Meaning / 这意味着什么
This was not a minor cosmetic issue.  
It meant the graphics stack was fundamentally incomplete.

Without proper acceleration, the machine could boot, but it could not truly behave like a modern macOS system.

---

## Phase 3 — Ventura Upgrade / 升级到 Ventura

The machine was later brought to **macOS Ventura 13.7.8**.

This was an important turning point.

Ventura itself did not magically fix the graphics problem, but it established the final target environment for the project.

The upgrade proved that the machine could move beyond its earlier Monterey state and still remain recoverable.

This was the foundation for the next decisive step.

---

## Phase 4 — OCLP Root Patch / OCLP 根补丁

After reaching Ventura, OpenCore Legacy Patcher became essential.

### Why it mattered / 为什么关键
The Broadwell graphics stack on Ventura required post-install patching to restore proper support.

### Result / 结果
After OCLP root patching was successfully applied, the machine moved much closer to real graphics recovery.

However, graphics were still not fully correct until BIOS memory-related settings were also tuned.

This was a crucial lesson:

> software patching alone was not enough; firmware-side graphics memory layout also mattered.

---

## Phase 5 — BIOS Graphics Memory Tuning / BIOS 显存相关调校

The true graphics breakthrough came only after the BIOS graphics parameters were corrected.

### Important working values / 关键有效值
- Internal Graphics: Enabled
- Primary Display: IGFX
- DVMT Pre-Allocated: 64M
- DVMT Total Gfx Mem: 256M
- Aperture Size: 256MB

### Final breakthrough / 最终突破
With Ventura, OCLP, and BIOS graphics memory settings aligned, the machine finally recovered:

- full graphics acceleration
- smooth video playback
- proper translucency and visual effects
- **1536MB reported VRAM**

This was the moment the project stopped being a half-working Hackintosh and became a serious Ventura machine.

---

## Phase 6 — Audio Repair / 音频修复

Audio was another major milestone.

### Initial condition / 初始状态
Audio outputs were incomplete or misleading during early tests.

### Final working method / 最终有效方法
The final fix was simple once the right layout was found:

- `AppleALC.kext`
- `alcid=1`

### Final result / 最终结果
The machine gained working:
- built-in output
- line output
- digital output
- built-in input
- line input

At that point, audio was no longer a blocker.

---

## Phase 7 — Wi-Fi Recovery / Wi-Fi 恢复

The Broadcom wireless card required proper injector logic.

### Hardware / 硬件
- Broadcom BCM94352HMB / DW1550

### What mattered / 真正关键的点
The fix was not about adding random Broadcom files.  
It depended on using the correct injector combination and avoiding conflicting ones.

### Final working direction / 最终有效方向
- `AirportBrcmFixup.kext` enabled
- `AirPortBrcmNIC_Injector.kext` enabled
- `AirPortBrcm4360_Injector.kext` disabled

### Final result / 最终结果
Wi-Fi became stable and fully usable.

This included practical network use and hotspot relay behavior with iPhone.

---

## Phase 8 — Bluetooth Failure and Recovery / 蓝牙失败与恢复

Bluetooth was the hardest subsystem to complete.

### Initial broken state / 初始坏状态
The controller was partially visible, but unusable.

Typical output looked like:
- `Address: NULL`
- `State: Off`
- `Firmware Version: v0 c0`

This meant the Bluetooth side was being detected, but not correctly initialized.

### Critical insight / 关键认知
For BCM94352HMB / DW1550:
- Wi-Fi uses the PCIe path
- Bluetooth uses the USB path

So it was entirely possible for Wi-Fi to work while Bluetooth remained broken.

### What finally fixed Bluetooth / 最终修好蓝牙的东西
Bluetooth required four things together:

1. proper Broadcom Bluetooth kext stack
2. correct USB mapping
3. required Bluetooth NVRAM variables
4. NVRAM reset after changes

### Working Bluetooth kext direction / 蓝牙 kext 方向
- `BrcmFirmwareData.kext`
- `BrcmPatchRAM3.kext`
- `BlueToolFixup.kext`

### Critical USB insight / USB 核心发现
The Bluetooth chain was attached through the USB path and had to be mapped correctly as an internal device path.

### Critical NVRAM keys / 决定性 NVRAM 键值
- `bluetoothExternalDongleFailed = 00`
- `bluetoothInternalControllerInfo = 0000000000000000000000000000`

### Final result / 最终结果
After these changes:
- Bluetooth address appeared correctly
- the controller turned on
- device pairing became possible
- Bluetooth keyboard pairing succeeded
- relay-related Apple features became much more functional

This was one of the most decisive repairs in the whole project.

---

## Phase 9 — USB Mapping as a Structural Fix / USB 定制作为结构修复

USB mapping was not just an optimization.  
It was structural.

The machine initially used a borrowed USB-related solution from another ASUS-oriented OpenCore setup.  
That was enough to boot, but not enough to guarantee correct internal device behavior.

The Bluetooth path proved that USB mapping was not optional on this machine.

It was part of the final architecture.

---

## Phase 10 — Apple Ecosystem Integration / 苹果生态接入

Once graphics, Wi-Fi, audio, and Bluetooth were stabilized, the machine crossed into a new stage.

It no longer merely ran macOS.  
It began participating in the Apple ecosystem.

### Confirmed working features / 已确认可用功能
- webpage handoff
- phone relay
- iPhone hotspot relay
- iPhone to Mac AirDrop
- iPhone screen projection to Mac
- wired continuity camera / microphone
- Bluetooth device pairing

### Partial or incomplete features / 部分或未完全功能
- Mac to iPhone AirDrop
- Universal Clipboard
- fully wireless continuity camera behavior

Even with these limitations, the machine achieved far more ecosystem functionality than expected from its original hardware profile.

---

## The Most Important Lessons / 最重要的经验

### 1. A bootable system is not a finished system / 能开机不等于完成
The project only became meaningful after graphics, wireless, audio, and ecosystem features were actually repaired.

### 2. Graphics required both software and firmware alignment / 图形需要软件和固件双对齐
Ventura + OCLP was necessary, but BIOS graphics memory tuning was equally decisive.

### 3. Wi-Fi and Bluetooth are not the same problem / Wi-Fi 和蓝牙不是一回事
On this Broadcom card:
- Wi-Fi is PCIe
- Bluetooth is USB

This distinction explained many misleading symptoms.

### 4. NVRAM matters more than people think / NVRAM 比想象中更重要
Several Bluetooth problems were not solved by changing kexts alone.  
They required the correct NVRAM state.

### 5. USB mapping is part of system architecture / USB 定制属于系统架构的一部分
It should not be treated as an afterthought.

---

## Final State / 最终状态

By the end of this process, the machine reached:

- macOS Ventura 13.7.8
- Intel HD 5500 with full acceleration
- 1536MB reported VRAM
- working audio
- working Wi-Fi
- working Bluetooth
- practical Apple ecosystem integration

This was the point where the machine stopped being a compromise and became a completed personal Hackintosh build.

---

## Personal Closing Note / 个人收束

This machine did not become good because one magic patch solved everything.

It became good because each broken layer was identified correctly:

- graphics
- BIOS memory layout
- audio layout
- Broadcom injector logic
- Bluetooth USB path
- NVRAM state
- ecosystem-level validation

The final result was not luck.

It was accumulated correctness.
