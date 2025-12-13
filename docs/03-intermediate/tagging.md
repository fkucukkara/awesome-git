# Tagging

Mark specific points in your repository's history as important.

---

## 🏷️ What are Tags?

Tags are references that point to specific commits. They're typically used to mark release versions (v1.0.0, v2.1.3, etc.).

---

## 📋 Types of Tags

### Lightweight Tags

Simple pointers to commits (like a branch that doesn't move):

```bash
git tag v1.0.0
```

### Annotated Tags (Recommended)

Full objects with tagger info, date, message, and can be signed:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

---

## ➕ Creating Tags

### Tag Current Commit

```bash
# Lightweight
git tag v1.0.0

# Annotated
git tag -a v1.0.0 -m "Version 1.0.0 - Initial release"
```

### Tag Specific Commit

```bash
git tag -a v1.0.0 abc1234 -m "Version 1.0.0"
```

### Signed Tag (GPG)

```bash
git tag -s v1.0.0 -m "Signed release 1.0.0"
```

---

## 📋 Listing Tags

### List All Tags

```bash
git tag
```

### List with Pattern

```bash
git tag -l "v1.*"
git tag -l "v2.0.*"
```

### Sort by Version

```bash
git tag -l --sort=-version:refname
```

---

## 🔍 Viewing Tag Information

### Show Tag Details

```bash
git show v1.0.0
```

Output for annotated tag:
```
tag v1.0.0
Tagger: Your Name <email@example.com>
Date:   Fri Dec 13 10:00:00 2025 +0000

Version 1.0.0 - Initial release

commit abc1234567890...
Author: Your Name <email@example.com>
Date:   Thu Dec 12 15:30:00 2025 +0000

    Add feature X
```

### Verify Signed Tag

```bash
git tag -v v1.0.0
```

---

## 📤 Sharing Tags

### Push Specific Tag

```bash
git push origin v1.0.0
```

### Push All Tags

```bash
git push origin --tags
```

### Push Only Annotated Tags

```bash
git push origin --follow-tags
```

---

## 🔀 Checking Out Tags

### Checkout a Tag

```bash
git checkout v1.0.0
```

This puts you in "detached HEAD" state.

### Create Branch from Tag

```bash
git checkout -b release-1.0 v1.0.0
```

---

## 🗑️ Deleting Tags

### Delete Local Tag

```bash
git tag -d v1.0.0
```

### Delete Remote Tag

```bash
git push origin --delete v1.0.0
# or
git push origin :refs/tags/v1.0.0
```

---

## ✏️ Moving/Updating Tags

### Update Tag to New Commit

```bash
# Delete and recreate
git tag -d v1.0.0
git tag v1.0.0

# Or force update
git tag -f v1.0.0
```

### Update Remote Tag

```bash
git push origin -f v1.0.0
```

⚠️ Avoid moving tags that others may have pulled.

---

## 🎨 Semantic Versioning

Follow [SemVer](https://semver.org/) for version tags:

```
MAJOR.MINOR.PATCH

v1.0.0 - Initial release
v1.1.0 - New feature (backward compatible)
v1.1.1 - Bug fix
v2.0.0 - Breaking changes
```

### Pre-release Versions

```
v1.0.0-alpha.1
v1.0.0-beta.2
v1.0.0-rc.1
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git tag name` | Create lightweight tag |
| `git tag -a name -m "msg"` | Create annotated tag |
| `git tag` | List tags |
| `git show name` | Show tag details |
| `git push origin name` | Push tag to remote |
| `git push --tags` | Push all tags |
| `git tag -d name` | Delete local tag |
| `git push origin --delete name` | Delete remote tag |
| `git checkout name` | Checkout tag |

---

## 💡 Best Practices

1. **Use annotated tags for releases**: Include version notes
2. **Follow semantic versioning**: Makes versions meaningful
3. **Tag after testing**: Only tag stable, tested code
4. **Don't move published tags**: Others may depend on them
5. **Include release notes**: Document what changed

---

## 📚 Next Steps

Learn about [cherry-picking](cherry-picking.md) to apply specific commits!
