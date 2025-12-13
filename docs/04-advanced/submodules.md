# Git Submodules

Include and manage external repositories within your project.

---

## 📦 What are Submodules?

Submodules allow you to keep a Git repository as a subdirectory of another Git repository. Useful for:
- Including external libraries
- Sharing code between projects
- Managing large projects with independent components

---

## ➕ Adding a Submodule

```bash
git submodule add https://github.com/user/repo.git path/to/submodule
```

This creates:
- `.gitmodules` file (tracks submodule URLs)
- Entry in `.git/config`
- Submodule directory with the repo content

### Example

```bash
git submodule add https://github.com/user/library.git libs/library
```

### With Specific Branch

```bash
git submodule add -b main https://github.com/user/repo.git path/to/submodule
```

---

## 📥 Cloning with Submodules

### Clone and Initialize

```bash
# Method 1: Clone then init
git clone https://github.com/user/project.git
cd project
git submodule init
git submodule update

# Method 2: All in one
git clone --recurse-submodules https://github.com/user/project.git

# Method 3: If already cloned
git submodule update --init --recursive
```

---

## 🔄 Updating Submodules

### Update to Latest Commit on Tracked Branch

```bash
# All submodules
git submodule update --remote

# Specific submodule
git submodule update --remote libs/library
```

### Update to Commit Specified in Parent

```bash
git submodule update
```

### Fetch and Merge

```bash
cd path/to/submodule
git fetch
git merge origin/main
cd ..
git add path/to/submodule
git commit -m "Update submodule to latest"
```

---

## 📋 Viewing Submodule Status

### List Submodules

```bash
git submodule status
```

Output:
```
 abc1234 libs/library (v1.0.0)
+def5678 libs/another (heads/main)
-ghi9012 libs/missing
```

Prefixes:
- ` ` (space) = Correct commit checked out
- `+` = Different commit checked out
- `-` = Submodule not initialized

### Show Submodule Summary

```bash
git submodule summary
```

---

## 🔧 Working Within Submodules

### Navigate to Submodule

```bash
cd path/to/submodule
```

### Make Changes

```bash
cd path/to/submodule
# Make changes
git add .
git commit -m "Update in submodule"
git push

# Back to parent
cd ..
git add path/to/submodule
git commit -m "Update submodule reference"
```

---

## 🔀 Submodule Branch Tracking

### Set Branch to Track

```bash
git config -f .gitmodules submodule.libs/library.branch main
```

### View Tracked Branch

```bash
git config -f .gitmodules --get submodule.libs/library.branch
```

---

## 🗑️ Removing a Submodule

```bash
# 1. Remove from .gitmodules
git config -f .gitmodules --remove-section submodule.path/to/submodule

# 2. Remove from .git/config
git config --remove-section submodule.path/to/submodule

# 3. Remove the submodule directory
git rm --cached path/to/submodule
rm -rf path/to/submodule
rm -rf .git/modules/path/to/submodule

# 4. Commit
git add .gitmodules
git commit -m "Remove submodule"
```

---

## 🔄 Foreach Command

Run a command in each submodule:

```bash
# Pull latest in all submodules
git submodule foreach git pull origin main

# Check status in all
git submodule foreach git status

# Custom script
git submodule foreach 'echo $name: $(git describe --tags)'
```

---

## ⚠️ Common Issues

### Submodule Directory Empty

```bash
git submodule update --init --recursive
```

### Detached HEAD in Submodule

```bash
cd path/to/submodule
git checkout main
```

### Submodule Out of Sync

```bash
git submodule sync
git submodule update --init --recursive
```

---

## 📊 Submodules vs Alternatives

| Feature | Submodules | Subtrees | npm/package manager |
|---------|------------|----------|---------------------|
| External repo dependency | ✅ | ✅ | ✅ |
| Easy to set up | ⚠️ | ✅ | ✅ |
| Bidirectional updates | ⚠️ | ✅ | ❌ |
| History preserved | ✅ | ✅ | ❌ |
| Nested repos | ✅ | ❌ | ✅ |

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git submodule add url path` | Add submodule |
| `git submodule init` | Initialize submodules |
| `git submodule update` | Update to recorded commit |
| `git submodule update --remote` | Update to latest remote |
| `git submodule status` | Show status |
| `git submodule foreach cmd` | Run command in each |
| `git clone --recurse-submodules` | Clone with submodules |

---

## 💡 Best Practices

1. **Always commit submodule changes first**: Before updating parent reference
2. **Use `--recurse-submodules`**: When cloning or pulling
3. **Document submodules**: Explain in README how to initialize
4. **Consider alternatives**: Subtrees or package managers might be simpler
5. **Pin to tags/releases**: More stable than tracking branches

---

## 📚 Next Steps

Learn about [worktrees](worktrees.md) for working on multiple branches simultaneously!
