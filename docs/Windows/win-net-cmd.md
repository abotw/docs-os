# Windows Common Network Commands

## 1. How to Open the Terminal

-   **Command Prompt**: `Win + R` → type `cmd`
-   **PowerShell**: `Win + X` → **Windows PowerShell**

>   💡 Tip: Many modern network commands work better in **PowerShell**.

------

## 2. `ipconfig` — View Network Configuration

### Purpose

Shows your IP address, gateway, DNS, and network adapter status.

### Common Usage

```bat
ipconfig
```

### Useful Options

```bat
ipconfig /all        # Detailed information
ipconfig /release    # Release IP address
ipconfig /renew      # Renew IP address
ipconfig /flushdns   # Clear DNS cache
```

### When to Use

-   Cannot access the internet
-   Need to check IP / gateway / DNS

------

## 3. `ping` — Test Network Connectivity

### Purpose

Tests whether another host is reachable.

### Basic Usage

```bat
ping google.com
ping 8.8.8.8
```

### Useful Options

```bat
ping -n 5 google.com   # Send 5 packets
ping -t google.com    # Ping continuously
```

### Result Meaning

-   **Reply from …** → network OK
-   **Request timed out** → packet loss or unreachable host

------

## 4. `tracert` — Trace Network Path

### Purpose

Shows the route packets take to reach a destination.

### Usage

```bat
tracert google.com
```

### When to Use

-   Network is slow
-   Want to see where connection fails

------

## 5. `netstat` — View Network Connections

### Purpose

Displays active connections, listening ports, and statistics.

### Common Usage

```bat
netstat -ano
```

### Useful Options

```bat
netstat -an     # All connections
netstat -ano    # Include process ID (PID)
netstat -r      # Routing table
```

### Practical Example

```bat
netstat -ano | findstr 80
```

Shows processes using port 80.

------

## 6. `nslookup` — DNS Query Tool

### Purpose

Checks DNS resolution.

### Basic Usage

```bat
nslookup google.com
```

### Advanced Example

```bat
nslookup
> server 8.8.8.8
> google.com
```

### When to Use

-   Website cannot be resolved
-   DNS issues

------

## 7. `arp` — View ARP Cache

### Purpose

Shows IP-to-MAC address mappings.

### Usage

```bat
arp -a
```

### When to Use

-   LAN issues
-   Diagnose IP conflicts

------

## 8. `route` — View or Modify Routing Table

### View Routes

```bat
route print
```

### Add a Route (Admin Required)

```bat
route add 10.0.0.0 mask 255.255.255.0 192.168.1.1
```

### When to Use

-   Multi-network environments
-   VPN / advanced routing

------

## 9. `net use` — Manage Network Drives

### Map a Network Drive

```bat
net use Z: \\192.168.1.10\share
```

### Disconnect

```bat
net use Z: /delete
```

------

## 10. `netsh` — Advanced Network Configuration

### Purpose

Powerful tool to manage network interfaces, firewall, and IP settings.

### Common Example

```bat
netsh interface ip show config
```

### Wi-Fi Info

```bat
netsh wlan show profiles
```

>   ⚠️ `netsh` is powerful — beginners should use read-only commands first.

------

## 11. `telnet` / `Test-NetConnection` — Port Testing

### PowerShell (Recommended)

```powershell
Test-NetConnection google.com -Port 443
```

### Legacy (`telnet`)

```bat
telnet google.com 80
```

------

## 12. Quick Troubleshooting Flow (Beginner)

1.  Check IP:

```bat
ipconfig
```

1.  Test local gateway:

```bat
ping 192.168.1.1
```

1.  Test internet:

```bat
ping 8.8.8.8
```

1.  Test DNS:

```bat
ping google.com
```

1.  Trace route:

```bat
tracert google.com
```

------

## 13. Summary Table

| Command              | Purpose             |
| -------------------- | ------------------- |
| `ipconfig`           | IP & adapter info   |
| `ping`               | Connectivity test   |
| `tracert`            | Path tracing        |
| `netstat`            | Connections & ports |
| `nslookup`           | DNS diagnosis       |
| `arp`                | MAC/IP mapping      |
| `route`              | Routing table       |
| `net use`            | Network drives      |
| `netsh`              | Advanced config     |
| `Test-NetConnection` | Port testing        |

------

## 14. Final Advice for Beginners

-   Start with **`ipconfig` + `ping`**
-   Prefer **PowerShell** for modern Windows
-   Avoid modifying routes or netsh settings unless you understand them

