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

#chek all configuration
git config --list
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

#Deletes the specified branch from the remote repository
`git push \<remote-name> --delete \<branch-name>`

```
# 4. Maintenance & "Save My Work"
Essential for middleware administration and debugging.
```
# Temporarily hide changes to switch tasks
git stash push -m "Debugging JBoss issue"
git stash list
git stash pop <stash@{n}>
git stash apply <stash@{n}>


# View a clean, graphical history
git log --oneline --graph --decorate --all

#Displays the differences between the working directory and the staging area.
git diff
# Inspect a specific file's history
git blame filename.conf
```
# 5. Recovery & Undoing
Standard DevOps "break-glass" commands.
* Undo last commit (keep files)
`git reset --soft HEAD~1`
* Undo last commit (delete files)
`git reset --hard \<commit-hash>`
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
# list all created aliases
git config --get-regexp alias

# Usage examples:
# git st
# git lg
```
# 7. Git Rebase: Linear History & Cleanup
Rebasing is the process of moving or combining a sequence of commits to a new base commit. In DevOps, this is used to keep a "clean" history without unnecessary merge commits.

* The Standard Rebase (Catching up with Main)
Use this when you are working on a feature branch and main has moved forward. It "replays" your work on top of the latest version of main.
```
# While on your feature branch:
git fetch origin
git rebase origin/main

# If there are conflicts:
# 1. Fix the files
# 2. git add <fixed-files>
# 3. git rebase --continue
```
* Interactive Rebase (Commit Cleanup)
Essential for cleaning up your commit history (squashing "fixup" commits) before pushing to a shared repository.
```
# Clean up the last 3 commits
git rebase -i HEAD~3
```
* The Golden Rule of Rebase
Stop! Never rebase a branch that you have already pushed to a public repository and that other people are working on. You will break their local history and cause a "diverged branch" nightmare.

# 8. Efficiency Shortcut
```
# Pull changes from remote and rebase your local work on top automatically
git pull --rebase origin main
```

# 9. Using cherry-pick (git cherry-pick):

#Applies the changes introduced by <commit-hash> to the current branch.
`git cherry-pick <commit-hash>`

#Applies all commits from \<commit-hash1> to \<commit-hash2> to the current branch, excluding \<commit-hash1>.
`git cherry-pick <commit-hash1>..<commit-hash2>`

# 10. Deleting/cleaning git repository

#Deletes the specified file from the working directory and stages the deletion so that it will be committed.\
`git rm <file-name>`

#Removes the file from the staging area but keeps the file in the working directory.\
`git rm --cached <file-name>`

#Lists all the untracked files and directories that would be deleted if git clean commands are used\
`git clean -n`

#Deletes untracked files from the working directory\
`git clean -f (-d for directory)`

#Deletes all untracked files, including those listed in the file .gitignore.\
`git clean -fx`

# 11. Using git tags 
#Displays a list of all the existing tags in the repository.
`git tag`

#Creates a new tag for the latest commit o for a specific hash
`git tag <tag-name> (<commit-hash>)`

#Creates a tag with some additional message. Annotated tags
include metadata like the tagger’s name, email, and date.
`git tag -a <tag-name> (<commit-hash>) -m "message"`

#Deletes the specified tag from the local Git repository
`git tag -d <tag-name>`

# 12 Exploring Repository History

#Displays a simplified view of the commit history of the current branch with only the commit hash and message, one line per commit.
`git log --oneline`

#Displays the commit history for the specified file in the current branch.
`git log <file-path>`

#This includes the differences (called a patch) introduced by each commit in the commit history
`git log -p`

#Provides a summary of changes in each commit, including file changes and line counts
`git log --stat`

#Displays the reference logs (reflogs) for the current branch. Each log includes an index, the commit hash, and a message describing the change.
`git reflog`

#Displays the reflog entries for the specified branch.
`git reflog <branch-name>`

#Displays a specific entry from the reflog. Replace ref with the reference (e.g., HEAD) and n with the entry number.
`git reflog show ref@{n}`

#Shows who last modified each line of the specified file.
`git blame <file> (<commit>)`

#Shows the blame information for a specific range of lines in a file
`git blame -L <start>,<end> <file>`

#Shows more comprehensive blame information like full commit
messages
`git blame -p <file>`

#Initiates a binary search to pinpoint the commit that introduced a change or a bug. Next, the search range must be specified by marking two commits as good and bad
```
git bisect start
git bisect bad OR git bisect bad <commit-hash>
git bisect good <commit-hash>
git bisect status
git bisect reset
```