## GIT n GITHUB

## GITHUB: 
Github is a cloud-based platform that hosts Git repositories. It allows developers to store, manage, share, and collaborate on code using Git(acts as Central Online Server).
---

## GIT:
Git is a powerful tool that constantly keeps track of every change we make to our files.

1. LOCAL(Own PC)-----> Git
2. REMOTE(Cloud)-----> GitHub

## What GIT records?
1. What Changed
2. When Changed
3. Who Changed
4. Where Changed

## Git's WorkFlow
1. Working Directory
2. Stages:My changes are ready and they can move to next step
3. Local Repository
4. Commit
5. Push

---  

## Note 
1. Any type of files can be committed to GIT
2. Stores different versions of any file.

--- 

## What is a Repository?
A repository is a place where all the versions of a project's files and their complete history of changes are stored.

---

## Note:
(GIT)LOCAL--Store code to remote-->REMOTE(GITHUB)

(GIT)LOCAL<--Pull Code to LOOCAL--REMOTE(GITHUB)

---

# Merge Conflicts

## What is a Merge Conflict?

A **merge conflict** occurs when Git is **unable to automatically merge changes** from two branches because the same part of a file has been modified differently or one branch deletes a file while the other modifies it.

> **Definition:** A merge conflict is a situation where Git cannot automatically decide which changes to keep during a merge. It requires manual intervention from the developer.

---

# Why Do Merge Conflicts Occur?

Merge conflicts usually occur when:

- Two branches modify the same line of a file.
- One branch deletes a file while another branch modifies it.
- Both branches rename the same file differently.
- Both branches add different content to the same file.

---

# Example

### main branch

```python
print("Hello")
```

### feature branch

```python
print("Hello World")
```

When you merge the `feature` branch into `main`, Git doesn't know which version should be kept.

---

# Git Conflict Markers

Git inserts conflict markers inside the file.

```text
<<<<<<< HEAD
print("Hello")
=======
print("Hello World")
>>>>>>> feature
```

### Meaning

- `<<<<<<< HEAD` → Current branch (main)
- `=======` → Separator
- `>>>>>>> feature` → Incoming branch (feature)

---

# How to Resolve a Merge Conflict

### Step 1: Open the conflicted file.

Git inserts conflict markers automatically.

### Step 2: Decide which code to keep.

Choose:
- Current changes
- Incoming changes
- Both changes
- Write your own final version

Example:

```python
print("Hello World!")
```

### Step 3: Remove all conflict markers.

Delete:

```text
<<<<<<< HEAD
=======
>>>>>>> feature
```

### Step 4: Stage the resolved file.

```bash
git add <file-name>
```

### Step 5: Complete the merge.

```bash
git commit
```

or

```bash
git commit -m "Resolve merge conflict"
```

---

# Git Workflow During a Merge Conflict

```text
git merge feature
        │
        ▼
Conflict Detected
        │
        ▼
Open File
        │
        ▼
Resolve Conflict
        │
        ▼
git add .
        │
        ▼
git commit
        │
        ▼
Merge Completed
```

---

# Check Conflicted Files

```bash
git status
```

Example Output:

```text
both modified: app.py
```

---

# Abort a Merge

If you want to cancel the merge:

```bash
git merge --abort
```

This restores the repository to the state before the merge started.

---

# Best Practices to Avoid Merge Conflicts

- Pull the latest changes before starting work.

```bash
git pull origin main
```

- Create separate branches for new features.
- Make small and frequent commits.
- Merge branches regularly.
- Communicate with teammates when working on the same files.
- Review changes before merging using:

```bash
git diff
```

---

# Real-Life Example

Suppose two developers are working on the same file.

Developer A:

```python
discount = 10
```

Developer B:

```python
discount = 15
```

When the branches are merged, Git cannot determine which value is correct. It pauses the merge and asks the developer to resolve the conflict manually.

---

# Interview Definition

> **A merge conflict occurs when Git cannot automatically merge changes from different branches because the same part of a project has been modified in incompatible ways. The developer must manually resolve the conflict before the merge can be completed.**

---

## NOTE:
LOCAL MACHINE---PUSH-->REMOTE REPO

LOCAL MACHINE<--FETCH--REMOTE REPO

LOCAL MACHINE<--PULL-->REMOTE REPO

---

## PUSH:
Sending local changes to remote

---

## FETCH:
Bringing remote chnges into our local repository, but not merging them yet

---

## PULL:
Fetching + merging remote changes, so our working directory immediately reflects the remote changes.

---

## Stash List: 
Newest at the top and oldest at bottom.

---
# Why Do We Use `git rebase`?

## What is `git rebase`?

`git rebase` is used to **move or replay the commits of one branch onto another branch**. It creates a **linear and cleaner commit history** by placing your branch's commits on top of the latest commits from another branch.

> **Definition:** `git rebase` is a Git command that integrates changes from one branch into another by replaying commits, resulting in a clean and linear project history.

---

# Why Do We Use `git rebase`?

We use `git rebase` for the following reasons:

- To keep the commit history clean and linear.
- To update a feature branch with the latest changes from the main branch.
- To avoid unnecessary merge commits.
- To make the project history easier to understand.
- To prepare a branch before merging it into the main branch.

---

# Example

Suppose your repository looks like this:

```text
A ─── B ─── C (main)
       \
        D ─── E (feature)
```

Now, another developer adds a new commit to `main`:

```text
A ─── B ─── C ─── F (main)
       \
        D ─── E (feature)
```

Your `feature` branch is now behind `main`.

Run:

```bash
git switch feature
git rebase main
```

Git moves your commits (`D` and `E`) on top of the latest commit (`F`).

Result:

```text
A ─── B ─── C ─── F ─── D' ─── E' (feature)
```

Notice that `D` and `E` become **new commits** (`D'` and `E'`) because Git replays them on top of `main`.

---

# How `git rebase` Works

```text
Feature Branch
      │
      ▼
Replay each commit
      │
      ▼
Place commits on top of the latest branch
      │
      ▼
Linear commit history
```

---

# Basic Syntax

```bash
git rebase <branch-name>
```

Example:

```bash
git rebase main
```

---

# Difference Between Merge and Rebase

## Merge

```text
      D ─── E
     /       \
A ── B ── C ── F
          \
           Merge Commit
```

History contains an extra merge commit.

---

## Rebase

```text
A ── B ── C ── F ── D' ── E'
```

History is clean and linear.

---

# Advantages of `git rebase`

- Cleaner commit history.
- Easier to read project history.
- No unnecessary merge commits.
- Makes `git log` easier to understand.
- Preferred before creating a Pull Request in many teams.

---

# Disadvantages

- Rewrites commit history.
- Can cause problems if used on commits that have already been shared with others.
- Should be used carefully on public branches.

---

# Important Rule

✅ Safe to rebase:

- Your own local feature branches.

❌ Avoid rebasing:

- Shared branches like `main` after pushing them to GitHub.
- Branches other developers are working on.

---

# Common Commands

Update your feature branch:

```bash
git switch feature
git rebase main
```

Continue after resolving a conflict:

```bash
git rebase --continue
```

Abort the rebase:

```bash
git rebase --abort
```

Skip the current commit during a rebase:

```bash
git rebase --skip
```

---

# Rebase Workflow

```text
Create Feature Branch
        │
        ▼
Write Code
        │
        ▼
New commits added to main
        │
        ▼
git rebase main
        │
        ▼
Resolve conflicts (if any)
        │
        ▼
git rebase --continue
        │
        ▼
Clean commit history
```

---

# Interview Definition

> **`git rebase` is used to integrate changes from one branch into another by replaying commits on top of the latest base commit. It creates a clean, linear commit history and avoids unnecessary merge commits.**

---

## Note:rebase rewrites xommit history even the commit id's are change

---

## Key Difference between git stash pop and git stash apply
1. git stash pop removes our changes from the stash list
2. git stash apply restore our changes but keep them in the stash list for future use.

---

## Git Commands!!

|Commands|Usage|
|--------|-----|
|git --version|Checking the requiremnets|
|cd folder_name|Changing directory|
|mkdir folder_name|Creating folder in the designated directory|
|touch filename|create files in the folder|
|git init|Initialize git|
|git clone https://github.com/Username/repostory.git|clone a repo|
|ls|lis of files|
|ls -la|to show hidden files|
|cd ../|Back to root folder|
|clear|To clear the terminal|
|git status|What changed|
|cd .. | move back to the root directory|
|git add --all|git takes every changes and take it to next commit|
|git add -A|git takes every changes and take it to next commit|
|git reset|back to old files|
|git add .|Stage the changes within the current directory|
|git add *| Stages all the changes except for the deleted file|
|git add * .file_extension|all files with the same extension|
|git commit -m "Commit Message"|Commit the changes|
|git reset HEAD~|Unstagged commit|
|git rm filename|Deleting the file and automatically stagging that files|
|git reset --hard|completely discard the changes|
|git rm -f filename|forcefullt deleted|
|git rm --cached filename|removes the file from stagging area physicall in our working directory|
|git rm -r <FOLDER>|recursively delete the folder as well as contents|
|git log|see the commit history|
|git log --oneline|Commit history in simpler format|
|git branch|which branch we're working|
|git branch branch_name|new branch|
|git checkout branch_name|change branch|
|git merge -=main -m "message"|merge the branch|
|git merge branch_name -m "message"|merging branch_name with 'main'|
|git push origin main|uploaded to github(cloud)|
|git fetch|fetch code from remote|
|git pull|push and pull commands together|
|git restore|revert any files or directory back to its previous state|
|git restore .|undo all changes in the repository|
|git restore --staged|staged some changes using git add .|
|git stash|temporarily set aside our unfinished work, switched to another branch to do make changes|
|git stash pop|The pop command restores the most recently stashed work and simultaneously remove it from the stashed list|
|git stash apply|to store saved changes|
|git stash list|list of stash|
|git stash drop|drop the stash|
|git revert|used to do undo changes in the previous commit, but instead of deleting the old commit, it creates a new commit that reverse those changes|
|git rebase|move or replay the commits of one branch onto another branch|
|git stash apply stash@{1}|To restore a specific stash|


# Pull Requests (PR)

## What is a Pull Request?

A **Pull Request (PR)** is a GitHub feature that allows developers to propose changes made in one branch and request that those changes be reviewed and merged into another branch.

A Pull Request is **not a Git command**. It is a **GitHub collaboration feature** used for code review, discussion, and merging changes.

> **Definition:** A Pull Request is a request to merge changes from one branch into another after they have been reviewed and approved.

---

# Why Do We Use Pull Requests?

Pull Requests are used to:

- Review code before merging.
- Discuss proposed changes with team members.
- Detect bugs before merging.
- Maintain code quality.
- Track changes and discussions.
- Enable collaboration among developers.
- Prevent direct changes to important branches like `main`.

---

# Why are Pull Requests Important?

Without Pull Requests:

```
Developer
    │
    ▼
Push directly to main
    │
    ▼
Code immediately becomes part of the project
```

If the code contains bugs, they immediately affect the project.

---

With Pull Requests:

```
Developer
    │
    ▼
Feature Branch
    │
    ▼
Create Pull Request
    │
    ▼
Code Review
    │
    ▼
Approval
    │
    ▼
Merge into main
```

The code is reviewed before becoming part of the project.

---

# Basic Pull Request Workflow

```
Create Feature Branch
        │
        ▼
Write Code
        │
        ▼
Commit Changes
        │
        ▼
Push Feature Branch
        │
        ▼
Create Pull Request
        │
        ▼
Code Review
        │
        ▼
Resolve Comments (if needed)
        │
        ▼
Merge Pull Request
        │
        ▼
Delete Feature Branch
```

---

# Step-by-Step Example

## Step 1: Create a Branch

```bash
git switch -c feature/login
```

---

## Step 2: Write Code

Example:

```
login.html
login.css
login.js
```

---

## Step 3: Commit Changes

```bash
git add .
git commit -m "Add login page"
```

---

## Step 4: Push Branch

```bash
git push origin feature/login
```

---

## Step 5: Open GitHub

GitHub automatically displays:

```
Compare & pull request
```

Click it.

---

## Step 6: Fill Pull Request Details

### Title

```
Add Login Page
```

### Description

```
Added

- Login UI
- Form validation
- Responsive design
```

---

## Step 7: Create Pull Request

Click

```
Create Pull Request
```

---

## Step 8: Code Review

Team members review your code.

Possible actions:

- Approve
- Request Changes
- Comment

---

## Step 9: Resolve Requested Changes

Example:

Reviewer says:

> Rename variable "a" to "username"

You update the code:

```bash
git add .
git commit -m "Rename variable"
git push
```

The Pull Request updates automatically.

---

## Step 10: Merge Pull Request

Once approved:

Click

```
Merge Pull Request
```

GitHub merges your branch into `main`.

---

# Types of Pull Request Reviews

## 1. Approve

The reviewer accepts the changes.

```
✓ Approved
```

---

## 2. Comment

Reviewer gives suggestions without blocking the merge.

Example:

> Please improve variable names.

---

## 3. Request Changes

Reviewer asks for modifications before approval.

Example:

> Fix validation before merging.

---

# Common Merge Options

## Merge Commit

Creates a merge commit.

```
A──B──C────────M
     \        /
      D──E──F
```

History keeps both branches and a merge commit.

---

## Squash and Merge

Combines all commits into one.

Before:

```
Feature Branch

Commit 1
Commit 2
Commit 3
Commit 4
```

After:

```
One Commit
```

Useful for keeping history clean.

---

## Rebase and Merge

Replays feature branch commits on top of the latest main branch.

```
A──B──C──D──E──F
```

No merge commit is created.

---

# Pull Request vs Merge Request

GitHub:

```
Pull Request (PR)
```

GitLab:

```
Merge Request (MR)
```

They serve the same purpose.

---

# Benefits of Pull Requests

- Better collaboration.
- Code review before merging.
- Fewer bugs.
- Better documentation.
- Easier discussion.
- Cleaner Git history.
- Maintains project quality.

---

# Best Practices

- Create small Pull Requests.
- Write meaningful titles.
- Add a clear description.
- Link related issues if applicable.
- Resolve merge conflicts before requesting review.
- Respond to review comments professionally.
- Delete feature branches after merging.

---

# Real-World Example

Suppose three developers are working on an E-commerce website.

Developer A

```
Adds Login Feature
```

Developer B

```
Adds Shopping Cart
```

Developer C

```
Fixes Bugs
```

Each developer creates a separate branch.

```
main
 │
 ├── feature/login
 ├── feature/cart
 └── bugfix/payment
```

Instead of pushing directly to `main`, each developer creates a Pull Request.

The team reviews each Pull Request before merging it into `main`.

This prevents bugs from reaching the production code and ensures code quality.

---

# Pull Request Workflow Diagram

```
                 GitHub

          main branch
               ▲
               │
        Merge Pull Request
               ▲
               │
      Code Review & Approval
               ▲
               │
      Create Pull Request
               ▲
               │
 git push origin feature/login
               ▲
               │
      git commit -m "Add Login"
               ▲
               │
          Write Code
               ▲
               │
 git switch -c feature/login
```

---

# Interview Definition

> **A Pull Request (PR) is a GitHub feature that allows developers to propose changes from one branch to another for review, discussion, and approval before merging. It helps teams collaborate, maintain code quality, and prevent bugs from being introduced into the main branch.**