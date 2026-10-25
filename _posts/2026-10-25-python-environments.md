---
title: "Python Environments"
description: "How to isolate and manage Python project dependencies using the built-in venv module as well as Conda and Miniforge. Created with AI support."
categories: [Programming]
tags: [Python]
image: /assets/img/2026-10-25/python-environments.png
---

# Python Environments

When building Python applications, keeping your project dependencies isolated is a non-negotiable best practice. Without isolation, packages from different projects can conflict, breaking your code when you least expect it.

Here is everything you need to know to set up, manage, and clean up your development environments using Python's built-in `venv`, as well as data-science-focused tools like **Conda** and **Miniforge**.

---

## 1. The Standard Approach: Python's Built-in `venv`

For general-purpose Python development (web dev, automation, scripting), Python’s native `venv` module (built-in since Python 3.4) is lightweight and requires no extra installations.

### Step 1: Create the Environment

Run this command in your project root directory to create a local virtual environment named `.venv`:

```bash
python3 -m venv .venv

```

### Step 2: Activate the Environment

Activation hooks your shell into the isolated environment so that any packages you install stay localized to this project.

* **Linux / macOS:**
```bash
source .venv/bin/activate

```


* **Windows (Command Prompt):**
```cmd
.venv\Scripts\activate.bat

```


* **Windows (PowerShell):**
```powershell
.venv\Scripts\Activate.ps1

```



### Step 3: Deactivate the Environment

When you are done working, exit the environment by simply typing:

```bash
deactivate

```

### Step 4: Delete the Environment (Optional)

Because a virtual environment is just a directory containing a copy of the Python interpreter and site-packages, deleting it is safe and straightforward:

1. Deactivate the environment first.
2. Delete the `.venv` folder manually or via terminal (`rm -rf .venv` on Unix or `rmdir /s /q .venv` on Windows).

---

## 2. The Data Science Alternative: Conda & Miniforge

If you are working with data science, machine learning, or heavy scientific computing libraries (like NumPy, PyTorch, or TensorFlow), you often need to manage non-Python dependencies (like C/C++ compilers or CUDA toolkits). This is where **Conda** shines.

* **Conda:** A cross-platform package and environment manager (commonly installed via Anaconda or Miniconda).
* **Miniforge:** A lean, community-driven alternative to Miniconda. It comes pre-configured to use **conda-forge** (a massive, community-led repository of packages) as its default channel and ships with the faster `mamba` solver out of the box.

### Step 1: Create a Conda/Miniforge Environment

To create a new environment specifying a particular Python version (e.g., Python 3.11):

```bash
conda create -n my_env python=3.11

```

*(Note: If using Miniforge with Mamba enabled, you can substitute `conda` with `mamba` for significantly faster resolution times: `mamba create -n my_env python=3.11`)*

### Step 2: Activate the Environment

Unlike `venv`, Conda environments live in a central directory rather than your project folder by default, but activation is uniform across all operating systems:

```bash
conda activate my_env

```

### Step 3: Deactivate the Environment

To step out of the active Conda environment back to your base shell:

```bash
conda deactivate

```

### Step 4: Delete the Environment

To completely remove a Conda environment and free up disk space:

```bash
conda env remove -n my_env

```

---

## Summary: Which one should you use?

* Use **`venv`** for web development, general scripting, and lightweight applications where standard `pip` packages suffice.
* Use **Miniforge / Conda** for data science, machine learning, or projects requiring complex binary dependencies that are difficult to compile via `pip`.