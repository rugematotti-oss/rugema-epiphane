# Bonus - Advanced Git Techniques

## Introduction

Welcome to the advanced Git exercises. You've mastered the basics - now it's time to learn techniques used by professional developers.

**Important:** For certain key commands, you'll need to research the solution yourself using Git documentation or online resources. This mirrors real-world development where finding solutions independently is essential.

**Prerequisites:** Complete Exercise 01 (Git Basics) first.

---

## Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Git Reference](https://git-scm.com/docs)
- Command line help: `git <command> --help`

---

## Exercise 1: Working with Branches

### Objective
Learn to create and navigate between branches to work on features independently.

### Tasks

**1.1 Explore Current Branches**

```bash
git branch
```

The `*` indicates your current branch.

---

**1.2 Create Your First Feature Branch**

**RESEARCH TASK:** Find the command to create a new branch called `feature/add-skills` and switch to it.

You can do this in one command or two separate commands.

---

**1.3 Make Changes**

Edit `profile.md` and add:

```markdown

## Technical Skills

- **Languages:** Python, JavaScript
- **Tools:** Git, GitHub, VS Code
- **Concepts:** Version control, Clean code
```

Commit your changes.

---

**1.4 Switch Branches**

**RESEARCH TASK:** Find how to switch back to the `main` branch.

Open `profile.md` - your changes aren't there. They're safe on your feature branch.

---

**1.5 Visualize Branches**

```bash
# See branches with last commits
git branch -v

# Visual graph
git log --oneline --graph --all
```

---

## Exercise 2: Merging Branches

### Objective
Merge your feature branch back into main.

### Tasks

**2.1 Merge Your Feature**

**RESEARCH TASK:** Find how to merge `feature/add-skills` into `main`.

Requirements:
- You must be on the `main` branch first
- Then merge the feature branch

---

**2.2 Clean Up**

**RESEARCH TASK:** Find how to delete the `feature/add-skills` branch after it's merged.

---

**2.3 Push Changes**

```bash
git push
```

---

## Exercise 3: Handling Merge Conflicts

### Objective
Create and resolve merge conflicts.

### Tasks

**3.1 Create Two Conflicting Branches**

Branch 1:
```bash
git checkout -b feature/update-title
```

Edit `profile.md` - change first line from `# My Profile` to `# Developer Profile`

Commit your changes.

Branch 2:
```bash
git checkout main
git checkout -b feature/better-title
```

Edit `profile.md` - change first line from `# My Profile` to `# Professional Profile`

Commit your changes.

---

**3.2 Merge First Branch**

```bash
git checkout main
git merge feature/update-title
```

This should work fine.

---

**3.3 Create the Conflict**

```bash
git merge feature/better-title
```

CONFLICT! Git can't decide which title to keep.

---

**3.4 Understand Conflict Markers**

Open `profile.md`. You'll see:

```
#<<<<<<< HEAD
## Developer Profile
#=======
## Professional Profile
#>>>>>>> feature/better-title
```

- `<<<<<<< HEAD` - Your current branch's version
- `=======` - Separator
- `>>>>>>>` - The incoming branch's version

---

**3.5 Resolve the Conflict**

**RESEARCH TASK:** Find how to resolve the conflict and complete the merge.

Steps needed:
1. Edit the file to choose which version to keep (or write a new one)
2. Remove conflict markers
3. Stage the resolved file
4. Complete the merge

---

**3.6 Clean Up**

Delete both feature branches and push to GitHub.

---

## Exercise 4: Git Stash

### Objective
Save uncommitted work temporarily.

### Scenario

You're working on a feature but need to switch branches urgently. Your work isn't ready to commit.

### Tasks

**4.1 Start Working**

```bash
git checkout -b feature/add-hobbies
```

Add a hobbies section to `profile.md` (but don't finish it). Don't commit yet.

---

**4.2 Try to Switch**

```bash
git checkout main
```

Git won't let you switch with uncommitted changes.

---

**4.3 Stash Your Changes**

**RESEARCH TASK:** Find how to temporarily save your uncommitted changes.

After stashing, you should be able to switch branches.

---

**4.4 Restore Stashed Work**

**RESEARCH TASK:** Find how to restore your stashed changes.

Look for the difference between:
- `git stash apply` - applies stash, keeps it in list
- `git stash pop` - applies stash, removes from list

---

**4.5 Complete Your Work**

Finish the hobbies section, commit, merge to main, and clean up.

---

## Exercise 5: Undoing Changes

### Objective
Learn different ways to undo changes safely.

### Tasks

**5.1 Discard Unstaged Changes**

Make an unwanted change to `profile.md`.

**RESEARCH TASK:** Find how to discard this change and restore the file.

Warning: This permanently deletes your changes.

---

**5.2 Unstage Files**

Make a change, stage it with `git add`.

**RESEARCH TASK:** Find how to unstage the file while keeping the changes.

---

**5.3 Amend Last Commit**

Create a commit with a typo in the message.

**RESEARCH TASK:** Find how to fix the last commit message.

Warning: Only amend commits that haven't been pushed.

---

**5.4 Undo Last Commit**

**RESEARCH TASK:** Find how to undo your last commit while keeping changes staged.

---

**5.5 Hard Reset (Dangerous)**

**RESEARCH TASK:** Find how to completely undo a commit and delete all changes.

Warning: This permanently deletes changes. Very dangerous.

---

## Exercise 6: Git Rebase

### Objective
Create linear history with rebase.

### Understanding Rebase

**RESEARCH TASK:** Research the difference between rebase and merge.

Questions to answer:
- When should you use rebase vs merge?
- What does "rewriting history" mean?
- What's the golden rule of rebasing?

### Tasks

**6.1 Create a Scenario**

```bash
git checkout -b feature/add-projects
```

Add a projects section to `profile.md` and commit.

```bash
git checkout main
```

Make a change to `notes.md` and commit.

Your branches have diverged.

---

**6.2 Rebase Your Feature**

**RESEARCH TASK:** Find how to rebase `feature/add-projects` onto `main`.

---

**6.3 Complete the Rebase**

Merge your feature into main. Notice it's a fast-forward merge.

```bash
git checkout main
git merge feature/add-projects
```

---

## Exercise 7: Interactive Rebase

### Objective
Clean up messy commit history.

### Tasks

**7.1 Create Messy Commits**

```bash
git checkout -b feature/cleanup-demo
```

Make 3 separate commits:
- Add education to `profile.md`
- Add location to `profile.md`
- Add languages to `profile.md`

These could logically be one commit.

---

**7.2 Squash Commits**

**RESEARCH TASK:** Find how to combine (squash) the last 3 commits into 1.

You need to:
1. Start interactive rebase for last 3 commits
2. Change `pick` to `squash` for commits to combine
3. Edit the final commit message

---

**7.3 Complete**

Merge to main, clean up, and push.

---

## Exercise 8: Advanced Git Log

### Tasks

**8.1 Custom Log Formats**

Try these:

```bash
# Graph with all branches
git log --oneline --graph --decorate --all

# Last 5 commits
git log --oneline -5

# Commits by author
git log --author="Your Name"
```

---

**8.2 Search History**

**RESEARCH TASK:** Find how to search for commits containing specific text in the message.

Example: Find all commits mentioning "profile"

---

**8.3 File History**

```bash
# See commits that modified a file
git log -- profile.md

# See actual changes
git log -p profile.md
```

---

**8.4 Create an Alias**

**RESEARCH TASK:** Find how to create a Git alias for a log command you like.

Example: Create `git lg` for a nice graph view.

---

## Exercise 9: Remote Branches

### Tasks

**9.1 View Remote Branches**

```bash
# All branches (local and remote)
git branch -a

# Only remote branches
git branch -r
```

---

**9.2 Push a New Branch**

Create a branch, make changes, commit.

**RESEARCH TASK:** Find how to push this new branch to GitHub and set it as upstream.

---

**9.3 Understanding Fetch vs Pull**

**RESEARCH TASK:** Research the difference between `git fetch` and `git pull`.

---

**9.4 Delete Remote Branch**

**RESEARCH TASK:** Find how to delete a branch from GitHub (remote repository).

---

## Exercise 10: Git Cherry-Pick

### Objective
Apply specific commits from one branch to another.

### Tasks

**10.1 Understanding Cherry-Pick**

**RESEARCH TASK:** Research what cherry-pick does and when it's useful.

---

**10.2 Create a Scenario**

```bash
git checkout -b feature/experimental
```

Make 3 different commits. Note the commit hashes (`git log --oneline`).

---

**10.3 Cherry-Pick a Specific Commit**

You've completed the advanced Git exercises! 
