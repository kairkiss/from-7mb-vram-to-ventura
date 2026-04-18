# Graphics Fix / 图形加速修复

## Overview / 总览

This document records the complete graphics recovery path of this machine, from a barely functional Intel HD 5500 state with only **7MB VRAM** to a fully accelerated macOS Ventura 13.7.8 system reporting **1536MB VRAM**.

This was not a one-step fix.  
The final result required alignment across:

- OpenCore base configuration
- Ventura compatibility
- OCLP root patching
- BIOS graphics memory settings

The decisive lesson was simple:

> graphics acceleration on this machine was not restored by software alone.  
> It required both software patching and firmware-side graphics memory correction.

---

## Initial State / 初始状态

At the beginning, the machine could boot into macOS, but graphics were fundamentally broken.

### Reported condition / 表面表现
- Intel HD Graphics 5500 detected
- **VRAM reported as 7MB**
- no proper graphics acceleration
- incomplete visual effects
- poor animation smoothness
- weak overall usability

### Why 7MB matters / 为什么 7MB 是红色警报
On macOS, 7MB VRAM is not a "small but acceptable" state.

It usually means the graphics stack is not initialized correctly for real acceleration.

In practice, that means:
- no full Metal-class behavior
- no correct framebuffer behavior
- poor UI rendering quality
- degraded video playback experience

At that stage, the machine was only superficially running macOS.

---

## Why OpenCore Alone Was Not Enough / 为什么单靠 OpenCore 不够

A working OpenCore setup is necessary, but it does not guarantee a fully accelerated graphics stack.

The system could:
- boot
- show desktop output
- accept basic interaction

but that was not the same as having proper graphics acceleration.

This distinction was essential to the whole project.

A bootable machine is not a finished machine.

---

## Ventura as the Final Target / Ventura 作为最终目标

The machine was eventually moved to **macOS Ventura 13.7.8**.

This mattered for two reasons:

1. Ventura became the final operating target of the build
2. Ventura also forced the graphics issue into a more explicit compatibility problem that had to be solved correctly

Ventura did not automatically fix graphics.

But it established the final environment in which the proper repair had to happen.

---

## OCLP Root Patch / OCLP 根补丁

Once Ventura was in place, OpenCore Legacy Patcher became essential.

### Why OCLP mattered / 为什么 OCLP 关键
Broadwell integrated graphics on Ventura required post-install patching to restore legacy support properly.

Without that patch layer, the machine could remain in an under-accelerated or incorrectly initialized graphics state.

### What OCLP changed / OCLP 改变了什么
OCLP restored missing support layers necessary for older Intel graphics to behave correctly on a newer macOS release.

It moved the machine much closer to usable graphics acceleration.

### But OCLP was not the full answer / 但 OCLP 不是全部答案
Even after successful OCLP patching, the graphics result was still incomplete until BIOS graphics memory settings were corrected.

This was the turning point in understanding the real problem.

---

## BIOS Graphics Memory Tuning / BIOS 显存相关调校

This was the decisive stage.

The project only became a true success after the graphics-related BIOS settings were aligned properly.

### Final important values / 最终关键值
- **Primary Display**: IGFX
- **Internal Graphics**: Enabled
- **DVMT Pre-Allocated**: 64M
- **DVMT Total Gfx Mem**: 256M
- **Aperture Size**: 256MB

### Why these values mattered / 为什么这些值关键

#### Internal Graphics
The iGPU had to be explicitly available as a real graphics device path.

#### Primary Display = IGFX
The system needed to treat the integrated graphics path as the primary display route.

#### DVMT Pre-Allocated = 64M
This was especially important.  
Broadwell graphics on macOS often become unstable or under-initialized when DVMT pre-allocation is too low.

#### DVMT Total Gfx Mem and Aperture Size
These settings helped establish a more realistic and usable graphics memory layout for macOS.

---

## The Breakthrough Moment / 决定性突破

Once the following layers were all aligned:

- OpenCore base boot configuration
- Ventura as final system target
- successful OCLP root patch
- corrected BIOS graphics memory settings

the graphics stack finally crossed the line from "boots with display" to "fully accelerated macOS graphics".

### Final result / 最终结果
The machine achieved:

- **Intel HD Graphics 5500**
- **1536MB reported VRAM**
- smooth video playback
- restored visual fluidity
- proper translucency / glass-like UI effects
- a much more native macOS feel

That was the true completion point of graphics recovery.

---

## What Counted as Real Success / 什么才算真正修好

Graphics recovery was not judged by one number alone.

The project treated graphics as truly fixed only when all of the following were true:

- VRAM no longer reported as 7MB
- the system reported **1536MB**
- video playback became smooth
- UI animations became normal
- transparency and visual effects returned
- the machine felt stable in daily use

A reported improvement without real visual improvement would not have counted as a full fix.

---

## What Failed or Was Misleading / 哪些东西曾经失败或误导

This project also showed what **did not** solve the problem on its own.

### 1. Booting successfully
A successful boot did not mean acceleration was fixed.

### 2. SMBIOS alone
Changing model identity alone was not enough to restore full graphics behavior.

### 3. OCLP alone
OCLP was necessary, but not sufficient.

### 4. Random BIOS changes
Blind BIOS experimentation was risky.  
Only a small number of graphics-related settings truly mattered.

---

## Practical Validation / 实际验证方式

The final graphics state was validated not just through system information, but through actual experience.

### Validation signals / 验证信号
- system profile showed **1536MB VRAM**
- video playback was smooth
- desktop effects returned
- the machine visually behaved like a real accelerated Ventura environment

This mattered more than any single screenshot.

---

## Final Configuration Logic / 最终配置逻辑

The graphics fix was the product of a layered logic:

### Layer 1 / 第一层
Build a bootable OpenCore environment

### Layer 2 / 第二层
Reach Ventura as the final target OS

### Layer 3 / 第三层
Apply OCLP root patch for Broadwell graphics compatibility

### Layer 4 / 第四层
Correct BIOS graphics memory settings

### Layer 5 / 第五层
Validate through both reported VRAM and real visual behavior

Only when all five layers aligned did the machine finally achieve full graphics recovery.

---

## Lessons Learned / 经验总结

### 1. 7MB VRAM is a structural failure / 7MB 显存是结构性故障
It is not a cosmetic bug.  
It signals that the graphics stack is fundamentally incomplete.

### 2. Graphics repair on legacy Intel iGPU is multi-layered / 老 Intel 核显修复是多层联动
No single patch solved everything.

### 3. BIOS matters / BIOS 很重要
Firmware-side graphics memory configuration can be just as important as OpenCore or OCLP.

### 4. Visual validation matters / 体感验证很重要
A working graphics stack must be proven by real system behavior, not just by a boot screen.

---

## Final State / 最终状态

By the end of this stage, the machine reached the following graphics condition:

- **GPU**: Intel HD Graphics 5500
- **Reported VRAM**: 1536MB
- **Acceleration**: restored
- **UI behavior**: smooth
- **Video playback**: smooth
- **Visual effects**: restored

This was the most dramatic transformation of the entire project.

It was the moment the machine stopped pretending to be a usable Mac and actually became one.

---

## Personal Closing Note / 个人收束

The graphics fix was the soul of this build.

Without it, the machine would have remained a technical curiosity:
bootable, visible, but not convincing.

With it, the entire project crossed into a different class.

From that point on, every other subsystem repair had a real platform worth completing.
