# 🖨️ Essae Label Weighing Driver v2.0

This repository contains the complete **user-space driver**, **GUI**, and **Debian installation packages** (`.deb`) for **Essae Label Weighing Scale with Label Printer**. This version supports both **AMD64 (PC/Desktop)** and **ARM64 (RK3568/ARM boards)** platforms.

---

## 📂 Contents

- `essae-label-driver-amd64.deb` – Debian package for 64-bit PC (Ubuntu 20.04+)
- `essae-label-driver-arm64.deb` – Debian package for ARM64-based boards
- `Essae_WSLPR_client_v2.0.py` – Python GUI client for label design and print
- `Essae_WSLPR_server_v2.0` – C binary service to communicate with printer
- `essae_logo.png` – Icon for GUI launcher
- Systemd service for auto-start
- `.desktop` entry for easy desktop launch

---

## ✅ Supported Platforms

| Platform         | Architecture | Status      |
|------------------|--------------|-------------|
| Ubuntu 20.04+    | amd64        | ✅ Tested   |
| Ubuntu 20.04+    | arm64        | ✅ Tested   |

---

## 🔧 Dependencies

All required packages are handled during `.deb` installation:
- `python3`
- `python3-pyqt5`
- `libsqlite3-0`
- `libjson-c5`

---

## 💾 Installation (Recommended)

### 🔹 For **AMD64** (PC/Ubuntu Desktop):

```bash
$ wget https://github.com/venkatesh4009/essae-label-weighing-driver/raw/label-weighing-driver-v2.0/essae-label-driver-amd64.deb
$ sudo apt install ./essae-label-driver-amd64.deb
```

### 🔹 For ARM64 (RK3568 or similar):
```bash
wget https://github.com/venkatesh4009/essae-label-weighing-driver/raw/label-weighing-driver-v2.0/essae-label-driver-arm64.deb
sudo apt install ./essae-label-driver-arm64.deb
```

### 🚀 After Installation
```bash
✅ GUI shortcut available in Applications menu
→ Essae Label Printer GUI

✅ Service automatically starts at boot
→ essae-label-driver.service (systemd)
```

### 🗂️ Files are installed at:

```bash
$ /usr/local/bin/Essae_WSLPR_client_v2.0.py
$ /usr/local/bin/Essae_WSLPR_server_v2.0
$ /usr/share/applications/EssaeLabelClient.desktop
$ /usr/share/pixmaps/essae_logo.png
```

### ▶️ Enable/Disable Driver Manually
```bash
$ sudo systemctl enable essae-label-driver
$ sudo systemctl start essae-label-driver
$ sudo systemctl stop essae-label-driver
$ sudo systemctl status essae-label-driver
$ sudo systemctl disable essae-label-driver

```
### 🔄 Uninstallation
To remove the driver completely:
```bash
$ sudo apt remove essae-label-driver
```

---

👨‍💼 Author

Developed by:

Venkatesh M – venkatesh.muninagaraju@essae.com

Embedded System Engineer

Essae Label Driver - Version 2.0

---
