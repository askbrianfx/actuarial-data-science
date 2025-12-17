# Complete Data Science Environment Setup

**Goal:** End-to-end setup from a fresh Windows machine to a fully scaffolded data science project with Jupyter Lab.

**No admin privileges required** – all installations are user-local.

---

## Table of Contents

1. [Overview](#overview)
2. [Quick Start (Bash)](#quick-start-bash)
3. [Method A: Bash Setup (Recommended)](#method-a-bash-setup-recommended)
4. [Method B: PowerShell Setup (Alternative)](#method-b-powershell-setup-alternative)
5. [Project Scaffolding](#project-scaffolding)
6. [Common Commands](#common-commands)
7. [Troubleshooting](#troubleshooting)
8. [Next Steps](#next-steps)

---

## Overview

| Aspect | Details |
|--------|---------|
| **Primary Shell** | Bash (Git Bash on Windows) |
| **Alternative Shell** | PowerShell (for comparison) |
| **Package Manager** | Scoop (user-space, no admin) |
| **Python Manager** | Poetry |
| **Notebook Environment** | Jupyter Lab |
| **Required Admin** | No |
| **Time to Setup** | ~15-20 minutes |

**Environment Path:**
- Windows: `C:\Users\<username>\code\data-science`
- Bash: `/c/Users/<username>/code/data-science` or `~/code/data-science`

---

## Quick Start (Bash)

**Already have Git, Python, and Poetry installed?** Run this in Git Bash:

```bash
# 1. Install Scoop (if not already installed)
powershell -NoProfile -Command "iwr -useb get.scoop.sh | iex"

# 2. Add paths to ~/.bashrc
echo 'export PATH="$HOME/scoop/shims:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 3. Create and setup project
mkdir -p ~/code/data-science && cd ~/code/data-science
git init
poetry init -n --name "data-science"
poetry config virtualenvs.in-project true

# 4. Add dependencies
poetry add numpy pandas matplotlib seaborn scikit-learn jupyter jupyterlab ipykernel

# 5. Install
poetry install

# 6. Register kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# 7. Launch Jupyter
poetry run jupyter lab
```

**For fresh Windows setup,** follow the full guide below.

---

# Method A: Bash Setup (Recommended)

Bash provides a cleaner, Unix-like environment ideal for data science tools and Docker.

## Step 1: Install Git for Windows (includes Git Bash)

**What:** Git version control + Git Bash terminal (Unix-like shell on Windows)

**Option 1A: Standard Installer**

1. Download Git for Windows (64-bit): https://git-scm.com/download/win
2. Run installer
3. **During installation, select:**
   - Use Git from Git Bash only (or "Git from command line and also from 3rd-party software")
   - Checkout as-is, commit Unix-style line endings
   - Use MinTTY (the default terminal)
   - Enable file system caching
4. Finish installation

**Option 1B: Portable Git (No Admin)**

If installers are blocked, download PortableGit:

```bash
# Download and extract manually (use browser or tools)
# https://github.com/git-for-windows/git/releases
# Extract to: C:\Users\<username>\AppData\Local\Programs\Git
# Then add to PATH via System Settings
```

**Verify Git Bash:**

Open "Git Bash" from Start Menu. You should see:

```bash
user@COMPUTERNAME MINGW64 ~
$
```

Test:
```bash
git --version
# Output: git version 2.52.0.windows.1 (or later)
```

---

## Step 2: Install Python

**What:** Python 3.14+ interpreter for data science packages

1. Download Python (64-bit): https://www.python.org/downloads/
2. Run installer
3. **CRITICAL:** Check "Add Python to PATH" before Install
4. Select "Install Now"
5. Wait for completion

**Verify in Git Bash:**

```bash
python --version
# Output: Python 3.14.2 (or later)

pip --version
```

**If not found in bash:**

Close and reopen Git Bash, or manually add:
```bash
export PATH="/c/Users/$USER/AppData/Local/Programs/Python/Python314:$PATH"
export PATH="/c/Users/$USER/AppData/Local/Programs/Python/Python314/Scripts:$PATH"
```

---

## Step 3: Install Poetry

**What:** Dependency manager for Python projects (replaces pip + venv)

In Git Bash:

```bash
# Download and install Poetry
curl -sSL https://install.python-poetry.org | python -

# Poetry installs to: ~/AppData/Roaming/Python/Scripts/poetry.exe
```

**Add Poetry to Bash PATH:**

```bash
# Add to ~/.bashrc
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc

# Reload
source ~/.bashrc

# Verify
poetry --version
# Output: Poetry (version 2.2.1 or later)
```

---

## Step 4: Install VS Code

**What:** Code editor with integrated terminal

1. Download VS Code (64-bit): https://code.visualstudio.com/
2. Run installer
3. **Select:**
   - Add "Open with Code" to context menu
   - Add to PATH
   - Register as editor for supported file types
4. Finish installation

**Configure VS Code to use Git Bash:**

In VS Code, press `Ctrl + ,` (Settings) and search for:

```
terminal.integrated.defaultProfile.windows
```

Set value to: `Git Bash`

**Or edit settings JSON directly** (`Ctrl + Shift + P` → "Preferences: Open Settings (JSON)"):

```json
{
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```

**Verify:**

1. Open VS Code
2. Press `` Ctrl + ` `` (backtick) to open terminal
3. Should see Git Bash with `user@COMPUTERNAME MINGW64 ~/path`

---

## Step 5: Install Scoop

**What:** Package manager for additional tools (no admin required)

In Git Bash:

```bash
# Install Scoop via PowerShell (wrapped command)
powershell -NoProfile -Command "iwr -useb get.scoop.sh | iex"

# Verify
scoop --version
# Output: Current Scoop version: ...
```

**Installation location:** `~/scoop/` → `C:\Users\<username>\scoop\`

---

## Step 6: Update Bash PATH

**What:** Make all installed tools accessible from Git Bash

Edit or create `~/.bashrc`:

```bash
# Add Scoop and Poetry to PATH
echo 'export PATH="$HOME/scoop/shims:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc

# Reload bash profile
source ~/.bashrc
```

**Verify all tools:**

```bash
git --version        # Should show 2.52.0+
python --version     # Should show 3.14.2+
poetry --version     # Should show 2.2.1+
scoop --version      # Should show version hash
```

---

## Step 7: Verify Complete Installation

```bash
# Run all verifications at once
echo "=== Installation Verification ==="
echo "Git: $(git --version)"
echo "Python: $(python --version)"
echo "Poetry: $(poetry --version)"
echo "Scoop: $(scoop --version)"
echo "Bash: $(bash --version | head -1)"
echo ""
echo "All tools installed successfully!"
```

---

# Method B: PowerShell Setup (Alternative)

If you prefer PowerShell or are in a PowerShell-only environment, use these commands.

## Bash Alternative: PowerShell Git Setup

```powershell
# Download and install Git for Windows
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

# Create install folder
New-Item -ItemType Directory -Path "$env:USERPROFILE\Apps\Git" -Force | Out-Null

# Download latest Git installer
$release = Invoke-RestMethod -Uri 'https://api.github.com/repos/git-for-windows/git/releases/latest'
$asset = $release.assets | Where-Object { $_.name -like 'Git-*-64-bit.exe' } | Select-Object -First 1
$installer = Join-Path $env:TEMP $asset.name

Invoke-WebRequest -Uri $asset.browser_download_url -OutFile $installer

# Run installer (interactive)
Start-Process -FilePath $installer -Wait

# Verify
git --version
```

## PowerShell Python Setup

```powershell
# Download Python installer
$pythonUrl = 'https://www.python.org/ftp/python/3.14.2/python-3.14.2-amd64.exe'
$installer = Join-Path $env:TEMP 'python-installer.exe'

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri $pythonUrl -OutFile $installer

# Run installer with PATH option
Start-Process -FilePath $installer -ArgumentList '/quiet InstallAllUsers=1 PrependPath=1' -Wait

# Verify
python --version
```

## PowerShell Poetry Setup

```powershell
# Install Poetry
$poetryUrl = 'https://install.python-poetry.org'
$tempFile = Join-Path $env:TEMP 'install-poetry.py'

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri $poetryUrl -OutFile $tempFile

python $tempFile

# Add to PATH for this session
$env:Path = "$env:APPDATA\Python\Scripts;$env:Path"

# Verify
poetry --version
```

## PowerShell Scoop Setup

```powershell
# Install Scoop (user-space package manager)
iwr -useb get.scoop.sh | iex

# Verify
scoop --version
```

## PowerShell Project Scaffolding

See "Project Scaffolding" section below for PowerShell commands.

---

# Project Scaffolding

Create a new data science project from scratch.

## Using Bash (Recommended)

```bash
# 1. Create project directory
mkdir -p ~/code/data-science
cd ~/code/data-science

# 2. Initialize git
git init
git config user.name "Your Name"
git config user.email "your.email@company.com"

# 3. Initialize Poetry project
poetry init

# Follow the interactive prompts:
# Project name: data-science
# Version: 0.1.0
# Description: Data science project with Poetry
# Author: Your Name <email>
# License: MIT
# Compatible Python versions: ^3.14

# 4. Configure Poetry to use local venv
poetry config virtualenvs.in-project true

# 5. Add core dependencies
poetry add numpy pandas matplotlib seaborn scikit-learn

# 6. Add Jupyter tools
poetry add jupyter jupyterlab ipykernel

# 7. Add optional data science packages
poetry add scipy statsmodels plotly

# 8. Add dev dependencies
poetry add --group dev pytest black ruff mypy

# 9. Install everything
poetry install

# 10. Register Jupyter kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# 11. Verify
poetry show

# 12. Launch Jupyter
poetry run jupyter lab
```

**Result:** Jupyter Lab opens in browser at `http://localhost:8888`

Create new notebook → select "Python (data-science)" kernel → start coding!

---

## Using PowerShell (Alternative)

```powershell
# 1. Create project directory
$projDir = Join-Path $env:USERPROFILE 'code\data-science'
New-Item -ItemType Directory -Path $projDir -Force | Out-Null
Set-Location $projDir

# 2. Initialize git
git init
git config user.name "Your Name"
git config user.email "your.email@company.com"

# 3. Initialize Poetry project
poetry init -n --name "data-science" --description "Data science project"

# 4. Configure Poetry
poetry config virtualenvs.in-project true

# 5. Add dependencies
poetry add numpy pandas matplotlib seaborn scikit-learn
poetry add jupyter jupyterlab ipykernel
poetry add scipy statsmodels plotly
poetry add --group dev pytest black ruff mypy

# 6. Install
poetry install

# 7. Register kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# 8. Launch Jupyter
poetry run jupyter lab
```

---

## Example pyproject.toml

This is automatically created by `poetry init`. Example:

```toml
[tool.poetry]
name = "data-science"
version = "0.1.0"
description = "Data science project with Poetry and Jupyter"
authors = ["Your Name <you@company.com>"]
license = "MIT"

[tool.poetry.dependencies]
python = "^3.14"
numpy = "^1.26"
pandas = "^2.0"
matplotlib = "^3.8"
seaborn = "^0.13"
scikit-learn = "^1.3"
jupyter = "^1.0"
jupyterlab = "^4.0"
ipykernel = "^6.26"
scipy = "^1.11"
statsmodels = "^0.14"
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

---

## Project Structure

After setup, your project looks like:

```
~/code/data-science/
├── .git/                  # Git repository
├── .venv/                 # Poetry virtual environment (local)
├── .gitignore             # Git ignore rules
├── pyproject.toml         # Poetry project definition
├── poetry.lock            # Locked dependency versions
├── README.md              # Project documentation
├── notebooks/             # Jupyter notebooks
│   └── analysis.ipynb
├── data/                  # Data files
│   ├── raw/
│   └── processed/
├── src/                   # Source code
│   └── analysis.py
└── tests/                 # Test files
    └── test_analysis.py
```

---

# Common Commands

## Poetry Workflow

```bash
# Show installed packages
poetry show

# Add new dependency
poetry add package-name

# Add dev dependency
poetry add --group dev package-name

# Update all dependencies
poetry update

# Activate Poetry shell (optional)
poetry shell

# Run command in Poetry environment
poetry run python script.py
poetry run pytest
poetry run jupyter lab

# Deactivate shell
exit

# Remove package
poetry remove package-name

# Export dependencies to requirements.txt
poetry export -f requirements.txt --output requirements.txt
```

## Jupyter Lab

```bash
# Launch Jupyter Lab
poetry run jupyter lab

# Launch with specific port
poetry run jupyter lab --port 8889

# Export notebook to HTML (no inputs)
poetry run jupyter nbconvert --to html --no-input notebook.ipynb --output notebook-presentation.html

# Export to PDF
poetry run jupyter nbconvert --to pdf notebook.ipynb

# Export to markdown
poetry run jupyter nbconvert --to markdown notebook.ipynb

# List installed kernels
jupyter kernelspec list
```

## Scoop Package Management

```bash
# Search for package
scoop search package-name

# Install package
scoop install package-name

# Update package
scoop update package-name

# Update all packages
scoop update '*'

# List installed packages
scoop list

# Remove package
scoop uninstall package-name
```

## Git Workflow

```bash
# Check status
git status

# Add all changes
git add -A

# Commit changes
git commit -m "Description of changes"

# View commit history
git log --oneline

# Push to remote
git push origin main

# Pull from remote
git pull origin main

# Create new branch
git checkout -b feature-name

# Switch branch
git checkout branch-name
```

## Bash Shell Tips

```bash
# Show full PATH
echo $PATH

# View contents of .bashrc
cat ~/.bashrc

# Edit .bashrc (nano editor)
nano ~/.bashrc

# Edit .bashrc (vim editor)
vim ~/.bashrc

# Reload .bashrc without restarting
source ~/.bashrc

# Find command location
which python
which poetry
which git

# List directory
ls -la

# Change to home directory
cd ~

# Print current directory
pwd
```

---

# Troubleshooting

## Tools Not Found

**Problem:** `poetry: command not found` (or git, python, scoop)

**Solution:**

```bash
# Reload bash profile
source ~/.bashrc

# Check if tool exists
which poetry

# If still not found, add to PATH manually
export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"
```

---

## Python Version Issues

**Problem:** `poetry install` fails due to Python version mismatch

**Solution:**

```bash
# Check Python version
python --version

# Tell Poetry to use specific Python
poetry env use /path/to/python

# Or update pyproject.toml version constraint
# Change: python = "^3.14"
# To: python = "^3.13"
```

---

## Scoop Installation Fails

**Problem:** Scoop installer fails in bash

**Solution:**

```bash
# Ensure PowerShell can execute scripts
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned

# Try installation again
powershell -NoProfile -Command "iwr -useb get.scoop.sh | iex"

# Or install via PowerShell directly (switch to PowerShell terminal)
iwr -useb get.scoop.sh | iex
```

---

## Poetry Kernel Not Available in Jupyter

**Problem:** Can't select "Python (data-science)" kernel in Jupyter

**Solution:**

```bash
# Re-register the kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)" --force

# Verify registration
jupyter kernelspec list

# Restart Jupyter Lab
# (Close browser, stop with Ctrl+C, re-run: poetry run jupyter lab)
```

---

## Git Bash Terminal Not Default in VS Code

**Problem:** VS Code opens PowerShell instead of Git Bash

**Solution:**

1. Press `Ctrl + ,` (Settings)
2. Search: `terminal.integrated.defaultProfile.windows`
3. Set to: `Git Bash`
4. Close all VS Code terminals
5. Open new terminal (`Ctrl + `` or Terminal → New Terminal)

---

## Cannot Create Project Due to Permissions

**Problem:** `Permission denied` when creating directories

**Solution:**

```bash
# Use full path with home expansion
mkdir -p ~/code/data-science

# Or explicit path
mkdir -p /c/Users/$USER/code/data-science

# Ensure you have write permissions
ls -ld ~/code

# If not writable, check Windows permissions (GUI)
```

---

## Dependencies Won't Install

**Problem:** `poetry install` fails with unresolved dependencies

**Solution:**

```bash
# Clear Poetry cache
poetry cache clear . --all

# Try install again
poetry install

# If still fails, check Python version compatibility
poetry run python --version

# Check if package is available for your Python version
pip index versions package-name
```

---

# Next Steps

## After Setup Complete

1. **Create a test notebook:**
   ```bash
   poetry run jupyter lab
   # Create notebook, select "Python (data-science)" kernel
   # Run: import pandas; print(pandas.__version__)
   ```

2. **Add more packages as needed:**
   ```bash
   poetry add new-package
   poetry install
   ```

3. **Commit to git:**
   ```bash
   git add -A
   git commit -m "Initial project setup with Poetry and Jupyter"
   ```

4. **Optional: Request Admin Access for Docker & WSL 2**
   
   Once your bash environment is working, you may want to request admin access for:
   - **Docker Desktop** (containerization)
   - **WSL 2** (native Linux environment)
   
   See `ADMIN_REQUEST.md` for details.

## Using WSL 2 (When Admin Access Approved)

Once you have admin privileges, you can set up a full Linux environment:

```bash
# Enable WSL 2 (requires admin)
wsl --install

# Install Ubuntu
wsl --install -d Ubuntu

# Enter WSL environment
wsl

# From WSL, access Windows files
cd /mnt/c/Users/<username>/code/data-science
```

WSL 2 benefits:
- Native Linux kernel
- Full package managers (`apt`, `yum`, `dnf`)
- Better performance for Linux-native tools
- Docker Desktop integration
- Direct file system access to Windows files

---

# Reference

## Installation Paths

| Tool | Bash Path | Windows Path |
|------|-----------|--------------|
| Git | `/mingw64/bin/git` | `C:\Program Files\Git\bin\git.exe` |
| Python | `/mingw64/bin/python` | `C:\Users\<user>\AppData\Local\Programs\Python\Python314\python.exe` |
| Poetry | `~/AppData/Roaming/Python/Scripts/poetry.exe` | `C:\Users\<user>\AppData\Roaming\Python\Scripts\poetry.exe` |
| Scoop | `~/scoop/shims` | `C:\Users\<user>\scoop\shims` |
| VS Code | `/mingw64/bin/code` | `C:\Users\<user>\AppData\Local\Programs\Microsoft VS Code\bin\code` |

## Bash vs Windows Paths

| Context | Bash Path | Windows Path |
|---------|-----------|--------------|
| Home | `~` or `$HOME` | `C:\Users\<username>` |
| Project | `~/code/data-science` | `C:\Users\<username>\code\data-science` |
| AppData | `~/AppData/Roaming` | `C:\Users\<username>\AppData\Roaming` |
| Temp | `/tmp` | `C:\Users\<username>\AppData\Local\Temp` |

## Quick Verification

```bash
echo "Git: $(git --version)"
echo "Python: $(python --version)"
echo "Poetry: $(poetry --version)"
echo "Scoop: $(scoop --version)"
echo "Jupyter: $(poetry run jupyter --version)"
```

---

## Additional Resources

- **Git Bash Documentation:** https://git-scm.com/
- **Python Documentation:** https://docs.python.org/
- **Poetry Documentation:** https://python-poetry.org/docs/
- **Jupyter Lab Documentation:** https://jupyterlab.readthedocs.io/
- **Scoop Documentation:** https://scoop.sh/

---

**Created:** December 16, 2025  
**Environment:** Windows 10/11 + Git Bash + Poetry + Jupyter Lab + Scoop  
**Status:** Production-ready, no admin required
