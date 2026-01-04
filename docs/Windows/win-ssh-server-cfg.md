# Configure SSH Server on Windows 

## 1. What is SSH?

**SSH (Secure Shell)** is a secure protocol that lets you:

-   Log in to another computer remotely
-   Execute commands on a remote machine
-   Transfer files securely (via `scp` / `sftp`)

Windows 10 (1809+) and Windows 11 include **OpenSSH Server** officially, so no third-party software is required.

------

## 2. Check Your Windows Version

This guide applies to:

-   Windows 10 **1809 or later**
-   Windows 11

Check version:

```
Win + R → winver
```

------

## 3. Install OpenSSH Server

### Method 1: Using Windows Settings (Recommended)

1.  Open **Settings**
2.  Go to **Apps → Optional features**
3.  Click **View features** (or **Add a feature**)
4.  Find **OpenSSH Server**
5.  Click **Install**

Wait until installation completes.

------

### Method 2: Using PowerShell (Admin)

Open **PowerShell as Administrator**:

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

Check installation:

```powershell
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

------

## 4. Start and Enable the SSH Service

### Start SSH Server

```powershell
Start-Service sshd
```

### Set SSH to Start Automatically

```powershell
Set-Service -Name sshd -StartupType Automatic
```

Check status:

```powershell
Get-Service sshd
```

Status should be **Running**.

------

## 5. Configure Windows Firewall (Very Important)

Usually Windows does this automatically, but check it.

### Verify Firewall Rule

```powershell
Get-NetFirewallRule -Name *ssh*
```

### Manually Add Rule (If Needed)

```powershell
New-NetFirewallRule `
  -Name sshd `
  -DisplayName "OpenSSH Server" `
  -Enabled True `
  -Direction Inbound `
  -Protocol TCP `
  -Action Allow `
  -LocalPort 22
```

>   Default SSH port is **22**

------

## 6. Test SSH Server Locally

Open **Command Prompt** or **PowerShell**:

```bash
ssh username@localhost
```

Example:

```bash
ssh matt@localhost
```

If you see:

```
Are you sure you want to continue connecting (yes/no)?
```

→ SSH server is working 🎉

------

## 7. Connect from Another Computer

### Find Windows IP Address

```powershell
ipconfig
```

Look for:

```
IPv4 Address: 192.168.1.100
```

### Connect from macOS / Linux / Another Windows PC

```bash
ssh username@192.168.1.100
```

------

## 8. Default SSH Configuration File

Location:

```
C:\ProgramData\ssh\sshd_config
```

Open as Administrator:

```powershell
notepad C:\ProgramData\ssh\sshd_config
```

Common options:

```text
Port 22
PasswordAuthentication yes
PubkeyAuthentication yes
```

After changes, restart SSH:

```powershell
Restart-Service sshd
```

------

## 9. (Recommended) Enable Key-Based Login

### Generate SSH Key (Client Side)

```bash
ssh-keygen
```

### Copy Public Key to Windows Server

```bash
scp ~/.ssh/id_rsa.pub username@windows_ip:C:\Users\username\.ssh\authorized_keys
```

Ensure permissions:

-   Folder: `.ssh`
-   File: `authorized_keys`

------

## 10. Common Problems & Fixes

### ❌ Connection Refused

-   SSH service not running
-   Firewall blocked port 22

### ❌ Permission Denied

-   Wrong username/password
-   Incorrect key permissions

### ❌ Port 22 Blocked

Change port in `sshd_config`:

```text
Port 2222
```

Then restart SSH.

------

## 11. Useful SSH Commands (Beginner)

```bash
ssh user@host            # login
exit                     # logout
scp file user@host:/path # copy file
sftp user@host           # file transfer
```

------

## 12. When Should You Use Windows SSH Server?

✔ Remote development
✔ Remote system management
✔ File transfer
✔ Connecting from macOS/Linux to Windows

------

## 13. Summary

| Step | Action                  |
| ---- | ----------------------- |
| 1    | Install OpenSSH Server  |
| 2    | Start & enable sshd     |
| 3    | Open firewall port      |
| 4    | Test locally            |
| 5    | Connect remotely        |
| 6    | (Optional) Use SSH keys |

