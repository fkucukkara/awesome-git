# Git Aliases

Boost your productivity with these useful Git aliases.

---

## ⚙️ How to Set Aliases

### Via Command Line

```bash
git config --global alias.co checkout
git config --global alias.br branch
```

### Via .gitconfig

Edit `~/.gitconfig`:

```ini
[alias]
    co = checkout
    br = branch
```

---

## 🚀 Essential Aliases

Add these to your `~/.gitconfig`:

```ini
[alias]
    # ===== BASICS =====
    s = status
    st = status
    co = checkout
    br = branch
    ci = commit
    cm = commit -m
    cma = commit -am
    
    # ===== BRANCHING =====
    sw = switch
    swc = switch -c
    nb = checkout -b
    bd = branch -d
    bD = branch -D
    
    # ===== STAGING =====
    a = add
    aa = add --all
    ap = add -p
    unstage = restore --staged
    
    # ===== COMMITTING =====
    amend = commit --amend --no-edit
    amendit = commit --amend
    undo = reset --soft HEAD~1
    
    # ===== LOGS =====
    lg = log --oneline --graph --all --decorate
    l = log --oneline -20
    ll = log --oneline
    lp = log -p
    last = log -1 HEAD
    
    # ===== DIFFS =====
    d = diff
    ds = diff --staged
    dc = diff --cached
    
    # ===== STASHING =====
    ss = stash
    sp = stash pop
    sl = stash list
    sa = stash apply
    sd = stash drop
    
    # ===== REMOTES =====
    f = fetch
    pl = pull
    plr = pull --rebase
    ps = push
    psf = push --force-with-lease
    psu = push -u origin HEAD
```

---

## 📜 Logging Aliases

```ini
[alias]
    # Pretty log with graph
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

    # Log with stats
    ls = log --stat --oneline

    # Log with files changed
    lf = log --name-only --oneline

    # Log today's commits
    today = log --since='midnight' --oneline --author='your.email@example.com'

    # Log this week
    week = log --since='1 week ago' --oneline

    # Show commits by author
    who = shortlog -sn --no-merges

    # Find commits by message
    find = log --all --oneline --grep

    # Find commits that changed a string
    search = log -S

    # History of a file
    filelog = log -u
```

---

## 🔄 Workflow Aliases

```ini
[alias]
    # Start new feature
    feature = "!f() { git checkout main && git pull && git checkout -b feature/$1; }; f"
    
    # Start hotfix
    hotfix = "!f() { git checkout main && git pull && git checkout -b hotfix/$1; }; f"
    
    # Sync with main
    sync = "!git checkout main && git pull && git checkout - && git rebase main"
    
    # Update current branch with main
    update = "!git fetch origin && git rebase origin/main"
    
    # Finish feature (merge and delete)
    done = "!f() { git checkout main && git pull && git merge --no-ff @{-1} && git branch -d @{-1}; }; f"
    
    # Publish branch
    publish = "!git push -u origin $(git branch --show-current)"
    
    # Unpublish branch
    unpublish = "!git push origin --delete $(git branch --show-current)"
```

---

## 🧹 Cleanup Aliases

```ini
[alias]
    # Delete merged branches
    cleanup = "!git branch --merged | grep -v '\\*\\|main\\|master' | xargs -n 1 git branch -d"
    
    # Prune remote branches
    prune = fetch --prune
    
    # Remove all local branches except main
    nuke = "!git branch | grep -v 'main' | xargs git branch -D"
    
    # List branches by last commit date
    recent = branch --sort=-committerdate --format='%(committerdate:short) %(refname:short)'
    
    # Show stale branches
    stale = "!git branch -vv | grep ': gone]'"
```

---

## 🔍 Information Aliases

```ini
[alias]
    # Current branch name
    current = branch --show-current
    
    # List all aliases
    aliases = config --get-regexp alias
    
    # Show contributors
    contributors = shortlog -sn
    
    # Show file stats
    stats = diff --stat
    
    # Count lines of code by file type
    cloc = "!git ls-files | xargs wc -l"
    
    # Show root directory
    root = rev-parse --show-toplevel
```

---

## ↩️ Undo Aliases

```ini
[alias]
    # Undo last commit (keep changes)
    uncommit = reset --soft HEAD~1
    
    # Undo last commit (discard changes)
    undohard = reset --hard HEAD~1
    
    # Discard all local changes
    discard = checkout -- .
    
    # Unstage everything
    unstageall = reset HEAD
    
    # Reset to remote state
    resetorigin = "!git fetch origin && git reset --hard origin/$(git branch --show-current)"
```

---

## 🚀 Power Aliases

```ini
[alias]
    # Interactive rebase last n commits
    ri = "!f() { git rebase -i HEAD~$1; }; f"
    
    # Fixup commit (for later squashing)
    fixup = commit --fixup
    
    # Autosquash rebase
    squash = rebase -i --autosquash
    
    # Cherry-pick shorthand
    cp = cherry-pick
    
    # Bisect shortcuts
    bs = bisect start
    bg = bisect good
    bb = bisect bad
    br = bisect reset
    
    # Worktree shortcuts
    wta = worktree add
    wtl = worktree list
    wtr = worktree remove
```

---

## 📊 Visual Aliases

```ini
[alias]
    # Beautiful log graph
    graph = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)'
    
    # Show branch history
    tree = log --graph --oneline --all
    
    # Visual diff
    visual = "!gitk"
```

---

## 📝 Complete .gitconfig Example

```ini
[user]
    name = Your Name
    email = your.email@example.com

[init]
    defaultBranch = main

[core]
    editor = code --wait
    autocrlf = input

[push]
    default = current
    autoSetupRemote = true

[pull]
    rebase = true

[alias]
    # Status
    s = status
    st = status -sb
    
    # Branching
    co = checkout
    sw = switch
    br = branch
    nb = checkout -b
    
    # Commits
    ci = commit
    cm = commit -m
    amend = commit --amend --no-edit
    
    # Staging
    a = add
    aa = add --all
    ap = add -p
    
    # Logs
    lg = log --oneline --graph --all --decorate
    l = log --oneline -15
    last = log -1 HEAD
    
    # Diffs
    d = diff
    ds = diff --staged
    
    # Stash
    ss = stash
    sp = stash pop
    sl = stash list
    
    # Remote
    f = fetch
    pl = pull
    ps = push
    psu = push -u origin HEAD
    psf = push --force-with-lease
    
    # Undo
    undo = reset --soft HEAD~1
    unstage = restore --staged
    discard = checkout -- .
    
    # Workflow
    sync = !git fetch origin && git rebase origin/main
    cleanup = !git branch --merged | grep -v 'main' | xargs git branch -d
    
    # Info
    aliases = config --get-regexp alias
    current = branch --show-current

[color]
    ui = auto
```

---

## 💡 Tips

1. **Start simple**: Add aliases as you need them
2. **Use short names**: `co`, `br`, `cm` for frequent commands
3. **Prefix complex ones**: `feature/`, `sync-`, etc.
4. **Document unusual ones**: Add comments in .gitconfig
5. **Share with team**: Keep aliases in a dotfiles repo

---

**🚀 Copy these to your `.gitconfig` and start being more productive!**
