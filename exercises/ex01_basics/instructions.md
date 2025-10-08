# Exercise 01 - Git Basics

## 📖 Introduction

Welcome to the first (and main) exercise of this Git workshop! This exercise will guide you through all the essential Git commands and workflows you need to know as a developer.

You'll learn by doing - each step builds on the previous one, and by the end, you'll have a solid understanding of Git fundamentals.

**Estimated time:** 45-60 minutes

---

## 🎯 Learning Objectives

- Configure Git with your identity
- Create and manage files with Git
- Write meaningful commit messages
- Push changes to GitHub
- Review your commit history

---

## ✅ Step 1: Repository Setup & Configuration

### 1.1 Fork and Clone the Repository

First, fork this repository to your own GitHub account, then clone it:

```bash
# Clone your forked repository (replace YOUR-USERNAME with your GitHub username)
git clone https://github.com/YOUR-USERNAME/workshop-git-github.git

# Navigate into the repository
cd workshop-git-github
```

### 1.2 Check Your Git Configuration

Git needs to know who you are to attribute commits correctly:

```bash
# Check your current configuration
git config user.name
git config user.email
```

### 1.3 Configure Git (if needed)

If the commands above don't show your name and email, configure them now:

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email (use the same email as your GitHub account)
git config --global user.email "your.email@example.com"
```

**✨ Tip:** The `--global` flag means this configuration applies to all your Git repositories.

### 1.4 Verify Everything is Working

```bash
# Check the repository status
git status
```

You should see a message like "nothing to commit, working tree clean" (or similar depending on current state).

---

## ✅ Step 2: Your First Commit

Now let's create your first file and make your first commit!

### 2.1 Create Your Profile

```bash
# Copy the template file to create your profile
cp assets/modele_profile.md profile.md
```

### 2.2 Personalize Your Profile

Open `profile.md` in your code editor and:
- Replace `XXXX` with your **first name**
- Replace `YYYY` with your **last name**

Save the file when you're done.

### 2.3 Check What Changed

```bash
# See what Git has detected
git status
```

You should see `profile.md` listed as an "untracked file" - this means Git sees it but isn't tracking it yet.

### 2.4 Stage Your Changes

```bash
# Add the file to the staging area
git add profile.md
```

**What does staging mean?** It's like putting items in a shopping cart before checkout. You're preparing what will be included in your next commit.

### 2.5 Check Status Again

```bash
git status
```

Now `profile.md` should appear as "Changes to be committed" - it's staged and ready!

### 2.6 Create Your First Commit

```bash
# Commit with a clear message
git commit -m "feat: add personal profile"
```

**Note the commit type:** We use `feat:` because we're adding a new feature (your profile).

### 2.7 Push to GitHub

```bash
# Push your changes to GitHub
git push
```

**🎉 Congratulations!** You just made your first proper commit and pushed it to GitHub. Go check your repository on GitHub - you should see your new file!

---

## ✅ Step 3: Making Corrections

Mistakes happen! Let's practice fixing them.

### 3.1 Fix the Typo

Open your `profile.md` file again. You'll notice there's an intentional typo in the template: "I am intrested in programming" should be "I am **interested** in programming".

Fix this typo and save the file.

### 3.2 Check What Changed

```bash
# See the file is modified
git status

# Optional: see the exact changes
git diff
```

**What is `git diff`?** It shows you exactly what changed in your files (additions in green, deletions in red).

### 3.3 Stage and Commit the Fix

```bash
# Stage the correction
git add profile.md

# Commit with a fix message
git commit -m "fix: correct typo in profile description"
```

**Note the commit type:** We use `fix:` because we're correcting an error.

### 3.4 Push Your Correction

```bash
git push
```

---

## ✅ Step 4: Adding Documentation

Good developers document their learning. Let's create a notes file.

### 4.1 Create Your Notes File

```bash
# Create a new file (you can also create it with your editor)
touch notes.md
```

### 4.2 Add Content to Your Notes

Open `notes.md` in your editor and add your learnings. For example:

```markdown
# My Git Learning Notes

## Commands I've Learned

- `git status` - Shows the current state of my repository
- `git add <file>` - Stages a file for commit
- `git commit -m "message"` - Creates a commit with a message
- `git push` - Sends my commits to GitHub
- `git diff` - Shows what changed in my files

## Key Concepts

- **Staging area**: Where I prepare files before committing
- **Commit**: A snapshot of my work at a specific point in time
- **Commit conventions**: Using prefixes like feat:, fix:, docs: to categorize changes
```

Feel free to add your own observations and learnings!

### 4.3 Commit Your Documentation

```bash
# Stage the new file
git add notes.md

# Commit with a docs type
git commit -m "docs: add personal learning notes"

# Push to GitHub
git push
```

**Note the commit type:** We use `docs:` because we're adding documentation.

---

## ✅ Step 5: Cleaning Up

Projects accumulate files. Let's practice removing unnecessary files.

### 5.1 Create a Test File

```bash
# Create a temporary test file
touch test.txt
```

### 5.2 Stage and Commit It (we'll remove it in the next step)

```bash
git add test.txt
git commit -m "chore: add test file"
git push
```

### 5.3 Remove the Test File

```bash
# Remove the file using Git
git rm test.txt

# Check status
git status
```

**Why use `git rm` instead of just deleting the file?** `git rm` deletes the file AND stages the deletion in one command.

### 5.4 Commit the Removal

```bash
git commit -m "chore: remove test file"
git push
```

**Note the commit type:** We use `chore:` for maintenance tasks like cleanup.

---

## ✅ Step 6: Review Your Work

Let's look at everything you've accomplished!

### 6.1 View Your Commit History

```bash
# See a compact log of all commits
git log --oneline
```

You should see all your commits listed with their messages. This is a great way to review what you've done.

### 6.2 View Detailed History

```bash
# See more detailed information
git log
```

This shows:
- Commit hash (unique identifier)
- Author (that's you!)
- Date and time
- Commit message

### 6.3 View a Pretty Graph (optional but cool!)

```bash
# See a visual representation
git log --oneline --graph --decorate
```

---

## ✅ Step 7: Final Documentation

Let's wrap up with one final commit documenting what you've learned.

### 7.1 Update Your Notes

Open `notes.md` again and add a section at the end:

```markdown

## What I Accomplished in This Workshop

- ✅ Configured Git with my identity
- ✅ Created my first commit
- ✅ Fixed mistakes using proper commit messages
- ✅ Added documentation
- ✅ Learned to clean up files properly
- ✅ Reviewed my commit history

## Next Steps

- Practice Git daily in my projects
- Explore branching and merging
- Learn about pull requests
- Contribute to open source projects
```

### 7.2 Final Commit

```bash
# Stage your updated notes
git add notes.md

# Commit your final documentation
git commit -m "docs: document workshop accomplishments"

# Push everything to GitHub
git push
```

### 7.3 Admire Your Work!

Go to your GitHub repository and:
- Check the commit history
- View your `profile.md`
- Read your `notes.md`
- Notice how clean and professional your commit messages are!

---

## 🎉 Congratulations!

You've completed the Git Basics workshop! You now know:

✅ How to configure Git  
✅ How to create meaningful commits  
✅ How to follow commit conventions  
✅ How to push changes to GitHub  
✅ How to review your work with `git log`  
✅ The fundamental Git workflow used by professional developers  

## 📚 What's Next?

Now that you've mastered the basics, you can:

1. **Practice regularly** - Use Git in all your projects
2. **Learn branching** - Create feature branches for new work
3. **Explore merging** - Combine different branches
4. **Try pull requests** - Collaborate with others on GitHub
5. **Contribute to open source** - Apply your skills to real projects

## 🤔 Quick Quiz (Self-Check)

Test your understanding:

1. What's the difference between `git add` and `git commit`?
2. When should you use `feat:` vs `fix:` in commit messages?
3. What command shows you the current status of your repository?
4. How do you push changes to GitHub?
5. What does the staging area do?

If you can answer these questions, you're ready to use Git in real projects!

## 💡 Remember

- **Commit often** - Small, frequent commits are better than large ones
- **Write clear messages** - Your future self (and teammates) will thank you
- **Use `git status` frequently** - It's your best friend when working with Git
- **Don't be afraid to experiment** - You can always undo changes before pushing

---

**Happy coding and happy Git-ing!** 🚀

