# Your First Repository

Learn how to create and clone Git repositories.

---

## 🆕 Creating a New Repository

### Initialize a Local Repository

```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git
git init
```

Output:
```
Initialized empty Git repository in /path/to/my-project/.git/
```

### What Happens?

Git creates a hidden `.git` folder containing:
- Repository configuration
- Object database (commits, trees, blobs)
- References (branches, tags)
- Hooks directory

---

## 📥 Cloning an Existing Repository

### Clone via HTTPS

```bash
git clone https://github.com/username/repository.git
```

### Clone via SSH

```bash
git clone git@github.com:username/repository.git
```

### Clone to a Specific Folder

```bash
git clone https://github.com/username/repository.git my-folder-name
```

### Clone a Specific Branch

```bash
git clone -b branch-name https://github.com/username/repository.git
```

### Shallow Clone (Latest Commit Only)

```bash
git clone --depth 1 https://github.com/username/repository.git
```

---

## 📁 Understanding Repository Structure

After `git init` or `git clone`:

```
my-project/
├── .git/                 # Git data (hidden)
│   ├── config            # Repository configuration
│   ├── HEAD              # Current branch reference
│   ├── hooks/            # Git hooks
│   ├── objects/          # Object database
│   └── refs/             # Branch and tag references
├── README.md             # Your files
└── ...                   # Other project files
```

---

## 🔗 Connecting to a Remote

If you created a local repository and want to connect it to GitHub:

```bash
# Add a remote called 'origin'
git remote add origin https://github.com/username/repository.git

# Verify the remote
git remote -v
```

Output:
```
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

---

## 📝 Your First Commit

```bash
# Create a README file
echo "# My Project" > README.md

# Check status
git status

# Stage the file
git add README.md

# Commit
git commit -m "Initial commit"

# Push to remote (first time)
git push -u origin main
```

---

## 🎯 Quick Reference

| Command | Description |
|---------|-------------|
| `git init` | Create a new repository |
| `git clone <url>` | Clone an existing repository |
| `git remote add origin <url>` | Connect to a remote |
| `git remote -v` | View remote connections |
| `git remote remove <name>` | Remove a remote |

---

## 💡 Tips

1. **Use SSH for convenience**: Set up SSH keys to avoid entering passwords
2. **Start with a .gitignore**: Add files to ignore before your first commit
3. **README matters**: Always include a README.md explaining your project

---

## 📚 Next Steps

Learn about the [basic workflow: add, commit, push](../02-basic-commands/add-commit-push.md)!
