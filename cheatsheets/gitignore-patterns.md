# Git Ignore Patterns

Common `.gitignore` patterns for different project types.

---

## 📖 How .gitignore Works

```bash
# Comment
file.txt          # Specific file
*.log             # All .log files
folder/           # Directory and contents
!important.log    # Negate (don't ignore)
**/temp           # Match in any directory
debug?.log        # Single character wildcard
```

---

## 🖥️ Operating Systems

### macOS
```gitignore
.DS_Store
.AppleDouble
.LSOverride
._*
.Spotlight-V100
.Trashes
```

### Windows
```gitignore
Thumbs.db
ehthumbs.db
Desktop.ini
$RECYCLE.BIN/
*.lnk
```

### Linux
```gitignore
*~
.fuse_hidden*
.Trash-*
.nfs*
```

---

## 📝 Editors & IDEs

### VS Code
```gitignore
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
*.code-workspace
```

### JetBrains (IntelliJ, PyCharm, etc.)
```gitignore
.idea/
*.iml
*.iws
*.ipr
out/
```

### Vim
```gitignore
*.swp
*.swo
*~
```

---

## 🟨 JavaScript / Node.js

```gitignore
# Dependencies
node_modules/
jspm_packages/

# Build output
dist/
build/
out/

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*
*.log

# Environment
.env
.env.local
.env.*.local

# Cache
.npm
.eslintcache
.cache/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Testing
coverage/

# Misc
*.tgz
.next/
```

---

## 🐍 Python

```gitignore
# Byte-compiled
__pycache__/
*.py[cod]
*$py.class
*.so

# Distribution
dist/
build/
*.egg-info/
.eggs/

# Virtual environments
venv/
env/
.venv/
ENV/

# IDEs
.idea/
.vscode/
*.sublime-*

# Jupyter
.ipynb_checkpoints/

# Testing
.tox/
.coverage
htmlcov/
.pytest_cache/

# Environment
.env
.env.local
*.env

# Misc
*.log
.mypy_cache/
.ruff_cache/
```

---

## ☕ Java

```gitignore
# Compiled
*.class
*.jar
*.war
*.ear

# Build directories
target/
build/
out/

# IDE
.idea/
*.iml
.eclipse/
.settings/
*.classpath
*.project

# Maven
pom.xml.tag
pom.xml.releaseBackup

# Gradle
.gradle/
gradle-app.setting
!gradle-wrapper.jar

# Logs
*.log
```

---

## 🔵 .NET / C#

```gitignore
# Build results
bin/
obj/
out/

# Visual Studio
.vs/
*.suo
*.user
*.userosscache
*.sln.docstates

# User-specific
*.rsuser
*.suo
*.userprefs

# Build
*.dll
*.exe
*.pdb

# NuGet
packages/
*.nupkg
project.lock.json

# Rider
.idea/

# Misc
*.log
*.cache
```

---

## 🐹 Go

```gitignore
# Binaries
*.exe
*.exe~
*.dll
*.so
*.dylib

# Test binary
*.test

# Output
/bin/
/pkg/

# Dependency directories
vendor/

# IDE
.idea/
.vscode/

# Misc
*.log
.env
```

---

## 📦 Universal Template

```gitignore
# ===== OS =====
.DS_Store
Thumbs.db
Desktop.ini

# ===== Editors =====
.vscode/
.idea/
*.swp
*.swo
*~

# ===== Logs =====
*.log
logs/

# ===== Environment =====
.env
.env.local
.env.*.local

# ===== Dependencies =====
node_modules/
vendor/
venv/

# ===== Build =====
dist/
build/
out/
target/

# ===== Cache =====
.cache/
*.cache

# ===== Testing =====
coverage/
.nyc_output/

# ===== Misc =====
*.tmp
*.temp
*.bak
```

---

## 🔧 Useful Commands

```bash
# Check why file is ignored
git check-ignore -v file.txt

# List all ignored files
git ls-files --ignored --exclude-standard

# Remove cached file (after adding to .gitignore)
git rm --cached file.txt

# Remove cached directory
git rm -r --cached folder/
```

---

## 🌐 Resources

- [gitignore.io](https://www.toptal.com/developers/gitignore) - Generate templates
- [GitHub's gitignore templates](https://github.com/github/gitignore)
