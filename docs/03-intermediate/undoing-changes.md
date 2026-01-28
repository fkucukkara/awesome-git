# Undoing Changes

Learn the different ways to undo changes in Git: reset, revert, and restore.

---

## 🎯 Choosing the Right Command

| Scenario | Command |
|----------|---------|
| Undo changes in working directory | `git restore` |
| Unstage files | `git restore --staged` |
| Undo commits (rewrite history) | `git reset` |
| Undo commits (preserve history) | `git revert` |

---

## 📂 Git Restore

### Discard Changes in Working Directory

```bash
# Restore a single file
git restore filename.txt

# Restore multiple files
git restore file1.txt file2.txt

# Restore all files in current directory
git restore .
```

### Unstage Files

```bash
# Unstage a file (keep changes in working directory)
git restore --staged filename.txt

# Unstage all files
git restore --staged .
```

### Restore to Specific Commit

```bash
# Restore file to version from specific commit
git restore --source=abc1234 filename.txt

# Restore to version from HEAD~2
git restore --source=HEAD~2 filename.txt
```

---

## 🔄 Git Reset

Reset moves the branch pointer and optionally modifies the staging area and working directory.

### Three Reset Modes

```
         --soft     --mixed (default)    --hard
           ↓              ↓                 ↓
Commit:   Undone        Undone            Undone
Staging:  Preserved     Cleared           Cleared
Working:  Preserved     Preserved         Cleared
```

### Soft Reset

Undo commits but keep changes staged:

```bash
git reset --soft HEAD~1
```

Use case: Combine multiple commits into one.

### Mixed Reset (Default)

Undo commits and unstage changes:

```bash
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

Use case: Undo commits but keep changes for editing.

### Hard Reset

Undo commits and discard all changes:

```bash
git reset --hard HEAD~1
```

⚠️ **Warning**: This permanently deletes uncommitted changes!

### Reset Specific Files

```bash
# Unstage a file (same as restore --staged)
git reset HEAD filename.txt
```

### Common Reset Targets

```bash
git reset --hard HEAD          # Discard all uncommitted changes
git reset --hard HEAD~1        # Undo last commit
git reset --hard HEAD~3        # Undo last 3 commits
git reset --hard abc1234       # Reset to specific commit
git reset --hard origin/main   # Reset to remote state
```

### Pushing After Reset

⚠️ **Important**: If you've already pushed commits that you're resetting, you'll need to force push:

```bash
# After any reset that moves HEAD backward
git push --force-with-lease

# Alternative (less safe)
git push --force
```

**When is force push needed?**
- ✅ After `git reset --soft HEAD~1` (if commits were pushed)
- ✅ After `git reset --mixed HEAD~1` (if commits were pushed)
- ✅ After `git reset --hard HEAD~1` (if commits were pushed)
- ❌ Not needed if commits were never pushed

**Use `--force-with-lease` instead of `--force`**:
- Safer option that checks if remote was updated
- Prevents accidentally overwriting others' work
- Only forces if remote is in the expected state

⚠️ **Warning**: Never force push to shared branches (main, develop) without team agreement!

---

## ↩️ Git Revert

Revert creates a new commit that undoes a previous commit. Safe for shared branches.

### Revert Last Commit

```bash
git revert HEAD
```

### Revert Specific Commit

```bash
git revert abc1234
```

### Revert Multiple Commits

```bash
# Revert a range
git revert HEAD~3..HEAD

# Revert multiple specific commits
git revert abc1234 def5678 ghi9012
```

### Revert Without Committing

```bash
git revert --no-commit abc1234
# Make additional changes, then commit
git commit -m "Revert changes and fix X"
```

### Revert a Merge Commit

```bash
# -m 1 specifies the parent to revert to (usually 1)
git revert -m 1 merge-commit-hash
```

---

## 📊 Comparison

| Aspect | `restore` | `reset` | `revert` |
|--------|-----------|---------|----------|
| Affects history | No | Yes | No (adds new commit) |
| Safe for shared branches | Yes | No | Yes |
| Can undo commits | No | Yes | Yes |
| Scope | Files | Commits | Commits |

---

## 🔧 Recovering from Mistakes

### Find Lost Commits

```bash
git reflog
```

### Recover After Hard Reset

```bash
# Find the commit hash in reflog
git reflog
# Reset to that commit
git reset --hard abc1234
```

### Recover Deleted Branch

```bash
# Find the commit hash in reflog
git reflog
# Create new branch at that commit
git branch recovered-branch abc1234
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git restore file` | Discard working directory changes |
| `git restore --staged file` | Unstage file |
| `git reset --soft HEAD~1` | Undo commit, keep staged |
| `git reset HEAD~1` | Undo commit, unstage changes |
| `git reset --hard HEAD~1` | Undo commit, discard all |
| `git revert HEAD` | Create commit to undo last |
| `git reflog` | View history of HEAD |

---

## 💡 Best Practices

1. **Use `revert` for shared branches**: Never rewrite public history
2. **Use `reset --hard` carefully**: Changes are permanently lost
3. **Check `reflog` for recovery**: Git keeps commits for 30 days
4. **Commit before risky operations**: Create a backup point

---

## 📚 Next Steps

Learn about [tagging](tagging.md) to mark important points in history!
