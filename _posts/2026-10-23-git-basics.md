---
title: Git Basics
tags: [Git]
description: Short overview of basic Git commands and workflows.
mermaid: true
image: /assets/img/2026-10-23/mermaid-gitgraph.png
---

## Create a new repository

```shell
echo "# blog" >> README.md
git init
git branch -m main
git add .
git commit -m "first commit"
```

## Push it to an existing repository

```shell
git remote add origin my_git_url
git push -u origin main
```

## Create a branch, commit and checkout branch to main

```shell
git checkout -b my_new_branch     # create new branch and switch zo new branch
git add .                         # standard workflow of changing and commiting to the branch  
git commit -m "commit message"
...
git checkout main                 # switch to target branch
git merge --squash my_new_branch  # merge target branch with new branch in one commit message
git branch -d my_new_branch       # delete new branch (optional) since everything is in main
```

## Use personal access token (PAT) in URL

In Github you can create a personal access token (PAT) which you can use as "password" for pushing changes.
But keep in mind that with that the PAT is stored in plain text in the local file `.git/config`.

```shell
git remote set-url origin https://my_user:my_pat@github.com/my_repo   
# remove it with git config --unset remote.origin.url
git push origin main                                                    
```

There is also the possibility to use the Git Credential Manager (GCM). If you work in Windows Subsystem fpr Linux (WSL) you have to configure GCM to use the Windows credential manager:

```shell
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"
```

## Example

```mermaid
gitGraph
    commit id: "Initial commit"
    commit id: "Setup blog framework"
    
    branch feature/dark-mode
    checkout feature/dark-mode
    commit id: "Add dark CSS variables"
    commit id: "Add toggle button component"
    commit id: "Fix local storage theme bug"
    
    checkout main
    branch fix/typo
    commit id: "Fix typo on home page"
    checkout main
    merge fix/typo id: "Merge quick fix" tag: "v1.0.1"
    
    checkout main
    %% Visualizing the squash merge: 3 commits combined into 1 clean commit
    merge feature/dark-mode id: "feat: Add dark mode feature (Squashed)" tag: "v1.1.0"
    
    commit id: "Next blog article layout"
```

