# Git Hooks

Automate tasks by running scripts at specific points in the Git workflow.

---

## 🪝 What are Git Hooks?

Hooks are scripts that Git executes automatically before or after specific events like commit, push, or merge. They're stored in `.git/hooks/`.

---

## 📁 Hook Location

```
.git/hooks/
├── pre-commit.sample
├── pre-push.sample
├── commit-msg.sample
└── ... other samples
```

To activate a hook:
1. Remove `.sample` extension
2. Make it executable: `chmod +x .git/hooks/hook-name`

---

## 🔄 Types of Hooks

### Client-Side Hooks

| Hook | When It Runs |
|------|--------------|
| `pre-commit` | Before commit message prompt |
| `prepare-commit-msg` | After default message, before editor |
| `commit-msg` | After message is entered |
| `post-commit` | After commit is complete |
| `pre-push` | Before push to remote |
| `pre-rebase` | Before rebase starts |
| `post-checkout` | After checkout/switch |
| `post-merge` | After merge completes |

### Server-Side Hooks

| Hook | When It Runs |
|------|--------------|
| `pre-receive` | Before any refs are updated |
| `update` | Per branch, before update |
| `post-receive` | After all refs are updated |

---

## 📝 Common Hook Examples

### Pre-commit: Run Tests

```bash
#!/bin/bash
# .git/hooks/pre-commit

echo "Running tests..."
npm test

if [ $? -ne 0 ]; then
    echo "Tests failed. Commit aborted."
    exit 1
fi
```

### Pre-commit: Lint Code

```bash
#!/bin/bash
# .git/hooks/pre-commit

# Get staged files
FILES=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(js|ts)$')

if [ -n "$FILES" ]; then
    echo "Linting staged files..."
    npx eslint $FILES
    
    if [ $? -ne 0 ]; then
        echo "Lint errors found. Fix them before committing."
        exit 1
    fi
fi
```

### Pre-commit: Check for Debug Statements

```bash
#!/bin/bash
# .git/hooks/pre-commit

if git diff --cached | grep -E "(console\.log|debugger|binding\.pry)" > /dev/null; then
    echo "Error: Debug statements found in staged changes."
    echo "Remove them before committing."
    exit 1
fi
```

### Commit-msg: Validate Message Format

```bash
#!/bin/bash
# .git/hooks/commit-msg

commit_msg=$(cat "$1")

# Check for conventional commit format
if ! echo "$commit_msg" | grep -qE "^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}"; then
    echo "Error: Commit message doesn't follow conventional format."
    echo "Expected: type(scope): description"
    echo "Example: feat(auth): add login functionality"
    exit 1
fi
```

### Pre-push: Run Full Test Suite

```bash
#!/bin/bash
# .git/hooks/pre-push

echo "Running full test suite before push..."
npm run test:all

if [ $? -ne 0 ]; then
    echo "Tests failed. Push aborted."
    exit 1
fi
```

### Post-checkout: Install Dependencies

```bash
#!/bin/bash
# .git/hooks/post-checkout

# Check if package.json changed
PREV_HEAD=$1
NEW_HEAD=$2

if git diff --name-only $PREV_HEAD $NEW_HEAD | grep -q "package.json"; then
    echo "package.json changed. Running npm install..."
    npm install
fi
```

### Post-merge: Update Dependencies

```bash
#!/bin/bash
# .git/hooks/post-merge

changed_files="$(git diff-tree -r --name-only --no-commit-id ORIG_HEAD HEAD)"

check_run() {
    echo "$changed_files" | grep -q "$1" && eval "$2"
}

check_run package.json "npm install"
check_run requirements.txt "pip install -r requirements.txt"
```

---

## 🔧 Sharing Hooks

### Problem

`.git/hooks` is not tracked by Git.

### Solution 1: Custom Hooks Directory

```bash
# Store hooks in repo
mkdir .githooks

# Configure Git to use it
git config core.hooksPath .githooks
```

### Solution 2: Use npm package (Husky)

```bash
npm install husky --save-dev
npx husky install

# Add a hook
npx husky add .husky/pre-commit "npm test"
```

### Solution 3: Symbolic Links

```bash
# In repo setup script
ln -s ../../.githooks/pre-commit .git/hooks/pre-commit
```

---

## 🚫 Bypassing Hooks

### Skip Pre-commit and Commit-msg

```bash
git commit --no-verify
# or
git commit -n
```

### Skip Pre-push

```bash
git push --no-verify
```

---

## 🎨 Hook Parameters

### commit-msg

```bash
#!/bin/bash
# $1 = path to temp file with commit message
message=$(cat "$1")
```

### pre-push

```bash
#!/bin/bash
# Receives on stdin: <local ref> <local sha> <remote ref> <remote sha>
while read local_ref local_sha remote_ref remote_sha; do
    # Check what's being pushed
done
```

### post-checkout

```bash
#!/bin/bash
# $1 = ref of previous HEAD
# $2 = ref of new HEAD
# $3 = 1 if branch checkout, 0 if file checkout
```

---

## 🎯 Quick Reference

| Hook | Use Case |
|------|----------|
| `pre-commit` | Lint, test, check formatting |
| `commit-msg` | Validate commit message |
| `pre-push` | Run full tests, check branch |
| `post-checkout` | Install deps, setup env |
| `post-merge` | Update dependencies |

---

## 💡 Best Practices

1. **Keep hooks fast**: Pre-commit should be quick
2. **Make them portable**: Use `/bin/sh` or check for dependencies
3. **Provide skip option**: Document how to bypass if needed
4. **Share with team**: Use Husky or custom hooks directory
5. **Fail loudly**: Clear error messages when hooks fail

---

## 📚 Next Steps

Learn about [submodules](submodules.md) for managing nested repositories!
