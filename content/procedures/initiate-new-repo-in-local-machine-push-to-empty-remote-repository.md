---
title: "Initiate new repo in local machine push to empty remote repository"
category: "GIT"
tags: ["General"]
updatedAt: "2026-07-23T02:07:36.259Z"
---

IN Local Machine:

git --version [not installed, sudo apt/yum install git -y]

mkdir <Local-repo-name>
cd <Local-repo-name>

 1. Initialize repository
git init

 2. Configure user (first time only)
git config user.name "Your Name"
git config user.email "you@example.com"

 3. Create a file
echo "Hello Git" > README.md

 4. Check status
git status

 5. Stage the file
git add README.md [targeting particular file]
or
git add . [targeting changes in current working dir]
or
git add --all / -A [targeting all changes in <Local-repo-name>]

 6. Commit
git commit -m "Initial commit"

7. Connect to a remote repository (GitHub, GitLab, Bitbucket)
git remote add origin <repository-url> [paste newly created empty remote repo]

8. git branch -M main

9 git push -u origin main
