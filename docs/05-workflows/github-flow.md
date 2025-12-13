# GitHub Flow

A lightweight, branch-based workflow perfect for continuous deployment.

---

## 🌊 What is GitHub Flow?

GitHub Flow is a simple workflow created by GitHub. It's designed for teams that deploy regularly and practice continuous deployment.

---

## 🔄 The Workflow

```
1. Create a branch from main
2. Make commits
3. Open a Pull Request
4. Discuss and review
5. Deploy and test
6. Merge to main
```

```
main:    ○───────────────●───○
          \             /
feature:   ○───○───○───○
               ↑
           Pull Request
```

---

## 📋 Step-by-Step

### 1. Create a Branch

```bash
git checkout main
git pull origin main
git checkout -b feature/add-user-profile
```

**Branch naming:**
- `feature/description`
- `fix/bug-description`
- `docs/what-changed`
- `refactor/what-improved`

### 2. Make Commits

```bash
# Work on your changes
git add .
git commit -m "Add user profile component"

git add .
git commit -m "Add profile picture upload"

git add .
git commit -m "Add profile edit form"
```

**Commit often** with clear messages.

### 3. Push and Open Pull Request

```bash
git push origin feature/add-user-profile
```

Then on GitHub:
1. Click "Compare & pull request"
2. Write a clear description
3. Request reviewers
4. Link related issues

### 4. Discuss and Review

- Team reviews code
- Automated tests run
- Discussion happens in PR comments
- Make requested changes:

```bash
git add .
git commit -m "Address review feedback"
git push origin feature/add-user-profile
```

### 5. Deploy and Test

Many teams deploy the branch to a staging environment:

```bash
# Example: Deploy to staging
./deploy.sh staging feature/add-user-profile
```

Test the changes in a production-like environment.

### 6. Merge to Main

Once approved and tested:
1. Click "Merge pull request" on GitHub
2. Delete the branch

```bash
# Or from command line
git checkout main
git pull origin main
git merge --no-ff feature/add-user-profile
git push origin main
git branch -d feature/add-user-profile
git push origin --delete feature/add-user-profile
```

---

## 📊 Comparison with Git Flow

| Aspect | GitHub Flow | Git Flow |
|--------|-------------|----------|
| Branches | main + feature | main, develop, feature, release, hotfix |
| Complexity | Simple | Complex |
| Releases | Continuous | Scheduled |
| Best for | Web apps, SaaS | Versioned software |
| Deployment | Every merge | Release branches |

---

## ✅ Rules of GitHub Flow

1. **Main is always deployable**
   - Never push broken code to main
   - All tests must pass

2. **Branch for everything**
   - Create a branch from main for any work
   - Even small changes

3. **Descriptive branch names**
   - Makes it clear what's being worked on
   - Example: `fix/login-timeout-issue`

4. **Push regularly**
   - Backup your work
   - Enable collaboration

5. **Open PR early**
   - Can be draft/WIP
   - Enables early feedback

6. **Merge after review**
   - At least one approval
   - All checks passing

---

## 🔧 Practical Tips

### Keep Main Up to Date

```bash
# Before starting new work
git checkout main
git pull origin main

# While working on a branch
git checkout feature/my-feature
git rebase main
# or
git merge main
```

### Draft Pull Requests

Open a draft PR for work in progress:
- Signals "don't merge yet"
- Gets early feedback
- Shows progress

### Squash Merging

For cleaner history:
```bash
# On GitHub: Use "Squash and merge"
# Or manually:
git checkout main
git merge --squash feature/my-feature
git commit -m "Add user profile (#123)"
```

### Protect Main Branch

Configure on GitHub:
- Require pull request reviews
- Require status checks to pass
- Require up-to-date branches
- Restrict who can push

---

## 🤖 Automation

### CI/CD Integration

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: npm test
```

### Auto-Merge

Enable auto-merge for PRs that pass all checks.

### Deploy on Merge

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to production
        run: ./deploy.sh production
```

---

## 🎯 Quick Reference

```bash
# Start new work
git checkout main
git pull
git checkout -b feature/my-feature

# Work and commit
git add .
git commit -m "Description"

# Push and create PR
git push -u origin feature/my-feature
# Open PR on GitHub

# After merge
git checkout main
git pull
git branch -d feature/my-feature
```

---

## 💡 Best Practices

1. **Small, focused PRs**: Easier to review
2. **Clear PR descriptions**: Explain the why
3. **Link issues**: Connect PRs to issues
4. **Review promptly**: Don't block teammates
5. **Delete merged branches**: Keep it clean
6. **Automate everything**: Tests, linting, deployment

---

## 📚 Next Steps

Learn about [Trunk-Based Development](trunk-based.md) for even faster iteration!
