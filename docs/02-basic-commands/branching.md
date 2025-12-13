# Branching

Branches allow you to work on different features or fixes in isolation.

---

## 🌿 What is a Branch?

A branch is a lightweight pointer to a commit. The default branch is typically `main` (or `master` in older repos).

```
          Feature Branch
               ↓
        ○───○───○
       /
○───○───○───○───○  ← main
```

---

## 📋 Listing Branches

### List Local Branches

```bash
git branch
```

Output:
```
  feature-login
* main
  bugfix-header
```

The `*` indicates the current branch.

### List Remote Branches

```bash
git branch -r
```

### List All Branches

```bash
git branch -a
```

### List with Last Commit

```bash
git branch -v
```

---

## ➕ Creating Branches

### Create a New Branch

```bash
git branch feature-name
```

### Create and Switch to New Branch

```bash
git checkout -b feature-name
# or (Git 2.23+)
git switch -c feature-name
```

### Create Branch from Specific Commit

```bash
git branch feature-name abc1234
```

### Create Branch from Remote

```bash
git checkout -b feature-name origin/feature-name
# or
git switch -c feature-name origin/feature-name
```

---

## 🔀 Switching Branches

### Using checkout

```bash
git checkout branch-name
```

### Using switch (Git 2.23+)

```bash
git switch branch-name
```

### Switch to Previous Branch

```bash
git checkout -
# or
git switch -
```

---

## ✏️ Renaming Branches

### Rename Current Branch

```bash
git branch -m new-name
```

### Rename Any Branch

```bash
git branch -m old-name new-name
```

### Rename Remote Branch

```bash
# Delete old remote branch
git push origin --delete old-name

# Push new branch
git push origin new-name
```

---

## 🗑️ Deleting Branches

### Delete Local Branch (Safe)

```bash
git branch -d branch-name
```

> Only works if branch is fully merged

### Delete Local Branch (Force)

```bash
git branch -D branch-name
```

### Delete Remote Branch

```bash
git push origin --delete branch-name
# or
git push origin :branch-name
```

---

## 📤 Pushing Branches

### Push New Branch to Remote

```bash
git push -u origin branch-name
```

### Push All Branches

```bash
git push --all origin
```

---

## 📥 Tracking Remote Branches

### Set Upstream Branch

```bash
git branch --set-upstream-to=origin/branch-name
# or
git push -u origin branch-name
```

### See Tracking Information

```bash
git branch -vv
```

---

## 🔍 Branch Information

### Show Current Branch

```bash
git branch --show-current
```

### Branches Containing Commit

```bash
git branch --contains abc1234
```

### Merged Branches

```bash
git branch --merged
```

### Unmerged Branches

```bash
git branch --no-merged
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git branch` | List local branches |
| `git branch -a` | List all branches |
| `git branch name` | Create branch |
| `git switch -c name` | Create and switch |
| `git switch name` | Switch to branch |
| `git branch -d name` | Delete merged branch |
| `git branch -D name` | Force delete branch |
| `git push origin --delete name` | Delete remote branch |

---

## 💡 Best Practices

1. **Use descriptive names**: `feature/user-authentication`, `bugfix/login-error`
2. **Keep branches short-lived**: Merge frequently to avoid conflicts
3. **Delete merged branches**: Keep your branch list clean
4. **Use branch prefixes**: `feature/`, `bugfix/`, `hotfix/`, `release/`

---

## 📚 Next Steps

Learn how to [merge branches](merging.md) to combine your work!
