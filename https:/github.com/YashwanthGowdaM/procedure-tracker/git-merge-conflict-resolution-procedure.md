---
title: "Git Merge Conflict Resolution Procedure"
category: "Git"
tags: ["git", "merge", "devops", "vcs"]
lastUpdated: "2026-07-23"
status: "Fresh"
estimatedMinutes: 15
author: "Lead SRE & DevOps Engineer"
version: "1.0"
summary: "Standard operational procedure for identifying, resolving, and verifying Git merge conflicts during branch integration. Requires local Git CLI installed and active repository access."
---

# Git Merge Conflict Resolution Procedure

> [!IMPORTANT]
> Always ensure you have stashed or committed all uncommitted work before starting conflict resolution. Never use force-push (`git push -f`) on shared primary branches such as `main` or `release`.

## Step 1: Identify and Locate Conflicts
Fetch the latest changes from the remote tracking repository and attempt to merge or rebase to identify conflicting files.

```bash
# Fetch all latest remote branches without modifying local state
git fetch origin

# Attempt to merge target branch into current feature branch
git merge origin/main

# Output unmerged and conflicting files
git status --short | grep -E '^(UU|AA|DD|AU|UA)'
```

## Step 2: Manually Resolve Conflict Markers
Inspect affected files for standard Git conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), make necessary source edits, and stage the resolved files.

```bash
# Search for remaining conflict markers across project files
grep -rnw '.' -e '<<<<<<<' --exclude-dir='.git'

# After editing files manually or via merge tool, stage the resolved files
git add <path-to-resolved-file>
```

## Step 3: Verification & Rollback
Validate that the application builds successfully, execute test suites, complete the merge commit, or abort if resolution fails.

```bash
# Verify that no unmerged paths remain staged
git status

# Run local build and automated test suite
npm test || pytest

# Complete the merge transaction
git commit -m 'fix: resolve merge conflicts with main'

# Emergency Rollback: To abort the merge entirely and restore previous HEAD
# git merge --abort
```
