# Add, Commit & Push

The fundamental Git workflow for saving and sharing your changes.

---

## 🔄 The Basic Workflow

```
Working Directory → Staging Area → Local Repository → Remote Repository
      |                |                |                  |
   git add          git commit       git push
```

---

## 📦 Staging Changes with `git add`

### Stage a Single File

```bash
git add filename.txt
```

### Stage Multiple Files

```bash
git add file1.txt file2.txt file3.txt
```

### Stage All Changes

```bash
# Stage all changes in current directory and subdirectories
git add .

# Stage all changes in the entire repository
git add -A
# or
git add --all
```

### Stage by Pattern

```bash
# All JavaScript files
git add *.js

# All files in a directory
git add src/
```

### Interactive Staging

```bash
git add -i
# or
git add -p  # Patch mode - stage parts of files
```

---

## ✅ Committing Changes with `git commit`

### Basic Commit

```bash
git commit -m "Your commit message"
```

### Commit with Detailed Message

```bash
git commit
# Opens your default editor for a longer message
```

### Stage and Commit Together

```bash
# Only works for already-tracked files
git commit -am "Your commit message"
```

### Amend the Last Commit

```bash
# Change the commit message
git commit --amend -m "New message"

# Add forgotten files to last commit
git add forgotten-file.txt
git commit --amend --no-edit
```

---

## 📤 Pushing Changes with `git push`

### Push to Remote

```bash
git push origin main
```

### First Push (Set Upstream)

```bash
git push -u origin main
# After this, you can just use: git push
```

### Push All Branches

```bash
git push --all origin
```

### Force Push (Use with Caution!)

```bash
git push --force origin main
# or safer:
git push --force-with-lease origin main
```

---

## 📥 Pulling Changes with `git pull`

### Basic Pull

```bash
git pull origin main
```

### Pull with Rebase

```bash
git pull --rebase origin main
```

### Fetch Without Merging

```bash
git fetch origin
# Then inspect changes before merging
git merge origin/main
```

---

## 🔍 Checking Status

### View Working Directory Status

```bash
git status
```

Output example:
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   newfile.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   existingfile.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        anotherfile.txt
```

### Short Status

```bash
git status -s
```

Output:
```
A  newfile.txt
 M existingfile.txt
?? anotherfile.txt
```

---

## 🔄 Viewing Differences

### Unstaged Changes

```bash
git diff
```

### Staged Changes

```bash
git diff --staged
# or
git diff --cached
```

### Between Commits

```bash
git diff commit1 commit2
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git add <file>` | Stage a file |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit with message |
| `git commit -am "msg"` | Stage tracked files and commit |
| `git push` | Push to remote |
| `git pull` | Pull from remote |
| `git status` | Check status |
| `git diff` | View unstaged changes |

---

## 💡 Best Practices

1. **Commit often**: Small, focused commits are easier to understand and revert
2. **Write meaningful messages**: Explain *why*, not just *what*
3. **Review before committing**: Use `git diff --staged` to check your changes
4. **Pull before push**: Always pull the latest changes before pushing

---

## 📚 Next Steps

Learn about [branching](branching.md) to work on features in isolation!
