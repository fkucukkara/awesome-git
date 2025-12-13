# Reflog

Git's safety net - track every change to HEAD and recover from mistakes.

---

## 🔍 What is Reflog?

Reflog (reference log) records when the tips of branches and HEAD are updated. It's like a local history of everything you've done.

Unlike `git log` which shows commit history, `reflog` shows the history of your HEAD movements.

---

## 📋 Viewing Reflog

### Basic Reflog

```bash
git reflog
# or
git reflog show HEAD
```

Output:
```
abc1234 HEAD@{0}: commit: Add new feature
def5678 HEAD@{1}: checkout: moving from main to feature
ghi9012 HEAD@{2}: reset: moving to HEAD~1
jkl3456 HEAD@{3}: commit: Previous commit
```

### With Timestamps

```bash
git reflog --date=relative
```

Output:
```
abc1234 HEAD@{5 minutes ago}: commit: Add new feature
def5678 HEAD@{10 minutes ago}: checkout: moving from main to feature
```

### For Specific Branch

```bash
git reflog show main
git reflog show feature-branch
```

### With More Details

```bash
git reflog --all
```

---

## 🧭 Understanding Reflog Entries

Each entry shows:
```
commit-hash HEAD@{n}: action: description
```

| Part | Meaning |
|------|---------|
| `abc1234` | Commit hash |
| `HEAD@{0}` | Reference at position 0 (most recent) |
| `commit:` | Action type |
| `Add feature` | Description |

### Common Action Types

- `commit` - New commit
- `checkout` - Changed branches
- `reset` - Reset command
- `rebase` - Rebase operation
- `merge` - Merge operation
- `pull` - Pull from remote
- `clone` - Initial clone

---

## 🔄 Recovering Lost Commits

### After Hard Reset

```bash
# Oops! Lost commits
git reset --hard HEAD~3

# Find them in reflog
git reflog
# abc1234 HEAD@{1}: commit: The commit I want back

# Recover
git reset --hard abc1234
# or create a branch
git branch recovered-work abc1234
```

### After Bad Rebase

```bash
# Rebase went wrong
git rebase main
# Everything is messed up!

# Find pre-rebase state
git reflog
# Look for entry before "rebase"

# Recover
git reset --hard HEAD@{5}
```

### After Deleted Branch

```bash
# Accidentally deleted branch
git branch -D important-feature

# Find the tip of deleted branch
git reflog
# or
git reflog | grep important-feature

# Recreate the branch
git branch important-feature abc1234
```

---

## 🕐 Time-Based References

Access commits by time:

```bash
# Where HEAD was 30 minutes ago
git show HEAD@{30.minutes.ago}

# Where HEAD was yesterday
git show HEAD@{yesterday}

# Where main was last week
git show main@{1.week.ago}

# Where HEAD was at specific date
git show HEAD@{2025-12-01}
```

### Use in Commands

```bash
# Diff with past state
git diff HEAD@{1.hour.ago}

# Log since yesterday
git log HEAD@{yesterday}..HEAD

# Reset to state from 2 hours ago
git reset --hard HEAD@{2.hours.ago}
```

---

## 🧹 Reflog Maintenance

### Reflog Expiration

By default, reflog entries expire:
- Reachable entries: 90 days
- Unreachable entries: 30 days

### Configure Expiration

```bash
# Change unreachable expiration to 60 days
git config gc.reflogExpireUnreachable 60

# Never expire
git config gc.reflogExpire never
```

### Manually Expire

```bash
# Expire old entries
git reflog expire --expire=now --all

# Run garbage collection after
git gc
```

### Delete Specific Entry

```bash
git reflog delete HEAD@{5}
```

---

## 🔧 Practical Recovery Scenarios

### 1. Recover from `commit --amend`

```bash
# You amended but want the original back
git reflog
# abc1234 HEAD@{0}: commit (amend): New message
# def5678 HEAD@{1}: commit: Original message

git reset --soft HEAD@{1}
```

### 2. Recover Stash

If you accidentally dropped a stash:

```bash
# Find stash commits
git fsck --no-reflog | grep commit

# Or search reflog
git reflog | grep stash

# Apply the found commit
git stash apply abc1234
```

### 3. Undo Merge

```bash
git merge feature-branch
# Oops, wrong branch!

git reflog
# Find state before merge

git reset --hard HEAD@{1}
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git reflog` | Show reflog for HEAD |
| `git reflog show branch` | Show reflog for branch |
| `git reflog --date=relative` | Show with timestamps |
| `git show HEAD@{n}` | Show commit at position n |
| `git show HEAD@{1.hour.ago}` | Show commit from 1 hour ago |
| `git reset --hard HEAD@{n}` | Reset to reflog position |
| `git branch name HEAD@{n}` | Create branch at position |

---

## 💡 Tips

1. **Check reflog first**: Before panicking about lost work
2. **Reflog is local**: Not shared via push/pull
3. **Act quickly**: Reflog entries eventually expire
4. **Use branches for recovery**: Safer than direct reset
5. **Reflog survives reset**: Even `--hard` reset is recoverable

---

## ⚠️ Limitations

- **Local only**: Each clone has its own reflog
- **Expires over time**: Old entries are garbage collected
- **Not for uncommitted changes**: Only tracks commits
- **Cleaned by gc**: `git gc` may remove unreachable commits

---

## 📚 Next Steps

Learn about [bisect](bisect.md) to find bugs efficiently!
