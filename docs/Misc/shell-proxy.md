# Shell Proxy

*(Terminal / Command-Line Proxy Explained Simply)*

## 1. What Is a Shell Proxy?

A **shell proxy** means **routing network traffic from command-line tools through a proxy server**.

Instead of your terminal tools (like `curl`, `git`, `apt`, `brew`, `pip`) connecting directly to the internet, they go through:

```
Terminal App → Proxy Server → Internet
```

This is useful when:

-   You are behind a firewall
-   You need to bypass network restrictions
-   You want faster or safer access to the internet
-   You already use tools like Clash / Shadowsocks / V2Ray / Surge

## 2. What Tools Are Affected by Shell Proxy?

Once enabled, **many CLI tools automatically follow proxy settings**, including:

-   `curl`, `wget`
-   `git`
-   `apt`, `yum`, `dnf`, `pacman`
-   `pip`, `npm`, `yarn`
-   `brew`
-   `docker` (partially)

## 3. Common Proxy Types

| Type         | Example                   |
| ------------ | ------------------------- |
| HTTP Proxy   | `http://127.0.0.1:7890`   |
| HTTPS Proxy  | `http://127.0.0.1:7890`   |
| SOCKS5 Proxy | `socks5://127.0.0.1:7891` |

>   ⚠️ Most modern proxy apps provide **SOCKS5** and **HTTP** ports.

## 4. Typical Local Proxy Apps & Ports

| App         | HTTP Port | SOCKS5 Port |
| ----------- | --------- | ----------- |
| Clash       | 7890      | 7891        |
| Surge       | 6152      | 6153        |
| Shadowsocks | 1080      | 1080        |
| V2Ray       | 10809     | 10808       |

You only need **one correct port**.

## 5. Temporary Shell Proxy

### 5.1 Enable Proxy (Current Terminal Only)

#### HTTP / HTTPS Proxy

```bash
export http_proxy="http://127.0.0.1:7890"
export https_proxy="http://127.0.0.1:7890"
```

#### SOCKS5 Proxy

```bash
export all_proxy="socks5://127.0.0.1:7891"
```

>   These settings **disappear when you close the terminal** 👍

### 5.2 Test If Proxy Works

```bash
curl ipinfo.io
```

If proxy is working:

-   IP ≠ your local ISP IP
-   Country may change

## 6. Disable Shell Proxy

```bash
unset http_proxy
unset https_proxy
unset all_proxy
```

Always remember this command.
Many “network problems” are caused by **forgotten proxy settings**.

------

## 7. Permanent Shell Proxy (Use Carefully)

### 7.1 Zsh (macOS default)

Edit config:

```bash
nano ~/.zshrc
```

Add:

```bash
export http_proxy="http://127.0.0.1:7890"
export https_proxy="http://127.0.0.1:7890"
```

Apply:

```bash
source ~/.zshrc
```

⚠️ **Not recommended unless you always need proxy**

------

## 8. Quick Toggle Scripts (Best Practice)

Add to `~/.zshrc`:

```bash
proxy_on() {
  export http_proxy="http://127.0.0.1:7890"
  export https_proxy="http://127.0.0.1:7890"
  export all_proxy="socks5://127.0.0.1:7891"
  echo "Proxy ON"
}

proxy_off() {
  unset http_proxy
  unset https_proxy
  unset all_proxy
  echo "Proxy OFF"
}
```

Usage:

```bash
proxy_on
proxy_off
```

✔ Clean
✔ Safe
✔ Beginner-friendly

------

## 9. Tool-Specific Proxy Examples

### Git

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

Remove:

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

------

### Docker

```bash
mkdir -p ~/.docker
nano ~/.docker/config.json
{
  "proxies": {
    "default": {
      "httpProxy": "http://127.0.0.1:7890",
      "httpsProxy": "http://127.0.0.1:7890"
    }
  }
}
```

Restart Docker.

------

## 10. Common Problems & Fixes

### ❌ `curl: (7) Failed to connect`

-   Proxy app not running
-   Wrong port

### ❌ `Connection reset`

-   Try switching HTTP ↔ SOCKS5
-   Use:

```bash
curl --proxy socks5://127.0.0.1:7891 https://google.com
```

### ❌ Network suddenly broken

```bash
proxy_off
```

------

## 11. Best Practices (Important!)

✔ Use **temporary proxy**
✔ Prefer **SOCKS5** if available
✔ Always know how to disable
✔ Test with `curl ipinfo.io`

❌ Do NOT leave proxy permanently enabled unless necessary
❌ Do NOT mix multiple proxy tools

------

## 12. Mental Model (Remember This)

>   **Shell proxy ≠ System proxy**
>
>   -   System proxy → GUI apps (browser)
>   -   Shell proxy → Terminal tools only

------

If you want, I can next:

-   Explain **SOCKS5 vs HTTP proxy deeply**
-   Teach **proxychains**
-   Show **Tailscale + shell proxy**
-   Provide **macOS/Linux/WSL differences**

Just tell me 👍