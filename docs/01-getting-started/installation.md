# Installing Git

This guide covers how to install Git on different operating systems.

---

## 🪟 Windows

### Option 1: Git for Windows (Recommended)

1. Download the installer from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer
3. Follow the setup wizard (default options work for most users)
4. Verify installation:
   ```bash
   git --version
   ```

### Option 2: Using winget

```bash
winget install --id Git.Git -e --source winget
```

### Option 3: Using Chocolatey

```bash
choco install git
```

---

## 🍎 macOS

### Option 1: Xcode Command Line Tools

```bash
xcode-select --install
```

### Option 2: Using Homebrew (Recommended)

```bash
brew install git
```

### Option 3: Download Installer

Download from [git-scm.com](https://git-scm.com/download/mac)

---

## 🐧 Linux

### Debian/Ubuntu

```bash
sudo apt update
sudo apt install git
```

### Fedora

```bash
sudo dnf install git
```

### Arch Linux

```bash
sudo pacman -S git
```

### CentOS/RHEL

```bash
sudo yum install git
```

---

## ✅ Verify Installation

After installation, verify Git is working:

```bash
git --version
```

Expected output:
```
git version 2.43.0
```

---

## 🔄 Updating Git

### Windows
Download and run the latest installer, or:
```bash
git update-git-for-windows
```

### macOS (Homebrew)
```bash
brew upgrade git
```

### Linux
Use your package manager's update command

---

## 📚 Next Steps

Now that Git is installed, let's [configure it](configuration.md) for your use.
