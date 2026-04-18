# Known Issues / 已知问题与边界

## Overview / 总览

This document records the remaining limitations of the project after the system reached a stable and practical Ventura state.

The purpose of this file is not to weaken the project.

It exists to define the real operating boundary of the machine:
- what is fully working
- what is partially working
- what is unstable
- what should not be overclaimed

A high-quality Hackintosh project should document its limits with the same precision used to document its successes.

---

## Philosophy / 文档原则

This machine is considered successful because it is:
- stable
- accelerated
- practically usable
- ecosystem-capable

It is **not** presented as a perfect 1:1 replacement for genuine Apple hardware.

That distinction is important.

The following limitations are documented honestly so future maintenance, migration, and reproduction can stay grounded in reality.

---

## 1. AirDrop Direction Asymmetry / 隔空投送方向不对称

### Status / 状态
- **iPhone to Mac** AirDrop: working
- **Mac to iPhone** AirDrop: partial, unstable, or not working reliably

### Interpretation / 理解
This means device discovery and at least part of the Apple proximity stack are functioning.

However, the implementation is not fully symmetrical in practice.

### Practical impact / 实际影响
This is not a blocker for daily use, but it remains one of the clearest signs that the ecosystem layer is not yet fully identical to genuine Apple hardware.

---

## 2. Universal Clipboard / 通用剪贴板

### Status / 状态
- tested
- inconsistent or not working reliably
- not treated as solved

### Interpretation / 理解
Universal Clipboard depends on a more delicate continuity chain than basic Bluetooth pairing or webpage handoff.

Its failure does not mean Bluetooth is broken in a general sense.  
It means the higher-level continuity path is not fully complete.

### Practical impact / 实际影响
This feature is convenient, but not critical for the practical identity of the machine.

---

## 3. Wireless Continuity Camera / 无线连续互通相机

### Status / 状态
- wired continuity camera: working
- wireless continuity camera: incomplete or unstable

### Interpretation / 理解
The feature-level handshake exists:
- the iPhone recognizes the Mac
- macOS can see the continuity path
- the devices acknowledge each other as continuity participants

However, the fully wireless media path is not stable enough to be treated as complete.

### Practical impact / 实际影响
This is acceptable because wired continuity camera already provides real practical use, but it remains a known limit.

---

## 4. Continuity Microphone / 连续互通麦克风

### Status / 状态
- wired continuity microphone behavior: usable
- purely wireless behavior: not treated as fully reliable

### Interpretation / 理解
The machine has crossed the continuity threshold, but not every wireless media-routing path is equally mature.

### Practical impact / 实际影响
Good enough for experimentation and partial workflow use, but not something that should be advertised as universally stable.

---

## 5. Message Sync Variability / 信息同步波动

### Status / 状态
- some synchronization behavior appeared
- behavior was not always consistent
- not treated as a core solved subsystem

### Interpretation / 理解
This may depend on:
- Apple ID state
- account trust state
- device proximity
- Apple service timing
- continuity service freshness

Because similar inconsistency can also appear on genuine Apple hardware, this issue was not prioritized as a deep repair target.

### Practical impact / 实际影响
Low strategic importance for this project.

---

## 6. Bluetooth UI Behavior Was Once Misleading / 蓝牙界面行为曾具有误导性

### Status / 状态
During troubleshooting, Bluetooth could appear in a half-broken state:
- controller visible
- address `NULL`
- state `Off`
- firmware `v0 c0`
- settings toggle behavior inconsistent

### Interpretation / 理解
This was not a normal “Bluetooth off” state.  
It was an incomplete initialization state.

The existence of a Bluetooth controller entry did **not** mean Bluetooth was truly working.

### Practical impact / 实际影响
This remains an important diagnostic lesson for future maintenance and migration:
do not trust appearance alone; trust actual initialization state.

---

## 7. Bluetooth Depends on More Than Kext Presence / 蓝牙不只是“kext 在不在”

### Status / 状态
The machine proved that Bluetooth can still fail even when:
- the Bluetooth chipset is detected
- Broadcom kexts are loaded
- the device appears in USB information

### Interpretation / 理解
Bluetooth on this machine depends on a multi-layer chain:
- kext stack
- USB mapping
- NVRAM state
- correct EFI actually being used at boot

### Practical impact / 实际影响
Future migrations to a new SSD may appear successful while Bluetooth silently regresses.

This is one of the most important known maintenance risks in the project.

---

## 8. USB Mapping Is Machine-Specific / USB 定制具有强机器依赖性

### Status / 状态
The machine originally relied on a borrowed USB-related solution from another OpenCore setup.

That was good enough for booting, but not good enough for complete internal-device correctness.

### Interpretation / 理解
USB mapping on this machine is not a generic configuration artifact.  
It is tied to:
- this board
- this controller layout
- this wireless card
- this internal USB topology

### Practical impact / 实际影响
Blindly copying the EFI to another machine, even a similar one, may break:
- Bluetooth
- internal USB behavior
- sleep-related device routing
- continuity features

---

## 9. BIOS Resets Are Dangerous / BIOS 重置具有风险

### Status / 状态
BIOS resets can silently destroy a previously stable system state.

### Why / 为什么
This build depends on a small set of critical BIOS settings, especially:
- Internal Graphics
- Primary Display
- DVMT Pre-Allocated
- DVMT Total Gfx Mem
- Aperture Size
- Azalia

### Practical impact / 实际影响
If BIOS resets:
- graphics can regress
- audio can become confusing
- the system may still boot, but no longer behave correctly

This is one of the highest-risk maintenance events in the project.

---

## 10. SSD Migration Risk / 换盘迁移风险

### Status / 状态
System migration to a new SSD is possible, but not trivial.

### Main risk / 主要风险
A disk clone does not guarantee preservation of:
- the correct EFI
- the correct USB mapping
- the effective NVRAM state
- the exact Bluetooth recovery state

### Interpretation / 理解
A new disk can produce the illusion of a successful migration while quietly losing:
- Bluetooth stability
- ecosystem behavior
- graphics consistency if the wrong EFI is used

### Practical impact / 实际影响
Migration should always be followed by structured validation, not by assumption.

---

## 11. Genuine Apple Parity Is Not Claimed / 不宣称与真苹果完全等价

### Status / 状态
This project reached a high level of practical Apple ecosystem integration.

However, it does not claim full parity with genuine Apple hardware in every continuity behavior.

### Interpretation / 理解
The machine is:
- highly usable
- technically convincing
- ecosystem-capable

But it still operates within the natural boundary of a non-native platform.

### Practical impact / 实际影响
This project should be presented as a high-fidelity Hackintosh, not as a perfect clone.

---

## Operational Boundary / 实际使用边界

The machine is considered fully practical for:

- daily Ventura use
- graphics-accelerated workflows
- media playback
- web and account-level Apple continuity
- Bluetooth keyboard and peripheral use
- Wi-Fi networking
- phone relay
- hotspot relay
- iPhone projection
- wired continuity camera / microphone

The machine is considered only partially complete for:

- universal clipboard
- fully symmetrical AirDrop
- fully wireless continuity camera
- completely Apple-native continuity behavior in all edge cases

---

## Maintenance Warning / 维护警告

Any of the following events may reintroduce partial breakage:

- BIOS reset
- SSD migration
- EFI replacement
- USB map replacement
- NVRAM reset without re-checking Bluetooth keys
- random Broadcom injector changes
- random OCLP reconfiguration without validation

This system is stable, but only because its working layers are aligned carefully.

That alignment should be treated as something to preserve, not something to casually modify.

---

## Final Assessment / 最终评估

This project should be understood as:

- stable
- accelerated
- well-documented
- highly practical
- ecosystem-capable

with a clearly defined set of partial limitations.

That is not a weakness.

That is what makes the project credible.

---

## Personal Closing Note / 个人收束

The final machine is not interesting because it became perfect.

It is interesting because it became coherent.

Its strengths are real.
Its limits are known.
Its behavior is documented.

That is enough to make it a finished project.
