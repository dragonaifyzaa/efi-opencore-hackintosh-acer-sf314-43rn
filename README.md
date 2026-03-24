<div align="center">

# 🍎 Hackintosh EFI — Acer Swift 3 SF314-43RN

**macOS Ventura running on AMD Ryzen 5 5500U**  
*Because why buy a Mac when you can build one?* 🛠️

[![macOS](https://img.shields.io/badge/macOS-Ventura_13.x-brightgreen?style=for-the-badge&logo=apple&logoColor=white)](https://www.apple.com/macos/ventura/)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.8.8-blue?style=for-the-badge)](https://github.com/acidanthera/OpenCorePkg)
[![Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)]()
[![AMD](https://img.shields.io/badge/CPU-AMD_Ryzen_5_5500U-ED1C24?style=for-the-badge&logo=amd&logoColor=white)]()

---

<img src="https://raw.githubusercontent.com/acidanthera/OpenCorePkg/master/Docs/Images/logo.png" width="200"/>

</div>

---

## 📋 Specs / Spesifikasi

| Component | Detail |
|-----------|--------|
| **Laptop** | Acer Swift 3 SF314-43RN |
| **CPU** | AMD Ryzen 5 5500U (Lucienne) |
| **iGPU** | AMD Radeon Vega 7 |
| **RAM** | 8GB DDR4 |
| **Storage** | Kingston OM3PDP3 NVMe SSD |
| **Audio** | Realtek ALC256 |
| **WiFi** | TP-Link USB Nano *(internal not supported)* |
| **Bootloader** | OpenCore 0.8.8 |
| **macOS** | Ventura 13.x |

---

## ✅ What Works / Yang Berfungsi

| Feature | Status | Notes |
|---------|--------|-------|
| 🔊 Audio (Speaker + Headphone) | ✅ Working | Layout-id 69 |
| 🔆 Brightness Control | ✅ Working | Via F3/F4 keys |
| 🔋 Battery | ✅ Working | Auto-cut charging works |
| 😴 Sleep / Wake | ✅ Working | Lid open/close normal |
| ⌨️ Keyboard | ✅ Working | |
| 🖱️ Trackpad | ✅ Working | Via `-vi2c-force-polling` |
| 💾 NVMe SSD | ✅ Working | |
| 🖥️ Display | ✅ Working | |
| 🌐 WiFi | ⚠️ Partial | TP-Link USB Nano only |
| 📶 Bluetooth | ❌ Not Working | |
| 🎮 GPU Acceleration | ⚠️ Partial | Metal supported, 512MB VRAM |

---

## ❌ What Doesn't Work / Yang Tidak Berfungsi

- **Internal WiFi** — Broadcom card not supported on macOS
- **Bluetooth** — Not working
- **AirDrop / Handoff / Continuity** — Requires native Apple WiFi/BT
- **HDMI Audio** — Not tested

---

## 🔧 Key Fixes / Solusi Penting

### 🔊 Audio Fix
Audio internal tidak terdeteksi secara default. Fix menggunakan:
- **PCI Path:** `PciRoot(0x1)/Pci(0x8,0x1)/Pci(0x0,0x6)`
- **Layout-ID:** `69` → `<45000000>` (Data type)

> ⚠️ Pastikan Data Type adalah **Data**, bukan Number!

### 🖱️ Trackpad Fix
Tambahkan `-vi2c-force-polling` di boot-args agar trackpad I2C terdeteksi.

### 🖥️ GPU Stability Fix
Tambahkan `agdpmod=pikera` di boot-args untuk mencegah blackscreen/glitch pada AMD iGPU.

---

## 🚀 Boot Arguments / Boot-Args

```
-v debug=0x100 keepsyms=1 -vi2c-force-polling ipc_control_port_options=0 agdpmod=pikera
```

| Argument | Fungsi |
|----------|--------|
| `-v` | Verbose mode (debug booting) |
| `debug=0x100` | Prevent auto-restart on kernel panic |
| `keepsyms=1` | Show symbols on kernel panic |
| `-vi2c-force-polling` | Fix trackpad I2C |
| `ipc_control_port_options=0` | Fix app crashes on Ventura |
| `agdpmod=pikera` | Fix AMD GPU blackscreen/glitch |

---

## 📦 Kexts Used

| Kext | Purpose |
|------|---------|
| `Lilu.kext` | Core patching engine |
| `AppleALC.kext` | Audio fix |
| `VirtualSMC.kext` | SMC emulation |
| `SMCBatteryManager.kext` | Battery status |
| `AMDRyzenCPUPowerManagement.kext` | CPU power management |
| `NootedRed.kext` | AMD iGPU support |
| `VoodooI2C.kext` | Trackpad support |
| `VoodooI2CHID.kext` | Trackpad HID |
| `RestrictEvents.kext` | Various patches |

---

## ⚠️ Important Notes / Catatan Penting

> **EN:** This EFI is specifically configured for Acer Swift 3 SF314-43RN. Using it on different hardware may cause issues. Always backup your original EFI before replacing.

> **ID:** EFI ini dikonfigurasi khusus untuk Acer Swift 3 SF314-43RN. Penggunaan pada hardware berbeda bisa menyebabkan masalah. Selalu backup EFI original sebelum mengganti.

---

## 📖 Installation / Instalasi

**EN:**
1. Format USB with GUID Partition Map + FAT32
2. Create macOS Ventura installer using `createinstallmedia`
3. Copy this EFI folder to the EFI partition of your USB
4. Boot and follow macOS installation steps
5. After install, copy EFI to your system drive's EFI partition

**ID:**
1. Format USB dengan GUID Partition Map + FAT32
2. Buat installer macOS Ventura menggunakan `createinstallmedia`
3. Copy folder EFI ini ke partisi EFI USB
4. Boot dan ikuti langkah instalasi macOS
5. Setelah install, copy EFI ke partisi EFI drive sistem

---

## 🙏 Credits

- [Acidanthera](https://github.com/acidanthera) — OpenCore, Lilu, AppleALC, VirtualSMC
- [NootInc](https://github.com/NootInc) — NootedRed (AMD iGPU)
- [AMD-OSX Community](https://amd-osx.com) — AMD Hackintosh support
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) — OpenCore Install Guide
- [Ben Baker](https://github.com/benbaker76) — Hackintool

---

<div align="center">

**Made with ❤️ and a lot of reboots**  
*If this helped you, leave a ⭐ !*

</div>
