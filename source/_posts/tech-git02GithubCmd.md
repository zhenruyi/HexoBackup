---
title: Git常用命令备忘
date: 2022-02-02 22:44:53
id: git2
categories:
- tech
tags:
- git
---







Git的一些常用命令备忘。



<!-- more -->





```bash
git --version
git config --global --list
git config --system --list
git config user.name ...
git config user.email ...

ssh-keygen -t -rsa

git init
git clone ...
git status
git add .
git cmmit -m ".."
git push

git branch -v
git branah ...
git checkout ...
git merge ...

git reset --hard HEAD^
git reset --hard HEAD~n
git reset --hard ...
git reset --mixed ...
git reset --soft ...

git remote -v
git remote add origin ...
git push origin master

pull = fetch + merge
git fetch origin master
git checkout orgin/master
git merge orgin/master
```

