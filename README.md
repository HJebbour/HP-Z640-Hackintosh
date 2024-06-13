# macOS on HP Z640 (Haswell-E)

OpenCore-based EFI for HP Z640 (Haswell-E)
<img align="right" src="./Docs/HP-Z640.png" alt="HP Z640" width="460">

**Status: Fully Working | Stable | Daily driver**

[![macOS](https://img.shields.io/badge/macOS-Sonoma-green.svg)](https://www.apple.com/macos/sonoma/)
[![Version](https://img.shields.io/badge/14.5-green.svg)](https://support.apple.com/en-us/109035#macos145)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.0-blue.svg)](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.0)
[![Model](https://img.shields.io/badge/Model-Z640-grey)](https://support.hp.com/us-en/document/c04496994)

This project was created from scratch using the [Dortania](https://dortania.github.io/getting-started/) guide specifically for the HP Z640, but should work on the Z440 and Z480 with a few [adjustments](https://github.com/HJebbour/Z640-Hackintosh/edit/main/README.md#pre-installation).

**DISCLAIMER:**
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start.

This Z640 Hackintosh project aims to be an all-in-one maintained hub for Opencore-based hackintoshes on the HP Zx40 family. In short, this Z640-Hackintosh is very stable and is currently my daily driver. I fully recommend this project to anyone looking for an old Mac Pro alternative.

This OpenCore-EFI should work as is with macOS Catalina, Big Sur, Monterey, Ventura, Sonoma and Sequoia (DP1).

You can find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

**Important:** In order to upgrade to macOS 14.4+ the value of `Misc -> Security -> SecureBootModel` must be set to `Disabled` in config.plist until the upgrade completely finishes.

Should you find an error, or improve anything, be it in the config itself or in the my documentation, please consider opening an issue or a pull request to contribute.

**I am not responsible for any damages you may cause.**

## Summary

<details>  

<summary><strong>WORKING ✅</strong></summary>
<br>

> ### Video and Audio
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Full Graphics Accleration (QE/CI) | ✅ | `WhateverGreen.kext` | AMD Radeon RX 580 is natively supported on macOS |
| Audio Output (Front/Back) | ✅ | `AppleALC.kext` with Layout ID = 11 | - |
| Audio Input (Front/Back) | ✅ | `AppleALC.kext` with Layout ID = 11 | - |
| Internal Speaker | ✅ | `AppleALC.kext` with Layout ID = 11 | - |
| Automatic Headphone Output Switching | ✅ | `AppleALC.kext` with Layout ID = 11 | - |
| DRM | ✅ | dGPU | - |

> ### Power Management
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| CPU Power Management | ✅ | `SSDT-PLUG.aml` | - |
| NVMe Compatibility | ✅ | `NVMeFix.kext` & `Innie.kext` | Improves NVMe compatibility with non-Apple SSDs |
| Sleep / Wake | ✅ | - | - |

> ### Connectivity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Wi-Fi | ✅ | `OpenCore Legacy Patcher` | Follow [this](https://www.reddit.com/r/hackintosh/comments/170q5wu/enable_wifi_in_sonoma_with_fenvi_t919/) guide to properly enable Wi-Fi and Bluetooth with macOS Sonoma. Wi-Fi is natively supported on previous macOS versions, no need to use OCLP. |
| Bluetooth | ✅ | `OpenCore Legacy Patcher` | Follow [this](https://www.reddit.com/r/hackintosh/comments/170q5wu/enable_wifi_in_sonoma_with_fenvi_t919/) guide to properly enable Wi-Fi and Bluetooth with macOS Sonoma. Bluetooth is natively supported on previous macOS versions, no need to use OCLP. |
| Ethernet | ✅ | `IntelMausi.kext` | - |
| USB 2.0 / USB 3.0 | ✅ | `USBMap.kext` | Create your own USBMap.kext using [CorpNewt](https://github.com/corpnewt/USBMap) |
| USB Power Properties in macOS | ✅ | - | - |

> ### macOS Continuity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| iCloud, iMessage, FaceTime | ✅ | Whitelisted Apple ID, Valid SMBIOS See [Dortania / OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) | - |
| Continuity Camera | ✅ | - | - |
| AirDrop | ✅ | - | - |
| Universal Control | ✅ | - | - |
| Apple Watch Auto Unlock | ✅ | - | - |
| Instant Hotspot | ✅ | - | - |
| Continuity Markup and Sketch | ✅ | - | - |
| Handoff | ✅ | - | - |
| Universal Clipboard | ✅ | - | - |
| SMS & Phone Call via iPhone | ✅ | - | - |
| AirPlay to Mac | ✅ | - | - |

> ### Miscellaneous
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Multiple Boot | ✅ | - | macOS, Windows, and Linux distributions (Use [this](https://dortania.github.io/OpenCore-Multiboot/empty/samedisk.html#precautions) guide to setup dual boot on the same drive) |
| Boot chime | ✅ | - | Working like a charme |


</details>  

<details>  
<summary><strong>NOT WORKING ❌</strong></summary>
<br>

| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Sidecar | ❌ | - | Cannot work on this machine as the there's no iGPU |
| FireVault 2 | ❌ | - | Cannot work when SecureBootModel is Disabled for OCLP |

</details>  

## Introduction

<details> 
<summary><strong>THIS IS NOT A GUIDE!</strong></summary>
</br>

This is not a guide. It shoud only be used as a reference. I provide some tips and tricks I learned on my journey in building a hackintosh. The best way of using this is as a supplement to the OpenCore guide. If you have questions about how to setup your specific hardware, are unclear about what to do, or would like to see the settings I've used.

I understand that some may simply add the OC and Boot folders to their EFI folder. For clarity the EFI partition needs a folder called EFI that contains the Boot and OC folder.

```EFI
EFI (drive)
	EFI
	├── BOOT
	├── OC
```

It should work and your HP Z640 should boot and work fine. **You will at minimum need to generate SMBIOS values if you want Apple services to work.** Note that all error reporting/logging has been turned off in the config.plist. You will have a difficult time trouble shooting with the setup provided. You can easily turn on the error reporting and logging if you follow the Dortania guide. Best of luck.

> **NOTE** if you simply wish to copy my EFI please do the following:
>
>1. [Generate SMBIOS values](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#nvram) and add them in the config.plist (Use MacPro7,1 or iMacPro1,1)
>2. Ensure the value of `showpicker` is  `true` in the config.plist file to provide the opencore menu when booting. 
>3. Prepare your install [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
>4. Move the entire EFI folder (with your modifications) to the proper partition on your [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-opencore-s-efi-environment) (or [SSD](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html) once the install is complete).
>5. [Install](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work) - You'll need to select Escape to get the boot menu options and **boot from the USB each time the computer restarts** until you've copied the EFI folder onto the hard drive. You may also need to select the correct boot option during install.

</details>  

<details> 
<summary><strong>THIS IS A GUIDE!</strong></summary>
</br>

**The one and only guide to install macOS, provided by [Dortania](https://dortania.github.io/OpenCore-Install-Guide/)**

</details>  

<details>
<summary><strong>HARDWARE</strong></summary>

### HP Z640 (Haswell-E)

These are relevant components on my machine which may differ from yours, keep these in mind as you will need to adjust accordingly, depending on your machine's configuration.

| Category  | Component                                       | Note                                                         |
| --------- | ----------------------------------------------- | ------------------------------------------------------------ |
| CPU | Intel Xeon E5-2699 v3 18-core (2,30 GHz) | - |
| GPU | AMD Radeon RX 580 8 GB | - |
| SSD | WDC PC SN720 SDAQNTW-512G-1001 | Using PCIe to M.2 adapter |
| Memory | 72 GB 2133 MHz DDR4 | - |
| Wi-Fi & BT | Fenvi T919 (Broadcom) | - |
| BIOS | M60 v02.61 23/03/2023 | Latest version to this date |

Refer to [HP Z640 Specs](https://support.hp.com/us-en/document/c04496994) for possible stock configurations.

</details>  

<details>

<summary><strong>SOFTWARE</strong></summary>
<br>

| Component      | Version |
| -------------- | ------- |
| OpenCore | 1.0.0 |
| macOS Sonoma | 14.5 |
| Windows 11 | 23H2 |
| Ubuntu | 22.04.4 LTS |
| Fedora | 40 |
| ESXi | 8 |
| Proxmox | 8.2 |

</details>

<details>
<summary><strong>ACPI</strong></summary>
<br>

| Component              |
| ---------------------- |
| SSDT-EC |
| SSDT-PLUG |
| SSDT-RTC0-RANGE |
| SSDT-UNC |
| SSDT-HPET |
| SSDT-USBX |

</details>

<details>
<summary><strong>KEXT</strong></summary>
<br>

| Kext                   | Version |
| ---------------------- | ------- |
| Lilu | 1.6.7 |
| VirtualSMC | 1.3.2 |
| AppleALC | 1.9.0 |
| IntelMausi | 1.0.7 |
| NVMeFix | 1.1.1 |
| Innie | 1.3.1 |
| SMCProcessor | 1.3.2 |
| SMCSuperIO | 1.3.2 |
| RestrictEvents | 1.1.3 |
| AMFIPass | 1.4.0 |
| WhateverGreen | 1.6.6 |
| USBMap | - |
| RTCMemoryFixup | 1.0.7 |
| IOSkywalkFamily | - |
| IO80211FamilyLegacy | - |

</details>

<details><summary><strong>UEFI DRIVERS</strong></summary>
<br>

|     Driver      | Version           |
| --------------- | ----------------- |
| OpenRuntime.efi | OpenCorePkg 1.0.0 |
| OpenCanopy.efi | OpenCorePkg 1.0.0 |
| OpenHfsPlus.efi | OpenCorePkg 1.0.0 |
| AudioDxe.efi | OpenCorePkg 1.0.0 |
| ResetNvramEntry.efi | OpenCorePkg 1.0.0 |
| ToggleSipEntry.efi | OpenCorePkg 1.0.0 |

</details>

<details>
<summary><strong>OTHER REPOSITORIES</strong></summary>
<br>

- Zx40-Hackintosh repositories:
  - [BillDH2k/Hackintosh-HP-Z440-Z640-Z840-OpenCore](https://github.com/BillDH2k/Hackintosh-HP-Z440-Z640-Z840-OpenCore/tree/main)
  - [DmitriyyyyS/HP-Z440](https://github.com/DmitriyyyyS/HP-Z440)
	
- Zx20-Hackintosh repositories:
  - [BillDH2k/Hackintosh-HP-Z420-Z620-Z820-OpenCore](https://github.com/BillDH2k/Hackintosh-HP-Z420-Z620-Z820-OpenCore)
  - [sagaciouszu/OpenCore-HP-Z620](https://github.com/sagaciouszu/OpenCore-HP-Z620)

</details>  

<details> 
<summary><strong>CREDITS</strong></summary>

### Credit to all these great people whom I don't know but have made my hackintosh dreams a reality:

- The guys from [Acidanthera](https://github.com/acidanthera) that make this possible
- [ben9923](https://github.com/ben9923) for [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C)
- [Apple](http://apple.com) for macOS
- [CorpNewt](https://github.com/corpnewt) for [USBMap](https://github.com/corpnewt/USBMap)
- [headkaze](https://github.com/headkaze) for [Hackintool](https://github.com/headkaze/Hackintool)
- [Mieze](https://github.com/Mieze) for [IntelMausiEthernet](https://github.com/Mieze/IntelMausiEthernet)
- People at [r/hackintosh](https://www.reddit.com/r/hackintosh/) for their advice and help
- And every other contributor

</details>

<details><summary><strong>SCREENSHOTS</strong></summary>
    <br>
    <p float="left">
        <img src="./Docs/HP-Z640-macOS-Sonoma-14.5.png" alt="Neofetch & About This Mac" width="1000">
	<img src="./Docs/OpenCore-Boot-Picker.png" alt="Multiboot: Windows 11, Ubuntu, Fedora, ESXi, Proxmox, and macOS" width="1000">
	<img src="./Docs/HP-Z640-macOS-Sequoia-15-DP1.png" alt="Experimental support of macOS Sequoia" width="1000">
    </p>
</details> 

## Pre-Installation

<details><summary><strong>UEFI SETTINGS</strong></summary>
<br>

**Security**

- **System Security**
  - `Virtualization Technology (VT-x)` **Enable**
  - `Intel VT for Directed I/O (VT-d)` **Disable**

**Advanced**

- **Boot Options**
  - `Fast Boot` **Disable**
  - `S5 Wake On LAN` **Disable**

- **Device Configurations**
  - `SATA Controller Mode` **AHCI**

- **Secure Boot Configuration**
  - `Configure Legacy Support and Secure Boot` **Disable Legacy Support and Disable Secure Boot**

- **Performance Options**
  - `Intel Hyper-Threading Technology` **Enable**

</details>

<details><summary><strong>ADJUSTMENTS</strong></summary>
<br>

**Broadwell-E**

To enable support for Xeon v4 CPUs, you must change the following values in `Kernel -> Emulate` under your config.plist file:

- **Cpuid1Data: D4060300 00000000 00000000 00000000**
  - Fake CPUID entry
- **Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000**
  - Mask for fake CPUID

**Haswell-E**

To enable support for Xeon v3 CPUs, you must change the following values in `Kernel -> Emulate` under your config.plist file (Already configured in the included EFI folder):

- **Cpuid1Data: C3060300 00000000 00000000 00000000**
  - Fake CPUID entry
- **Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000**
  - Mask for fake CPUID

**Z840 Support**

- **2nd LAN port must be disabled in BIOS for Z840 workstations**
- **Add the following kexts to enable SAS controller**
  - AstekFusion2Family.kext
  - AstekFusion2Adapter.kext

</details>

<details><summary><strong>KEYBOARD LAYOUT</strong></summary>
<br>

Either add as a `String` or as a `Data` (HEX Data [ProperTree](https://github.com/corpnewt/ProperTree))

Format is lang-COUNTRY:keyboard

🇺🇸 | [0] en_US - U.S --> en-US:0 --> (656e2d55 533a30 in HEX)

| Key           | Type   | Value   |
| ------------- | ------ | ------- |
| prev-lang:kbd | String | en-US:0 |


Pick your keyboard layout here:

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

## Post-Installation

<details><summary><strong>OpenCore Installation</strong></summary>
<br>

Move the entire EFI folder from the prepared USB (with your modifications) to the EFI partition on your hard drive or SSD.
