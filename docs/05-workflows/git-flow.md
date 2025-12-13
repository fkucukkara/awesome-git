# Git Flow

A branching model for managing releases and features in larger projects.

---

## 🌊 What is Git Flow?

Git Flow is a branching strategy published by Vincent Driessen in 2010. It defines a strict branching model designed around project releases.

---

## 🌿 Branch Types

### Main Branches (Permanent)

| Branch | Purpose |
|--------|---------|
| `main` | Production-ready code. Every commit is a release. |
| `develop` | Integration branch. Latest development changes. |

### Supporting Branches (Temporary)

| Branch | Created From | Merges Into | Naming |
|--------|--------------|-------------|--------|
| Feature | `develop` | `develop` | `feature/*` |
| Release | `develop` | `main` & `develop` | `release/*` |
| Hotfix | `main` | `main` & `develop` | `hotfix/*` |

---

## 📊 Visual Overview

```
main:     ○───────────○─────────────────○───────○
           \         /                 /       /
release:    \    ○──○                 /       /
             \  /    \               /       /
develop:      ○───○───○───○───○───○───○     /
               \     /   \       /   \     /
feature:        ○───○     ○─────○     \   /
                                       \ /
hotfix:                                 ○
```

---

## 🔧 Setting Up Git Flow

### Using Git Flow Extension

```bash
# Install (macOS)
brew install git-flow

# Install (Windows)
# Included with Git for Windows

# Install (Linux)
apt-get install git-flow
```

### Initialize

```bash
git flow init
```

Prompts:
```
Branch name for production releases: [main]
Branch name for "next release" development: [develop]
Feature branches: [feature/]
Release branches: [release/]
Hotfix branches: [hotfix/]
Support branches: [support/]
Version tag prefix: []
```

---

## 🚀 Feature Workflow

### Start a Feature

```bash
# Using git-flow
git flow feature start user-authentication

# Manual
git checkout develop
git checkout -b feature/user-authentication
```

### Work on Feature

```bash
git add .
git commit -m "Add login form"
git commit -m "Add authentication logic"
```

### Finish Feature

```bash
# Using git-flow
git flow feature finish user-authentication

# Manual
git checkout develop
git merge --no-ff feature/user-authentication
git branch -d feature/user-authentication
```

### Publish Feature (for collaboration)

```bash
git flow feature publish user-authentication

# Or manual
git push origin feature/user-authentication
```

---

## 📦 Release Workflow

### Start a Release

```bash
# Using git-flow
git flow release start 1.0.0

# Manual
git checkout develop
git checkout -b release/1.0.0
```

### Prepare Release

- Fix bugs
- Update version numbers
- Update documentation
- No new features!

```bash
git commit -m "Bump version to 1.0.0"
git commit -m "Update changelog"
```

### Finish Release

```bash
# Using git-flow
git flow release finish 1.0.0

# Manual
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
```

### Push Everything

```bash
git push origin main
git push origin develop
git push origin --tags
```

---

## 🔥 Hotfix Workflow

### Start a Hotfix

```bash
# Using git-flow
git flow hotfix start 1.0.1

# Manual
git checkout main
git checkout -b hotfix/1.0.1
```

### Fix the Issue

```bash
git commit -m "Fix critical security vulnerability"
```

### Finish Hotfix

```bash
# Using git-flow
git flow hotfix finish 1.0.1

# Manual
git checkout main
git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1 -m "Version 1.0.1"
git checkout develop
git merge --no-ff hotfix/1.0.1
git branch -d hotfix/1.0.1
```

---

## 🎯 Quick Reference

| Action | Git Flow Command | Manual Commands |
|--------|------------------|-----------------|
| Start feature | `git flow feature start name` | `git checkout -b feature/name develop` |
| Finish feature | `git flow feature finish name` | merge into develop, delete branch |
| Start release | `git flow release start 1.0.0` | `git checkout -b release/1.0.0 develop` |
| Finish release | `git flow release finish 1.0.0` | merge into main & develop, tag, delete |
| Start hotfix | `git flow hotfix start 1.0.1` | `git checkout -b hotfix/1.0.1 main` |
| Finish hotfix | `git flow hotfix finish 1.0.1` | merge into main & develop, tag, delete |

---

## ✅ Advantages

- Clear structure for releases
- Parallel feature development
- Isolated hotfixes
- Supports scheduled releases
- Great for versioned software

---

## ⚠️ Disadvantages

- Complex for small projects
- Long-lived branches can diverge
- Merge conflicts accumulate
- Not ideal for continuous deployment
- Overhead for simple changes

---

## 💡 When to Use Git Flow

**Good for:**
- Software with explicit versioning (v1.0, v2.0)
- Apps with scheduled releases
- Teams needing structured workflow
- Projects with multiple versions in production

**Not ideal for:**
- Continuous deployment
- Simple projects
- Web apps deployed frequently
- Small teams

---

## 📚 Next Steps

Learn about [GitHub Flow](github-flow.md) for a simpler alternative!
