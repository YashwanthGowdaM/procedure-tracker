---
title: "Cloning Remote Repository to local machine[ 2 branches, main(default), Remote_branch [example: Remote_development] Make local branches, update change in local_branch later merge local_branch with local_main (main) Push local_main (main) to remote branch (Remote_development) Raise PR to Merge Remote_branch to Main(default)"
category: "GIT"
tags: ["Push Local to Remote"]
updatedAt: "2026-07-23T02:10:19.481Z"
---

git clone <main(default) - clone url>

git branch --all [to list all branch remote + local]

#create local branch
git checkout -b "local_branch" [create & switch]

#made some changes 
touch file.txt 

git add .

git status

git commit -m "commiting on local_branch"

#merge local_branch with local_main

git checkout main
git merge local_branch

#push local changes to remote branch
[Local changes is in : main (local)
 Remote Branch: Remote_developemt (our example)]

git push origin main:Remote_development


In GitHub
---------------------------------------------------
Review changes, Raise PR & Merge Remote_development to Main(default)
