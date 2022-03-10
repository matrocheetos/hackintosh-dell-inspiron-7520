# Dell Inspiron 7520 Hackintosh
[![OpenCore](https://img.shields.io/badge/OpenCore-0.7.8-brightgreen)](https://github.com/acidanthera/OpenCorePkg)
[![macOS](https://img.shields.io/badge/macOS-10.15-blue)](https://en.wikipedia.org/wiki/MacOS_Catalina)

Guide used: [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)

## Contents
* [Hardware Info](#hardware-info)
* [EFI/OC files](#efioc-files)
    * [ACPI](#acpi)
    * [Drivers](#drivers)
    * [Kexts](#kexts)
* [Issues](#issues)
* [Installation](#installation)
* [Triple Boot macOS/Windows/Linux using GRUB](#triple-boot-macoswindowslinux-using-grub)

## Hardware Info

| Hardware | Model |
| :--- | :--- |
| Computer | DELL Inspiron 15R SE 7520
| Chipset | Intel 7 Series C216 Chipset Family
| Processor | Intel Core i5-3210M (Ivy Bridge)
| Memory | 6GB 1600MHz DDR3
| GPU | Intel HD Graphics 4000
| dGPU | AMD Radeon HD 7730M (disabled)
| Display | 1920x1080 Built-In Display
| Sound Card | Conexant Cx20590 (layout-id 28)
| Ethernet | Realtek RTL8168/8111
| Wireless | Qualcomm Atheros AR9485/AR3012 (DW1703)
| Touchpad | Elan Microelectronics (PS2)
| SD Card Reader | Realtek RTS5179

## EFI/OC Files

### ACPI
* [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-methods/ssdttime.html#wrapping-up) and [SSDT-HPET](https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html)
    * Created using [SSDTTime](https://github.com/corpnewt/SSDTTime)
* [SSDT-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management)
    * Created using [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh)
* [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)
    * Used [prebuilt](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-dGPU-Off](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/laptop-disable.html)
    * Edited [sample SSDT](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/decompiled/SSDT-dGPU-Off.dsl.zip)
* [SSDT-XOSI](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)
    * Edited [sample SSDT](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/decompiled/SSDT-GPI0.dsl)

### Drivers
* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
* [OpenRuntime.efi](https://github.com/acidanthera/OpenCorePkg/releases) (from OpenCore 0.7.8)

### Kexts
* [Lilu.kext](https://github.com/acidanthera/Lilu/releases) (1.6.0)
* [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases) (1.2.8)
* SMCProcessor.kext
* SMCBatteryManager.kext
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases) (1.5.7)
* [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases) (1.6.9)
* [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases) (2.4.2)
* USBMap.kext
    * Created using [USBMap](https://github.com/corpnewt/USBMap)
* [VoodooPS2Controller.kext](https://github.com/acidanthera/VoodooPS2/releases) (2.2.7)
* [AirPortAtheros40.kext](https://www.insanelymac.com/forum/files/file/1008-io80211family-modif/) and HS80211Family.kext
    * Wi-Fi support for the AR9485
* Ath3kBT.kext and Ath3kBTInjector.kext
    * Bluetooth support for the AR3012
* [RealtekCardReader.kext](https://github.com/0xFireWolf/RealtekCardReader) (0.9.6)
    * **Not confirmed working**

## Issues

* **HDMI**: external monitor isn't working on current config, [iGPU patching](https://dortania.github.io/OpenCore-Post-Install/gpu-patching/intel-patching/) may fix it
* **VGA**: not supported
* **Hardware based DRM**: not supported
* **Continuity (AirDrop, Airplay, etc.)**: not fully supported
* **SD Card Reader** and **DVD drive** not tested
* **Audio Input** works as Line-In but not as Mic (at least on tested headset mic), integrated mic works fine
* Lack of hardware acceleration when macOS is booted from a reboot
* Everything else works

## Installation

Download the EFI directly from the webpage or by running the command:
```shell
git clone https://github.com/matrocheetos/hackintosh-dell-inspiron-7520.git
```
`PlatformInfo` has to be set up using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). This specific model is best paired with the MacBookPro10,2 SMBIOS.

Follow [this guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) for further instructions.

## Triple Boot macOS/Windows/Linux using GRUB
Check [Triple Boot Guide](https://github.com/matrocheetos/hackintosh-dell-inspiron-7520/blob/master/TripleBootGuide.md) to triple boot macOS(OpenCore), Windows and Linux.