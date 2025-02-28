---
icon: https://git-scm.com/images/logos/downloads/Git-Icon-Black.svg
tags:
  - git
  - command-line
---
# Git Commands to Save Your Time

Git can be complex, but mastering these commands can save you hours and enhance your workflow.

## Restore

Restore specified paths in the working tree.

```bash
# Undo changes in files
git restore <file-name>
# Unstage a file
git restore --staged <file-name>
```

## Switch

Switch to a specified branch or create before switching.

```bash
# Switch to an existing branch
git switch <branch-name>
# Create and switch to a new branch 
git switch -c <new-branch>
# Create/reset and switch to a branch
git switch -C <new-branch>
```

## Sparse-checkout

Restrict your working directory to a set of directories

```bash
# Initialize sparse-checkout
git sparse-checkout init --cone
# Set directories to be checked out
git sparse-checkout set <dir1> <dir2>
```

## Range-diff

Shows the differences between two versions of a patch series

```bash
# Compare two commit ranges
git range-diff <commit-range-1> <commit-range-2>
```

## Notes

Add metadata to commits without modify history.

```bash
# Add a note to a commit
git notes add -m "Your note here" <commit-hash>
# Show notes in commit log
git log --show-notes
```

## Worktree

Work on multiple branches simultaneously.

```bash
# Create a worktree at <path> based on <branch-name>
git worktree add ../<path> <branch-name>
# List details of each worktree
git worktree list
```

## alias

Create shortcuts for frequently used commands.

```bash
# Create an alias for switch
git config --global alias.sw switch
# Use the alias
git sw <branch-name>
```

Sources: 
* [Sparse-Checkout](https://github.blog/open-source/git/bring-your-monorepo-down-to-size-with-sparse-checkout/)