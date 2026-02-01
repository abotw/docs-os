# Asahi Linux

## **1. What is Asahi Linux?**

Asahi Linux is a project aimed at porting Linux to **Apple Silicon Macs** (M1, M1 Pro, M1 Max, M2, etc.). It allows you to run Linux natively on these machines, taking advantage of their hardware while providing a fully functional Linux environment.

**Key points:**

-   Developed by the Asahi team, led by Hector Martin.
-   Focuses on Apple Silicon, which has a custom ARM64 architecture.
-   Supports GUI, terminal, GPU acceleration, and peripherals over time.
-   You can run it either **natively** on Mac hardware or **dual-boot** alongside macOS.

## 2. Supported Hardware

Asahi Linux primarily supports:

-   **Apple Silicon Macs**:
    -   M1 MacBook Air / Pro
    -   M1 Mac Mini
    -   M1 iMac
    -   M1 Mac Studio
    -   M2 Macs (partial support)

Older Intel-based Macs are not the focus since they already run standard Linux well.

**Tip:** Check the official compatibility list before installing: [Asahi Linux Supported Devices](https://asahilinux.org/).

## 3. Installation Options

There are two main ways to try Asahi Linux:

### **Option 1: Native Install (Recommended)**

-   Replaces macOS entirely or sets up a dual-boot.
-   Best for those who want full Linux performance.

### **Option 2: Virtual Machine**

-   Use UTM or Parallels to run Asahi Linux inside macOS.
-   Safer for beginners who don’t want to touch disk partitions.

## 4. Preparing Your Mac

Before installation:

1.  **Backup macOS** using Time Machine.

2.  **Update macOS** to the latest version.

3.  **Free up space**: You’ll need at least 20–30 GB for Asahi Linux.

4.  **Check Apple Silicon model**:

    ```bash
    system_profiler SPHardwareDataType
    ```

5.  **Enable External Boot (optional for dual-boot)**:

    -   Reboot → Hold `Command + R` → Utilities → Startup Security Utility → Allow booting from external media.

## 5. Installing Asahi Linux

### **Step 1: Boot into macOS Terminal**

Open Terminal and run:

```bash
curl https://alx.sh | sh
```

-   This downloads the Asahi Linux installer.
-   The script will guide you through partitioning and installation.

### Step 2: Choose Installation Type

-   **Full Installation:** Replaces macOS with Linux.
-   **Dual Boot (Recommended):** Installs Linux alongside macOS. The installer will automatically resize macOS partitions.

### Step 3: Configure Your System

-   Select your preferred **desktop environment** (currently Asahi Linux supports **GNOME** by default).
-   Set your **username and password**.

### Step 4: Installation Process

-   The installer downloads necessary packages and sets up your Linux root filesystem.
-   This may take **20–60 minutes** depending on your internet speed.

### Step 5: Reboot

-   After installation, reboot your Mac.
-   You will see a boot menu to choose **macOS** or **Asahi Linux** if dual-booting.

## 6. Post-Installation Tips

1.  **Update Your System**

    ```bash
    sudo pacman -Syu
    ```

    Asahi Linux uses **Arch Linux** as its base.

2.  **Install Basic Tools**

    ```bash
    sudo pacman -S git vim htop
    ```

3.  **GPU & Hardware Acceleration**

    -   M1 GPU support is integrated via Asahi Linux kernel.
    -   Some features (e.g., full video acceleration) are still under development.

4.  **Check System Info**

    ```bash
    uname -a          # Kernel info
    lscpu             # CPU info
    free -h           # Memory info
    df -h             # Disk usage
    ```

## 7. Useful Resources

-   **Official Website:** [https://asahilinux.org](https://asahilinux.org/)
-   **Installation Guide:** https://asahilinux.org/install
-   **Community:** [Asahi Linux Discord](https://discord.gg/asahilinux)
-   **Development Blog:** https://asahilinux.org/blog

## 8. Beginner Tips

-   Use **GNOME desktop** for simplicity.
-   Keep macOS installed until you’re confident.
-   Follow the Asahi Linux blog for updates on GPU and peripherals support.
-   Use **pacman** to install software, since it’s Arch-based.

------

**Summary:**

Asahi Linux brings Linux to Apple Silicon Macs with good hardware support and growing software compatibility. Beginners should start with **dual-boot**, use the **official installer**, and gradually explore Linux tools and desktop environments.