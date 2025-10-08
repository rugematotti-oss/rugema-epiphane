# Solutions - Advanced Git Exercises

This file contains the solutions for all bonus exercises. Use it only after attempting to solve the exercises yourself, or as a reference for instructors.

---

## Exercise 1: Working with Branches

### 1.2 Create Your First Feature Branch

**One command:**
```bash
git checkout -b feature/add-skills
```

**Or modern syntax:**
```bash
git switch -c feature/add-skills
```

**Two separate commands:**
```bash
git branch feature/add-skills
git checkout feature/add-skills
```

### 1.4 Switch Branches

```bash
git checkout main
```

**Or modern syntax:**
```bash
git switch main
```

---

## Exercise 2: Merging Branches

### 2.1 Merge Your Feature

```bash
# Make sure you're on main
git checkout main

# Merge the feature branch
git merge feature/add-skills
```

### 2.2 Clean Up

```bash
# Delete the merged branch
git branch -d feature/add-skills
```

---

## Exercise 3: Handling Merge Conflicts

### 3.5 Resolve the Conflict

**After editing the file to resolve conflicts:**

```bash
# Stage the resolved file
git add profile.md

# Complete the merge (Git will auto-generate message or you can specify)
git commit -m "merge: resolve title conflict between branches"

# Or just
git commit
```

### 3.6 Clean Up

```bash
git branch -d feature/update-title
git branch -d feature/better-title
git push
```

---

## Exercise 4: Git Stash

### 4.3 Stash Your Changes

```bash
# Basic stash
git stash

# Or with a message
git stash push -m "WIP: hobbies section"

# Or using save (older syntax)
git stash save "WIP: hobbies section"
```

### 4.4 Restore Stashed Work

```bash
# Apply and keep in stash list
git stash apply

# Apply and remove from stash list (recommended)
git stash pop

# Apply a specific stash
git stash apply stash@{0}
git stash pop stash@{0}
```

**See stash list:**
```bash
git stash list
```

---

## Exercise 5: Undoing Changes

### 5.1 Discard Unstaged Changes

```bash
# Modern syntax
git restore profile.md

# Old syntax
git checkout -- profile.md
```

### 5.2 Unstage Files

```bash
# Modern syntax
git restore --staged profile.md

# Old syntax
git reset HEAD profile.md
```

### 5.3 Amend Last Commit

```bash
git commit --amend -m "feat: add contact section"

# Or to open editor
git commit --amend
```

### 5.4 Undo Last Commit (Keep Changes Staged)

```bash
# Undo commit, keep changes staged
git reset --soft HEAD~1
```

### 5.5 Hard Reset (Dangerous)

```bash
# Undo commit and DELETE all changes
git reset --hard HEAD~1
```

**Reset types explained:**
- `--soft` - Undo commit, keep changes staged
- `--mixed` (default) - Undo commit, keep changes unstaged
- `--hard` - Undo commit and DELETE all changes

---

## Exercise 6: Git Rebase

### Understanding Rebase

**Rebase vs Merge:**

- **Merge:** Creates a merge commit, preserves history as it happened
- **Rebase:** Rewrites history, creates linear timeline

**When to use:**
- Use **merge** for shared/public branches
- Use **rebase** for local branches to clean up history

**Golden rule:** Never rebase commits that have been pushed to a shared repository

### 6.2 Rebase Your Feature

```bash
# Make sure you're on the feature branch
git checkout feature/add-projects

# Rebase onto main
git rebase main
```

**If there are conflicts during rebase:**
```bash
# After resolving conflicts
git add <resolved-files>
git rebase --continue

# To abort rebase
git rebase --abort
```

---

## Exercise 7: Interactive Rebase

### 7.2 Squash Commits

```bash
# Start interactive rebase for last 3 commits
git rebase -i HEAD~3
```

**In the editor, change from:**
```
pick abc123 add education
pick def456 add location
pick ghi789 add languages
```

**To:**
```
pick abc123 add education
squash def456 add location
squash ghi789 add languages
```

**Or using shorthand:**
```
pick abc123 add education
s def456 add location
s ghi789 add languages
```

Save and close. Another editor will open for the commit message.

**Interactive rebase commands:**
- `pick` (p) - Use commit as is
- `reword` (r) - Use commit, but edit message
- `edit` (e) - Use commit, but stop to amend
- `squash` (s) - Combine with previous commit, edit message
- `fixup` (f) - Combine with previous commit, discard message
- `drop` (d) - Remove commit

---

## Exercise 8: Advanced Git Log

### 8.2 Search History

```bash
# Search for commits with "profile" in message
git log --grep="profile"

# Case insensitive search
git log --grep="profile" -i

# Search in commit content (code changes)
git log -S "profile"
```

### 8.4 Create an Alias

```bash
# Create an alias for nice log graph
git config --global alias.lg "log --oneline --graph --decorate --all"

# Now you can use
git lg
```

**More useful aliases:**
```bash
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.cm "commit -m"
git config --global alias.last "log -1 HEAD"
```

---

## Exercise 9: Remote Branches

### 9.2 Push a New Branch

```bash
# Push and set upstream in one command
git push -u origin feature/branch-name

# Or
git push --set-upstream origin feature/branch-name

# After setting upstream once, just use
git push
```

### 9.3 Understanding Fetch vs Pull

**Fetch:**
```bash
git fetch origin
```
- Downloads changes from remote
- Does NOT merge them
- Safe to run anytime

**Pull:**
```bash
git pull origin main
```
- Downloads changes AND merges them
- Equivalent to: `git fetch` + `git merge`

**Pull is essentially:**
```bash
git fetch origin
git merge origin/main
```

### 9.4 Delete Remote Branch

```bash
# Delete remote branch
git push origin --delete feature/branch-name

# Or using colon syntax
git push origin :feature/branch-name
```

**Delete local branch:**
```bash
git branch -d feature/branch-name
```

---

## Exercise 10: Git Cherry-Pick

### 10.1 Understanding Cherry-Pick

Cherry-pick applies a specific commit from one branch to another without merging the entire branch.

**Use cases:**
- Apply a bug fix from one branch to another
- Pick specific features without merging everything
- Recover commits from deleted branches

### 10.3 Cherry-Pick a Specific Commit

```bash
# Get the commit hash
git log --oneline

# Cherry-pick the specific commit
git cherry-pick <commit-hash>

# Example
git cherry-pick a1b2c3d
```

**If there's a conflict:**
```bash
# After resolving conflicts
git add <resolved-files>
git cherry-pick --continue

# To abort
git cherry-pick --abort
```

**Cherry-pick multiple commits:**
```bash
git cherry-pick <hash1> <hash2> <hash3>
```

**Cherry-pick a range:**
```bash
git cherry-pick <start-hash>..<end-hash>
```

---

## Final Challenge - Complete Solution

```bash
# 1. Create feature branch
git checkout -b feature/final-challenge

# 2. Make 5 commits
echo "change 1" >> file.txt && git add . && git commit -m "commit 1"
echo "change 2" >> file.txt && git add . && git commit -m "commit 2"
echo "change 3" >> file.txt && git add . && git commit -m "commit 3"
echo "change 4" >> file.txt && git add . && git commit -m "commit 4"
echo "change 5" >> file.txt && git add . && git commit -m "commit 5"

# 3. Interactive rebase to squash into 2 commits
git rebase -i HEAD~5
# In editor: keep first 2 as "pick", squash the rest into those

# 4. Rebase onto main
git checkout main
# Make a change on main
echo "main change" >> notes.md && git add . && git commit -m "update notes"
git checkout feature/final-challenge
git rebase main

# 5. Create and resolve merge conflict
git checkout main
git checkout -b feature/conflict-branch
# Edit same file as feature/final-challenge
git add . && git commit -m "conflicting change"
git checkout main
git merge feature/final-challenge  # This works
git merge feature/conflict-branch  # This conflicts
# Resolve conflict, then:
git add .
git commit -m "merge: resolve conflict"

# 6. Use stash
git checkout -b feature/stash-demo
echo "incomplete work" >> temp.txt
git stash
git checkout main
git checkout feature/stash-demo
git stash pop

# 7. Cherry-pick a commit
git log --oneline  # Find a commit hash
git checkout main
git cherry-pick <commit-hash>

# 8. Clean up all branches
git branch -d feature/final-challenge
git branch -d feature/conflict-branch
git branch -d feature/stash-demo

# 9. Push to GitHub
git push
```

---

## Common Issues and Solutions

### Issue: Can't switch branches (uncommitted changes)

**Solution:**
```bash
# Option 1: Commit changes
git add .
git commit -m "WIP"

# Option 2: Stash changes
git stash

# Option 3: Discard changes (dangerous!)
git restore .
```

### Issue: Merge conflict

**Solution:**
```bash
# 1. Open conflicted files
# 2. Edit to resolve (remove markers: <<<<, ====, >>>>)
# 3. Stage resolved files
git add <file>
# 4. Complete merge
git commit
```

### Issue: Accidentally committed to wrong branch

**Solution:**
```bash
# On wrong branch
git log  # Copy the commit hash

# Switch to correct branch
git checkout correct-branch
git cherry-pick <commit-hash>

# Go back and remove from wrong branch
git checkout wrong-branch
git reset --hard HEAD~1
```

### Issue: Need to undo last pushed commit

**Solution (if working alone):**
```bash
git reset --hard HEAD~1
git push --force
```

**Solution (if working with others):**
```bash
git revert HEAD
git push
```

### Issue: Lost commits after reset

**Solution (use reflog):**
```bash
# Find lost commit
git reflog

# Restore it
git reset --hard <commit-hash>
```

---

## Useful Commands Reference

### Branch Management
```bash
git branch                    # List local branches
git branch -a                 # List all (local + remote)
git branch -d <name>          # Delete branch (safe)
git branch -D <name>          # Force delete branch
git branch -m <old> <new>     # Rename branch
```

### Stash Management
```bash
git stash                     # Stash changes
git stash list                # List all stashes
git stash pop                 # Apply and remove latest
git stash apply               # Apply but keep in list
git stash drop                # Remove latest stash
git stash clear               # Remove all stashes
git stash show -p             # Show stash contents
```

### Reset Types
```bash
git reset --soft HEAD~1       # Undo commit, keep staged
git reset --mixed HEAD~1      # Undo commit, keep unstaged (default)
git reset --hard HEAD~1       # Undo commit, delete changes
```

### Rebase
```bash
git rebase main               # Rebase current branch onto main
git rebase -i HEAD~n          # Interactive rebase last n commits
git rebase --continue         # Continue after resolving conflicts
git rebase --abort            # Abort rebase
git rebase --skip             # Skip current commit
```

### Advanced Log
```bash
git log --oneline             # Compact format
git log --graph               # Show graph
git log --all                 # All branches
git log -p                    # Show patches (diffs)
git log --since="2 weeks ago" # Filter by date
git log --author="Name"       # Filter by author
git log --grep="text"         # Search commit messages
git log -S "code"             # Search code changes
git log -- <file>             # History of specific file
```

### Remote Operations
```bash
git remote -v                 # List remotes
git fetch origin              # Download from remote
git pull origin main          # Fetch + merge
git push -u origin branch     # Push and set upstream
git push origin --delete br   # Delete remote branch
```

### Other Useful Commands
```bash
git cherry-pick <hash>        # Apply specific commit
git revert <hash>             # Undo commit with new commit
git reflog                    # Show all ref changes (recover lost commits)
git clean -fd                 # Remove untracked files (dangerous!)
git diff HEAD~1 HEAD          # Compare commits
git show <hash>               # Show commit details
git blame <file>              # See who changed each line
```

---

## Pro Tips

1. **Always check status:** `git status` before any operation
2. **Create backup branch:** `git branch backup` before risky operations
3. **Use aliases:** Speed up common commands
4. **Read error messages:** Git tells you what to do
5. **Commit often:** Small commits are easier to manage
6. **Never force push to shared branches:** Use `git push --force-with-lease` if absolutely necessary
7. **Use `--dry-run`:** Test commands safely (e.g., `git clean -fd --dry-run`)
8. **Learn reflog:** Your safety net for recovering lost commits

---

This solutions file should be used as a reference. The best way to learn is by doing and making mistakes!

