# Git Worktrees

Work on multiple branches simultaneously without stashing or switching.

---

## 🌳 What are Worktrees?

A worktree is a linked working copy of your repository. Each worktree has its own working directory with a different branch checked out, but they share the same Git history.

```
main-repo/          ← main branch
├── .git/
└── src/

main-repo-feature/  ← feature branch (linked worktree)
└── src/

main-repo-hotfix/   ← hotfix branch (linked worktree)
└── src/
```

---

## ➕ Creating Worktrees

### Create from Existing Branch

```bash
git worktree add ../path/to/worktree branch-name
```

### Create with New Branch

```bash
git worktree add -b new-branch ../path/to/worktree
```

### Create from Specific Commit

```bash
git worktree add ../path/to/worktree abc1234
```

### Examples

```bash
# Work on feature while keeping main clean
git worktree add ../project-feature feature-branch

# Quick hotfix while in middle of feature work
git worktree add ../project-hotfix -b hotfix/urgent-fix main
```

---

## 📋 Listing Worktrees

```bash
git worktree list
```

Output:
```
/home/user/project           abc1234 [main]
/home/user/project-feature   def5678 [feature-branch]
/home/user/project-hotfix    ghi9012 [hotfix/urgent-fix]
```

### With More Details

```bash
git worktree list --porcelain
```

---

## 🗑️ Removing Worktrees

### Remove a Worktree

```bash
git worktree remove ../path/to/worktree
```

### Force Remove (If Dirty)

```bash
git worktree remove --force ../path/to/worktree
```

### Clean Up Stale References

If you manually deleted the worktree directory:

```bash
git worktree prune
```

---

## 🔒 Worktree Locking

Prevent accidental removal:

```bash
# Lock a worktree
git worktree lock ../path/to/worktree

# Lock with reason
git worktree lock --reason "Work in progress" ../path/to/worktree

# Unlock
git worktree unlock ../path/to/worktree
```

---

## 🎯 Use Cases

### 1. Code Review While Working

```bash
# You're working on feature-a
# Need to review feature-b

git worktree add ../project-review feature-b
cd ../project-review
# Review, test, then go back to work
cd ../project
git worktree remove ../project-review
```

### 2. Parallel Development

```bash
# Work on frontend and backend simultaneously
git worktree add ../project-frontend frontend
git worktree add ../project-backend backend
```

### 3. Test on Different Branches

```bash
# Compare behavior across versions
git worktree add ../project-v1 v1.0.0
git worktree add ../project-v2 v2.0.0
```

### 4. Emergency Hotfix

```bash
# Don't interrupt current work
git worktree add -b hotfix/urgent ../project-hotfix main

cd ../project-hotfix
# Fix the issue
git commit -am "Fix critical bug"
git push origin hotfix/urgent

cd ../project
git worktree remove ../project-hotfix
```

---

## 📂 Worktree Structure

Each worktree has:
- Its own working directory
- Its own index (staging area)
- A `.git` file (not directory) pointing to main repo

```bash
cat ../project-feature/.git
# gitdir: /home/user/project/.git/worktrees/project-feature
```

---

## ⚠️ Rules and Limitations

### Can't Check Out Same Branch Twice

```bash
git worktree add ../another main
# fatal: 'main' is already checked out at '/home/user/project'
```

### Shared Objects

All worktrees share:
- `.git` directory (commits, objects)
- Remote configuration
- Hooks

---

## 🔄 Moving Worktrees

```bash
git worktree move ../old-path ../new-path
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git worktree add path branch` | Create worktree |
| `git worktree add -b name path` | Create worktree with new branch |
| `git worktree list` | List all worktrees |
| `git worktree remove path` | Remove worktree |
| `git worktree prune` | Clean stale references |
| `git worktree lock path` | Lock worktree |
| `git worktree move old new` | Move worktree |

---

## 💡 Best Practices

1. **Use clear naming**: `project-feature`, `project-hotfix`
2. **Keep worktrees nearby**: Sibling directories work well
3. **Clean up when done**: Remove worktrees you're finished with
4. **Lock important ones**: Prevent accidental removal
5. **Don't forget commits**: Remember to push from each worktree

---

## 📊 Worktrees vs Alternatives

| Scenario | Worktree | Stash | Clone |
|----------|----------|-------|-------|
| Quick branch switch | ✅ | ✅ | ❌ |
| Parallel work | ✅ | ❌ | ✅ |
| Disk usage | Low | N/A | High |
| Shared history | ✅ | N/A | ❌ |
| Independent repo | ❌ | ❌ | ✅ |

---

## 📚 Next Steps

Explore [workflows](../05-workflows/git-flow.md) for team collaboration!
