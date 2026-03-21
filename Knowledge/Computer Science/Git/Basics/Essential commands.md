## 🧠 Git Essentials — Quick Reference (Obsidian-Friendly)

## 🌱 Getting Started

```Bash
git init                # Initialize a new repository
git clone <url>         # Clone an existing repo
```

## 👤 Configure Your Identity (IMPORTANT)

```Bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Check your config:

```Bash
git config --list
```

👉 Use the same email as your GitHub account for proper commit attribution.

---

## 🔗 GitHub Repository URL (How it Looks)

A typical GitHub repo URL:

```Bash
https://github.com/username/repository-name.git
```

Example:

```Bash
https://github.com/john-doe/my-project.git
```

Two common ways to clone:

**HTTPS (easiest)**

```Bash
git clone https://github.com/username/repository-name.git
```

**SSH (recommended once set up)**

```Bash
git clone git@github.com:username/repository-name.git
```
## 📄 Tracking Changes

```Bash
git status              # Show current changes
git add <file>          # Stage a file
git add .               # Stage all changes
git commit -m "message" # Save snapshot with message
```

## 🔍 Viewing History

```Bash
git log                 # Full commit history
git log --oneline       # Compact history
git diff                # Show unstaged changes
git diff --staged       # Show staged changes
```

## 🌿 Branching & Merging

```Bash
git branch              # List branches
git branch <name>       # Create branch
git checkout <branch>   # Switch branch
git switch <branch>     # (Modern alternative)
git merge <branch>      # Merge into current branch
```

## 🚀 Working with Remote

```Bash
git remote -v           # Show remotes
git push                # Upload changes
git push -u origin main # First push
git pull                # Fetch + merge
git fetch               # Fetch without merging
```

## 🧹 Undo & Fix

```Bash
git restore <file>      # Discard changes (unstaged)
git reset <file>        # Unstage file
git reset --hard        # Reset everything (⚠️ destructive)
git revert <commit>     # Undo commit safely
```

## 🏷️ Tags & Releases

```Bash
git tag                 # List tags
git tag <name>          # Create tag
git push --tags         # Push tags
```

## ⚡ Stashing (Work in Progress)

```Bash
git stash               # Save changes temporarily
git stash pop           # Reapply changes
```

---

## 🚀 How to Push Commits to Remote (Origin)

## 🧭 First-Time Push (New Repository)

After creating commits locally, connect your repo and push:

```bash
git remote add origin https://github.com/username/repository-name.git
git branch -M main
git push -u origin main
```

✅ What happens:

- `origin` = name of the remote repo
    
- `main` = your branch
    
- `-u` = sets upstream (so future pushes are easier)
    

---

## 🔁 Regular Push (After First Time)

Once upstream is set, just run:

```bash
git push
```

---

## 🌿 Pushing a New Branch

```bash
git switch -c feature-branch
git add .
git commit -m "Add new feature"
git push -u origin feature-branch
```

---

## 🔄 If Remote Has New Changes

Always pull first to avoid conflicts:

```bash
git pull origin main
git push
```

---

## ⚠️ Common Issues

### ❌ Rejected Push

If you see:

```
! [rejected] (non-fast-forward)
```

Fix:

```bash
git pull --rebase origin main
git push
```

---

### 🔐 Authentication

- HTTPS → may require token instead of password
    
- SSH → no password once configured
    

---

## 🧠 Simple Mental Flow

```bash
# edit files
git add .
git commit -m "your message"
git push
```

---

✨ _If it’s your first push → use `-u`. After that → just `git push`._

## 💡 Pro Tips

- Commit often, write clear messages
- Use branches for features/fixes
- Pull before pushing to avoid conflicts
- Prefer `git switch` and `git restore` (modern commands)

---

## 🧭 Basic Workflow

```Git
git clone <repo>
git switch -c feature # make changes
git add .
git commit -m "Add feature"
git push -u origin feature
```

---

## 🧩 Mental Model

- **Working Directory** → your files
- **Staging Area** → selected changes
- **Repository** → saved history