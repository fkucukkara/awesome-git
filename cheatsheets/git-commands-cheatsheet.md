# Git Commands Cheatsheet

Quick reference for the most commonly used Git commands.

---

## 🚀 Getting Started

| Command | Description |
|---------|-------------|
| `git init` | Create a new repository |
| `git clone <url>` | Clone a repository |
| `git clone --depth 1 <url>` | Shallow clone (latest only) |

---

## ⚙️ Configuration

| Command | Description |
|---------|-------------|
| `git config --global user.name "Name"` | Set username |
| `git config --global user.email "email"` | Set email |
| `git config --list` | List all settings |
| `git config --global core.editor "code --wait"` | Set editor |
| `git config --global init.defaultBranch main` | Set default branch |

---

## 📁 Basic Workflow

| Command | Description |
|---------|-------------|
| `git status` | Check status |
| `git add <file>` | Stage file |
| `git add .` | Stage all changes |
| `git add -p` | Interactive staging |
| `git commit -m "message"` | Commit with message |
| `git commit -am "message"` | Stage tracked & commit |
| `git commit --amend` | Modify last commit |

---

## 🌿 Branching

| Command | Description |
|---------|-------------|
| `git branch` | List local branches |
| `git branch -a` | List all branches |
| `git branch <name>` | Create branch |
| `git switch <name>` | Switch branch |
| `git switch -c <name>` | Create & switch |
| `git checkout <name>` | Switch branch (old) |
| `git checkout -b <name>` | Create & switch (old) |
| `git branch -d <name>` | Delete merged branch |
| `git branch -D <name>` | Force delete branch |
| `git branch -m <new>` | Rename current branch |

---

## 🔀 Merging & Rebasing

| Command | Description |
|---------|-------------|
| `git merge <branch>` | Merge branch |
| `git merge --no-ff <branch>` | Merge with commit |
| `git merge --squash <branch>` | Squash merge |
| `git merge --abort` | Abort merge |
| `git rebase <branch>` | Rebase onto branch |
| `git rebase -i HEAD~3` | Interactive rebase |
| `git rebase --continue` | Continue rebase |
| `git rebase --abort` | Abort rebase |

---

## 📡 Remote Operations

| Command | Description |
|---------|-------------|
| `git remote -v` | List remotes |
| `git remote add origin <url>` | Add remote |
| `git remote remove <name>` | Remove remote |
| `git fetch` | Fetch from remote |
| `git pull` | Pull from remote |
| `git pull --rebase` | Pull with rebase |
| `git push` | Push to remote |
| `git push -u origin <branch>` | Push & set upstream |
| `git push --force-with-lease` | Safe force push |
| `git push origin --delete <branch>` | Delete remote branch |

---

## 📜 History & Diff

| Command | Description |
|---------|-------------|
| `git log` | View history |
| `git log --oneline` | Compact history |
| `git log --graph --all` | Visual history |
| `git log -p` | History with diffs |
| `git log --author="name"` | Filter by author |
| `git log -- <file>` | History of file |
| `git show <commit>` | Show commit details |
| `git diff` | Unstaged changes |
| `git diff --staged` | Staged changes |
| `git diff <a> <b>` | Diff between commits |
| `git blame <file>` | Line-by-line history |

---

## ↩️ Undoing Changes

| Command | Description |
|---------|-------------|
| `git restore <file>` | Discard changes |
| `git restore --staged <file>` | Unstage file |
| `git reset HEAD~1` | Undo last commit (keep changes) |
| `git reset --hard HEAD~1` | Undo last commit (discard) |
| `git revert <commit>` | Revert commit (new commit) |
| `git reflog` | View history of HEAD |

---

## 📦 Stashing

| Command | Description |
|---------|-------------|
| `git stash` | Stash changes |
| `git stash push -m "msg"` | Stash with message |
| `git stash -u` | Include untracked |
| `git stash list` | List stashes |
| `git stash show` | Show stash contents |
| `git stash pop` | Apply & remove stash |
| `git stash apply` | Apply stash (keep it) |
| `git stash drop` | Remove stash |
| `git stash clear` | Remove all stashes |

---

## 🏷️ Tagging

| Command | Description |
|---------|-------------|
| `git tag` | List tags |
| `git tag <name>` | Create lightweight tag |
| `git tag -a <name> -m "msg"` | Create annotated tag |
| `git show <tag>` | Show tag info |
| `git push origin <tag>` | Push tag |
| `git push --tags` | Push all tags |
| `git tag -d <name>` | Delete local tag |
| `git push origin --delete <tag>` | Delete remote tag |

---

## 🍒 Cherry-pick

| Command | Description |
|---------|-------------|
| `git cherry-pick <commit>` | Apply commit |
| `git cherry-pick -n <commit>` | Apply without commit |
| `git cherry-pick --continue` | Continue after conflict |
| `git cherry-pick --abort` | Abort operation |

---

## 🔍 Advanced

| Command | Description |
|---------|-------------|
| `git bisect start` | Start binary search |
| `git bisect bad` | Mark current as bad |
| `git bisect good <commit>` | Mark as good |
| `git bisect reset` | End bisect |
| `git worktree add <path> <branch>` | Create worktree |
| `git worktree list` | List worktrees |
| `git submodule add <url>` | Add submodule |
| `git submodule update --init` | Initialize submodules |

---

## 🧹 Cleanup

| Command | Description |
|---------|-------------|
| `git clean -n` | Preview untracked removal |
| `git clean -f` | Remove untracked files |
| `git clean -fd` | Remove untracked files & dirs |
| `git gc` | Garbage collection |
| `git prune` | Remove unreachable objects |

---

## 📊 Information

| Command | Description |
|---------|-------------|
| `git --version` | Show Git version |
| `git help <command>` | Get help |
| `git shortlog -sn` | Commit count by author |
| `git rev-parse HEAD` | Get current commit hash |
| `git branch --show-current` | Get current branch name |

---

## 🔗 Useful Combinations

```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# See what you're about to push
git log origin/main..HEAD

# Find commits containing specific text
git log -S "search term" --oneline

# Interactive rebase to clean up last 5 commits
git rebase -i HEAD~5

# Stash only staged changes
git stash push --staged

# Create branch from stash
git stash branch new-branch-name

# Diff file between branches
git diff main feature -- path/to/file

# Find when a file was deleted
git log --all --full-history -- path/to/file

# List files changed in commit
git show --name-only <commit>
```

---

**💡 Tip:** Print this cheatsheet or save it for quick reference!
