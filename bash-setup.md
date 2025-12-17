# Bash Setup Guide (Git Bash on Windows)

This document provides **complete setup from a fresh Windows machine** for data science development using Git Bash.

## Overview

**Environment:** Git Bash on Windows (MINGW64)  
**Shell:** `/bin/bash`  
**Package Manager:** Scoop (user-space, no admin required)  
**Goal:** Reproducible data science environment without admin privileges

---

## Prerequisites

- Windows 10 or Windows 11
- No admin access required (all user-local installs)

---

## Complete Setup from Zero

### Step 1: Install Git for Windows (includes Git Bash)

Download and install Git for Windows which includes Git Bash terminal.

**Option A: Standard Installer (Recommended)**

1. Download Git for Windows: https://git-scm.com/download/win
2. Run installer (64-bit version)
3. **Important selections during install:**
   - Use Git from Git Bash only (or from command line if you prefer)
   - Checkout as-is, commit Unix-style line endings
   - Use MinTTY (the default terminal)
   - Enable file system caching
4. Complete installation

**Option B: Portable Git (No Admin)**

If you cannot run installers, use PortableGit (see `configuration.md` for PowerShell commands to download/extract manually).

**Verify Git Bash:**

Open "Git Bash" from Start Menu, you should see:
```bash
user@COMPUTER MINGW64 ~
$
```

Test Git:
```bash
git --version
# Output: git version 2.52.0.windows.1 (or later)
```

---

### Step 2: Install Python

Download and install Python from https://www.python.org/downloads/

**Installation:**

1. Download Python 3.14+ (64-bit)
2. Run installer
3. **CRITICAL:** Check "Add Python to PATH" before clicking Install
4. Click "Install Now"
5. Wait for installation to complete

**Verify in Git Bash:**

```bash
python --version
# Output: Python 3.14.2 (or later)

# Also test pip
pip --version
```

**If Python not found in bash:**

Close and reopen Git Bash to pick up new PATH, or manually add:
```bash
export PATH="/c/Users/$USER/AppData/Local/Programs/Python/Python314:$PATH"
export PATH="/c/Users/$USER/AppData/Local/Programs/Python/Python314/Scripts:$PATH"
```

---

### Step 3: Install Poetry (Python Package Manager)

Install Poetry using the official installer:

```bash
# Download and run Poetry installer
curl -sSL https://install.python-poetry.org | python -

# Poetry installs to: ~/AppData/Roaming/Python/Scripts/poetry.exe
```

**Add Poetry to PATH:**

```bash
# Add to ~/.bashrc for permanent access
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc

# Reload bashrc
source ~/.bashrc

# Verify
poetry --version
# Output: Poetry (version 2.2.1 or later)
```

---

### Step 4: Install VS Code

Download and install VS Code: https://code.visualstudio.com/

**Installation:**

1. Download VS Code (64-bit)
2. Run installer
3. **Recommended selections:**
   - Add "Open with Code" to context menu
   - Add to PATH
   - Register Code as editor for supported file types
4. Complete installation

**Configure VS Code to use Git Bash:**

After opening VS Code:

1. Press `Ctrl + ,` (Settings)
2. Search: `terminal.integrated.defaultProfile.windows`
3. Set to: `Git Bash`

Or edit settings JSON (`Ctrl + Shift + P` → "Preferences: Open Settings (JSON)"):

```json
{
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```

**Verify:**

1. Open VS Code
2. Press `` Ctrl + ` `` (open terminal)
3. Should see Git Bash with: `user@COMPUTER MINGW64 ~/path`

---

## Installation Steps (Tools & Packages)

### Step 5: Install Scoop (Package Manager)

Scoop enables easy installation of tools without admin privileges.

```bash
# Download and install Scoop
powershell -NoProfile -Command "iwr -useb get.scoop.sh | iex"

# Verify installation
scoop --version
```

**Note:** This runs a PowerShell command from bash. Scoop itself uses PowerShell for installation.

**Scoop Location:** `~/scoop/` → `C:\Users\<username>\scoop\`

---

### Step 6: Add Scoop to Bash PATH

Update your `.bashrc` to include Scoop in PATH (Poetry already added in Step 3):

```bash
# Add Scoop to ~/.bashrc
echo 'export PATH="$HOME/scoop/shims:$PATH"' >> ~/.bashrc

# Reload bashrc
source ~/.bashrc

# Verify
scoop --version
```

---

### Step 7: Verify All Tools

Check that all required tools are accessible:

```bash
# Git
git --version
# Output: git version 2.52.0.windows.1

# Python
python --version
# Output: Python 3.14.2

# Poetry (dependency manager)
poetry --version
# Output: Poetry (version 2.2.1)

# Scoop (package manager)
scoop --version
# Output: Current Scoop version: b588a06e ...
```

---

## Installed Tools

### Git
- **Location:** `/mingw64/bin/git`
- **Version:** 2.52.0+
- **Type:** PortableGit (user-local)
- **Usage:** `git clone`, `git commit`, etc.

### Python
- **Location:** `C:\Users\bbrewer1\AppData\Local\Microsoft\WindowsApps\python`
- **Version:** 3.14.2
- **Type:** System Python
- **Usage:** `python script.py`, `python -m pip install package`

### Poetry
- **Location:** `~/AppData/Roaming/Python/Scripts/poetry.exe`
- **Version:** 2.2.1
- **Type:** User-space package manager
- **Usage:** `poetry install`, `poetry run jupyter lab`

### Scoop
- **Location:** `~/scoop/`
- **Version:** 0.5.3+
- **Type:** User-space package manager
- **Usage:** `scoop install <package>`

### Jupyter Lab
- **Installation:** Via Poetry (`poetry install`)
- **Launch:** `poetry run jupyter lab`
- **Kernel:** Python venv created by Poetry

---

## Poetry & Jupyter Setup

### Initialize New Poetry Project

```bash
# Create project directory
mkdir my-project
cd my-project

# Initialize git repo
git init
git config user.name "Brian Brewer"
git config user.email "brian.brewer@example.com"

# Initialize Poetry project
poetry init

# Follow prompts:
# Project name: my-project
# Version: 0.1.0
# Description: Data science project
# Author: Brian Brewer
# License: MIT (or your choice)
# Compatible Python versions: ^3.14
```

### Add Dependencies

```bash
# Add core data science packages
poetry add numpy pandas matplotlib seaborn scikit-learn

# Add Jupyter & notebook tools
poetry add jupyter jupyterlab ipykernel

# Add optional packages (as needed)
poetry add scipy statsmodels plotly dask

# Add dev dependencies
poetry add --group dev pytest black ruff mypy
```

### Install Dependencies

```bash
# Install all dependencies and create venv
poetry install

# Verify installation
poetry show

# Check Python version in venv
poetry run python --version
```

### Create & Register Jupyter Kernel

```bash
# Register the Poetry venv as a Jupyter kernel
poetry run python -m ipykernel install --user --name my-project --display-name "Python (my-project)"

# Verify kernel installation
jupyter kernelspec list
```

### Launch Jupyter Lab

```bash
# From project directory
poetry run jupyter lab

# Jupyter will open in default browser (usually http://localhost:8888)
# Select "Python (my-project)" kernel when creating new notebook
```

### Example pyproject.toml

```toml
[tool.poetry]
name = "data-science"
version = "0.1.0"
description = "Data science project with Poetry"
authors = ["Brian Brewer <brian.brewer@example.com>"]
license = "MIT"

[tool.poetry.dependencies]
python = "^3.14"
numpy = "^1.26"
pandas = "^2.0"
matplotlib = "^3.8"
seaborn = "^0.13"
scikit-learn = "^1.3"
jupyterlab = "^4.0"
ipykernel = "^6.26"
scipy = "^1.11"
plotly = "^5.17"

[tool.poetry.group.dev.dependencies]
pytest = "^7.4"
black = "^23.11"
ruff = "^0.1"
mypy = "^1.7"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

### Jupyter Lab Configuration

Export notebooks without inputs (for presentations):

```bash
# Convert notebook to HTML without code cells
poetry run jupyter nbconvert --to html --no-input notebook.ipynb --output notebook-presentation.html

# Convert to PDF
poetry run jupyter nbconvert --to pdf notebook.ipynb

# Convert to markdown
poetry run jupyter nbconvert --to markdown notebook.ipynb
```

### Poetry Workflow

```bash
# Activate Poetry shell (optional)
poetry shell

# Run commands in Poetry environment
poetry run python script.py
poetry run jupyter lab
poetry run pytest tests/

# Add new dependency
poetry add new-package

# Update all dependencies
poetry update

# Show installed packages
poetry show

# Deactivate Poetry shell
exit
```

---

## Complete Reproduction from Scratch

Full commands to recreate this setup from zero:

```bash
# 1. Install Scoop (if not already installed)
iwr -useb get.scoop.sh | iex

# 2. Add Scoop & Poetry to PATH (add to ~/.bashrc)
nano ~/.bashrc
# Add:
# export PATH="$HOME/scoop/shims:$PATH"
# export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"
source ~/.bashrc

# 3. Verify base tools
git --version
python --version
poetry --version
scoop --version

# 4. Create project
mkdir data-science
cd data-science
git init
git config user.name "Brian Brewer"
git config user.email "brian.brewer@example.com"

# 5. Initialize Poetry
poetry init -n
poetry config virtualenvs.in-project true

# 6. Add dependencies
poetry add numpy pandas matplotlib seaborn scikit-learn jupyter jupyterlab ipykernel

# 7. Install
poetry install

# 8. Register Jupyter kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# 9. Verify everything
poetry show
jupyter kernelspec list

# 10. Launch Jupyter
poetry run jupyter lab
```

---

## Common Commands

### Poetry Workflow

```bash
# Install dependencies from pyproject.toml
poetry install

# Activate Poetry shell (optional)
poetry shell

# Run commands in Poetry environment
poetry run python script.py
poetry run jupyter lab
poetry run pytest

# Add new dependency
poetry add package-name

# Update dependencies
poetry update
```

### Scoop Package Management

```bash
# Search for package
scoop search package-name

# Install package
scoop install package-name

# Update all packages
scoop update '*'

# List installed packages
scoop list
```

### Git Commands

```bash
# Initialize repo
git init

# Configure user
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Standard workflow
git add -A
git commit -m "Your message"
git push origin main
```

---

## PATH Configuration

Your bash PATH includes (in order of priority):

1. `~/scoop/shims` - Scoop-installed tools
2. `~/AppData/Roaming/Python/Scripts` - Poetry & Python tools
3. `/mingw64/bin` - Git Bash core tools
4. `/usr/bin`, `/bin` - Standard Unix utilities
5. Windows system paths

**View full PATH:**
```bash
echo $PATH
```

---

## File System Notes

- **Windows Path:** `C:\Users\bbrewer1\code\data-science`
- **Bash Path:** `/c/Users/bbrewer1/code/data-science`
- **Home:** `~` = `$HOME` = `C:\Users\bbrewer1`

**Path conversion:**
```bash
# Windows to Unix
C:\Users\bbrewer1 → /c/Users/bbrewer1 or ~

# Unix to Windows
/c/Users/bbrewer1/scoop/shims → C:\Users\bbrewer1\scoop\shims
```

---

## Project Setup

### Initialize New Project

```bash
# Create project directory
mkdir my-project
cd my-project

# Initialize git
git init
git config user.name "Brian Brewer"
git config user.email "brian.brewer@example.com"

# Initialize Poetry
poetry init
# Follow prompts for project name, version, etc.

# Add dependencies
poetry add python=^3.14
poetry add jupyter jupyterlab pandas numpy scikit-learn

# Install
poetry install

# Create Jupyter kernel
poetry run python -m ipykernel install --user --name my-project --display-name "Python (my-project)"

# Launch Jupyter
poetry run jupyter lab
```

---

## Troubleshooting

### Scoop Not Found

If `scoop` command not found after installation:

```bash
# Reload bash profile
source ~/.bashrc

# Or manually add to PATH for current session
export PATH="$HOME/scoop/shims:$PATH"
```

### Poetry Not Found

```bash
# Add Poetry to PATH
export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"

# Make permanent by adding to ~/.bashrc
```

### Git Not Found

Git should be available through Git Bash. If missing:

```bash
which git
# Should return: /mingw64/bin/git

# If not, verify Git installation or use full path
/mingw64/bin/git --version
```

### Python Version Issues

```bash
# Check Python version
python --version

# If wrong version, update PATH or use explicit path
python3.14 --version
```

---

## Switching to WSL 2 (When Admin Access Approved)

Once you have admin privileges, WSL 2 provides a full Linux environment:

```bash
# Enable WSL 2 features (requires admin)
wsl --install

# Install Ubuntu
wsl --install -d Ubuntu

# Enter WSL from Windows
wsl

# Access Windows files from WSL
cd /mnt/c/Users/bbrewer1/code/data-science
```

WSL 2 will provide:
- Native Linux kernel
- Full Linux package managers (`apt`, `yum`)
- Better file system performance for Linux tools
- Docker Desktop integration

---

## VS Code Terminal Configuration

Configure VS Code to use Git Bash as default terminal.

### Option 1: Settings JSON

Edit `.vscode/settings.json` in your workspace:

```json
{
  "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": ["--login", "-i"],
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```

**Or if using PortableGit:**

```json
{
  "terminal.integrated.shell.windows": "C:\\Users\\bbrewer1\\Apps\\Git\\PortableGit\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": ["--login", "-i"],
  "terminal.integrated.defaultProfile.windows": "Git Bash (PortableGit)"
}
```

### Option 2: VS Code UI

1. Open VS Code
2. `Ctrl + ,` (Settings)
3. Search: `terminal.integrated.defaultProfile.windows`
4. Set to: `Git Bash`
5. Search: `terminal.integrated.shell.windows`
6. Set to: `C:\Program Files\Git\bin\bash.exe` (or your PortableGit path)

### Verify

Open new terminal in VS Code (`Ctrl + `` or Terminal → New Terminal`). Should see:

```bash
user@COMPUTER MINGW64 ~/code/data-science
$
```

---

## Quick Reference

| Tool | Command | Version |
|------|---------|---------|
| **Git** | `git --version` | 2.52.0+ |
| **Python** | `python --version` | 3.14.2+ |
| **Poetry** | `poetry --version` | 2.2.1+ |
| **Scoop** | `scoop --version` | 0.5.3+ |
| **Bash** | `bash --version` | GNU bash 3.1+ |
| **Jupyter** | `poetry run jupyter --version` | (via Poetry) |

---

## Bash Bootstrap Script (Alternative to PowerShell)

Once you have Git Bash, Python, and Poetry installed (Steps 1-3), you can use this bash script instead of the PowerShell bootstrap:

**Create `bootstrap-bash.sh`:**

```bash
#!/bin/bash
# Bootstrap data science environment in bash

set -e  # Exit on error

echo "=== Data Science Environment Bootstrap (Bash) ==="

# Install Scoop
echo "Installing Scoop..."
powershell -NoProfile -Command "iwr -useb get.scoop.sh | iex"

# Add to PATH for this session
export PATH="$HOME/scoop/shims:$PATH"
export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"

# Verify tools
echo "Verifying tools..."
git --version
python --version
poetry --version
scoop --version

# Create project directory
PROJ_DIR="$HOME/code/data-science"
echo "Creating project: $PROJ_DIR"
mkdir -p "$PROJ_DIR"
cd "$PROJ_DIR"

# Initialize git
git init
git config user.name "Brian Brewer"
git config user.email "brian.brewer@example.com"

# Initialize Poetry project
echo "Initializing Poetry project..."
poetry init -n --name "data-science" --description "Data science environment"

# Configure Poetry
poetry config virtualenvs.in-project true

# Add dependencies
echo "Adding dependencies..."
poetry add numpy pandas matplotlib seaborn scikit-learn
poetry add jupyter jupyterlab ipykernel

# Install
echo "Installing dependencies..."
poetry install

# Register Jupyter kernel
echo "Registering Jupyter kernel..."
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# Add to bashrc permanently
echo 'export PATH="$HOME/scoop/shims:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc

echo ""
echo "=== Setup Complete! ==="
echo "Project: $PROJ_DIR"
echo "Launch Jupyter: poetry run jupyter lab"
echo ""
echo "Restart your terminal or run: source ~/.bashrc"
```

**Run the script:**

```bash
bash bootstrap-bash.sh
```

**What it does:**
1. Installs Scoop (via PowerShell command)
2. Verifies all tools installed
3. Creates project directory
4. Initializes git repo
5. Creates Poetry project with pyproject.toml
6. Adds data science dependencies
7. Installs packages and creates venv
8. Registers Jupyter kernel
9. Updates ~/.bashrc with PATH

This is the **bash equivalent** of `data-science-bootstrap.ps1` PowerShell script.

---

## Complete Setup Checklist

**Initial Setup (from fresh Windows):**
- [ ] Git for Windows installed (includes Git Bash)
- [ ] Git Bash opens and works (`git --version`)
- [ ] Python 3.14+ installed & in PATH (`python --version`)
- [ ] Poetry installed (`poetry --version`)
- [ ] VS Code installed
- [ ] VS Code terminal set to Git Bash

**Environment Configuration:**
- [ ] Scoop installed (`~/scoop/`)
- [ ] `.bashrc` updated with Scoop & Poetry paths
- [ ] `source ~/.bashrc` executed
- [ ] All tools verified: `git`, `python`, `poetry`, `scoop`

**Project Setup:**
- [ ] Project directory created
- [ ] Git initialized (`git init`)
- [ ] Poetry project initialized (`poetry init`)
- [ ] Dependencies added (`poetry add ...`)
- [ ] `poetry install` run successfully
- [ ] Jupyter kernel registered
- [ ] `poetry run jupyter lab` launches successfully

---

## Notes

- All tools installed user-local (no admin required)
- Git Bash provides Unix-like environment on Windows
- Poetry manages Python dependencies and virtual environments
- Scoop allows easy installation of additional tools
- This setup is reversible - can uninstall without affecting system
- Bash is cleaner & simpler than PowerShell for development

---

**Created:** December 16, 2025  
**Last Updated:** December 16, 2025  
**Environment:** Windows 10/11 + Git Bash + Scoop + Poetry + VS Code
