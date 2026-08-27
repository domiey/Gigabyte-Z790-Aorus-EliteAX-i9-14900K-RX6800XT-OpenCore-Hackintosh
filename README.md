# Hackintosh EFI OpenCore 1.0.7 · macOS Tahoe 26.6.2

> **Important:**
>
> All published SMBIOS and system identity values have been removed or anonymized. Generate your own SMBIOS values (Serial Number, MLB, System UUID, and ROM) and add them to `config.plist` before using this EFI.

 ![](https://outline.nexzt.de/api/files.get?sig=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJ1cGxvYWRzL2U2NGUyOTBkLWVkMjgtNDA5Mi1iYmRiLWI3YmI1MTVmNTRlMi8zNDFiOTZiNy01MDdhLTRhYzMtOTI0NS0zOTkwYjBmZWVmZGUvYWJvdXQtdGhpcy1tYWMucG5nIiwidHlwZSI6ImF0dGFjaG1lbnQiLCJpYXQiOjE3ODc4NTQ4NTMsImV4cCI6MTc4ODQ1OTY1M30.SyLzu8qKwj-uBm4BNNPKpf-qPSqB7W-I5adLChPCKZU " =740x446")

<br>

## 🎯 This will be my final Hackintosh — and, for me, the end of an era.

macOS Tahoe is expected to be the last macOS release line to support Intel-based Macs. The goal of this project is to keep this EFI maintained, stable, and compatible with macOS Tahoe updates for as long as reasonably possible.

No upgrade to a future major macOS version is planned. This machine will remain on Tahoe, marking the final chapter of my Hackintosh journey.

<br><br>

## 🖥️ System Information

- **macOS:** Tahoe 26.6.2 · Build `25G83`
- **OpenCore Bootloader:** `1.0.7`
- **SMBIOS:** `iMacPro1,1`
- **BIOS:** `F0a` · 28.04.2026

### BIOS Settings

> 🚧 Detailed BIOS settings will be added later.

<br><br>

## Hardware

| Component | Specification |
|---|---|
| **CPU** | Intel(R) Core i9-14900K · 8 P-Cores · 16 E-Cores · 32 Threads |
| **Mainboard** | Gigabyte Z790 AORUS ELITE AX · Rev. 1.X |
| **Memory** | Corsair Vengeance RGB 48 GB · 2 × 24 GB · DDR5-6000<br>CMH48GX5M2E6000C36 |
| **GPU** | XFX AMD Radeon RX 6800 XT · 16 GB GDDR6 |
| **Audio** | Creative Sound Blaster G3 · USB (primary)<br>Realtek ALC897 · Onboard (secondary) |
| **Ethernet** | Realtek RTL8125 · 2.5 GbE |
| **Wi-Fi / Bluetooth** | Intel(R) Wi-Fi 6E AX211 / Bluetooth 5.3 · Onboard |
| **NVMe / Storage** | WD Black SN770 NVMe · 1 TB |

<br><br>

## Features

### Status

| Feature | Status |
|---|---|
| **Graphics Acceleration / Metal** | ✅ Working |
| **CPU Power Management** | ✅ Working |
| **iMessage / FaceTime** | ✅ Working |
| **DRM / FairPlay** | ✅ Working |
| **USB Port Mapping** | ✅ Working |
| **Wi-Fi (AX211)** | ✅ Working (itlwm / HeliPort) |
| **Bluetooth (AX211)** | ✅ Working (IntelBluetoothFirmware / IntelBTPatcher / BlueToolFixup) |
| **Audio (USB · Sound Blaster G3)** | ✅ Working (native) |
| **Audio (Onboard · ALC897)** | ✅ Working (modified VoodooHDA 4.1) |
| **Dual Boot Windows** | ✅ Working |

### Not working

The onboard Intel® Wi-Fi 6E AX211 does not provide AWDL (Apple Wireless Direct Link) support under macOS. As a result, Continuity features that depend on AWDL are unavailable. A Fenvi T919 (BCM94360CD) was also tested, but currently has no working driver/KEXT support under macOS Tahoe.

| Feature | Status |
|---|---|
| **Handoff / Universal Clipboard** | ⛔ Not available |
| **AirDrop** | ⛔ Not available |
| **Instant Hotspot** | ⛔ Not available |
| **iPhone Mirroring** | ⛔ Not available |
| **Auto Unlock via Apple Watch** | ⛔ Not available |

### Not tested / tests postponed

| Feature | Status | Note |
|---|---|---|
| **Sidecar** | ⏸️ Deferred | Maybe wired. |
| **Continuity Camera** | ⏸️ Deferred | Maybe wired. |
| **Sleep / Wake** | ⏸️ Deferred | Not a priority. Tests will follow. |

### Known Issues & Limitations

- **AppleALC:** macOS Tahoe no longer includes `AppleHDA.kext`, which AppleALC depends on. Onboard ALC897 audio therefore requires the optional VoodooHDA 4.1 method.
- **Broadcom:** Native BCM94360/BCM4360 support ended with macOS Sonoma 14. To keep this configuration root-patch-free and update-friendly, Broadcom Wi-Fi is not used under Tahoe. Consequently, AWDL-based Continuity features such as AirDrop and Handoff are unavailable.

<br><br>

## EFI Components

### Kexts

| Kext | Version | Purpose |
|---|---:|---|
| **Lilu.kext** | 1.7.2 | Patching framework |
| **VirtualSMC.kext** | 1.3.7 | SMC emulation |
| **SMCProcessor.kext** | 1.3.7 | CPU sensors |
| **SMCSuperIO.kext** | 1.3.7 | System sensors |
| **SMCRadeonSensors.kext** | 2.4.0 | AMD GPU sensors |
| **WhateverGreen.kext** | 1.7.0 | GPU support |
| **LucyRTL8125Ethernet.kext** | 1.2.0 | Realtek 2.5 GbE |
| **CpuTopologyRebuild.kext** | 1.1.0 | Hybrid CPU topology |
| **HibernationFixup.kext** | 1.5.4 | Sleep & hibernation fixes |
| **NVMeFix.kext** | 1.1.3 | NVMe power management |
| **RestrictEvents.kext** | 1.1.6 | macOS compatibility |
| **USBPorts.kext** | 1.0 | USB port mapping |
| **macUSPCIO_Smbus.kext** | 1.0.0d1 | SMBus support |
| **itlwm.kext** | 2.3.0 | Intel AX211 Wi-Fi |
| **IntelBluetoothFirmware.kext** | 2.5.1 | Intel Bluetooth firmware |
| **IntelBTPatcher.kext** | 2.5.1 | Intel Bluetooth patches |
| **BlueToolFixup.kext** | 2.7.2 | Bluetooth compatibility |

### ACPI & Compatibility Patches

- SSDT-AWAC — system clock compatibility
- SSDT-EC-USBX-DESKTOP — embedded controller and USB power properties
- SSDT-GPRW with GPRW → XPRW rename — wake handling
- SSDT-PLUG-ALT — CPU power-management attachment
- SSDT-RHUB — USB controller compatibility
- Comet Lake CPUID emulation for the Intel Core i9-14900K
- PlatformSupport.plist board-ID check bypass for macOS Tahoe with iMacPro1,1
- RestrictEvents `cpuname,sbvmm` patches for CPU naming and unsupported SMBIOS compatibility
- `agdpmod=pikera` for the Radeon RX 6800 XT
- `-wegnoigpu` to disable the unused Intel iGPU
- `-ctrsmt` for the hybrid P/E-core topology

<br><br>

## Software Requirements

> ### ⚠️ Important
>
> The software listed below is not included in this repository or EFI and must be downloaded and installed separately.

- [**HeliPort 2.0.0-alpha**](https://github.com/OpenIntelWireless/HeliPort/releases) is required to manage Intel AX211 Wi-Fi connections provided by `itlwm`.

- **Optional onboard audio**

  The onboard Realtek ALC897 was successfully tested with VoodooHDA 4.1 using the [Olarila Tahoe audio method](https://olarila.com/topic/42836-easy-audio-solution-on-hackintosh-on-macos-tahoe/).

  The tested configuration was restricted to the native `HDAS` device to avoid interfering with AMD HDMI/DisplayPort audio. Manual installation and approval of the kernel extension in System Settings are required.

<br><br>

## Credits ❤️

This EFI would not be possible without the work of:

- **Acidanthera** — OpenCore and core Hackintosh components
- **Dortania** — OpenCore documentation and guides
- **OpenIntelWireless** — Intel Wi-Fi and Bluetooth support
- **Olarila** — modified VoodooHDA 4.1
- **Mieze** — Realtek RTL8125 Ethernet support
- **VoodooHDA** — onboard audio support
- **CpuTopologyRebuild** — Intel hybrid CPU support
- **My boys:** Claude, GPT and DeepSeek

**A huge thank you to all developers and contributors in the Hackintosh community.**

<br><br>

## Disclaimer

**This EFI is provided as-is for reference and educational purposes only.**

It is specifically configured and tested for the hardware listed in this repository. Hardware revisions, BIOS versions and individual system configurations may differ.

Use at your own risk. Always create your own SMBIOS and system identity values before using this EFI.

Apple and macOS are trademarks of Apple Inc. This project is not affiliated with or endorsed by Apple Inc.
