# Configuring Git

Before you start using Git, you need to configure your identity and preferences.

---

## 🆔 Setting Your Identity

Git needs to know who you are for commit history:

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"
```

> 💡 Use the same email as your GitHub/GitLab account for proper attribution.

---

## ⚙️ Configuration Levels

Git has three configuration levels:

| Level | Flag | Location | Scope |
|-------|------|----------|-------|
| System | `--system` | `/etc/gitconfig` | All users on the system |
| Global | `--global` | `~/.gitconfig` | Current user, all repos |
| Local | `--local` | `.git/config` | Current repository only |

Local settings override global, which override system.

---

## 📝 Essential Settings

### Default Branch Name

```bash
# Set default branch to 'main'
git config --global init.defaultBranch main
```

### Default Editor

```bash
# VS Code
git config --global core.editor "code --wait"

# Vim
git config --global core.editor "vim"

# Nano
git config --global core.editor "nano"

# Notepad++ (Windows)
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

### Line Endings

```bash
# Windows
git config --global core.autocrlf true

# macOS/Linux
git config --global core.autocrlf input
```

### Colorized Output

```bash
git config --global color.ui auto
```

---

## 🔍 Viewing Configuration

### View All Settings

```bash
git config --list
```

### View Specific Setting

```bash
git config user.name
git config user.email
```

### View Settings with Origin

```bash
git config --list --show-origin
```

---

## 🎨 Useful Optional Settings

### Enable Helpful Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
```

### Push Behavior

```bash
# Only push current branch
git config --global push.default current

# Auto-setup remote tracking
git config --global push.autoSetupRemote true
```

### Pull Behavior

```bash
# Rebase instead of merge on pull
git config --global pull.rebase true
```

### Credential Caching

```bash
# Cache credentials for 1 hour (3600 seconds)
git config --global credential.helper 'cache --timeout=3600'

# Windows: Use Windows Credential Manager
git config --global credential.helper manager

# macOS: Use Keychain
git config --global credential.helper osxkeychain
```

---

## 📄 Sample .gitconfig

Here's what a complete `~/.gitconfig` might look like:

```ini
[user]
    name = Your Name
    email = your.email@example.com

[init]
    defaultBranch = main

[core]
    editor = code --wait
    autocrlf = input

[color]
    ui = auto

[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    lg = log --oneline --graph --all

[push]
    default = current
    autoSetupRemote = true

[pull]
    rebase = true
```

---

## 📚 Next Steps

With Git configured, you're ready to [create your first repository](first-repository.md)!
