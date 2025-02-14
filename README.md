# Hackintosh | Gigabyte z390i Aorus Pro Wifi
- Catalina 10.15.7
- Windows 10
- OC 0.6.6

### Hardware
Type|Item
:----|:----
**CPU** | Intel Core i5-9500k
**CPU Cooler** | Noctua NH-L9i
**Motherboard** | Gigabyte Z390i Aorus Pro Wifi
**Memory** | Crucial Ballistix Sport LT BLS2K16G4D32AESB 3200 MHz
**Storage (macOS)** | WD SN750 500GB
**Storage (Windows)** | Samsung SSD 750 EVO 250GB
**Video Card** | AMD RX580 8GB
**WiFi + Bluetooth** | BCM943602CS with B+M Adapter in rear M2 slot
**Case** | Dan A4
**Power Supply** | Corsair SF Series SF600 80 PLUS Gold SFX
**Monitor** | BenQ PD2700U

### Bios

- Bios version: [F8c](https://www.gigabyte.com/ie/Motherboard/Z390-I-AORUS-PRO-WIFI-rev-10/support#support-dl-bios)
- Bios profile: [Z390IAPW.F8c](https://github.com/smithc42/hackintosh_gigabyte_z390i_dan_a4/raw/master/BIOS/Z390IAPW.F8c)

CFG-Lock must be turned off manually. Follow guide [here](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#what-is-cfg-lock). When using UEFITool, the `CFG Lock` string can be found at the following path:

```
Intel image -> BIOS region -> 4F1C52D3-D824-4D2A-A2F0-EC40C23C5916 -> 9E21FD93-9C72-4C15-8C4B-E77F1DB2D792 -> LzmaCustomDecompressGuid -> Volume image section -> 5C60F367-A505-419A-859E-2A4FF6CA6FE5 -> Setup
```

To disable CFG-Lock and verify its disabled, add the following in `EFI/OC/Tools` folder and config.plist:

- [VerifyMsrE2](https://github.com/acidanthera/OpenCorePkg/releases)
- [Modified GRUB Shell](https://github.com/datasone/grub-mod-setup_var/releases)

Once its disabled we can remove both from our EFI.

CFG Offset:

```
CFG Lock, VarStoreInfo (VarOffset/VarName): 0x5C1
```

Execute the following in Modified GRUB Shell:

`setup_var 0x5C1 0x00`

#### Bios settings

- Settings -> I0 Ports -> Internal Graphics -> Disabled
- Settings -> I0 Ports -> Wi-Fi -> Disabled
- Settings -> I0 Ports -> Above 4G Decoding -> Enabled
- Settings -> I0 Ports -> Wake on LAN Enable -> Disabled
- Settings -> I0 Ports -> USB Configuration -> Legacy USB Support -> Disabled
- Settings -> I0 Ports -> USB Configuration -> XHCI Hand-off -> Enabled
- Settings -> Miscellaneous -> Software Guard Extensions(SGX) -> Disabled
- Settings -> Miscellaneous -> Trusted Computing -> Security Device Support -> Disabled

Note: It's recommended to disable CSM Support, but disabling it prevents OC from booting, so it's enabled for now.

### USB mapping (based on [this](https://github.com/markosmk/Pynty-Hackintosh-Gigabyte-Z390-I-Aorus-Pro-Wifi/blob/master/images/portsusb.jpg) image):

![USB ports](media/usb_ports.jpg)

### Tools

- [ProperTree](https://github.com/corpnewt/ProperTree) (`git clone git@github.com:corpnewt/ProperTree.git`)
- [MountEFI](https://github.com/corpnewt/MountEFI) (`git clone https://github.com/corpnewt/MountEFI`)
- [MaciASL](https://github.com/acidanthera/MaciASL/releases)
- [OpenCore Sanity Checker](https://opencore.slowgeek.com/)
- [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [OpenCore Releases](https://github.com/acidanthera/OpenCorePkg/releases/)

### Misc
[How to update OC versions](https://www.reddit.com/r/hackintosh/comments/gen0fm/on_how_i_updated_my_open_core_desktop_from_057_to/)
