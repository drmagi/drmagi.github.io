---
layout: post
title: Git Basics
categories: [git]
published: true
---

## Create a new repository on the command line

```shell
echo "# blog" >> README.md
git init
git branch -m main
git add .
git commit -m "first commit"
```

## Push it to an existing repository

```shell
git remote add origin https://github.com/dr-magic/blog.git
git push -u origin main
```