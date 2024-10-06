# Git Guide for DevOps

## Table of Contents
1. [Introduction](#introduction)
2. [Installation and Setup](#installation-and-setup)
3. [Basic Git Commands](#basic-git-commands)
4. [Branching and Merging](#branching-and-merging)
5. [Remote Repositories](#remote-repositories)
6. [Git Workflow for DevOps](#git-workflow-for-devops)
7. [Advanced Git Concepts](#advanced-git-concepts)
8. [Best Practices](#best-practices)
9. [Troubleshooting Common Issues](#troubleshooting-common-issues)

## Introduction
Git is an essential tool for version control in DevOps practices. This guide covers everything from basic commands to advanced concepts and best practices for using Git in a DevOps environment.

## Installation and Setup

### Installing Git
- **Windows**: Download and install from [git-scm.com](https://git-scm.com/)
- **Linux (Ubuntu/Debian)**:
  ```bash
  sudo apt update
  sudo apt install git
  ```
- **macOS**:
  ```bash
  brew install git
  ```

### Initial Configuration
```bash
# Set your username
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"

# Check your configuration
git config --list
```

## Basic Git Commands

### Initializing a Repository
```bash
# Create a new repository
git init

# Clone an existing repository
git clone <repository-url>
```

### Basic Operations
```bash
# Check status of working directory
git status

# Add files to staging area
git add <filename>      # Add specific file
git add .               # Add all files

# Commit changes
git commit -m "Commit message"

# View commit history
git log
git log --oneline      # Condensed view
```

## Branching and Merging

### Branch Management
```bash
# Create a new branch
git branch <branch-name>

# Switch to a branch
git checkout <branch-name>

# Create and switch to a new branch
git checkout -b <branch-name>

# List all branches
git branch -a

# Delete a branch
git branch -d <branch-name>
```

### Merging
```bash
# Merge a branch into current branch
git merge <branch-name>

# Abort a merge in case of conflicts
git merge --abort
```

## Remote Repositories

### Managing Remotes
```bash
# Add a remote repository
git remote add origin <repository-url>

# List remote repositories
git remote -v

# Push to remote repository
git push origin <branch-name>

# Pull from remote repository
git pull origin <branch-name>

# Fetch updates from remote
git fetch origin
```

## Git Workflow for DevOps

### Feature Branch Workflow
1. Create a feature branch
   ```bash
   git checkout -b feature/new-feature
   ```

2. Make changes and commit
   ```bash
   git add .
   git commit -m "Implement new feature"
   ```

3. Push feature branch to remote
   ```bash
   git push origin feature/new-feature
   ```

4. Create Pull Request (on GitHub/GitLab)

5. After review, merge into main branch
   ```bash
   git checkout main
   git pull origin main
   git merge feature/new-feature
   git push origin main
   ```

### Continuous Integration Workflow
```bash
# Update local repository
git pull origin main

# Create feature branch
git checkout -b feature/ci-update

# Make changes and commit
git add .
git commit -m "Update CI configuration"

# Push changes
git push origin feature/ci-update
```

## Advanced Git Concepts

### Rebasing
```bash
# Rebase current branch onto main
git checkout feature-branch
git rebase main

# Interactive rebase
git rebase -i HEAD~3
```

### Stashing
```bash
# Stash changes
git stash save "Work in progress"

# List stashes
git stash list

# Apply stash
git stash apply stash@{0}

# Pop stash
git stash pop

# Drop stash
git stash drop stash@{0}
```

### Git Hooks
Located in `.git/hooks/`, common hooks:
- pre-commit
- post-commit
- pre-push

Example pre-commit hook:
```bash
#!/bin/sh
# Run tests before committing
npm test
```

## Best Practices

1. **Commit Messages**
   - Use clear, descriptive commit messages
   - Follow format: `<type>: <description>`
   Example:
   ```
   feat: add user authentication
   fix: resolve memory leak in worker process
   ```

2. **Branching Strategy**
   - Use feature branches for all new work
   - Keep main/master branch stable
   - Delete branches after merging

3. **Code Review**
   - Create Pull Requests for all changes
   - Use descriptive PR titles and descriptions
   - Include relevant tests and documentation

4. **Continuous Integration**
   - Run tests automatically on all branches
   - Use Git hooks for pre-commit checks
   - Automate deployment when possible

## Troubleshooting Common Issues

### Fixing a Bad Commit
```bash
# Amend last commit
git commit --amend

# Revert a commit
git revert <commit-hash>

# Reset to a previous state
git reset --hard <commit-hash>
```

### Resolving Merge Conflicts
1. Identify conflicting files:
   ```bash
   git status
   ```

2. Open conflicting files and resolve conflicts manually

3. After resolving, mark as resolved:
   ```bash
   git add <resolved-file>
   ```

4. Complete the merge:
   ```bash
   git commit
   ```

### Recovering Lost Changes
```bash
# Show reflog
git reflog

# Recover lost commit
git checkout -b recovery-branch <commit-hash>
```

---

Remember to regularly update this guide as you learn more about Git and discover new DevOps practices. Good luck with your DevOps journey!
