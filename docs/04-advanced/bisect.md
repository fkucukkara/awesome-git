# Git Bisect

Binary search through commits to find the one that introduced a bug.

---

## 🔍 What is Bisect?

Git bisect uses binary search to efficiently find the commit that introduced a problem. Instead of checking every commit, it halves the search space each time.

```
100 commits to search → 7 steps maximum (log₂100 ≈ 7)
1000 commits to search → 10 steps maximum
```

---

## 🚀 Basic Bisect Workflow

### 1. Start Bisect

```bash
git bisect start
```

### 2. Mark Current State as Bad

```bash
git bisect bad
# or specify a commit
git bisect bad abc1234
```

### 3. Mark a Known Good Commit

```bash
git bisect good v1.0.0
# or
git bisect good def5678
```

### 4. Test Each Commit

Git checks out a commit in the middle. Test it and mark:

```bash
# If bug exists
git bisect bad

# If bug doesn't exist
git bisect good
```

### 5. Repeat Until Found

Git continues halving until it finds the first bad commit:

```
abc1234 is the first bad commit
commit abc1234
Author: Name <email@example.com>
Date:   Mon Dec 9 10:00:00 2025

    This commit introduced the bug
```

### 6. End Bisect

```bash
git bisect reset
```

---

## 🤖 Automated Bisect

Run a script to test each commit automatically:

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
git bisect run ./test-script.sh
```

### Test Script Requirements

- Exit code 0 = good (bug not present)
- Exit code 1-124, 126, 127 = bad (bug present)
- Exit code 125 = skip (can't test this commit)

### Example Test Script

```bash
#!/bin/bash
# test-script.sh

# Build the project
make || exit 125  # Skip if build fails

# Run specific test
./run-test feature-x
```

### Using npm/pytest/etc.

```bash
git bisect run npm test
git bisect run pytest tests/test_feature.py
git bisect run make test
```

---

## 🔄 Bisect Commands

### Skip a Commit

If you can't test a commit (won't compile, etc.):

```bash
git bisect skip
```

### Skip a Range

```bash
git bisect skip abc1234..def5678
```

### View Bisect Log

```bash
git bisect log
```

### Replay Bisect Session

```bash
git bisect log > bisect.log
# Later...
git bisect replay bisect.log
```

### Visualize Remaining Commits

```bash
git bisect visualize
# or
git bisect view
```

---

## 📊 Bisect Status

### View Progress

```bash
git bisect log
```

Shows:
```
git bisect start
# bad: [abc1234] Commit message
git bisect bad abc1234
# good: [def5678] Commit message
git bisect good def5678
```

### Remaining Steps

Git shows remaining steps:
```
Bisecting: 15 revisions left to test after this (roughly 4 steps)
```

---

## 🎯 Practical Examples

### Find When Test Broke

```bash
git bisect start
git bisect bad                    # Test fails now
git bisect good HEAD~50           # Test passed 50 commits ago
git bisect run npm test -- --grep "failing test"
```

### Find Performance Regression

```bash
#!/bin/bash
# perf-test.sh
time_taken=$(./benchmark.sh | grep "Time:" | awk '{print $2}')
if [ "$time_taken" -gt 1000 ]; then
    exit 1  # Bad - too slow
else
    exit 0  # Good - acceptable
fi

git bisect run ./perf-test.sh
```

### Find When Bug Was Fixed

Reverse good/bad to find when something was fixed:

```bash
git bisect start
git bisect good HEAD              # Bug is fixed now
git bisect bad v1.0.0             # Bug existed then
```

---

## 📋 Terms: Old and New

For situations not involving "bugs":

```bash
git bisect start --term-old=slow --term-new=fast
git bisect fast HEAD
git bisect slow v1.0.0
```

---

## 🔧 Bisect with Merge Commits

Bisect automatically handles complex histories with merges. However, you can skip merge commits:

```bash
git bisect start --first-parent
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git bisect start` | Begin bisect |
| `git bisect bad [commit]` | Mark as bad |
| `git bisect good [commit]` | Mark as good |
| `git bisect skip` | Skip current commit |
| `git bisect reset` | End bisect |
| `git bisect run script` | Automate with script |
| `git bisect log` | Show bisect log |
| `git bisect visualize` | View remaining commits |

---

## 💡 Tips

1. **Start with clear endpoints**: Know a good and bad commit
2. **Make a test script**: Automate when possible
3. **Use exit 125 for untestable**: Don't mark as good/bad if unsure
4. **Bisect on clean tree**: Stash or commit changes first
5. **Save bisect log**: Can replay if interrupted

---

## ⚠️ Common Issues

### Can't Build at Certain Commits

Use `git bisect skip` or exit 125 in scripts.

### Test Takes Too Long

Consider a faster subset of tests targeting the bug.

### Commit Depends on Another

If commits are interdependent, bisect might miss the true cause.

---

## 📚 Next Steps

Learn about [Git hooks](hooks.md) to automate workflows!
