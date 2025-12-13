# Commit Conventions

Write consistent, meaningful commit messages for better collaboration.

---

## 📝 Why Conventions Matter

- **Readable history**: Easy to scan and understand
- **Automated changelogs**: Generate release notes automatically
- **Semantic versioning**: Determine version bumps from commits
- **Better collaboration**: Team speaks the same language

---

## 🎯 Conventional Commits

The most popular standard. Format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Examples

```
feat: add user authentication

fix(api): handle null response from server

docs: update installation instructions

feat(auth)!: change login API response format

BREAKING CHANGE: login now returns user object instead of token
```

---

## 📋 Commit Types

| Type | Description | Version Bump |
|------|-------------|--------------|
| `feat` | New feature | Minor |
| `fix` | Bug fix | Patch |
| `docs` | Documentation only | None |
| `style` | Formatting, no code change | None |
| `refactor` | Code change, no feature/fix | None |
| `perf` | Performance improvement | Patch |
| `test` | Adding/fixing tests | None |
| `build` | Build system or dependencies | None |
| `ci` | CI configuration | None |
| `chore` | Other changes (not src/test) | None |
| `revert` | Revert a previous commit | Varies |

---

## 🔍 Anatomy of a Good Commit

### Subject Line

```
feat(auth): add password reset functionality
│    │      │
│    │      └── Description (imperative mood)
│    └── Scope (optional)
└── Type
```

**Rules:**
- Use imperative mood: "add" not "added" or "adds"
- Don't capitalize first letter after colon
- No period at the end
- Max 50-72 characters

### Body (Optional)

```
feat(auth): add password reset functionality

Users can now reset their password via email.
The reset link expires after 24 hours.

Implements a secure token-based reset flow.
```

**Rules:**
- Separate from subject with blank line
- Wrap at 72 characters
- Explain what and why, not how

### Footer (Optional)

```
feat(api): add user preferences endpoint

BREAKING CHANGE: /api/settings renamed to /api/preferences

Closes #123
Refs #456
Co-authored-by: Name <email@example.com>
```

---

## 💥 Breaking Changes

Two ways to indicate:

### 1. Exclamation Mark

```
feat(api)!: change authentication flow
```

### 2. Footer

```
feat(api): change authentication flow

BREAKING CHANGE: JWT tokens now expire after 1 hour
```

---

## 📊 Scope Examples

Common scopes by project type:

### Web Application
```
feat(auth): ...
fix(ui): ...
refactor(api): ...
test(utils): ...
```

### Monorepo
```
feat(frontend): ...
fix(backend): ...
docs(shared): ...
```

### Library
```
feat(parser): ...
fix(validator): ...
perf(core): ...
```

---

## ✍️ Good vs Bad Examples

### ❌ Bad

```
fixed stuff
update
WIP
asdfasdf
changes
fix bug
```

### ✅ Good

```
fix(auth): prevent session timeout during active use
feat(search): add fuzzy matching for product names
docs(readme): add Docker installation steps
refactor(api): extract validation into middleware
test(cart): add edge cases for discount calculation
```

---

## 🔧 Enforcing Conventions

### Commitlint

```bash
# Install
npm install --save-dev @commitlint/cli @commitlint/config-conventional

# Configure
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

### With Husky

```bash
npm install --save-dev husky
npx husky install
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

### Git Hook (Manual)

```bash
#!/bin/bash
# .git/hooks/commit-msg

commit_msg=$(cat "$1")
pattern="^(feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert)(\(.+\))?(!)?: .{1,50}"

if ! echo "$commit_msg" | grep -qE "$pattern"; then
    echo "Error: Invalid commit message format"
    echo "Expected: type(scope): description"
    exit 1
fi
```

---

## 🤖 Automated Changelogs

### Using standard-version

```bash
npm install --save-dev standard-version

# Generate changelog and bump version
npx standard-version
```

### Using semantic-release

```bash
npm install --save-dev semantic-release

# Fully automated releases
npx semantic-release
```

### Sample Generated Changelog

```markdown
## [1.2.0] - 2025-12-13

### Features
- **auth:** add password reset functionality (#123)
- **search:** add fuzzy matching for product names (#125)

### Bug Fixes
- **api:** handle null response from server (#124)

### Breaking Changes
- **auth:** change login API response format
```

---

## 🎨 Templates

### Git Commit Template

Create `.gitmessage`:

```
# <type>(<scope>): <subject>
# |<----  Using a Maximum Of 50 Characters  ---->|

# Explain why this change is being made
# |<----   Try To Limit Each Line to a Maximum Of 72 Characters   ---->|

# Provide links or keys to any relevant tickets, articles or other resources
# Example: Closes #23

# --- COMMIT END ---
# Type can be:
#    feat     (new feature)
#    fix      (bug fix)
#    docs     (changes to documentation)
#    style    (formatting, missing semicolons, etc)
#    refactor (refactoring code)
#    test     (adding tests, refactoring tests)
#    chore    (updating build tasks, etc)
# --------------------
```

Configure:
```bash
git config --global commit.template ~/.gitmessage
```

---

## 🎯 Quick Reference

```
feat:     New feature (minor version bump)
fix:      Bug fix (patch version bump)
docs:     Documentation changes
style:    Code style changes (formatting)
refactor: Code refactoring
perf:     Performance improvements
test:     Adding/updating tests
build:    Build system changes
ci:       CI configuration changes
chore:    Other changes
revert:   Revert previous commit

Breaking changes: Add ! after type or BREAKING CHANGE in footer
```

---

## 💡 Best Practices

1. **Commit early, commit often**: Small, focused commits
2. **One logical change per commit**: Don't mix unrelated changes
3. **Write for your future self**: Be clear and descriptive
4. **Reference issues**: Link to tickets/issues
5. **Use tooling**: Commitlint, templates, hooks
6. **Review before push**: `git log --oneline -5`

---

## 📚 Resources

- [Conventional Commits Spec](https://www.conventionalcommits.org/)
- [Angular Commit Guidelines](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit)
- [Commitlint](https://commitlint.js.org/)
- [Standard Version](https://github.com/conventional-changelog/standard-version)
