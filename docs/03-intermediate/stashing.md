# Stashing

Temporarily save your uncommitted changes to work on something else.

---

## 📦 What is Stashing?

Stashing takes your modified tracked files and staged changes and saves them on a stack. You can then reapply them later.

```
Working Directory (dirty) → Stash → Working Directory (clean)
```

---

## 💾 Creating a Stash

### Basic Stash

```bash
git stash
# or
git stash push
```

### Stash with Message

```bash
git stash push -m "Work in progress on login feature"
```

### Stash Including Untracked Files

```bash
git stash -u
# or
git stash --include-untracked
```

### Stash Everything (Including Ignored Files)

```bash
git stash -a
# or
git stash --all
```

### Stash Specific Files

```bash
git stash push -m "Stash specific files" file1.txt file2.txt
```

### Interactive Stash

```bash
git stash push -p
# Prompts for each hunk
```

---

## 📋 Viewing Stashes

### List All Stashes

```bash
git stash list
```

Output:
```
stash@{0}: WIP on main: abc1234 Add header component
stash@{1}: On feature: def5678 Work in progress
stash@{2}: On main: ghi9012 Initial commit
```

### Show Stash Contents

```bash
# Show latest stash
git stash show

# Show with diff
git stash show -p

# Show specific stash
git stash show stash@{1}
git stash show -p stash@{1}
```

---

## 📤 Applying Stashes

### Apply Latest Stash (Keep in Stack)

```bash
git stash apply
```

### Apply and Remove from Stack

```bash
git stash pop
```

### Apply Specific Stash

```bash
git stash apply stash@{2}
git stash pop stash@{2}
```

### Apply to Different Branch

```bash
git checkout other-branch
git stash apply
```

---

## 🗑️ Removing Stashes

### Drop Specific Stash

```bash
git stash drop stash@{0}
```

### Clear All Stashes

```bash
git stash clear
```

---

## 🌿 Creating a Branch from Stash

If you stashed changes a while ago and want to continue on a new branch:

```bash
git stash branch new-branch-name
# or with specific stash
git stash branch new-branch-name stash@{2}
```

This creates a new branch, checks it out, applies the stash, and drops it.

---

## ⚠️ Handling Stash Conflicts

When applying a stash causes conflicts:

```bash
git stash apply
# CONFLICT: Merge conflict in file.txt
```

Resolve like a regular merge conflict:

1. Open conflicted files
2. Resolve conflicts
3. Stage the resolved files: `git add file.txt`
4. The stash remains in the list (use `git stash drop` to remove)

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git stash` | Stash changes |
| `git stash push -m "msg"` | Stash with message |
| `git stash -u` | Include untracked files |
| `git stash list` | List stashes |
| `git stash show` | Show stash summary |
| `git stash show -p` | Show stash diff |
| `git stash apply` | Apply latest stash |
| `git stash pop` | Apply and remove stash |
| `git stash drop` | Remove stash |
| `git stash clear` | Remove all stashes |
| `git stash branch name` | Create branch from stash |

---

## 💡 Use Cases

1. **Quick context switch**: Stash current work to fix an urgent bug
2. **Experiment safely**: Stash before trying risky changes
3. **Clean working directory**: Stash to pull/rebase cleanly
4. **Transfer changes**: Move changes to a different branch

---

## ⚠️ Things to Remember

- Stashes are local only (not pushed to remote)
- Stashes can become stale if branches diverge significantly
- Don't rely on stash for long-term storage (commit instead)
- Stash stack is LIFO (Last In, First Out)

---

## 📚 Next Steps

Learn about [undoing changes](undoing-changes.md) with reset, revert, and restore!
