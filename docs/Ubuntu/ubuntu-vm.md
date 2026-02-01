# Ubuntu: VM

>   Setting up and configuraing an Ubuntu VM on VMware Workstation in Windows.

## Step 1: Download the Required Software

1.  **VMware Workstation Player (Free for personal use)**
    -   Go to [VMware Workstation Player Download](https://www.vmware.com/products/workstation-player.html).
    -   Choose **Windows** version and download.
    -   Install it on your Windows PC.
2.  **Ubuntu ISO**
    -   Go to [Ubuntu Downloads](https://ubuntu.com/download/desktop).
    -   Download the **latest LTS version** (for beginners, 24.04 LTS is recommended).

## Step 2: Create a New Virtual Machine

1.  Open **VMware Workstation Player**.
2.  Click **“Create a New Virtual Machine”**.
3.  **Select Installation Media**:
    -   Choose **Installer disc image file (ISO)**.
    -   Browse to the Ubuntu ISO you downloaded.
4.  Click **Next**.

## Step 3: Name the VM and Set Location

1.  Give your VM a **name** (e.g., `UbuntuVM`).
2.  Choose a **location** on your PC where the VM files will be stored.
    -   Make sure there’s enough space (at least 20 GB recommended).
3.  Click **Next**.

## Step 4: Specify Disk Capacity

1.  Set **Maximum Disk Size**:
    -   20–50 GB is usually enough for a beginner VM.
2.  Choose **Store virtual disk as a single file** (simpler) or **split into multiple files**.
3.  Click **Next**.

## Step 5: Customize Hardware (Optional but Recommended)

1.  Click **Customize Hardware**.
2.  Adjust settings based on your PC specs:
    -   **Memory (RAM)**: 2–4 GB minimum.
    -   **Processors**: 2 cores if possible.
    -   **Network Adapter**: NAT is default and works for most cases.
    -   **USB Controller**: Enable if needed.
    -   **CD/DVD**: Make sure it points to the ISO.
3.  Click **Close**, then **Finish**.

## Step 6: Start the VM and Install Ubuntu

1.  Select your VM and click **Play virtual machine**.
2.  The Ubuntu installer will boot.
3.  **Follow the Ubuntu installation steps**:
    -   Choose **Language** → English.
    -   Choose **Normal Installation** (includes browser, utilities, etc.).
    -   Select **Install third-party software** if you want multimedia codecs.
    -   **Disk Setup**: Use default **Erase disk and install Ubuntu** (VM disk is isolated, safe).
    -   Set **username, password, and computer name**.
    -   Continue until installation finishes.
4.  Once installation is complete, **restart the VM** when prompted.

## Step 7: Post-Installation Configurations

### 1. VMware Tools (Optional but Recommended)

-   VMware Tools improves performance, screen resolution, and shared clipboard.

-   In VMware Player:

    1.  Go to **Player → Manage → Install VMware Tools**.

    2.  In Ubuntu, a **virtual CD** will appear.

    3.  Open it, extract the contents, and run the installer:

        ```bash
        sudo ./vmware-install.pl
        ```

    4.  Follow the default options.

### 2. Update Ubuntu

-   Open Terminal (`Ctrl+Alt+T`) and run:

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

### 3. Adjust Screen Resolution

-   After installing VMware Tools, you can **resize the VM window** and Ubuntu will auto-adjust.

## Step 8: Network Setup (Optional)

-   By default, VMware uses **NAT**, which allows internet access.
-   If you want the VM to appear as a separate device on your network:
    -   Go to **VM Settings → Network Adapter → Bridged**.

## Step 9: Snapshots (Optional but Useful)

-   Snapshots let you save the current VM state.
-   Use them before making risky changes:
    -   **Player → Manage → Snapshot → Take Snapshot**.
    -   Later you can **restore** to this point.

## Tips for Beginners

1.  **Don’t allocate too much RAM**; leave some for Windows host.
2.  **Use NAT networking** initially—it’s simpler.
3.  **VM snapshots** are lifesavers if you make mistakes.
4.  **Shared folders**: You can enable host-guest file sharing via VMware Tools.
5.  **Keyboard shortcuts**:
    -   `Ctrl+Alt` releases mouse/keyboard from VM.
    -   `Ctrl+Alt+T` opens terminal in Ubuntu.

------

Once done, you have a fully functional **Ubuntu VM running inside Windows**. From here, you can install software, practice Linux commands, or even set up a server environment.

