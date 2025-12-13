# Merging

Combine changes from different branches into one.

---

## 🔀 What is Merging?

Merging integrates changes from one branch into another. There are two types of merges:

### Fast-Forward Merge

When the target branch has no new commits:

```
Before:
main:    ○───○───○
                  \
feature:           ○───○

After (fast-forward):
main:    ○───○───○───○───○
```

### Three-Way Merge

When both branches have new commits:

```
Before:
main:    ○───○───○───○
                  \
feature:           ○───○

After (merge commit):
main:    ○───○───○───○───●
                  \     /
feature:           ○───○
```

---

## 📥 Basic Merge

### Merge a Branch into Current Branch

```bash
# Switch to the target branch
git checkout main

# Merge the feature branch
git merge feature-branch
```

### Merge with Commit Message

```bash
git merge feature-branch -m "Merge feature-branch into main"
```

---

## 🎯 Merge Strategies

### Fast-Forward (Default when possible)

```bash
git merge feature-branch
```

### No Fast-Forward (Always create merge commit)

```bash
git merge --no-ff feature-branch
```

### Fast-Forward Only (Fail if not possible)

```bash
git merge --ff-only feature-branch
```

### Squash Merge (Combine all commits into one)

```bash
git merge --squash feature-branch
git commit -m "Add feature X"
```

---

## ⚠️ Handling Merge Conflicts

### When Conflicts Occur

```bash
git merge feature-branch
```

Output:
```
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Conflict Markers in Files

```
<<<<<<< HEAD
Your current branch changes
=======
Incoming branch changes
>>>>>>> feature-branch
```

### Resolving Conflicts

1. **Open the conflicted file**
2. **Choose which changes to keep** (or combine them)
3. **Remove the conflict markers**
4. **Stage the resolved file**:
   ```bash
   git add file.txt
   ```
5. **Complete the merge**:
   ```bash
   git commit
   ```

### Abort a Merge

```bash
git merge --abort
```

### View Conflicts

```bash
git diff
# or
git status
```

---

## 🛠️ Useful Merge Tools

### Use a Merge Tool

```bash
git mergetool
```

### Configure Merge Tool

```bash
# VS Code
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Configure other tools similarly
```

---

## 📋 Merge Verification

### Preview Merge (Dry Run)

```bash
git merge --no-commit --no-ff feature-branch
# Inspect the result
git merge --abort  # If you don't want to proceed
```

### Check for Merge Conflicts Before Merging

```bash
git merge --no-commit feature-branch
git diff --cached
git merge --abort
```

---

## 🔍 Viewing Merge History

### Show Merge Commits

```bash
git log --merges
```

### Show Graph

```bash
git log --oneline --graph --all
```

### Find Merge Base

```bash
git merge-base main feature-branch
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git merge branch` | Merge branch into current |
| `git merge --no-ff branch` | Always create merge commit |
| `git merge --squash branch` | Squash commits |
| `git merge --abort` | Abort merge |
| `git mergetool` | Open merge tool |

---

## 💡 Best Practices

1. **Pull before merging**: Ensure you have the latest changes
2. **Test after merging**: Run tests to verify the merge
3. **Use `--no-ff` for features**: Preserves branch history
4. **Keep commits atomic**: Easier to resolve conflicts
5. **Communicate with team**: Avoid merging others' work simultaneously

---

## 📚 Next Steps

Learn about [viewing history](viewing-history.md) to understand your project's evolution!
