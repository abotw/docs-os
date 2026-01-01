# macOS Shell

## 1. What Is a Shell?

A **shell** is a program that lets you interact with macOS using **text commands** instead of clicking buttons.

-   You type commands
-   The shell executes them
-   You get text output

On macOS, you access the shell through **Terminal.app**.

>   Think of the shell as:
>   **You → Shell → Operating System**

------

## 2. Open the Terminal on macOS

### Method 1: Spotlight (Recommended)

1.  Press **⌘ Command + Space**
2.  Type `Terminal`
3.  Press **Enter**

### Method 2: Finder

```
Applications → Utilities → Terminal
```

------

## 3. Common Shells on macOS

macOS supports multiple shells.

| Shell  | Description                                     |
| ------ | ----------------------------------------------- |
| `zsh`  | **Default** shell since macOS Catalina (10.15+) |
| `bash` | Older default (still widely used)               |
| `sh`   | Original Unix shell (minimal)                   |
| `fish` | User-friendly, needs installation               |

### Check your current shell

```bash
echo $SHELL
```

Example output:

```text
/bin/zsh
```

------

## 4. Basic Shell Usage

### 4.1 Where am I?

```bash
pwd
```

Prints the **current directory**.

------

### 4.2 List files

```bash
ls
ls -l
ls -a
```

| Command | Meaning              |
| ------- | -------------------- |
| `ls`    | List files           |
| `ls -l` | Long format          |
| `ls -a` | Include hidden files |

------

### 4.3 Change directory

```bash
cd Documents
cd ..
cd ~
```

| Path | Meaning          |
| ---- | ---------------- |
| `..` | Parent directory |
| `~`  | Home directory   |

------

### 4.4 Create & remove files

```bash
touch test.txt
rm test.txt
```

Create / delete directories:

```bash
mkdir mydir
rmdir mydir
```

------

### 4.5 View file contents

```bash
cat file.txt
less file.txt
```

-   `less` allows scrolling (press `q` to quit)

------

## 5. Command Structure

A shell command usually looks like:

```bash
command options arguments
```

Example:

```bash
ls -l /Applications
```

-   `ls` → command
-   `-l` → option
-   `/Applications` → argument

------

## 6. Useful Keyboard Shortcuts

| Shortcut   | Function              |
| ---------- | --------------------- |
| `↑ / ↓`    | Command history       |
| `Tab`      | Auto-completion       |
| `Ctrl + C` | Stop command          |
| `Ctrl + D` | Exit shell            |
| `Cmd + K`  | Clear terminal screen |

------

## 7. Environment Variables

Shells use **environment variables**.

### View all variables

```bash
env
```

### View one variable

```bash
echo $PATH
```

`PATH` tells the shell **where to find commands**.

------

## 8. Shell Configuration Files (Very Important)

Your shell behavior is controlled by config files.

### For zsh (default)

| File          | Purpose                 |
| ------------- | ----------------------- |
| `~/.zshrc`    | Main config (most used) |
| `~/.zprofile` | Login shell settings    |

### For bash

| File              |
| ----------------- |
| `~/.bashrc`       |
| `~/.bash_profile` |

Edit with:

```bash
nano ~/.zshrc
```

Apply changes:

```bash
source ~/.zshrc
```

------

## 9. How to Change Your Default Shell

### 9.1 List available shells

```bash
cat /etc/shells
```

------

### 9.2 Change shell using `chsh`

```bash
chsh -s /bin/zsh # -s: switch
```

Or switch to bash:

```bash
chsh -s /bin/bash
```

You must **log out and back in** for it to take effect.

------

### 9.3 Temporary shell switch

Run another shell inside the current one:

```bash
bash
zsh
sh
```

Exit with:

```bash
exit
```

------

## 10. zsh vs bash (macOS Perspective)

| Feature           | zsh       | bash      |
| ----------------- | --------- | --------- |
| Default on macOS  | ✅         | ❌         |
| Better completion | ✅         | ⚠️         |
| Plugin ecosystem  | Excellent | Good      |
| Compatibility     | High      | Very high |

**Recommendation:**
👉 Stick with **zsh** unless you have a specific reason.

------

## 11. Installing a Better Shell Experience (Optional)

### Oh My Zsh (Popular)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Adds:

-   Git status
-   Themes
-   Plugins

Beginner-friendly and widely used on macOS.

------

## 12. Common Beginner Mistakes

❌ Running Linux-only commands on macOS
❌ Editing `/etc/*` files unnecessarily
❌ Using `sudo` blindly
❌ Deleting files with `rm -rf` without understanding

------

## 13. Summary

-   A **shell** is a text interface to macOS
-   **zsh** is the default and recommended shell
-   Learn basic commands: `ls`, `cd`, `pwd`, `cat`
-   Customize behavior via `~/.zshrc`
-   Change shells using `chsh`

