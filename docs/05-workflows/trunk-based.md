# Trunk-Based Development

A source control strategy where developers work on a single branch (trunk/main).

---

## 🌳 What is Trunk-Based Development?

Trunk-Based Development (TBD) is a branching model where all developers work on a single branch called "trunk" (or `main`). It emphasizes small, frequent commits and continuous integration.

---

## 🔄 Core Principles

1. **Single shared branch** (trunk/main)
2. **Small, frequent commits** (multiple times per day)
3. **Short-lived feature branches** (if any, max 1-2 days)
4. **Feature flags** for incomplete features
5. **Continuous integration** with automated tests

```
main: ○─○─○─○─○─○─○─○─○─○─○─○─○─○─○
       ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑
       All developers commit here
```

---

## 📊 Two Styles

### 1. Committing Straight to Trunk

For mature teams with excellent CI:

```bash
git checkout main
git pull
# Make small change
git add .
git commit -m "Add validation for email"
git push
```

### 2. Short-Lived Feature Branches

Branches live for hours, max 1-2 days:

```bash
git checkout main
git pull
git checkout -b feature/add-email-validation
# Work for a few hours
git add .
git commit -m "Add email validation"
git push
# Immediately open PR and merge
git checkout main
git pull
git branch -d feature/add-email-validation
```

---

## 🚩 Feature Flags

Hide incomplete features behind flags:

```python
# Python example
if feature_flags.is_enabled('new_checkout_flow'):
    return new_checkout()
else:
    return old_checkout()
```

```javascript
// JavaScript example
if (featureFlags.newUserProfile) {
  return <NewProfilePage />;
} else {
  return <OldProfilePage />;
}
```

### Benefits of Feature Flags

- Commit incomplete code safely
- Gradual rollouts (1%, 10%, 50%, 100%)
- Easy rollback (just flip the flag)
- A/B testing

---

## 🔧 Making It Work

### Prerequisites

1. **Strong CI/CD pipeline**
   - Automated tests
   - Fast builds (< 10 minutes)
   - Automated deployment

2. **Code review process**
   - Pair programming, OR
   - Quick PR reviews

3. **Feature flags infrastructure**
   - For hiding incomplete work

4. **Team discipline**
   - Small commits
   - Don't break the build

---

## 📋 Daily Workflow

### Morning

```bash
git checkout main
git pull
```

### During the Day

```bash
# Small, focused change
git add .
git commit -m "Extract validation logic"
git pull --rebase
git push

# Another small change
git add .
git commit -m "Add unit tests for validation"
git pull --rebase
git push
```

### If Using Short Branches

```bash
git checkout -b feature/quick-fix
# Work for 1-2 hours max
git add .
git commit -m "Fix validation edge case"
git push -u origin feature/quick-fix
# Open PR, get quick review, merge
```

---

## 📊 Comparison

| Aspect | Trunk-Based | GitHub Flow | Git Flow |
|--------|-------------|-------------|----------|
| Main branches | 1 | 1 | 2 |
| Feature branches | None/Short | Yes | Yes |
| Branch lifetime | Hours | Days | Days-Weeks |
| Merge frequency | Very high | High | Low |
| Feature flags | Required | Optional | Rarely |
| Best for | Continuous delivery | Web apps | Versioned releases |

---

## ✅ Advantages

- **Fewer merge conflicts**: No long-lived branches
- **Faster delivery**: Changes go live quickly
- **Better collaboration**: Everyone on same page
- **Simpler model**: Less to understand
- **Continuous integration**: Always integrating

---

## ⚠️ Challenges

- **Requires discipline**: Can't commit broken code
- **Strong CI/CD needed**: Must have good test coverage
- **Feature flags overhead**: Extra infrastructure
- **Cultural shift**: Different from branch-heavy workflows

---

## 🛡️ Protecting Trunk

### Pre-commit Hooks

```bash
#!/bin/bash
# .git/hooks/pre-commit
npm test
npm run lint
```

### Branch Protection (for PR style)

On GitHub:
- Require status checks
- Require up-to-date branch
- Optional: require review

### CI Pipeline

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: npm ci
      - name: Test
        run: npm test
      - name: Lint
        run: npm run lint
```

---

## 🎯 Quick Reference

### Direct to Trunk

```bash
git checkout main
git pull
# Make change
git add .
git commit -m "Small focused change"
git pull --rebase  # Get latest
git push
```

### Short-Lived Branch

```bash
git checkout main
git pull
git checkout -b feature/quick-task
# Work for max 1-2 days
git add .
git commit -m "Complete task"
git push -u origin feature/quick-task
# Open PR → Review → Merge same day
```

---

## 💡 Best Practices

1. **Commit small**: Each commit should be deployable
2. **Commit often**: Multiple times per day
3. **Use feature flags**: For incomplete features
4. **Fast CI**: Keep build under 10 minutes
5. **Review quickly**: Don't let PRs sit
6. **Rebase before push**: Avoid merge commits
7. **Delete branches immediately**: After merging

---

## 🚀 Scaling

### For Larger Teams

- Use short-lived feature branches with PR review
- Implement codeowners for automatic review assignment
- Use merge queues to manage multiple PRs

### For High Traffic

- Implement merge queues
- Use CI caching
- Parallelize tests

---

## 📚 Next Steps

Learn about [commit conventions](commit-conventions.md) for better commit messages!
