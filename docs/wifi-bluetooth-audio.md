# Wi-Fi, Bluetooth, Audio / 无线、蓝牙、音频

## Audio / 音频

Audio was eventually restored with AppleALC.

### Final working method / 最终有效方法
- `AppleALC.kext`
- `alcid=1`

This exposed:
- built-in output
- line output
- digital output
- built-in input
- line input

---

## Wi-Fi / 无线网络

The final Wi-Fi card is:

- **Broadcom BCM94352HMB / DW1550**

### Final working direction / 最终有效方向
Wi-Fi was not fixed by OCLP itself.  
It was fixed by selecting the correct Broadcom injector strategy and avoiding conflicting injector combinations.

### Final logic / 最终逻辑
- `AirportBrcmFixup.kext` enabled
- `AirPortBrcmNIC_Injector.kext` enabled
- `AirPortBrcm4360_Injector.kext` disabled

---

## Bluetooth / 蓝牙

Bluetooth was the most stubborn part of the project.

### Symptoms / 初始症状
- controller visible
- address was `NULL`
- state remained `Off`
- firmware looked uninitialized

### What finally mattered / 最终关键点
1. updated Broadcom Bluetooth kexts
2. corrected USB mapping logic
3. required Bluetooth NVRAM variables

### Required NVRAM keys / 必要 NVRAM 键值
- `bluetoothExternalDongleFailed = 00`
- `bluetoothInternalControllerInfo = 0000000000000000000000000000`

### Final result / 最终结果
- Bluetooth keyboard pairing successful
- phone relay successful
- Apple ecosystem Bluetooth chain functional

---

## Final Status / 最终状态

- **Audio**: working
- **Wi-Fi**: working
- **Bluetooth**: working
