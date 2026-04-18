# BIOS Settings / BIOS 关键设置

## Important Working Settings / 最关键有效设置

The following BIOS settings were critical to reaching a stable and fully accelerated Ventura system:

- **VT-d**: Disabled
- **Primary Display**: IGFX
- **Internal Graphics**: Enabled
- **DVMT Pre-Allocated**: 64M
- **DVMT Total Gfx Mem**: 256M
- **Aperture Size**: 256MB
- **Azalia**: Enabled

---

## Why They Matter / 为什么它们关键

### Graphics / 图形
The machine originally booted with only 7MB VRAM and no proper acceleration.

The decisive breakthrough came from:
- enabling the integrated GPU explicitly
- forcing IGFX as primary display
- setting DVMT Pre-Allocated to 64M
- keeping a reasonable graphics memory layout in BIOS

### Audio / 音频
Azalia had to remain enabled for onboard audio to become usable under AppleALC.

---

## Dangerous Settings / 风险设置

The following settings are risky and should not be changed casually after reaching a stable state:

- CSM video related options
- random display initialization modes
- PCIe graphics priority settings without clear reason

---

## Recovery Advice / 恢复建议

If BIOS gets reset:
1. restore the graphics settings first
2. save and boot OpenCore
3. reset NVRAM
4. only then evaluate graphics, Wi-Fi, and Bluetooth behavior
