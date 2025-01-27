# Fujitsu Celcius H730 Hackintosh OpenCore


**macOS Version: Monterey 12.7.6**

[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.2-blue.svg)](https://github.com/acidanthera/OpenCorePkg)

## Introduction

**DISCLAIMER:**
Read the entire [Dortania](https://dortania.github.io/OpenCore-Install-Guide) guide before you start.
If you think that configuration is useful for you, consider to give a star for this repository :).

<details>
<summary>
    <strong>Hardware configuration</strong>
</summary>

### **Fujitsu Celcius H730**


[![Fujitsu](https://img.shields.io/badge/Fujitsu-Specs-red)](https://gzhls.at/blob/ldb/1/c/f/3/6b552fee192ea5db796e5d12740ed8caaae4.pdf) 

 | Component       | Manufacturer and model                                | Additional description           |
 | --------------- | ----------------------------------------------------- | -------------------------------- |
 | CPU             | Intel Core i7-vPro                                    |i7-4810MQ @2.8GHz                 |
 | GPU             | Intel Graphics 4th  Gen                               |                                  |
 | External GPU    | NVIDIA Quadro k2100M Graphics 4 GB GDDR5              | Disabled                         |
 | Audio           | Realtek ALC282                                        |                                  |
 | Wireless        |                                                       |                                  |
 | LAN             | I217-LM                                               |                                  |
 | Trackpad        |PS/2                                                   |                                  |
 | Keyboard        |ps/2                                                   |                                  |
 | BIOS version    | v1.12                                                 |                                  |
 

</details>  

<details>
<summary>
    <strong>Kernel extensions</strong>
</summary>

| Kext                        | Version        |
| :-------------------------: | :------------: |
| [AirportItlwm](https://github.com/OpenIntelWireless/itlwm/releases)         | 2.3.0 |
| [AppleALC](https://github.com/acidanthera/AppleALC/releases)                | 1.9.3 |
| [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases)| 2.4.0 |
| [Lilu](https://github.com/acidanthera/lilu/releases)                        | 1.7.0 |
| [SMCBatteryManager](https://github.com/acidanthera/virtualsmc/releases)     | 1.2.0 |
| [SMCProcessor](https://github.com/acidanthera/virtualsmc/releases)          | 1.2.0 | 
| [SMCSuperIO](https://github.com/acidanthera/virtualsmc/releases)            | 1.2.0 | 
| [VirtualSMC](https://github.com/acidanthera/virtualsmc/releases)            | 1.3.4 | 
| [VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2/releases)    | 2.3.7 | 
| [WhateverGreen](https://github.com/acidanthera/whatevergreen/releases)      | 1.6.9 | 
|[IntelMausi](https://github.com/acidanthera/IntelMausi/releases)             |1.0.8  |
|[ECEnabler](https://github.com/1Revenger1/ECEnabler/releases)                |1.0.5  |
|[BrightnessKeys](https://github.com/acidanthera/BrightnessKeys/releases)     |1.0.3  |

</details>

<details>
<summary>
    <strong>UEFI drivers</strong>
</summary>

|     Driver      | 
| :-------------: | 
| HfsPlus.efi | 
| OpenCanopy.efi  |
| OpenRuntime.efi | 
| ResetNvranEntry.efi|

</details>


## Configuration advices (config.plist)

You can find the detailed configuration guide for Haswell laptops on [dortania.github.io](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/haswell.html#starting-point) site.
However below configuration is working for the specified laptop.
<details>
<summary>
    <strong>ACPI</strong>
</summary>

- **Add**
  - Patches recommended via Dortania guide:
    - `SSDT-EC-LAPTOP.aml`
    - `SSDT-PLUG-DRTNIA.aml`
    - `SSDT-PNLF.aml`
    - `SSDT-XOSI.aml`

- **Patch**
  - Change _OSI to XOSI:
    - `Comment -> Change _OSI to XOSI`
    - `Enabled -> True`
    - `Count -> 0`
    - `Limit -> 0`
    - `Find -> 5F4F5349`
    - `Replace -> 584F5349`

</details>

<details>
<summary>
    <strong>DeviceProperties</strong>
</summary>

- **Add**
  - Audio support
    - `PciRoot(0x0)/Pci(0x1B,0x0)`
      - `layout-id -> 4`


  - IGPU support
    - `PciRoot(0x0)/Pci(0x2,0x0)`
      - `AAPL,ig-platform-id -> 0600260A`
      - `framebuffer-patch-enable -> 01000000`
      - `framebuffer-cursormem -> 00009000`
      - `device-id -> 12040000`

</details>

<details>
<summary>
    <strong>Kernel</strong>
</summary>

- **Quirks**
  - `AppleCpuPmCfgLock -> False`
  - `AppleXcpmCfgLock -> True`
  - `AppleXcpmExtraMsrs -> False`
  - `AppleXcpmForceBoost -> False`
  - `CustomSMBIOSGuid -> False`
  - `DisableIoMapper -> True`
  - `DisableLinkeditJettison -> True`
  - `DisableRtcChecksum -> False`
  - `ExtendBTFeatureFlags -> False`
  - `ExternalDiskIcons -> False`
  - `ForceSecureBootScheme -> False`
  - `IncreasePciBarSize -> False`
  - `LapicKernelPanic -> False`
  - `LegacyCommpage -> False`
  - `PanicNoKextDump -> True`
  - `SetApfsTrimTimeout -> -1`
  - `ThirdPartyDrives -> False`
  - `XhciPortLimit -> True`

</details>

<details>
<summary>
    <strong>Misc</strong>
</summary>

- **Boot**
  - `ConsoleAttributes -> 0`
  - `HibernateMode -> None`
  - `HideAuxiliary -> True`
  - `LauncherOption -> Disabled`
  - `LauncherPath -> Default`
  - `PickerAttributes -> 1`
  - `PickerAudioAssist -> False`
  - `PickerMode -> Builtin`
  - `PickerVariant -> Auto`
  - `PollAppleHotKeys -> False`
  - `ShowPicker -> False`
  - `TakeoffDelay -> 0`
  - `Timeout -> 0`

- **Security**
  - `AllowSetDefault -> True`
  - `ApECID -> 0`
  - `AuthRestart -> False`
  - `BlacklistAppleUpdate -> True`
  - `DmgLoading -> Signed`
  - `EnablePassword -> False`
  - `ExposeSensitiveData -> 6`
  - `HaltLevel -> 2147483648`
  - `PasswordHash -> <>(empty value)`
  - `PasswordSalt -> <>(empty value)`
  - `ScanPolicy -> 0`
  - `SecureBootModel -> Default`
  - `Vault -> Optional`

</details>

<details>
<summary>
    <strong>NVRAM</strong>
</summary>
    LegacyOverwrite -> False
    WriteFlash -> True

- **Add**
  - System Integrity Protection bitmask
  `7C436110-AB2A-4BBB-A880-FE41995C9F82`
    - `boot-args -> keepsyms=1 debug=0x100 -wegnoegpu`

</details>

<details>
<summary>
    <strong>PlatformInfo</strong>
</summary>

 **Note**: You need to generate your own values for `SystemProductName`, `SystemSerialNumber`, `MLB` and `SystemUUID` using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

</details>

<details>
<summary>
    <strong>UEFI</strong>
</summary>

- **Quirks**
  - `DisableSecurityPolicy -> False`
  - `ExitBootServicesDelay -> 0`
  - `IgnoreInvalidFlexRatio -> True`
  - `ReleaseUsbOwnership -> True`
  - `RequestBootVarRouting -> True`
  - `TscSyncTimeout -> 0`
  - `UnblockFsConnect -> False`

</details>

## Status



<details>  
<summary>
    <strong>Working ✅</strong>
</summary>


- `Audio` - Realtek ALC282 
- `Brightness Keys` 
- `Battery` (management, percentage and actual work time)
- `Bluetooth and Wi-Fi` 
- `Ethernet port` - 
- `Keyboard`
- `Intel IGPU`
- `Internal microphone`
- `Shutdown / Reboot functions`
- `Sleep/Wake` - using Sleep from menu and after laptop lid close/open
- `Speakers and headphones combo jack`
- `System updates` 
- `Touchpad`
- `USB Ports`
- `Web camera`

</details>

<details>  
<summary>
    <strong>Not working ❌</strong>
</summary>

- `SD Card Reader`

</details>

<details>  
<summary>
    <strong>Untested ❓</strong>
</summary>

- `App Store`
- `iMessage, FaceTime, iTunes Store`
- `DRM`
- `Sidecar`
- `FireVault 2`

</details>


## Credits

<summary>
    <strong>Thanks to:</strong>
</summary>

- [Apple](https://www.apple.com) - for [macOS](https://www.apple.com/pl/macos/)
- [Acidanthera](https://github.com/acidanthera) team - for OpenCore and necessary kernel extensions
- [Dortania](https://github.com/dortania) team - for great Hackintosh tutorials
- [r/hackintosh](https://www.reddit.com/r/hackintosh) - for troubleshoot advises
- [OpenIntelWireless](https://github.com/OpenIntelWireless) team - for enable of laptop default Intel Wireless Wi-Fi card.

- [VoodooI2C](https://github.com/VoodooI2C) team - for enable of laptop keyboard
- ... and big thanks all the people who works on Hackintosh project :)
