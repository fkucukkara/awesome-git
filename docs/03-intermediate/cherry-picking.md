# Cherry-picking

Apply specific commits from one branch to another.

---

## 🍒 What is Cherry-picking?

Cherry-pick allows you to pick individual commits and apply them to your current branch. Unlike merge or rebase, you select exactly which commits to bring over.

```
Before:
main:    ○───○───○───○
                      \
feature:               A───B───C───D

After cherry-pick B to main:
main:    ○───○───○───○───B'
                      \
feature:               A───B───C───D
```

---

## 📥 Basic Cherry-pick

### Apply a Single Commit

```bash
git cherry-pick abc1234
```

### Apply Multiple Commits

```bash
git cherry-pick abc1234 def5678 ghi9012
```

### Apply a Range of Commits

```bash
# From commit A (exclusive) to commit B (inclusive)
git cherry-pick A..B

# Include both endpoints
git cherry-pick A^..B
```

---

## ⚙️ Cherry-pick Options

### Don't Commit Immediately

```bash
git cherry-pick --no-commit abc1234
# or
git cherry-pick -n abc1234
```

Useful for combining multiple cherry-picks into one commit.

### Edit Commit Message

```bash
git cherry-pick --edit abc1234
# or
git cherry-pick -e abc1234
```

### Append Reference to Original Commit

```bash
git cherry-pick -x abc1234
```

Adds "(cherry picked from commit abc1234...)" to the message.

### Use Mainline Parent for Merge Commits

```bash
git cherry-pick -m 1 merge-commit-hash
```

---

## ⚠️ Handling Conflicts

When cherry-pick encounters conflicts:

```bash
git cherry-pick abc1234
# CONFLICT: Merge conflict in file.txt
```

### Resolve and Continue

```bash
# 1. Resolve conflicts in the file
# 2. Stage resolved files
git add file.txt

# 3. Continue cherry-pick
git cherry-pick --continue
```

### Abort Cherry-pick

```bash
git cherry-pick --abort
```

### Skip Current Commit

```bash
git cherry-pick --skip
```

---

## 📊 Cherry-pick vs Other Commands

| Feature | Cherry-pick | Merge | Rebase |
|---------|-------------|-------|--------|
| Selects specific commits | ✅ | ❌ | ❌ |
| Creates new commits | ✅ | ⚠️ (merge commit) | ✅ |
| Preserves original commit | ❌ | ✅ | ❌ |
| Good for hotfixes | ✅ | ❌ | ❌ |

---

## 🎯 Use Cases

### 1. Hotfix to Multiple Branches

```bash
# Fix bug on development branch
git checkout develop
# ... make fix, commit as abc1234

# Apply to main
git checkout main
git cherry-pick abc1234

# Apply to release branch
git checkout release/1.0
git cherry-pick abc1234
```

### 2. Pull Specific Feature

```bash
# Want only the authentication commit from feature branch
git checkout main
git cherry-pick feature-branch~2  # Second-to-last commit
```

### 3. Recover Accidentally Deleted Commit

```bash
# Find commit hash in reflog
git reflog
# Cherry-pick it back
git cherry-pick abc1234
```

---

## 🔍 Finding Commits to Cherry-pick

### View Commits on Another Branch

```bash
git log feature-branch --oneline
```

### Commits Not in Current Branch

```bash
git log main..feature-branch --oneline
```

### With File Changes

```bash
git log feature-branch --oneline -- path/to/file
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git cherry-pick hash` | Apply commit |
| `git cherry-pick A B C` | Apply multiple commits |
| `git cherry-pick A..B` | Apply range |
| `git cherry-pick -n hash` | Apply without committing |
| `git cherry-pick -e hash` | Edit message |
| `git cherry-pick -x hash` | Add reference to original |
| `git cherry-pick --continue` | Continue after conflict |
| `git cherry-pick --abort` | Abort operation |
| `git cherry-pick --skip` | Skip current commit |

---

## 💡 Best Practices

1. **Use for hotfixes**: Perfect for applying fixes across branches
2. **Avoid for large changes**: Use merge or rebase instead
3. **Document cherry-picks**: Use `-x` to reference original
4. **Be aware of duplicates**: Cherry-picked commits have new hashes
5. **Test after cherry-picking**: Changes might not work in new context

---

## ⚠️ Caveats

- **Creates duplicate commits**: Different hashes for same changes
- **May cause merge conflicts later**: When branches are merged
- **Loses context**: Doesn't include dependent commits
- **Not for complex features**: Use merge for interconnected changes

---

## 📚 Next Steps

Move to advanced topics like [rebasing](../04-advanced/rebasing.md)!
