# Hackintosh-DELL-Vostro-5468

![macOs Ventura](Screenshot/1.png)

<p align = "center">
macOS Ventura
</p>

* macOS:
  - macOS Ventura ✅
* Windows:
  - Windows 11 ✅
* Bootloader: OpenCore 0.8.8
* EFI can be used for both for installation and booting from SSD.

## Introduction

<details>
<summary><strong>System Overview</strong></summary>
</br>

**Dell Vostro-14 5468**

| Type | Item |
| ---- | ---- |
| CPU | Intel Core i3-7100U @ 2.40 GHz, 3M Cache |
| RAM | Samsung 8GB DDR4-2133MHz |
| SSD1 | Digital Alliance 128GB M.2 SATA III |
| HDD2 | Western Digital WD5000LPCX 500GB SATA Hard Drive |
| Sound | Realtek ALC256 |
| Wireless, Bluetooth | Intel 3165 |
| Integrated GPU | Intel HD Graphics 620 |

</details>

<details>
<summary><strong>Current Status</strong></summary>
</br>

| Feature | Status |
| ------------- | ------------- |
| CPU Power Management | ✅ Working |
| Sleep/Wake | ✅ Working |
| Intel HD620 Graphics Acceleration | ✅ Working |
| Intel Quartz Extreme and Intel Core Image (QE/CI) | ✅ Working |
| Brightness control slider | ✅ Working |
| Special function keys (audio, brightness...) | ✅ Working |
| Ethernet | ✅ Working |
| Audio and HDMI Audio | ✅ Working |
| Multi-Touch Trackpad | ✅ Working |
| Battery | ✅ Working |
| iMessage/Facetime and App Store | ✅ Working  |
| Speakers and Headphones | ✅ Working |
| Built-in Microphone | ✅ Working |
| Webcam | ✅ Working |
| Wi-Fi/Bluetooth | ✅ Working |
| Hibernation | ✅ Working |
| FileVault | ✅ Working |
| ClamShell | ✅ Working |
| BootCamp | [-] Not Tested |
| Airdrop/Handoff | ❌ Not Working |
| SD Card | ❌ Not Working (Disable) |
| Fingerprint reader | ❌ Not Working (Disable) |

</details>

## Installation

<details>
<summary><strong>BIOS Configuration</strong></summary>
</br>

**Recommend you should restore the BIOS setting to BIOS Setting first. Then configure the following things:**

  | Sub-menu | Key: Value | Comment |
  | --- | --- | --- |
  | UEFI Boot Path Security | `Disabled` | |
  | Enable Legacy Option ROMs | `Disabled` | Disable will help OpenCanopy load faster |
  | SATA Operation | `AHCI` | |
  | Enabled USB Boot Support | `Enabled` | |
  | Enable External USB Port | `Enabled` | |
  | Secure Boot | `Disabled` | Can set to `Enabled` if you have already custom secure boot keys and signed OpenCore binaries |
  | Wake on USB | `Enabled` | Wake from keyboard works correctly | |

</details>

<details>
<summary><strong>Mainly Configuration</strong></summary>

### Graphic Display
* Integrated Intel HD Graphics 620 support is handled by WhateverGreen, and configured in the `DeviceProperties` section of `config.plist`.

### Audio
* For ALC256 on this my Machine, I use `layout-id = 69` (Patched on DSDT).
<!-- * Without any modifications, the headphone jack is buggy. External microphones aren't detected and the audio output may randomly stop working or start making weird noises.
* Start from this version, I change to use `ComboJack`. It gives better sound experience and performance when using the headset/headphone. -->

</details>

<details>
<summary><strong>Other Configuration</strong></summary>

### Wireless, Bluetooth
* The stock Intel AC 3165 can be worked well with [OpenIntelWireless](https://github.com/OpenIntelWireless).

### Sleep, Wake and Hibernation
* Config in Terminal ( Optional ) :
 - `sudo pmset powernap 0`
 - `sudo pmset proximitywake 0`
 - `sudo pmset standby 0`
 - `sudo pmset tcpkeepalive 0`
 - `sudo pmset lidwake 0`
* NOTE: please use powernap 0 to fix itlwm try reconnect many times.

### Keyboard, Trackpad and Magic Trackpad
- Look up & data detectors
- Secondary click (with two fingers, in bottom left corner*, in bottom right corner*)
- Tap to click
- Scrolling
- Zoom in or out
- Smart zoom
- Enable Drag and Drop use Clickpad: Some trackpad settings have been moved on 10.12+, this is the case for tap to drag. Navigate to the Accessibility PrefPane. On the left, select 'Mouse & Trackpad' and then 'Trackpad Option'. Here you must select 'Enable Drag' and set "Without drag lock"
- Etc ...

### CPU Power Management
* Native CPU Power Management

### Disable CFG Lock
* Removing the CFG Lock enables better compatibility with Mac and better CPU and power management
![cfg](Screenshot/cfg.png)
* For set CFG LOCK Disabled `setup_var 0x4DE 0x0` in [modGRUBShell.efi](https://github.com/datasone/grub-mod-setup_var/releases)
* After this mod set false the quirks AppleXcpmCfgLock

</details>

<details>
<summary><strong>iServices</strong></summary>

* To use iMessage and other Apple services, you need to generate your own serial numbers. This can be done using [CorpNewt's GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Make sure model is `MacBookPro14,1`. Then, go [Apple Check Coverage page](https://checkcoverage.apple.com/) to check your generated serial numbers. If the website tells you that the serial number **is not valid**, that is fine. Otherwise, you have to generate a new set.

* Next you will have to copy the following values to your `config.plist`:
  - Serial Number -> `PlatformInfo/Generic/SystemSerialNumber`.
  - Board Number -> `PlatformInfo/Generic/MLB`.
  - SmUUID -> `/PlatformInfo/Generic/SystemUUID`.
  Reboot and Apple services should work.

* If they don't, follow [this in-depth guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html). It goes deeper into ROM, clearing NVRAM, clearing Keychain (missing this step might cause major issues), and much more.
</details>

<details>
<summary><strong>Kext Docs</strong></summary>
</br>

* AirportItlwm.kext: Intel AC 3165 Wireless
* AppleALC.kext: Enable Audio with layout-id=69
* BlueToolFixup.kext: Enable bluetooth in Ventura (if you on BigSur you can remove this, because Native on Big Sur)
* CPUFriend.kext : For handle cpu-frequency data providing patch CPU-Frequency_data from CPUFriend
* Lilu.kext: Kernel extension bringing a platform for arbitrary kext, library, and program patching throughout the system for macOS
* PropertyInjector.kext: Inject Thermal Subsystem
* RealtekRTL8111.kext: Driver Ethernet for the Realtek RTL8111/8168 family
* VoodooI2C and VoodooI2CHID: Fix Trackpad, pair with extension VoodooI2CHID.kext
* VirtualSMC.kext: Advanced Apple SMC emulator in the kernel
* VoodooPS2Controller.kext: Enable Keyboard and Touchpad
* WhateverGreen.kext: Lilu plugin providing patches to select GPUs on macOS
<!-- * VerbStub.kext: for Handle ComboJack ( Headphone Fix ) -->

</details>

<details>
<summary><strong>DSDT Patch Docs</strong></summary>
</br>

* Fix _WAK Arg0 v2 : For wake from sleep to turn on various.
* HPET : Patches out IRQ conflicts.
* SMBUS : Adds missing SMBUS (Intel System Management Bus) device to the system and added AppleMikeyDriver under SMBUS.
* IRQ Fix : Fixes non-working audio on certain OEM (Dell, HP) machines.
* RTC : Fix the system clocks found on newer hardware.
* Fix Mutex with non-zero SyncLevel : Fixes Failed Battery Status and other related issues.
* Add MCHC : Adds missing MCHC Device.
* Patch USB_7/8 series : Injects Power Properties for USB.
* Sb_prw_0x6d (instant wake) : To fix the sleep/wake function.
* Dmac : Adds a DMA Controller to the LPCB (Low Pin Count Bus).
* Dtgp : Method that passes through calls to _DSM methods on various Device objects.
* Slpb : Fix sleep power button.
* Usbx : Supply USB power properties for Skylake and newer, so we will bundle this device in with the EC fix.
* AlsD : Add Fake Ambient Light Sensor.
* Pnlf : Fix Brightness Slider.
* Xosi : Fixing I2C trackpads and Brightness Keyss is enabling them within ACPI.
* Cpu power management : Fix power management CPU-Frequency.
* Brightness keys : Fix brightness keyss up and down.
* Audio patch : Patch layout-id audio in DSDT.
* USB Patch Native without Kext/Injector.
* _PLD Buffer/Package : For return a variable length Package of Buffers.
* Cleanup unused code.

</details>

<details>
<summary><strong>Screenshot</strong></summary>
</br>

![1](Screenshot/1.png)
![2](Screenshot/2.png)
![3](Screenshot/3.png)
![4](Screenshot/4.png)
![5](Screenshot/5.png)
![6](Screenshot/6.png)
![7](Screenshot/7.png)
![8](Screenshot/8.png)
![9](Screenshot/9.png)
![10](Screenshot/10.png)
![11](Screenshot/11.png)
![12](Screenshot/12.png)
![13](Screenshot/13.png)
![14](Screenshot/14.png)
![15](Screenshot/15.png)
![25](Screenshot/25.png)
![26](Screenshot/26.png)
![27](Screenshot/27.png)
![28](Screenshot/28.png)
![16](Screenshot/16.png)
![17](Screenshot/17.png)
![18](Screenshot/18.png)
![19](Screenshot/19.png)
![20](Screenshot/20.png)
![21](Screenshot/21.png)
- New Update CPU Management</br>
![22](Screenshot/22.png)
- New Update USB Port Mapping</br>
![23](Screenshot/23.png)
- New Update Cleanup Unused Code DSDT</br>
![24](Screenshot/24.png)
</details>

## Credit
- [Apple](https://apple.com) for macOS;
- [Acidanthera](https://github.com/acidanthera) for OpenCore and all the lovely hackintosh work.
- [Dortania](https://github.com/dortania) For their detailed guides.
- [Olarila](Olarila.com) For Installer
- Etc ...
