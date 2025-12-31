# `systemctl` Tutorial for Beginners

## 1. What is `systemctl`?

`systemctl` is the main command-line tool used to **control and manage services** on Linux systems that use **systemd**.

In simple terms:

-   **service** = a background program (e.g. `ssh`, `nginx`, `mysql`)
-   **systemd** = the system that starts, stops, and monitors those services
-   **systemctl** = the tool you use to talk to systemd

Most modern Linux distributions use systemd, including:

-   Ubuntu (16.04+)
-   Debian (8+)
-   CentOS / Rocky / Alma
-   Arch Linux
-   Raspberry Pi OS

------

## 2. Basic Syntax

```bash
systemctl [OPTIONS] COMMAND [UNIT]
```

-   **COMMAND**: what you want to do (start, stop, status, …)
-   **UNIT**: the target service (e.g. `ssh`, `nginx`, `mysql`)

Example:

```bash
systemctl status ssh
```

------

## 3. Understanding “Units”

In systemd, everything is called a **unit**.

Common unit types:

| Type    | Suffix     | Meaning                    |
| ------- | ---------- | -------------------------- |
| Service | `.service` | Background service         |
| Target  | `.target`  | Group of units             |
| Mount   | `.mount`   | Mount point                |
| Timer   | `.timer`   | Scheduled task (cron-like) |

👉 Usually, you can omit the suffix:

```bash
systemctl status ssh
# same as
systemctl status ssh.service
```

------

## 4. Checking Service Status

### Check if a service is running

```bash
systemctl status nginx
```

You will see:

-   Active / inactive
-   Running / failed
-   Recent logs
-   PID and resource usage

Key status lines:

```
Active: active (running)
Active: inactive (dead)
Active: failed
```

------

## 5. Starting and Stopping Services

### Start a service

```bash
sudo systemctl start nginx
```

### Stop a service

```bash
sudo systemctl stop nginx
```

### Restart a service

```bash
sudo systemctl restart nginx
```

### Reload configuration (if supported)

```bash
sudo systemctl reload nginx
```

🔹 **restart** = stop + start
🔹 **reload** = reread config without stopping

------

## 6. Enable vs Start (Very Important!)

This is a common beginner confusion.

| Command  | Meaning           |
| -------- | ----------------- |
| `start`  | Start **now**     |
| `enable` | Start **at boot** |

### Enable service at boot

```bash
sudo systemctl enable mysql
```

### Disable service at boot

```bash
sudo systemctl disable mysql
```

### Enable and start immediately

```bash
sudo systemctl enable --now mysql
```

------

## 7. Listing Services

### List all running services

```bash
systemctl list-units --type=service
```

### List all installed services (including disabled)

```bash
systemctl list-unit-files --type=service
```

### Show only failed services

```bash
systemctl --failed
```

------

## 8. Viewing Logs with `journalctl`

systemd uses a centralized logging system.

### View logs for a service

```bash
journalctl -u nginx
```

### Follow logs in real time

```bash
journalctl -u nginx -f
```

### View logs since boot

```bash
journalctl -u nginx -b
```

------

## 9. Checking System Boot and Targets

### Check current default target

```bash
systemctl get-default
```

Common targets:

-   `multi-user.target` → server mode (no GUI)
-   `graphical.target` → desktop mode

### Change default target

```bash
sudo systemctl set-default multi-user.target
```

------

## 10. Common Beginner Mistakes

### ❌ Forgetting `sudo`

Most service operations require root:

```bash
sudo systemctl restart ssh
```

### ❌ Mixing `service` and `systemctl`

Older systems used:

```bash
service nginx restart
```

Modern systems should use:

```bash
systemctl restart nginx
```

### ❌ Confusing enable and start

-   `enable` does **not** start immediately
-   `start` does **not** persist across reboot

------

## 11. Useful Shortcuts

| Task                         | Command                         |
| ---------------------------- | ------------------------------- |
| Check if service is active   | `systemctl is-active ssh`       |
| Check if enabled at boot     | `systemctl is-enabled ssh`      |
| Mask a service (fully block) | `sudo systemctl mask service`   |
| Unmask a service             | `sudo systemctl unmask service` |

------

## 12. When Should You Use `systemctl`?

You will use `systemctl` when:

-   Managing web servers (nginx, apache)
-   Managing databases (mysql, postgresql)
-   Managing SSH
-   Debugging boot issues
-   Writing server automation scripts

------

## 13. Summary

-   `systemctl` is the **control center** for services on modern Linux
-   Learn these first:
    -   `status`
    -   `start / stop / restart`
    -   `enable / disable`
-   Understand the difference between **now** and **at boot**
-   Combine with `journalctl` for debugging