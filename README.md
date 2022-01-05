# Hackintosh-DELL-Vostro-5468

## READ THE ENTIRE README.MD BEFORE YOU START

### I am not responsible for any damages you may cause

- Complete EFI packs are available in the releases page.
- I will try my best to keep the repo updated with the latest kexts and OpenCore version.
- Please **do not clone or download** the main branch for daily use: it may include **unstable code** just because it is my repository.
- This EFI is configured with Monterey. (Not tested for Catalina and Big Sur ).
- With every EFI update you retrieve from here please remember to go through the post install guide.


> ## Update

## 2022-01-05

<details>
<summary><strong> SUMMARY </strong></summary>
<br>

> ### Non-Fuctional

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Fingerprint Reader                   | ❌   | `Not Work` |
| Card Reader                         | ❌   | `Not Work` |

> ### Video and Audio

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Full Graphics Accleration (QE/CI)    | ✅   | `WhateverGreen.kext`  |
| Audio Jack                     | ✅   | `AppleALC.kext` with Layout ID = 17 and `ComboJack`   |

> ### Power, Charge, Sleep and Hibernation

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Battery Percentage Indication        | ✅   | `SMCBatteryManager.kext`            | 
| iGPU Power Management                | ✅   | `CPUFriend.kext` and `CPUFriendDataProvider.kext` |
| S3 Sleep/ Hibernation Mode 3         | ✅   | `SSDT-GPRW.aml` | 

> ### Input/ Output

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| WiFi                                 | ✅   | `AirportItlwm.kext`  |
| Bluetooth                            | ✅   | `BlueToolFixup.kext`  |
| Ethernet                             | ✅   | `RealtekRTL8111.kext`  |
| USB 2.0, USB 3.0                     | ✅   | `USBMap.kext`    |
| USB Power Properties in macOS        | ✅   | `SSDT-EC-USBX-LAPTOP.aml` |

> ### Display, TrackPad, TrackPoint, and Keyboard

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Brightness Adjustments | ✅  | `WhateverGreen.kext`, `SSDT-PNLF.aml`, `Patch XOSI`, `VoodooI2C.kext`, `VoodooI2CHID.kext` and `BrightnessKeys.kext`|
| TrackPoint             | ✅  | `VoodooI2CHID.kext` and `VoodooI2C.kext` |
| TrackPad               | ✅  | `VoodooI2CHID.kext` and `VoodooI2C.kext` |
| Built-in Keyboard      | ✅  | `VoodooPS2Controller.kext` |
| Multimedia Keys        | ✅  | `BrightnessKeys.kext`|

> ### macOS Continuity

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| iCloud, iMessage, FaceTime           | ✅   | Whitelisted Apple ID, Valid SMBIOS  |
| AirDrop                              | ✅   | Not tested  |

> ### SSDT Patch

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Many SSDT Patch                  | ✅   | `SSDTTime` |

</details>

<details>
<summary><strong> REFERENCES </strong></summary>
<br>

Read these before you start:

- [dortania's Hackintosh guides](https://github.com/dortania).
- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/).
- [dortania/ Getting Started with ACPI](https://dortania.github.io/Getting-Started-With-ACPI/).
- [dortania/ opencore `multiboot`](https://github.com/dortania/OpenCore-Multiboot).
- [dortania/ `USB map` guide](https://dortania.github.io/OpenCore-Post-Install/usb/).
- [WhateverGreen Intel HD Manual](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md).
- `Configuration.pdf` and `Differences.pdf` in each `OpenCore` releases.

</details>

<details>
<summary><strong> REQUIREMENTS </strong></summary>
<br>

- A macOS machine(optional): to create the macOS installer.
- Flash drive, 12GB or more, for the above purpose.  
- Xcode works fine for editing plist files on macOS, but I prefer [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/).  
- [ProperTree](https://github.com/corpnewt/ProperTree) if you need to edit plist files on Windows.  
- [MaciASL](https://github.com/acidanthera/MaciASL), for patching ACPI tables and editing ACPI patches.
- [MountEFI](https://github.com/corpnewt/MountEFI) to quickly mount EFI partitions.  
- [IORegistryExplorer](https://developer.apple.com/downloads), for diagnosis.  
- [Hackintool](https://www.insanelymac.com/forum/topic/335018-hackintool-v286/), for diagnostic ONLY, Hackintool should not be used for patching, it is outdated.
- Patience and time, especially if this is your first time Hackintosh-ing.

</details>

<details>
<summary><strong> HARDWARE </strong></summary>
<br>

| Category  | THINKPAD X230            | 
| --------- | ------------------------ |
| CPU       | Intel Core i3-7100U ( Kaby Lake )     | 
| SSD       | Sata M.2 DigitalAlience & HDD WDC 500GB    |
| Display   | 14" (1366x768) |
| WiFi & BT | Intel Wireless-AC 3165   |
| RAM | 4GB DDR4 2133Mhz   |
| Audio | Realtek ALC256   |
| Trackpad | Dell I2C   |
| Bootloader | OpenCore 0.7.7   |
| macOS | Monterey 12.2   |

</details>

<details>
<summary><strong> GETTING STARTED </strong></summary>
<br>

Before you do anything, please familiarize yourself with basic Hackintosh terminologies and the basic Hackintosh process by throughly reading Dortania guides as linked in `REFERENCES`

- Creating a macOS installer: refer to [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
- [**README-HARDWARE**](/Other/README_HARDWARE.md): Requirements before installing.
- [**README-OTHERS**](/Other/README_OTHERS.md): for post installation settings and other remarks.

</details>

<details>
<summary><strong> BENCHMARKS </strong></summary>
</br>

- macOS 12.2, EFI OpenCore 0.7.7

| CPU            | Single-Core | Multi-Core |
| :------------- | ----------: | ---------: |
| Geekbench 5    |         595 |       1346 |

| GPU            | OpenCL      |
| :------------- | ----------: |
| Geekbench 5    |        3809 |


> ## CONTACT

- Email: bryanhafidz@hack.id

> ## SUPPORT

<details>
<summary><strong> CREDITS </strong></summary>
<br>

- [Apple](https://www.apple.com) for macOS.
- [Acidanthera](https://github.com/acidanthera) for all the kexts/utilities that they made.
- [Rehabman](https://github.com/RehabMan) and [Daliansky](https://github.com/daliansky) for the patches and guides and kexts.
- [Dortania](https://github.com/dortania) for for the OpenCore Install Guide.
- Etc ...

</details>
