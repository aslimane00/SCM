🏗️ Professional Git & DevOps Cheat Sheet
# 1. Global Setup & Identity
These should be configured once on every new environment.

```
# Identity
git config --global user.name "Slimane"
git config --global user.email "slimane00@gmail.com"

# Standardize branch naming to 'main'
git config --global init.defaultBranch main

# Handle line endings (Crucial for DevOps/Middleware on Linux)
git config --global core.autocrlf input

# UI and Pruning
git config --global color.ui auto
git config --global fetch.prune true
```
# 2. The Core Workflow
The standard loop for local development and GitHub synchronization.
```
# Start a new repo
git init

# Check status frequently
git status

# Stage and Commit
git add .
git commit -m "feat: detailed message here"

# Linking and Pushing
git remote add origin https://github.com/username/repo.git
git push -u origin main
```
# 3. Branching & Tracking (Exam Priority)
Focus on these for the LPI 701-100 objectives regarding Source Code Management.
```
# Create and switch to a new branch
git switch -c feature/api-setup

# List all branches and their remote correspondence
git branch -vv

# Merge a branch into your current one
git merge feature/api-setup

# Delete a branch (after merging)
git branch -d feature/api-setup
```
# 4. Maintenance & "Save My Work"
Essential for middleware administration and debugging.
```
# Temporarily hide changes to switch tasks
git stash push -m "Debugging JBoss issue"
git stash list
git stash pop

# View a clean, graphical history
git log --oneline --graph --decorate --all

# Inspect a specific file's history
git blame filename.conf
```
# 5. Recovery & Undoing
Standard DevOps "break-glass" commands.
* Undo last commit (keep files)
`git reset --soft HEAD~1`
* Undo last commit (delete files)
`Undo last commit (delete files)`
* Fix the last commit message
`git commit --amend`
* Safe undo on public repo
`git revert <commit-id>`

# 6. Time-Saving Aliases
Add these to your ~/.gitconfig for maximum efficiency.
```
# Set these up once
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br "branch -vv"
git config --global alias.lg "log --oneline --graph --decorate"

# Usage examples:
# git st
# git lg
```