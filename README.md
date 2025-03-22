# Git Essentials - Complete Guide

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Creating a Repository](#creating-a-repository)
- [Basic Git Workflow](#basic-git-workflow)
- [Commit Message Conventions](#commit-message-conventions)
- [Branch Management](#branch-management)
- [Pull Requests](#pull-requests)
- [Resolving Conflicts](#resolving-conflicts)
- [Best Practices](#best-practices)
- [Useful Git Commands](#useful-git-commands)

## Introduction

Git is a distributed version control system that allows developers to track changes in their code, collaborate with others, and maintain a history of their project. This guide provides essential Git commands and best practices for effective version control.

## Installation

### Linux
```bash
# Debian/Ubuntu
sudo apt-get install git

# Fedora
sudo dnf install git

# Arch Linux (btw)
sudo pacman -S git
```

### macOS
```bash
# Using Homebrew
brew install git

# Or download the installer from https://git-scm.com/download/mac
```

### Windows
Download and install from https://git-scm.com/download/win

### Configuration
```bash
# Set your username
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"
```

## Creating a Repository

### Initialize a New Repository
```bash
# Navigate to your project directory
cd /path/to/your/project

# Initialize a new Git repository
git init
```

### Clone an Existing Repository
```bash
# Clone a repository from GitHub/GitLab/etc.
git clone https://github.com/username/repository.git

# Clone to a specific folder
git clone https://github.com/username/repository.git my-folder
```

## Basic Git Workflow

### Checking Status
```bash
# View the status of your working directory
git status
```

### Adding Files
```bash
# Add a specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.txt

# Add all files in the current directory
git add .

# Add all files with a specific extension
git add *.js
```

### Committing Changes
```bash
# Commit with a message
git commit -m "Add feature X"

# Add and commit in one command (only for tracked files)
git commit -am "Fix bug in feature X"
```

### Viewing History
```bash
# View commit history
git log

# View compact history
git log --oneline

# View history with changes
git log -p

# View history with graph
git log --graph --oneline --all
```

## Commit Message Conventions

A good commit message clearly communicates what changes were made and why. A widely used format is:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation changes
- **style**: Code style changes (formatting, semicolons, etc.)
- **refactor**: Code changes that neither fix bugs nor add features
- **perf**: Performance improvements
- **test**: Adding or fixing tests
- **chore**: Changes to the build process, auxiliary tools, etc.

### Example
```
feat(auth): implement login functionality

Add login form and authentication service to allow users to log in
with email and password.

Closes #123
```

### Best Practices for Commit Messages
1. Keep the subject line under 50 characters
2. Capitalize the subject line
3. Do not end the subject line with a period
4. Use imperative mood in the subject line
5. Separate subject from body with a blank line
6. Wrap the body at 72 characters
7. Use the body to explain what and why vs. how

## Branch Management

### Creating Branches
```bash
# Create a new branch
git branch branch-name

# Create and switch to a new branch
git checkout -b branch-name

# Using the newer switch command (Git 2.23+)
git switch -c branch-name
```

### Switching Branches
```bash
# Switch to an existing branch
git checkout branch-name

# Using the newer switch command
git switch branch-name
```

### Listing Branches
```bash
# List local branches
git branch

# List remote branches
git branch -r

# List all branches (local and remote)
git branch -a
```

### Branching Strategies

#### Git Flow
A robust branching model with specific branches for different purposes:
- **main/master**: Production-ready code
- **develop**: Latest development changes
- **feature/**: New features
- **release/**: Preparing for a release
- **hotfix/**: Quick fixes for production

![Git Flow](https://nvie.com/img/git-model@2x.png)

#### GitHub Flow
A simpler approach:
- **main**: Always deployable
- **feature branches**: For all changes

#### Trunk-Based Development
An even simpler approach with short-lived feature branches merging frequently to main/trunk.

### Merging
```bash
# Switch to the target branch
git checkout main

# Merge a branch into the current branch
git merge feature-branch

# Merge with no fast-forward (creates a merge commit)
git merge --no-ff feature-branch
```

### Rebasing
```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase (for cleaning up commits)
git rebase -i HEAD~3  # Rebase the last 3 commits
```

## Pull Requests

Pull Requests (PRs) are a way to propose changes to a repository. They're central to how teams collaborate on GitHub, GitLab, and similar platforms.

### Creating a Pull Request

1. **Push your branch to the remote repository**
   ```bash
   git push origin feature-branch
   ```

2. **Go to the repository on GitHub/GitLab**
   - Click "New pull request" or "Create merge request"
   - Select your branch as the source and the target branch (e.g., main)
   - Add a title and description
   - Submit the PR

### PR Best Practices

1. **Keep PRs small and focused** - They're easier to review and less likely to introduce bugs
2. **Provide a clear description** - Explain what the PR does and why
3. **Link to related issues** - Use keywords like "Fixes #123" or "Closes #456"
4. **Include tests** - Ensure your changes work as expected
5. **Respond to feedback** - Be receptive to suggestions from reviewers
6. **Update your PR when needed** - Make requested changes and push updates to the same branch

### Reviewing Pull Requests

When reviewing PRs, check for:
- Code correctness
- Test coverage
- Code style/consistency
- Potential bugs
- Security concerns
- Documentation

## Resolving Conflicts

Conflicts occur when Git can't automatically merge changes.

### Identifying Conflicts
```bash
# When merging
git merge feature-branch
# Git will report conflicts if they exist

# When rebasing
git rebase main
# Git will pause at each commit with conflicts
```

### Resolving Conflicts
1. **Open conflicted files** - Look for markers like `<<<<<<<`, `=======`, and `>>>>>>>`
2. **Edit the files** - Choose which changes to keep or combine them
3. **Mark as resolved**
   ```bash
   git add resolved-file.txt
   ```
4. **Continue the operation**
   ```bash
   # If merging
   git merge --continue
   
   # If rebasing
   git rebase --continue
   ```

### Tools for Conflict Resolution
```bash
# Use a visual tool to resolve conflicts
git mergetool
```

## Best Practices

1. **Commit often** - Small, focused commits are easier to understand and revert if needed
2. **Pull before pushing** - Keep your local repository up to date
3. **Use branches for features/fixes** - Don't work directly on main
4. **Write meaningful commit messages**
5. **Review your changes before committing**
   ```bash
   git diff
   ```
6. **Use .gitignore** - Exclude build artifacts, dependencies, and sensitive information
7. **Tag important releases**
   ```bash
   git tag -a v1.0.0 -m "Version 1.0.0"
   ```

## Useful Git Commands

### Stashing Changes
```bash
# Stash uncommitted changes
git stash

# List stashes
git stash list

# Apply the most recent stash
git stash apply

# Apply a specific stash
git stash apply stash@{2}

# Remove a stash after applying
git stash pop
```

### Remote Repositories
```bash
# View remote repositories
git remote -v

# Add a remote repository
git remote add origin https://github.com/username/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git

# Fetch from a remote
git fetch origin

# Pull from a remote (fetch + merge)
git pull origin main

# Push to a remote
git push origin feature-branch
```

### Undoing Changes
```bash
# Discard changes in working directory
git restore file.txt  # Git 2.23+
git checkout -- file.txt  # Older Git versions

# Unstage a file
git restore --staged file.txt  # Git 2.23+
git reset HEAD file.txt  # Older Git versions

# Amend the last commit
git commit --amend

# Reset to a previous commit (careful!)
git reset --soft HEAD~1  # Keep changes staged
git reset --mixed HEAD~1  # Keep changes unstaged (default)
git reset --hard HEAD~1  # Discard changes (dangerous!)
```

### Git Aliases
Set up shortcuts for common commands in your Git config:
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
```

### Advanced Features
```bash
# Cherry-pick commits from another branch
git cherry-pick commit-hash

# Bisect to find bugs
git bisect start
git bisect bad  # Current version has the bug
git bisect good older-commit  # This version was good

# Reflog - recovery tool
git reflog
```

## Further Learning Resources

- [Pro Git Book](https://git-scm.com/book/en/v2) - Comprehensive free book
- [GitHub Learning Lab](https://lab.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
