# Viewing History

Explore your repository's commit history and changes over time.

---

## 📜 Git Log

### Basic Log

```bash
git log
```

Output:
```
commit abc1234567890def (HEAD -> main, origin/main)
Author: Your Name <your.email@example.com>
Date:   Fri Dec 13 10:00:00 2025 +0000

    Add user authentication feature

commit def0987654321abc
Author: Your Name <your.email@example.com>
Date:   Thu Dec 12 15:30:00 2025 +0000

    Initial commit
```

### One Line Per Commit

```bash
git log --oneline
```

Output:
```
abc1234 Add user authentication feature
def0987 Initial commit
```

### With Graph

```bash
git log --oneline --graph
```

### All Branches

```bash
git log --oneline --graph --all
```

### Decorated (Show Branches/Tags)

```bash
git log --oneline --decorate
```

---

## 🔍 Filtering Log

### By Number of Commits

```bash
git log -5  # Last 5 commits
```

### By Author

```bash
git log --author="Your Name"
git log --author="email@example.com"
```

### By Date

```bash
git log --since="2025-01-01"
git log --until="2025-12-31"
git log --since="2 weeks ago"
git log --after="yesterday"
```

### By Commit Message

```bash
git log --grep="bug fix"
git log --grep="feature" --grep="auth" --all-match
```

### By File

```bash
git log -- path/to/file.txt
git log --follow -- path/to/file.txt  # Follow renames
```

### By Content (Pickaxe)

```bash
git log -S "function_name"  # Commits that add/remove this string
git log -G "regex_pattern"  # Commits matching regex
```

---

## 📊 Log Formatting

### Custom Format

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Output:
```
abc1234 - Your Name, 2 hours ago : Add user authentication feature
def0987 - Your Name, 1 day ago : Initial commit
```

### Format Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%H` | Full commit hash |
| `%h` | Abbreviated hash |
| `%an` | Author name |
| `%ae` | Author email |
| `%ar` | Author date (relative) |
| `%ad` | Author date (absolute) |
| `%s` | Subject (first line) |
| `%b` | Body |
| `%d` | Ref names (branches, tags) |

### Show Stats

```bash
git log --stat  # Files changed
git log --shortstat  # Summary only
```

### Show Patches

```bash
git log -p  # Show full diffs
git log -p -2  # Last 2 commits with diffs
```

---

## 🔎 Examining Commits

### Show a Specific Commit

```bash
git show abc1234
```

### Show Specific File from Commit

```bash
git show abc1234:path/to/file.txt
```

### Show Only File Names

```bash
git show --name-only abc1234
```

### Show Status of Each File

```bash
git show --name-status abc1234
```

---

## 📝 Git Blame

See who changed each line of a file:

```bash
git blame filename.txt
```

Output:
```
abc1234 (Author Name 2025-12-13 10:00:00 +0000 1) Line content here
def0987 (Author Name 2025-12-12 15:30:00 +0000 2) Another line here
```

### Blame Specific Lines

```bash
git blame -L 10,20 filename.txt
```

### Ignore Whitespace

```bash
git blame -w filename.txt
```

### Show Commit Message

```bash
git blame -c filename.txt
```

---

## 📈 Shortlog

Summarize commits by author:

```bash
git shortlog
```

### Count Only

```bash
git shortlog -s -n
```

Output:
```
    42  Author One
    28  Author Two
    15  Author Three
```

---

## 🔄 Comparing Changes

### Between Commits

```bash
git diff abc1234 def0987
```

### Between Branches

```bash
git diff main feature-branch
```

### What's in One Branch But Not Another

```bash
git log main..feature-branch
git log feature-branch --not main
```

### Changes Introduced by Branch

```bash
git log main...feature-branch --left-right
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git log` | Show commit history |
| `git log --oneline` | Compact history |
| `git log --graph` | Show branch graph |
| `git log -5` | Last 5 commits |
| `git log --author="name"` | Filter by author |
| `git log -- file` | History of a file |
| `git show commit` | Show commit details |
| `git blame file` | Show line-by-line history |
| `git shortlog -sn` | Commit count by author |

---

## 💡 Useful Aliases

Add these to your Git config:

```bash
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.last "log -1 HEAD"
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
```

---

## 📚 Next Steps

Move to intermediate topics like [stashing](../03-intermediate/stashing.md)!
