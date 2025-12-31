# Firewall

*(with PowerShell examples)*

## 1. What Is Windows Firewall?

**Windows Defender Firewall** is a built-in security feature of Windows that:

-   Controls **which programs or ports can send or receive network traffic**
-   Protects your computer from **unauthorized access**
-   Works automatically in the background, but can be customized

Think of it as a **gatekeeper**:

-   ❌ Blocks unwanted traffic
-   ✅ Allows trusted traffic

------

## 2. Key Firewall Concepts (Very Important)

Before touching commands, understand these basics:

### 2.1 Inbound vs Outbound

| Direction    | Meaning                                  |
| ------------ | ---------------------------------------- |
| **Inbound**  | Traffic coming **into** your computer    |
| **Outbound** | Traffic going **out from** your computer |

👉 Most security risks come from **inbound connections**, so firewall rules often focus there.

------

### 2.2 Ports

A **port** is like a door number for network traffic.

Common examples:

| Port | Service              |
| ---- | -------------------- |
| 22   | SSH                  |
| 80   | HTTP                 |
| 443  | HTTPS                |
| 3389 | Remote Desktop (RDP) |

------

### 2.3 Protocols

Most rules use:

-   **TCP** – reliable, used by HTTP, SSH, RDP
-   **UDP** – faster, used by DNS, video streaming

------

### 2.4 Profiles

Windows Firewall applies rules based on **network location**:

| Profile     | Used When                               |
| ----------- | --------------------------------------- |
| **Domain**  | In a corporate domain                   |
| **Private** | Home or trusted network                 |
| **Public**  | Coffee shop, airport (most restrictive) |

------

## 3. GUI vs PowerShell

### GUI (Beginner-friendly)

-   Control Panel → Windows Defender Firewall
-   Advanced Settings → Inbound / Outbound Rules

### PowerShell (Professional & Scriptable)

-   Faster
-   Repeatable
-   Ideal for servers and automation

👉 This tutorial focuses on **PowerShell**.

------

## 4. Check Firewall Status

Open **PowerShell as Administrator**, then run:

```powershell
Get-NetFirewallProfile
```

You’ll see something like:

```text
Name     : Public
Enabled  : True
```

This means the firewall is **ON** for that profile.

------

## 5. View Existing Firewall Rules

### List all rules

```powershell
Get-NetFirewallRule
```

### Find rules related to a program or port

```powershell
Get-NetFirewallRule | Select DisplayName, Enabled, Direction
```

------

## 6. Create a Firewall Rule (Core Skill)

### 6.1 Allow an Inbound TCP Port (Example: Port 8080)

```powershell
New-NetFirewallRule `
  -DisplayName "Allow TCP 8080" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 8080 `
  -Action Allow
```

✅ This allows inbound traffic on port **8080**.

------

### 6.2 Allow SSH (Port 22)

```powershell
New-NetFirewallRule `
  -DisplayName "Allow SSH" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 22 `
  -Action Allow
```

------

### 6.3 Allow a Program Instead of a Port

Example: allow a specific app:

```powershell
New-NetFirewallRule `
  -DisplayName "Allow My App" `
  -Direction Inbound `
  -Program "C:\MyApp\app.exe" `
  -Action Allow
```

👉 This is **safer** than opening a port globally.

------

## 7. Block Traffic (Yes, You Can Block Too)

### Block inbound traffic on port 3306 (MySQL)

```powershell
New-NetFirewallRule `
  -DisplayName "Block MySQL" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 3306 `
  -Action Block
```

------

## 8. Limit Rules to a Network Profile

Example: only allow SSH on **Private** networks:

```powershell
New-NetFirewallRule `
  -DisplayName "Allow SSH Private" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 22 `
  -Profile Private `
  -Action Allow
```

🚫 SSH will NOT be accessible on Public networks.

------

## 9. Enable, Disable, or Remove Rules

### Disable a rule

```powershell
Disable-NetFirewallRule -DisplayName "Allow SSH"
```

### Enable it again

```powershell
Enable-NetFirewallRule -DisplayName "Allow SSH"
```

### Delete a rule

```powershell
Remove-NetFirewallRule -DisplayName "Allow SSH"
```

------

## 10. Common Beginner Mistakes

❌ Opening ports unnecessarily
❌ Allowing everything on **Public** profile
❌ Forgetting to run PowerShell as **Administrator**
❌ Using `Any` protocol when TCP/UDP is enough

------

## 11. Recommended Beginner Rule Pattern

A safe default template:

```powershell
New-NetFirewallRule `
  -DisplayName "Allow Service Name" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort <PORT> `
  -Profile Private `
  -Action Allow
```

------

## 12. When Should You Use PowerShell Firewall Rules?

-   Setting up **development servers**
-   Enabling **SSH / RDP / HTTP**
-   Managing **Windows Server**
-   Automating security via scripts

------

## 13. Summary

-   Windows Firewall controls **network access**
-   `New-NetFirewallRule` is the **core command**
-   Always:
    -   Know **which port**
    -   Know **which direction**
    -   Limit to **Private** when possible