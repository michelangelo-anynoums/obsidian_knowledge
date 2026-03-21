
### **YouTube lesson:** https://youtu.be/mJ-qvsxPHpY

### Git Basics – Quick Start Guide

**What is Git?** Git = time machine for your files. It saves versions (snapshots) of your project. You can go back, compare changes, recover deleted work, and work together with others without chaos.

**Most important first 8 commands** (these cover ~80% of daily use)

1. **git config --global user.name "Your Name"**  
2. **git config --global user.email "example.com"** → Tell Git who you are (only once). Commits will show your name/email.
3. **git init** → Create new Git project in current folder. Example:

```
cd my-cool-project
git init
```

4. **git status** → Shows what changed / what is ready to save. Use this command very often!
5. **git add file** or **git add .** → Put file(s) into the "ready to save" area (staging). Examples:

```
git add notes.md           ← only this file
git add .                  ← everything changed
```

6. **git commit -m "short message"** → Save snapshot with a message (like taking a photo). Good messages: "Add homepage layout", "Fix login bug", "Update readme" Example:

```
git commit -m "Create initial project structure"
```

7. **git log** or **git log --oneline** → See history of commits. --oneline makes it short and clean.

8. **git branch git branch new-feature**
	**git checkout new-feature** (or newer: **git switch new-feature**) → Create and move to a new branch (safe place to experiment). Main branch is usually called **main** or **master**.

9. **git add . git commit -m "Finished feature X"** 
	**git checkout main git merge new-feature** → Finish work → go back to main → mix (merge) changes into main.

### Typical daily flow (most common pattern)

text

```
1. git status                  ← always check first
2. Make changes in files
3. git add .                   ← stage everything
4. git commit -m "Fix typo in readme"
5. (later when ready to share) git push
```

### How to connect to GitHub / GitLab (remote)

First time only:

text

```
git remote add origin https://github.com/yourname/your-repo.git
```

Then normal flow becomes:

text

```
git add .
git commit -m "Update dashboard"
git push origin main       ← send to internet
```

Get updates from internet:

text

```
git pull origin main       ← download others' changes
```

### Quick undo helpers (very useful)

- **git restore file** → Throw away changes in one file (back to last commit)
- **git restore .** → Throw away **all** unsaved changes
- Forgot to add message? **git commit --amend -m "Better message"**

### .gitignore file (super important)

Create file called .gitignore in project root. Write names/patterns Git should ignore:

text

```
node_modules/
*.log
.DS_Store
secrets.json
```

Git will never track these.

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Computer Science/Git/Introduction|Introduction]]