# Raspberry Pi OS

## 1. What Is Raspberry Pi OS?

**Raspberry Pi OS** (formerly called *Raspbian*) is the **official operating system** for Raspberry Pi computers.

It is:

-   **Free and open-source**
-   **Based on Debian Linux**
-   **Optimized specifically for Raspberry Pi hardware**
-   Designed for **learning, programming, and everyday use**

If you are new to Raspberry Pi or Linux, **Raspberry Pi OS is the best starting choice**.

## 2. Why Choose Raspberry Pi OS?

For beginners, Raspberry Pi OS is popular because:

-   ✅ Officially supported by the Raspberry Pi Foundation
-   ✅ Large community and tutorials
-   ✅ Lightweight and fast on Pi hardware
-   ✅ Comes with useful preinstalled tools
-   ✅ Very stable

Typical use cases:

-   Learning Linux basics
-   Programming (Python, C/C++)
-   Networking and servers
-   Robotics and electronics
-   Home projects (NAS, Pi-hole, smart home)

## 3. Raspberry Pi OS Editions

Raspberry Pi OS comes in **three main versions**:

### 1️⃣ Raspberry Pi OS (64-bit / 32-bit) with Desktop

-   Graphical desktop (similar to Windows/macOS)
-   Best for beginners
-   Recommended if you use a monitor

### 2️⃣ Raspberry Pi OS Lite

-   No graphical interface (command line only)
-   Uses less memory
-   Ideal for servers and headless setups

### 3️⃣ Raspberry Pi OS with Desktop and Recommended Software

-   Desktop + many extra apps
-   Good for education, but larger size

👉 **Beginner recommendation:**
**Raspberry Pi OS (64-bit) with Desktop**

## 4. Basic System Requirements

You will need:

-   Raspberry Pi (Pi 3, 4, or 5 recommended)
-   microSD card (16 GB or larger)
-   Power supply
-   (Optional) Monitor, keyboard, mouse
-   (Optional) Network cable or Wi-Fi

## 5. Installing Raspberry Pi OS

### Step 1: Download Raspberry Pi Imager

-   Available for Windows, macOS, and Linux
-   Official tool for flashing OS to SD card

### Step 2: Flash the OS

1.  Insert microSD card into your computer
2.  Open **Raspberry Pi Imager**
3.  Choose:
    -   **Device** → your Raspberry Pi model
    -   **OS** → Raspberry Pi OS
    -   **Storage** → your SD card
4.  Click **Write**

### Step 3: First Boot

-   Insert the SD card into the Raspberry Pi
-   Power it on
-   Follow the on-screen setup (language, Wi-Fi, password)

## 6. The Raspberry Pi OS Desktop

The desktop environment is called **PIXEL**.

Main components:

-   **Top panel**: menus, network, sound, clock
-   **Desktop icons**: Home folder, Trash
-   **File Manager**: manage files like Finder / Explorer
-   **Terminal**: command-line interface

You can use the system fully with the mouse, but **learning the terminal is strongly recommended**.

## 7. Understanding the File System

Raspberry Pi OS uses a Linux file structure.

Important directories:

-   `/home/pi` or `/home/username` → your personal files
-   `/etc` → system configuration
-   `/usr` → installed software
-   `/var` → logs and variable data

Your daily work should stay inside:

```text
/home/yourname
```

## 8. Using the Terminal (Very Important)

Open **Terminal** from the menu.

Common beginner commands:

```bash
pwd        # show current directory
ls         # list files
cd folder  # change directory
mkdir test # create folder
rm file    # delete file
```

Update the system:

```bash
sudo apt update
sudo apt upgrade
```

Install software:

```bash
sudo apt install vim
```

## 9. Networking Basics

### Check IP address

```bash
ip a
```

### Test network

```bash
ping google.com
```

### Enable SSH (remote login)

```bash
sudo raspi-config
```

-   Interface Options → SSH → Enable

Then connect from another computer:

```bash
ssh username@pi_ip_address
```

## 10. Programming on Raspberry Pi OS

Raspberry Pi OS is great for learning programming.

Preinstalled or easily available:

-   **Python** (default language)
-   **C / C++**
-   **Scratch**
-   **Node.js**

Example Python test:

```bash
python3
print("Hello Raspberry Pi")
```

## 11. Updating and Maintaining the System

Regular maintenance:

```bash
sudo apt update
sudo apt upgrade
sudo reboot
```

Check disk usage:

```bash
df -h
```

## 12. Common Beginner Mistakes

-   ❌ Removing system files with `sudo rm`
-   ❌ Forgetting passwords
-   ❌ Using random commands from the internet
-   ❌ Powering off without shutdown

Correct shutdown:

```bash
sudo shutdown now
```

## 13. When to Use Raspberry Pi OS Lite

Choose **Lite** if:

-   No monitor is attached
-   You only use SSH
-   You want better performance
-   You build servers or services

## 14. Raspberry Pi OS vs Other Systems

| System          | Best For            |
| --------------- | ------------------- |
| Raspberry Pi OS | Beginners, learning |
| Ubuntu Server   | Cloud, servers      |
| Ubuntu Desktop  | Familiar UI         |
| OpenWrt         | Routers, networking |
| RetroPie        | Gaming              |

## 15. Next Steps After Installation

Good things to learn next:

-   Linux permissions (`chmod`, `chown`)
-   SSH and SCP
-   System services (`systemctl`)
-   Networking basics
-   Shell scripting

## Summary

Raspberry Pi OS is:

-   Beginner-friendly
-   Powerful enough for real projects
-   A great way to learn Linux and computing

