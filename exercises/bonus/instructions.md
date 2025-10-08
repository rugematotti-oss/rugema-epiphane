# Bonus - Advanced Git Techniques

## 📖 Introduction

Welcome to the advanced Git exercises! 🎉

You've mastered the basics - now it's time to learn the powerful techniques that professional developers use every day. These exercises will teach you how to work with branches, handle complex workflows, and recover from mistakes.

**Prerequisites:** Complete Exercise 01 (Git Basics) first!

---

## 🎯 What You'll Learn

- Creating and managing branches
- Merging branches and resolving conflicts
- Rebasing for cleaner history
- Stashing work in progress
- Undoing changes safely
- Advanced Git commands and workflows

---

## ✅ Exercise 1: Working with Branches

Branches allow you to work on features independently without affecting the main codebase.

### 1.1 Understanding Branches

```bash
# See all branches (you should only have 'main' for now)
git branch

# See which branch you're on
git branch --show-current
```

The `*` symbol indicates your current branch.

### 1.2 Create Your First Branch

Let's create a new feature - adding a skills section to your profile.

```bash
# Create a new branch called 'feature/add-skills'
git branch feature/add-skills

# Switch to the new branch
git checkout feature/add-skills

# Or do both in one command (recommended!)
git checkout -b feature/add-skills
```

**💡 Naming convention:** Use `feature/` for new features, `fix/` for bug fixes, `docs/` for documentation.

### 1.3 Make Changes on Your Branch

Edit `profile.md` and add a new section at the end:

```markdown

## Technical Skills

- **Languages:** Python, JavaScript
- **Tools:** Git, GitHub, VS Code
- **Concepts:** Version control, Clean code
```

### 1.4 Commit on Your Branch

You should know how to commit on your branch by now !

### 1.5 Switch Back to Main

```bash
# Go back to main branch
git checkout main

# Open profile.md - your changes aren't here!
cat profile.md
```

**🤔 What happened?** Your changes are safe on the `feature/add-skills` branch. This is the power of branching!

### 1.6 View All Branches

```bash
# See all branches and their last commits
git branch -v

# See a visual graph
git log --oneline --graph --all
```

---

## ✅ Exercise 2: Merging Branches

Now let's bring your changes back to the main branch.

### 2.1 Merge Your Feature Branch

```bash
# Make sure you're on main
git checkout main

# Merge the feature branch
git merge feature/add-skills
```

If it's a "fast-forward" merge, Git will simply move the main pointer forward. Easy!

### 2.2 Verify the Merge

```bash
# Check profile.md - your skills section should be there!
cat profile.md

# View the history
git log --oneline --graph
```

### 2.3 Delete the Merged Branch

Once merged, you can delete the feature branch:

```bash
# Delete the branch (it's merged, so it's safe)
git branch -d feature/add-skills

# Verify it's gone
git branch
```

### 2.4 Push to GitHub

```bash
git push
```

---

## ✅ Exercise 3: Handling Merge Conflicts

Conflicts happen when the same lines are changed in different branches. Let's create and resolve one!

### 3.1 Create Two Conflicting Branches

**Branch 1: Update title**

```bash
# Create and switch to a new branch
git checkout -b feature/update-title

# Edit profile.md - change the title to "# Developer Profile"
# (edit the first line from "# My Profile" to "# Developer Profile")
```

Edit the file, then:

commit your changes

**Branch 2: Different title update**

```bash
# Go back to main
git checkout main

# Create another branch
git checkout -b feature/better-title

# Edit profile.md - change the title to "# Professional Profile"
# (edit the first line from "# My Profile" to "# Professional Profile")
```

Edit the file, then:

commit your changes

### 3.2 Merge First Branch (No Conflict)

```bash
# Go to main
git checkout main

# Merge the first feature
git merge feature/update-title
```

This should work fine!

### 3.3 Merge Second Branch (CONFLICT!)

```bash
# Try to merge the second feature
git merge feature/better-title
```

**💥 CONFLICT!** Git can't decide which title to use.

### 3.4 Identify the Conflict

```bash
# See the conflict status
git status
```

Git tells you which files have conflicts.

### 3.5 Resolve the Conflict

Open `profile.md` and you'll see something like:

```
<<<<<<< HEAD
# Developer Profile
=======
# Professional Profile
>>>>>>> feature/better-title
```

**How to resolve:**

1. Delete the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
2. Choose which version to keep (or combine them)
3. Save the file

For example, choose a new title:

```markdown
# My Developer Profile
```

### 3.6 Complete the Merge

commit and log your changes

### 3.7 Clean Up

```bash
# Delete both feature branches
git branch -d feature/update-title
git branch -d feature/better-title

# Push to GitHub
git push
```

**🎉 You just resolved your first merge conflict!**

---

## ✅ Exercise 4: Git Stash - Save Work for Later

Sometimes you need to switch branches but your work isn't ready to commit.

### 4.1 Start Working on Something

```bash
# Create a new branch
git checkout -b feature/add-hobbies

# Edit profile.md - add a hobbies section (but don't finish it)
echo -e "\n## Hobbies\n\n- TODO: add hobbies" >> profile.md

# Check status
git status
```

### 4.2 Urgent: Switch to Main (But Work Isn't Ready!)

```bash
# Try to switch branches
git checkout main
```

Git will warn you about uncommitted changes!

### 4.3 Stash Your Changes

```bash
# Save your work temporarily
git stash

# Or with a message
git stash push -m "work in progress on hobbies section"

# Check status - working directory is clean!
git status
```

### 4.4 Switch Branches and Do Other Work

```bash
# Now you can switch
git checkout main

# Your incomplete changes are safely stored
# Do other work here...
```

### 4.5 Return and Restore Your Work

```bash
# Go back to your feature branch
git checkout feature/add-hobbies

# See stashed changes
git stash list

# Restore your work
git stash pop
```

**💡 `git stash pop`** applies the latest stash and removes it from the stash list.

### 4.6 Complete Your Work

Finish editing the hobbies section, then:

```bash
# Edit profile.md to complete the hobbies section and commit your changes
# For example: replace TODO with actual hobbies

# Merge to main
git checkout main
git merge feature/add-hobbies
git branch -d feature/add-hobbies

git push
```

---

## ✅ Exercise 5: Undoing Changes

Mistakes happen! Let's learn how to fix them.

### 5.1 Undo Unstaged Changes

```bash
# Make a change to profile.md (add some random text)
echo "RANDOM MISTAKE" >> profile.md

# Check the change
git diff

# Undo it (restore from last commit)
git restore profile.md

# Or the old way:
# git checkout -- profile.md
```

### 5.2 Unstage Changes (Keep the Changes)

```bash
# Make a change and stage it
echo -e "\n## Contact\n\nemail@example.com" >> profile.md

# Oops, I staged too early! Unstage it
git restore --staged profile.md

# Or the old way:
# git reset HEAD profile.md

# The change is still there, just unstaged
git status
```

### 5.3 Amend the Last Commit

```bash
# Stage and commit (but with a typo in the message, for example "contcat" should be "contact")

# Oops! "contcat" should be "contact"
# Amend the commit message
git commit --amend -m "feat: add contact section"
```

**⚠️ Warning:** Only amend commits that haven't been pushed yet!

### 5.4 Undo the Last Commit (Keep Changes)

```bash
# Undo the last commit but keep the changes
git reset --soft HEAD~1

# Your changes are still staged
git status

# You can now modify and recommit
git commit -m "feat: add contact information"
```

### 5.5 Undo the Last Commit (Discard Changes)

```bash
# Create a test file and commit it
echo "test" > temp.txt

# Completely undo it (⚠️ DANGER: this deletes changes!)
git reset --hard HEAD~1

# temp.txt is gone!
ls temp.txt  # file not found
```

**⚠️ DANGER:** `--hard` deletes all changes. Use with caution!

### 5.6 Push Your Final Changes

```bash
git push
```

---

## ✅ Exercise 6: Git Rebase (Advanced)

Rebasing rewrites history to create a cleaner, linear timeline.

### 6.1 Create a Feature Branch

```bash
# Create a new branch
git checkout -b feature/add-projects

# Add a projects section to profile.md
echo -e "\n## My Projects\n\n- Workshop Git - This repository!" >> profile.md

# commit your changes
```

### 6.2 Simulate Changes on Main

```bash
# Go to main
git checkout main

# Make a change to notes.md
echo -e "\n## Advanced Concepts\n\n- Branching and merging" >> notes.md

# commit your changes
```

### 6.3 Rebase Your Feature Branch

```bash
# Go back to your feature
git checkout feature/add-projects

# Rebase on top of main
git rebase main
```

**What happened?** Git took your feature commits and "replayed" them on top of the latest main.

### 6.4 View the Result

```bash
# See the linear history
git log --oneline --graph --all
```

Notice how your feature branch commits now come AFTER the main branch commits!

### 6.5 Merge (Fast-Forward)

```bash
# Merge into main (will be a fast-forward)
git checkout main
git merge feature/add-projects

# Clean up
git branch -d feature/add-projects

git push
```

**🤔 Rebase vs Merge?**
- **Merge:** Preserves history, shows when branches were merged
- **Rebase:** Creates clean, linear history, but rewrites commits

**⚠️ Golden Rule:** Never rebase commits that have been pushed to a shared repository!

---

## ✅ Exercise 7: Interactive Rebase (Clean Up History)

Interactive rebase lets you edit, combine, or reorder commits.

### 7.1 Create Multiple Commits

```bash
# Create a new branch
git checkout -b feature/cleanup-demo

# Make several small commits
echo "Education: University" >> profile.md
git add profile.md
git commit -m "add education"

echo "Location: France" >> profile.md
git add profile.md
git commit -m "add location"

echo "Languages: French, English" >> profile.md
git add profile.md
git commit -m "add languages"
```

### 7.2 View the Commits

```bash
git log --oneline
```

You should see your three new commits.

### 7.3 Interactive Rebase (Squash Commits)

```bash
# Rebase the last 3 commits interactively
git rebase -i HEAD~3
```

An editor will open showing:

```
pick abc123 add education
pick def456 add location
pick ghi789 add languages
```

**Change it to:**

```
pick abc123 add education
squash def456 add location
squash ghi789 add languages
```

Save and close. Another editor will open for the combined commit message:

```
feat: add personal information (education, location, languages)
```

Save and close.

### 7.4 View the Cleaned History

```bash
git log --oneline
```

Now you have ONE clean commit instead of three!

### 7.5 Merge to Main

```bash
git checkout main
git merge feature/cleanup-demo
git branch -d feature/cleanup-demo

git push
```

---

## ✅ Exercise 8: Advanced Git Log and History

Master Git's powerful history exploration tools.

### 8.1 Pretty Log Formats

```bash
# Compact with graph
git log --oneline --graph --decorate --all

# With dates
git log --oneline --graph --decorate --all --date=short --pretty=format:"%h %ad %s"

# Last 5 commits
git log --oneline -5

# Commits by author
git log --author="Your Name" --oneline
```

### 8.2 Search History

```bash
# Find commits that mention "profile"
git log --grep="profile" --oneline

# Find commits that changed a specific file
git log --oneline -- profile.md

# See what changed in each commit for a file
git log -p profile.md
```

### 8.3 Compare Commits

```bash
# Show changes between two commits
git diff HEAD~2 HEAD

# Show changes in a specific commit
git show HEAD~1
```

### 8.4 Create a Git Alias (Bonus)

Make your life easier with aliases:

```bash
# Create a nice log alias
git config --global alias.lg "log --oneline --graph --decorate --all"

# Now you can use:
git lg
```

---

## ✅ Exercise 9: Working with Remote Branches

Learn to collaborate with remote branches on GitHub.

### 9.1 View Remote Branches

```bash
# See all branches (local and remote)
git branch -a

# See only remote branches
git branch -r
```

### 9.2 Create and Push a New Branch

```bash
# Create a new branch
git checkout -b feature/readme-update

# Make a change to README.md
echo -e "\n## My Progress\n\nCompleted all Git exercises!" >> notes.md

# commit your changes

# Push to GitHub and set upstream
git push -u origin feature/readme-update
```

### 9.3 Fetch Remote Changes

```bash
# See what's on the remote (doesn't download)
git fetch origin

# See all branches again
git branch -a
```

### 9.4 Merge Remote Branch

```bash
# Go to main
git checkout main

# Merge the remote branch
git merge origin/feature/readme-update

# Or pull (fetch + merge in one command)
# git pull origin main
```

### 9.5 Delete Remote Branch

```bash
# Delete the branch locally
git branch -d feature/readme-update

# Delete the branch on GitHub
git push origin --delete feature/readme-update
```

---

## ✅ Exercise 10: Git Cherry-Pick

Apply specific commits from one branch to another.

### 10.1 Create a Feature with Multiple Commits

```bash
# Create a branch
git checkout -b feature/experimental

# Make two distinct changes
echo -e "\n## Achievements\n\n- Git Master" >> profile.md
git add profile.md
git commit -m "feat: add achievements section"

echo -e "\n- Merge Conflict Resolver" >> profile.md
git add profile.md
git commit -m "feat: add second achievement"

# Note the commit hashes
git log --oneline -2
```

### 10.2 Cherry-Pick a Specific Commit

```bash
# Go to main
git checkout main

# Pick only the first commit (replace <hash> with the actual hash)
git cherry-pick <hash-of-first-commit>

# Check profile.md - only the first achievement is there!
```

### 10.3 Clean Up

```bash
# Delete the experimental branch
git branch -D feature/experimental  # -D forces deletion of unmerged branch

git push
```

---

## 🎉 Congratulations!

You've completed the advanced Git exercises! You now know:

✅ **Branching** - Create and manage feature branches  
✅ **Merging** - Combine work from different branches  
✅ **Conflict Resolution** - Handle merge conflicts professionally  
✅ **Stashing** - Save work in progress  
✅ **Undoing Changes** - Fix mistakes safely  
✅ **Rebasing** - Create clean, linear history  
✅ **Interactive Rebase** - Clean up commit history  
✅ **Advanced Logging** - Explore repository history  
✅ **Remote Branches** - Work with GitHub branches  
✅ **Cherry-Picking** - Apply specific commits  

## 📚 Next Steps

You're now equipped with professional Git skills! Here's what you can do next:

1. **Practice on Real Projects** - Apply these techniques in your own repositories
2. **Learn Git Workflows** - Explore Git Flow, GitHub Flow, or Trunk-Based Development
3. **Contribute to Open Source** - Find projects on GitHub and submit pull requests
4. **Master Git Hooks** - Automate tasks with pre-commit and post-commit hooks
5. **Explore Advanced Topics** - Git submodules, subtrees, worktrees

## 🛠️ Essential Commands Summary

### Branching
```bash
git branch                    # List branches
git branch <name>             # Create branch
git checkout <name>           # Switch branch
git checkout -b <name>        # Create and switch
git branch -d <name>          # Delete branch
git branch -D <name>          # Force delete
```

### Merging
```bash
git merge <branch>            # Merge branch
git merge --abort             # Abort merge
```

### Stashing
```bash
git stash                     # Stash changes
git stash list                # List stashes
git stash pop                 # Apply and remove latest stash
git stash apply               # Apply but keep stash
git stash drop                # Remove latest stash
```

### Undoing
```bash
git restore <file>            # Discard changes
git restore --staged <file>   # Unstage file
git reset --soft HEAD~1       # Undo commit, keep changes
git reset --hard HEAD~1       # Undo commit, discard changes
git commit --amend            # Modify last commit
```

### Rebasing
```bash
git rebase <branch>           # Rebase on branch
git rebase -i HEAD~n          # Interactive rebase (n commits)
git rebase --abort            # Abort rebase
git rebase --continue         # Continue after conflict
```

### History
```bash
git log --oneline --graph     # Visual history
git log --grep="text"         # Search commits
git log -- <file>             # File history
git diff <commit1> <commit2>  # Compare commits
git cherry-pick <hash>        # Apply specific commit
```

## 💡 Pro Tips

1. **Commit Often** - Small commits are easier to manage and revert
2. **Branch for Everything** - Create branches for all features and fixes
3. **Pull Before Push** - Always pull latest changes before pushing
4. **Never Rebase Shared Commits** - Only rebase local, unpushed commits
5. **Write Clear Messages** - Future you (and your team) will thank you
6. **Use Git Aliases** - Save time with custom shortcuts
7. **Read Error Messages** - Git's errors are usually helpful
8. **Backup Before Risky Operations** - Create a backup branch before rebasing

## 🎯 Challenge Yourself

Try these scenarios to solidify your knowledge:

1. Create a feature branch, make 5 commits, squash them into 1 using interactive rebase
2. Create two branches with conflicting changes, merge them and resolve conflicts
3. Use stash to switch between multiple features in progress
4. Rebase a feature branch onto an updated main branch
5. Use cherry-pick to apply a single commit from one branch to another

---

**You're now a Git power user! Happy coding!** 🚀🎊

