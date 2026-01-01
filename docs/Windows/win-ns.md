# netsh

## 1. What is `netsh`?

`netsh` (**Network Shell**) is a built-in **Windows command-line tool** used to **view, configure, and troubleshoot network settings**.

You can use `netsh` to:

-   Configure IP addresses, DNS, gateways
-   Manage network interfaces
-   Set up **port forwarding (portproxy)**
-   View routing tables
-   Configure firewall and advanced networking features

>   Think of `netsh` as **a command-line control panel for networking**.

------

## 2. How `netsh` Works (Contexts)

`netsh` is **context-based**.

Basic structure:

```cmd
netsh <context> <command> <parameters>
```

Examples:

```cmd
netsh interface ip show config
netsh interface portproxy show all
```

Common contexts:

-   `interface` → Network interfaces (IP, DNS, ports)
-   `interface ip` → IPv4 settings
-   `interface ipv6` → IPv6 settings
-   `interface portproxy` → Port forwarding
-   `advfirewall` → Windows Firewall (older alternative to PowerShell)

------

## 3. Entering Interactive Mode (Optional)

You can run `netsh` in **interactive mode**:

```cmd
netsh
```

Prompt changes to:

```cmd
netsh>
```

Then:

```cmd
netsh> interface
netsh interface> ip
netsh interface ip> show config
```

To exit:

```cmd
exit
```

>   Beginners usually prefer **one-line commands**, which we’ll use below.

------

## 4. `netsh interface` – Network Interfaces

### 4.1 List All Network Interfaces

```cmd
netsh interface show interface
```

Output shows:

-   Interface name (e.g. `Ethernet`, `Wi-Fi`)
-   Status (Connected / Disconnected)
-   Type

------

### 4.2 Show IP Configuration

```cmd
netsh interface ip show config
```

Equivalent to `ipconfig /all`, but more detailed and script-friendly.

------

### 4.3 Set a Static IP Address

```cmd
netsh interface ip set address name="Ethernet" static 192.168.1.100 255.255.255.0 192.168.1.1
```

Parameters:

-   `name="Ethernet"` → Interface name
-   `static` → Static IP mode
-   `192.168.1.100` → IP address
-   `255.255.255.0` → Subnet mask
-   `192.168.1.1` → Default gateway

------

### 4.4 Switch Back to DHCP

```cmd
netsh interface ip set address name="Ethernet" dhcp
```

Set DNS to automatic:

```cmd
netsh interface ip set dns name="Ethernet" dhcp
```

------

### 4.5 Set DNS Manually

Primary DNS:

```cmd
netsh interface ip set dns name="Ethernet" static 8.8.8.8
```

Secondary DNS:

```cmd
netsh interface ip add dns name="Ethernet" 8.8.4.4 index=2
```

------

## 5. `netsh interface portproxy` – Port Forwarding (Very Important)

### 5.1 What Is `portproxy`?

`portproxy` allows Windows to:

-   **Listen on a local port**
-   **Forward traffic to another IP and port**

Typical use cases:

-   Forward Windows ports to **WSL**
-   Access Linux services from other machines
-   Redirect ports without installing extra software

>   It works at the **TCP level**, not application level.

------

### 5.2 Show Existing Port Forwarding Rules

```cmd
netsh interface portproxy show all
```

------

### 5.3 Add a Port Forwarding Rule

Example:
Forward **Windows port 8080** to **192.168.1.10:80**

```cmd
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=8080 connectaddress=192.168.1.10 connectport=80
```

Explanation:

-   `v4tov4` → IPv4 to IPv4
-   `listenaddress=0.0.0.0` → Listen on all local IPs
-   `listenport=8080` → Local port
-   `connectaddress=192.168.1.10` → Target IP
-   `connectport=80` → Target port

------

### 5.4 Delete a Port Forwarding Rule

```cmd
netsh interface portproxy delete v4tov4 listenport=8080 listenaddress=0.0.0.0
```

------

### 5.5 Common Mistakes with `portproxy`

1.  **Firewall blocks the port**

    ```cmd
    netsh advfirewall firewall add rule name="PortProxy 8080" dir=in action=allow protocol=TCP localport=8080
    ```

2.  `portproxy` only supports **TCP**

    -   ❌ UDP is not supported

3.  Service must be running on target machine

------

## 6. Other Useful `netsh` Commands

### 6.1 Show Routing Table

```cmd
netsh interface ip show route
```

------

### 6.2 Reset Network Stack (Troubleshooting)

Reset TCP/IP:

```cmd
netsh int ip reset
```

Reset Winsock:

```cmd
netsh winsock reset
```

(Usually followed by a reboot)

------

## 7. When to Use `netsh` vs PowerShell

| Task              | Tool                               |
| ----------------- | ---------------------------------- |
| Legacy scripts    | `netsh`                            |
| Port forwarding   | `netsh portproxy`                  |
| Modern automation | PowerShell (`NetTCPIP`)            |
| Firewall rules    | PowerShell (`New-NetFirewallRule`) |

>   `netsh` is **older but still essential**, especially for port proxying.

------

## 8. Summary

-   `netsh` is a **powerful Windows networking CLI tool**
-   Uses **context-based commands**
-   `interface` → IP, DNS, NIC management
-   `portproxy` → TCP port forwarding
-   Still widely used in servers, labs, WSL, and legacy environments