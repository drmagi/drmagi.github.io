---
title: Git Basics
tags: [Git]
description: Short overview of the basic Git commands and workflows.
mermaid: true
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

## Push changes to remote

```shell
git remote set-url origin https://my_user:my_pat@github.com/my_repo     # user personal access token in URL 
                                                                        # important: this store the PAT in local .git/config
git push origin main                                                    
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

