# Rebasing

Reapply commits on top of another base commit for a cleaner history.

---

## 🔄 What is Rebasing?

Rebasing moves or combines commits to a new base commit. It rewrites commit history to create a linear progression.

```
Before:
main:    ○───○───○───M
              \
feature:       A───B───C

After rebase:
main:    ○───○───○───M
                      \
feature:               A'──B'──C'
```

---

## 📥 Basic Rebase

### Rebase Current Branch onto Another

```bash
git checkout feature
git rebase main
```

### Rebase onto Specific Commit

```bash
git rebase abc1234
```

---

## 🔀 Rebase vs Merge

| Aspect | Rebase | Merge |
|--------|--------|-------|
| History | Linear | Preserves branches |
| Commit hashes | Changed | Preserved |
| Safe for shared branches | ❌ | ✅ |
| Cleaner history | ✅ | ❌ |
| Shows true development | ❌ | ✅ |

### When to Rebase

- Local branches before pushing
- Feature branches before merging
- Cleaning up commits before PR

### When to Merge

- Shared/public branches
- When history preservation matters
- Collaborative feature branches

---

## ⚙️ Interactive Rebase

The most powerful rebase feature. Edit, reorder, squash, or drop commits.

### Start Interactive Rebase

```bash
# Last 3 commits
git rebase -i HEAD~3

# From specific commit
git rebase -i abc1234
```

### Interactive Commands

Your editor opens with:
```
pick abc1234 First commit message
pick def5678 Second commit message
pick ghi9012 Third commit message

# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like squash, but discard this commit's message
# d, drop = remove commit
# x, exec = run command
```

### Common Operations

#### Squash Commits

```
pick abc1234 Add feature
squash def5678 Fix typo
squash ghi9012 Add tests
```

Result: One commit with combined changes.

#### Reword Commit Message

```
reword abc1234 Old message to fix
pick def5678 Keep this one
```

#### Reorder Commits

```
pick def5678 This goes first now
pick abc1234 This was first, now second
```

#### Drop a Commit

```
pick abc1234 Keep this
drop def5678 Remove this
pick ghi9012 Keep this too
```

#### Edit a Commit

```
edit abc1234 Stop here to make changes
pick def5678 Continue with this
```

Then:
```bash
# Make your changes
git add .
git commit --amend
git rebase --continue
```

---

## ⚠️ Handling Rebase Conflicts

When conflicts occur:

```bash
git rebase main
# CONFLICT: Merge conflict in file.txt
```

### Resolve and Continue

```bash
# 1. Resolve conflicts in the file
# 2. Stage resolved files
git add file.txt

# 3. Continue rebase
git rebase --continue
```

### Abort Rebase

```bash
git rebase --abort
```

### Skip Current Commit

```bash
git rebase --skip
```

---

## 🔄 Rebase Options

### Preserve Merge Commits

```bash
git rebase --rebase-merges main
# or short form
git rebase -r main
```

### Autosquash

If you have commits with messages starting with "fixup!" or "squash!":

```bash
git rebase -i --autosquash main
```

### Autostash

Automatically stash and reapply local changes:

```bash
git rebase --autostash main
```

---

## 📤 Rebasing and Pushing

After rebasing, you need to force push:

```bash
git push --force-with-lease origin feature
```

`--force-with-lease` is safer than `--force`:
- Fails if remote has new commits you haven't seen
- Prevents accidentally overwriting others' work

---

## 🔧 Recovering from Rebase Mistakes

### Using Reflog

```bash
# Find the state before rebase
git reflog

# Reset to that state
git reset --hard HEAD@{5}
```

### Using ORIG_HEAD

```bash
# Immediately after a rebase
git reset --hard ORIG_HEAD
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git rebase main` | Rebase onto main |
| `git rebase -i HEAD~3` | Interactive rebase last 3 |
| `git rebase --continue` | Continue after conflict |
| `git rebase --abort` | Abort rebase |
| `git rebase --skip` | Skip current commit |
| `git push --force-with-lease` | Safe force push |

---

## 💡 Best Practices

1. **Never rebase public branches**: Only rebase local/private branches
2. **Rebase before merging**: Keep feature branch updated
3. **Use interactive rebase to clean up**: Squash WIP commits
4. **Use `--force-with-lease`**: Safer than `--force`
5. **Test after rebasing**: Ensure code still works

---

## 🎨 Example Workflow

```bash
# Working on a feature branch
git checkout feature-x

# Periodically update from main
git fetch origin
git rebase origin/main

# Before opening PR, clean up commits
git rebase -i origin/main
# Squash WIP commits, reword messages

# Push (first time or after rebase)
git push --force-with-lease origin feature-x
```

---

## 📚 Next Steps

Learn about [reflog](reflog.md) to recover from mistakes!
