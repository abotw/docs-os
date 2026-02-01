---
title: "OpenWrt: Compilation"
icon: simple/openwrt
status: done
---

## 1. What Is OpenWrt Compilation?

**OpenWrt compilation** means:

-   Downloading **OpenWrt source code**
-   Selecting your router model and features
-   Building (compiling) a custom firmware image
-   Flashing it onto your router

Why compile OpenWrt yourself?

-   Add or remove packages (e.g. LuCI apps, VPN tools)
-   Optimize for your hardware
-   Fix missing packages in official images
-   Learn how OpenWrt really works (huge bonus)

## 2. What You Need Before Starting

### Hardware

-   A **Linux machine** (Ubuntu 20.04 / 22.04 recommended)
-   At least:
    -   **4 GB RAM** (8 GB+ recommended)
    -   **20–30 GB disk space**
-   Internet connection

>   macOS and WSL can work, but **native Linux is strongly recommended** for beginners.

## 3. Install Build Dependencies

On **Ubuntu**:

```bash
sudo apt update
sudo apt install -y \
  build-essential clang flex bison g++ gawk gcc-multilib \
  gettext git libncurses-dev libssl-dev python3-distutils \
  rsync unzip zlib1g-dev file wget
```

⚠️ Missing dependencies are the **#1 reason compilation fails**.

## 4. Download OpenWrt Source Code

Go to a working directory:

```bash
mkdir -p ~/openwrt
cd ~/openwrt
```

Clone the official repository:

```bash
git clone https://github.com/openwrt/openwrt.git
cd openwrt
```

Checkout a **stable release** (recommended for beginners):

```bash
git checkout openwrt-23.05
```

## 5. Update and Install Feeds

Feeds are **package sources** (LuCI, network tools, etc.).

```bash
./scripts/feeds update -a
./scripts/feeds install -a
```

If you see warnings here, they’re usually safe unless they mention **missing core packages**.

## 6. Configure the Build (menuconfig)

Run:

```bash
make menuconfig
```

This is the **most important step**.

### Key Sections Explained

#### 6.1 Target System

Choose your CPU architecture, for example:

-   MediaTek
-   Qualcomm Atheros
-   x86

#### 6.2 Subtarget

Specific SoC family (e.g. MT7621, IPQ807x)

#### 6.3 Target Profile

Your **exact router model**

>   If your model is listed, always select it.

### 6.4 LuCI (Web UI)

Enable LuCI:

```
LuCI  --->
  Collections  --->
    <*> luci
```

Optional but recommended:

-   `luci-ssl` (HTTPS)
-   `luci-app-firewall`
-   `luci-app-opkg`

### 6.5 Common Useful Packages

Examples:

```
Network  --->
  <*> wget
  <*> curl

Utilities  --->
  <*> htop
```

💡 Don’t select too many packages at first.

### Save and Exit

-   Press **Save**
-   Exit `menuconfig`

Your config is saved to `.config`.

## 7. Start Compilation

### First Build (slow!)

```bash
make -j$(nproc)
```

-   First build can take **30–120 minutes**
-   CPU will be at 100% — that’s normal

If it fails:

```bash
make -j1 V=s
```

This gives **detailed error logs**.

## 8. Where Is the Firmware?

After success:

```bash
ls bin/targets/
```

Example path:

```text
bin/targets/mediatek/mt7621/
```

You’ll find:

-   `*-factory.bin` → Flash from **vendor firmware**
-   `*-sysupgrade.bin` → Upgrade from **existing OpenWrt**

## 9. Flashing the Firmware

### From Stock Firmware

-   Use router’s web UI
-   Upload `factory.bin`

### From OpenWrt

```bash
sysupgrade your-firmware-sysupgrade.bin
```

⚠️ Double-check:

-   Correct **router model**
-   Correct **target**
    Wrong firmware = soft brick.

## 10. Cleaning and Rebuilding

### Clean build files (safe)

```bash
make clean
```

### Full reset (slow)

```bash
make dirclean
```

### Reconfigure

```bash
make menuconfig
make -j$(nproc)
```

## 11. Common Beginner Problems

### ❌ Missing dependency

Solution:

```bash
sudo apt install <missing-package>
```

### ❌ Feeds warning

Usually OK unless:

-   `host dependency does not exist`
-   `package not found`

### ❌ Out of memory

-   Reduce jobs:

```bash
make -j2
```

-   Add swap

## 12. Recommended Learning Path

1.  Compile **official OpenWrt** with LuCI only
2.  Add small packages (htop, curl)
3.  Add VPN / proxy tools
4.  Learn to:
    -   Create custom packages
    -   Modify `.config`
    -   Patch source code

## 13. Useful Commands Cheat Sheet

```bash
make menuconfig      # Configure
make -j$(nproc)      # Build
make clean           # Clean build
./scripts/feeds update -a
./scripts/feeds install -a
```

