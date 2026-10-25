---
title: Git Basics
tags: [Git]
categories: [Programming]
description: Short overview of basic Git commands and workflows (AI supported).
mermaid: true
image: /assets/img/2026-10-23/mermaid-gitgraph.png
---

# Git and Github

[Git](https://git-scm.com) is a powerful distributed version control system designed to help developers track code changes, collaborate, and manage project history. Its fast branching, robust offline functionality, and industry-standard reliability make it an indispensable tool for modern software development.

[GitHub](https://github.com) is a cloud-based hosting platform built on Git that enables teams to store, share, and collaborate on code repositories. It provides centralized project management, issue tracking, and automated CI/CD workflows to streamline software development.

## 1. Create a new local repository

```shell
mkdir my_repo                     # Create a new directory for your project
cd my_repo                        # Navigate into the newly created project folder
git init                          # Initialize a local Git repository in this folder
git branch -m main                # Optional: Ensure your default branch is named 'main'

echo "First content" >> README.md # Create a README file with initial sample content
git add .                         # Stage all changes in the current directory for the next commit
git commit -m "first commit"      # Record a snapshot of your staged changes with a commit message
```

`git init` creates a **new, empty Git repository** in your current project folder. 

* It sets up a hidden `.git` subdirectory, which contains all the necessary metadata and version control tracking information for your project.
* Once initialized, you can begin staging files (`git add`) and recording commits (`git commit`) to track your project's history locally.

`git branch -m main` (or `-M main`) renames your **current active branch** to `main`.

* **`-m`** stands for **move** (used to rename branches). 
* **`-M`** (capitalized) forces the rename even if a branch named `main` already exists.

This command is commonly used to change the default local branch name from legacy terms like `master` to `main` before pushing your code to a remote repository.

`git add` (The Staging Phase) Prepares your changes for the next commit. It moves modified or new files from your working directory into the **staging area** (index), letting you choose *what* goes into the next snapshot.

`git add .` stages **all new, modified, and deleted files** in your current directory and all of its subdirectories, preparing them to be included in your next commit.

* **What the `.` stands for:** In Unix-based command lines and Git, the period (`.`) represents the **current directory**. 
* **How it works:** By using `.`, you tell Git to scan your current folder and everything inside it, automatically finding and staging all changes at once instead of requiring you to name each file individually.
* **To stage a specific subset of files** instead of everything, you can 
  * specify individual files or folders: `git add index.html src/style.css`
  * Use wildcards `git add *.js`


`git commit` (The Recording Phase): Permanently saves your staged changes to your local repository history. Every commit acts as a secure snapshot or checkpoint of your project, accompanied by a descriptive message.


## 2. Push it to an remote repository

```bash
git remote add origin <REMOTE_REPOSITORY_URL>
git push -u origin main
```

Setting up and pushing your code to a remote repository involves three key steps:

### 2.1. Create a Remote Repository
First, create a blank repository on your hosting service (such as GitHub). Do not initialize it with a README or `.gitignore` if you already have local code. Once created, copy the repository's SSH or HTTPS URL:
* **HTTPS Example:** `https://github.com/username/repository-name.git`
* **SSH Example:** `git@github.com:username/repository-name.git`


### 2.2. Connect Your Local Repo to the Remote

`git remote add origin <REMOTE_REPOSITORY_URL>`

* **`git remote add`**: Adds a new remote reference to your configuration.
* **`origin`**: The standard default alias used to refer to your primary remote server.
* (Optional) You can verify the link with `git remote -v`.


### 2.3. Push Your Local Commits

`git push -u origin main`

* **`git push`**: Sends your committed local changes to the remote server.
* **`-u` (or `--set-upstream`)**: Remembers the connection between your local `main` branch and the `main` branch on `origin`.
* **`origin main`**: Specifies the remote (`origin`) and the target branch (`main`).
* **Tip:** After running `git push -u origin main` once, future pushes from this branch only require typing **`git push`**.


## 3. Create a branch, commit and checkout branch to main

```shell
git checkout -b feature-branch     # create new branch and switch zo new branch
git add .                         # standard workflow of changing and commiting to the branch  
git commit -m "commit message"
...
git checkout main                 # switch to target branch
git merge --squash my_new_branch  # merge target branch with new branch in one commit message
git branch -d my_new_branch       # delete new branch (optional) since everything is in main
```

The standard Git workflow for collaborative or feature-based development revolves around creating branches, making commits, and merging your work. Here is how it works step by step:

### 3.1. Create and Switch to a New Branch
Before making changes, it is best practice to create a dedicated branch (e.g., for a new feature or bug fix) to keep your work isolated from the main codebase.

```bash
git checkout -b feature-branch
```

* **`git checkout -b`**: Creates a new branch and immediately switches you to it. *(Alternatively, you can use `git switch -c feature-branch`).*


### 3.2. Make and Commit Changes
Edit your files, stage them, and record your changes as checkpoints using commits.

```bash
git add .
git commit -m "Add new feature implementation"
```

* **`git add .`**: Stages all modified or new files in your working directory.
* **`git commit -m`**: Permanently saves the staged changes to your local history with a descriptive message.

### 3.3. Switch Back and Merge the Branch
Switch back to your main integration branch (usually `main`), ensure it is up to date, and integrate the changes from your feature branch.

```bash
git checkout main
git pull origin main
git merge feature-branch

# or alteratively
git merge --squash feature-branch
git commit -m "Add complete feature in a single clean commit"
```

* **`git checkout main`**: Returns you to the main production branch.
* **`git pull origin main`**: Pulls the latest remote updates to ensure your local `main` is fresh before merging.
* **`git merge feature-branch`**: Combines the history and changes of your feature branch into your current active branch (`main`).
* **Tip:** Unlike a standard merge, `git merge --squash` combins multiple commits into a single one. It is a great way to clean up your history. Note it **does not** automatically create a commit.  

### 3.4. Clean Up (Optional)
Once the branch has been successfully merged, you can safely delete it to keep your repository organized:

```bash
git branch -d feature-branch
```


## 4. Authentication

GitHub requires secure authentication for all HTTPS-based Git operations (such as `git push` or `git pull`), as standard account passwords are no longer accepted. A **Personal Access Token (PAT)** acts as a secure replacement for your password.

### 4.1. What is a Personal Access Token (PAT)?
A PAT is a secure string of characters generated on GitHub that you use instead of your account password when authenticating via HTTPS.
* **How to create one:** Go to GitHub -> **Settings** -> **Developer Settings** -> **Personal Access Tokens** (Classic or Fine-grained) -> **Generate new token**.
* **Scopes:** You assign specific permissions (e.g., `repo`, `workflow`) depending on what operations the token needs to perform.
* **Usage:** When Git prompts you for a password during a push or pull, you paste your PAT (`ghp_...` or `github_pat_...`).

### 4.2. Using Git Credential Manager (GCM)
Manually typing or pasting a PAT every time you interact with a remote repository can be tedious. **Git Credential Manager (GCM)** is a secure, cross-platform credential helper that stores your PAT safely and handles authentication automatically.

### Windows
* **Setup:** GCM comes pre-installed with **Git for Windows**.
* **How it works:** The first time you push or pull via HTTPS, a modern browser window or a popup prompt will appear allowing you to sign in to GitHub. GCM intercepts this, securely saves the token in the **Windows Credential Manager**, and handles subsequent requests automatically.

### Linux
* **Setup:** You can install GCM using packages provided in the official GitHub repository (e.g., via `.deb`, `.rpm`, or a dotnet tool).
* **How it works:** GCM integrates with your Linux desktop environment's native secure secret storage service (such as **GNOME Keyring**, **KWallet**, or `libsecret`) to securely encrypt and save your credentials.

### WSL (Windows Subsystem for Linux)
* **Setup:** WSL can leverage the Windows host's GCM installation seamlessly, avoiding the need to install separate Linux keyrings. Inside your WSL terminal, configure Git to point to the Windows Git Credential Manager executable:
```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"
```

### 4.3. Adding the PAT Directly to the Remote URL (Alternative Method)

If you prefer not to use a credential manager, you can embed your PAT directly inside the remote repository URL. **Security Warning:** This stores your PAT in plaintext inside your local .git/config file. Anyone with access to your computer or project folder can read your token. Use this cautiously (e.g., in temporary CI/CD environments or containerized setups).

* **How to set it up:** Instead of a standard URL, configure your remote origin with your token embedded right before the hostname:

```shell
git remote set-url origin https://my_user:my_pat@github.com/my_repo   
# remove it with git config --unset remote.origin.url
git push origin main                                                    
```
Once configured this way, subsequent commands like git push or git pull will authenticate automatically using the embedded token without prompting for user input or relying on an external credential helper.


## 5. Example

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

## 6. Best Practices

Using a dual-branch strategy with a **`main`** branch and a **`develop`** branch (often associated with Git Flow) is a powerful way to manage collaborative projects, staging, and production deployments[cite: 1]. 

Here are the core best practices for maintaining and using `main` and `develop` branches:

### 6.1. Define Branch Roles Clearly
* **The `main` Branch (Production):** 
  * Always reflects the production-ready state of your software.
  * Only stable, thoroughly tested code should ever live here.
  * Every merge into `main` should ideally correspond to a tagged release version (e.g., Release v1.1)[cite: 1].
* **The `develop` Branch (Integration):** 
  * Serves as the integration branch for upcoming releases and ongoing features.
  * Contains the latest delivered development changes, which may not yet be in production[cite: 1].

### 6.2. Isolate Feature Development
* **Branch off `develop`:** Never write code directly on `main` or `develop`. Always create dedicated feature or bugfix branches branching directly off `develop` (e.g., `feature/user-auth`)[cite: 1].
* **Keep features focused:** Group related commits logically (e.g., basic setup, implementation, tests, refactoring) on your feature branch before merging back[cite: 1].

### 6.3. Control the Flow of Merges
* **Feature to Develop:** Once a feature is complete and reviewed, merge it back into `develop`[cite: 1]. This acts as your staging ground where multiple features are combined and tested together.
* **Develop to Main:** Only merge from `develop` into `main` when you are ready to ship a stable release to production.

### 6.4. Protect Your Branches
* **Enable Branch Protection Rules:** On platforms like GitHub, enforce rules on both `main` and `develop`:
  * Require pull requests (PRs) before merging.
  * Require status checks (automated tests/CI pipelines) to pass.
  * Prevent direct force pushes (`git push --force`) to protect history.
