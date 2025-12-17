# Complete Python & Data Science Environment Setup

**Goal:** End-to-end setup from a fresh Windows machine to a fully scaffolded data science project with:
- ✅ Git Bash + Git version control
- ✅ Python 3.14+ with scientific packages
- ✅ Poetry for dependency management
- ✅ VS Code IDE with Python/Data Science extensions
- ✅ Jupyter Lab for interactive notebooks
- ✅ Complete scaffolded project structure

**No admin privileges required** – all installations are user-local.

---

## Table of Contents

1. [Overview](#overview)
2. [Quick Start (Bash)](#quick-start-bash)
3. [Method A: Bash Setup (Recommended)](#method-a-bash-setup-recommended)
   - Step 1: Git for Windows & Git Bash
   - Step 2: Python 3.14+
   - Step 3: Poetry
   - Step 4: VS Code + Extensions
   - Step 5: Scoop
   - Step 6: Update Bash PATH
   - Step 7: Verify Installation
4. [VS Code IDE Setup](#vs-code-ide-setup)
5. [Method B: PowerShell Setup (Alternative)](#method-b-powershell-setup-alternative)
6. [Project Scaffolding](#project-scaffolding)
7. [Python/Data Science Environment](#pythondata-science-environment)
8. [Common Commands](#common-commands)
9. [Troubleshooting](#troubleshooting)
10. [Next Steps](#next-steps)

---

## Overview

| Aspect | Details |
|--------|---------|
| **Primary Shell** | Bash (Git Bash on Windows) |
| **Alternative Shell** | PowerShell (for comparison) |
| **Python Version** | 3.14+ (latest scientific stack) |
| **Python Manager** | Poetry 2.2.1+ |
| **Package Manager** | Scoop (user-space, no admin) |
| **IDE** | VS Code + Python extensions |
| **Notebook Environment** | Jupyter Lab |
| **Version Control** | Git 2.52.0+ |
| **Data Science Stack** | NumPy, Pandas, Matplotlib, Seaborn, Scikit-learn, SciPy |
| **Required Admin** | No |
| **Time to Setup** | ~20-25 minutes |

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

# VS Code IDE Setup

**VS Code** is your primary development environment for data science work. Configure it for Python development.

## Step 8: VS Code Configuration

### Terminal Configuration (Git Bash Default)

After opening VS Code:

**Option 1: Settings UI**

1. Press `Ctrl + ,` (Settings)
2. Search for: `terminal.integrated.defaultProfile.windows`
3. Set to: `Git Bash`
4. Search for: `terminal.integrated.shell.windows`
5. Set to: `C:\Program Files\Git\bin\bash.exe` (or your Git installation path)

**Option 2: Settings JSON**

Press `Ctrl + Shift + P` → "Preferences: Open Settings (JSON)" and add:

```json
{
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": ["--login", "-i"]
}
```

**Verify:**

1. Open VS Code
2. Press `` Ctrl + ` `` (backtick) to open terminal
3. Should see: `user@COMPUTERNAME MINGW64 ~/path`

### Python Extension Setup

1. Press `Ctrl + Shift + X` (Extensions sidebar)
2. Search and install **"Python"** (by Microsoft)
   - ID: `ms-python.python`
3. Search and install **"Pylance"** (by Microsoft)
   - ID: `ms-python.vscode-pylance`
   - Provides IntelliSense, type checking, code navigation

VS Code will auto-detect your Poetry virtual environment.

**Verify Python detection:**

1. Press `` Ctrl + Shift + ` `` (open terminal in project directory)
2. Press `Ctrl + Shift + P` → "Python: Select Interpreter"
3. Should show Poetry venv path: `/path/to/project/.venv/bin/python`

### Recommended Data Science Extensions

Install these via `Ctrl + Shift + X`:

| Extension | Publisher | ID | Purpose |
|-----------|-----------|----|---------| 
| **Python** | Microsoft | `ms-python.python` | Core Python support |
| **Pylance** | Microsoft | `ms-python.vscode-pylance` | IntelliSense & type checking |
| **Jupyter** | Microsoft | `ms-toolsai.jupyter` | Jupyter notebook support |
| **Pylint** | Microsoft | `ms-python.pylint` | Code linting |
| **Black Formatter** | Microsoft | `ms-python.black-formatter` | Code formatting |
| **Even Better TOML** | tamasfe | `tamasfe.even-better-toml` | TOML syntax highlighting |
| **Git Graph** | mhutchie | `mhutchie.git-graph` | Git visualization |
| **Thunder Client** | Thunder Client | `thunderclient.thunderclient` | API testing (optional) |
| **Markdown Preview** | Microsoft | `ms-vscode.markdown-all-in-one` | Enhanced markdown |

**Quick Install:**

```bash
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-toolsai.jupyter
code --install-extension ms-python.pylint
code --install-extension ms-python.black-formatter
code --install-extension tamasfe.even-better-toml
code --install-extension mhutchie.git-graph
code --install-extension ms-vscode.markdown-all-in-one
```

### Python Settings in VS Code

Add to `settings.json` (or configure via Settings UI):

```json
{
  "[python]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.codeActionsOnSave": {
      "source.organizeImports": "explicit"
    }
  },
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "python.testing.pytestEnabled": true,
  "python.testing.pytestArgs": [
    "tests"
  ],
  "jupyter.notebookFileRoot": "${workspaceFolder}",
  "python.analysis.extraPaths": [
    "${workspaceFolder}/src"
  ]
}
```

**What this does:**
- Auto-format Python code with Black on save
- Organize imports automatically
- Enable Pylint for code linting
- Configure pytest for testing
- Set Jupyter notebook root
- Add `src/` to Python path for imports

### Workspace Settings

Create `.vscode/settings.json` in your project directory:

```json
{
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": ["--login", "-i"],
  
  "[python]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "ms-python.black-formatter"
  },
  
  "python.linting.pylintEnabled": true,
  "python.testing.pytestEnabled": true,
  "python.analysis.extraPaths": ["${workspaceFolder}/src"],
  
  "editor.rulers": [80, 100, 120],
  "editor.wordWrap": "on",
  "files.exclude": {
    "**/__pycache__": true,
    "**/*.pyc": true,
    "**/.pytest_cache": true,
    "**/.mypy_cache": true
  }
}
```

### Debugging Python Code

Create `.vscode/launch.json` for debugging:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "justMyCode": true
    },
    {
      "name": "Python: Poetry Run",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "env": { "PYTHONPATH": "${workspaceFolder}/src" }
    },
    {
      "name": "pytest: Current File",
      "type": "python",
      "request": "launch",
      "module": "pytest",
      "args": ["${file}", "-v"],
      "console": "integratedTerminal"
    }
  ]
}
```

**Use debugging:**
1. Set breakpoint by clicking line number (red dot)
2. Select debug configuration from Run menu (or `Ctrl + Shift + D`)
3. Press F5 to start debugging
4. Step through code with F10/F11

### Jupyter Notebook Support in VS Code

With the **Jupyter extension** installed, you can:

1. Create notebooks directly in VS Code
2. Open `.ipynb` files for interactive editing
3. Run cells with `Ctrl + Enter` or `Shift + Enter`
4. Select kernel from notebook toolbar

**Create new notebook:**
- `Ctrl + Shift + P` → "Create: New Jupyter Notebook"
- Save as `analysis.ipynb`
- Select Python kernel (Poetry environment)

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

# 3. Create .gitignore (see section below)
cat > .gitignore << 'EOF'
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
ENV/
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg

# Poetry
poetry.lock

# Virtual environments
.venv/
.env

# Jupyter
.ipynb_checkpoints/
*.ipynb_checkpoints

# IDEs
.vscode/
.idea/
*.swp
*.swo
*~
.DS_Store

# Data
data/raw/
data/processed/

# Models
models/*.pkl
models/*.joblib

# Testing
.pytest_cache/
.coverage
htmlcov/

# Type checking
.mypy_cache/

# Linting
.ruff_cache/
EOF

# 4. Initialize Poetry project
poetry init

# Follow the interactive prompts:
# Project name: data-science
# Version: 0.1.0
# Description: Data science project with Poetry
# Author: Your Name <email>
# License: MIT
# Compatible Python versions: ^3.14

# 5. Configure Poetry to use local venv
poetry config virtualenvs.in-project true

# 6. Add core dependencies
poetry add numpy pandas matplotlib seaborn scikit-learn

# 7. Add Jupyter tools
poetry add jupyter jupyterlab ipykernel

# 8. Add optional data science packages
poetry add scipy statsmodels plotly

# 9. Add dev dependencies
poetry add --group dev pytest black ruff mypy

# 10. Install everything
poetry install

# 11. Register Jupyter kernel
poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

# 12. Create project directories
mkdir -p notebooks data/{raw,processed} src tests models

# 13. Create initial files
cat > README.md << 'EOF'
# Data Science Project

Description of your project here.

## Quick Start

```bash
poetry install
poetry run jupyter lab
```

## Project Structure

- `notebooks/` - Jupyter notebooks for analysis
- `data/` - Raw and processed data
- `src/` - Source code modules
- `tests/` - Unit tests
- `models/` - Trained models
EOF

cat > src/__init__.py << 'EOF'
"""Data science project module."""
__version__ = "0.1.0"
EOF

# 14. Initial commit
git add -A
git commit -m "Initial project setup with Poetry and Jupyter"

# 15. Verify
poetry show

# 16. Launch Jupyter
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

# Python & Data Science Environment

## Python 3.14+ Overview

**Version:** 3.14.2+ (latest stable)

**Key Features:**
- Modern async/await support
- Type hints and generics
- Performance improvements
- Improved error messages

## Core Data Science Stack

Your environment includes proven data science packages:

| Package | Version | Purpose | Install |
|---------|---------|---------|---------|
| **NumPy** | ^1.26 | Numerical computing, arrays | `poetry add numpy` |
| **Pandas** | ^2.0 | Data manipulation & analysis | `poetry add pandas` |
| **Matplotlib** | ^3.8 | 2D plotting and visualization | `poetry add matplotlib` |
| **Seaborn** | ^0.13 | Statistical data visualization | `poetry add seaborn` |
| **Scikit-learn** | ^1.3 | Machine learning algorithms | `poetry add scikit-learn` |
| **SciPy** | ^1.11 | Scientific computing utilities | `poetry add scipy` |
| **Statsmodels** | ^0.14 | Statistical modeling | `poetry add statsmodels` |
| **Plotly** | ^5.17 | Interactive visualizations | `poetry add plotly` |

### Optional Packages

```bash
# Add any of these as needed
poetry add jupyter jupyterlab ipykernel    # Already included
poetry add dask                             # Distributed computing
poetry add tensorflow                       # Deep learning
poetry add torch torchvision               # PyTorch
poetry add xgboost lightgbm                # Gradient boosting
poetry add networkx                         # Network analysis
poetry add sympy                            # Symbolic math
```

### Development Dependencies

```bash
poetry add --group dev pytest              # Testing
poetry add --group dev black               # Code formatting
poetry add --group dev ruff                # Fast linting
poetry add --group dev mypy                # Type checking
poetry add --group dev sphinx              # Documentation
poetry add --group dev pre-commit          # Git hooks
```

## Virtual Environment Management

Poetry creates isolated Python environments per project.

**View current environment:**

```bash
poetry env info
# Shows: Path, Python version, installed packages

poetry env list
# Lists all Poetry environments for this project
```

**Use specific Python version:**

```bash
poetry env use 3.14
# Creates venv with Python 3.14

poetry env use /path/to/python.exe
# Use custom Python installation
```

**Remove environment:**

```bash
poetry env remove data-science
# Removes the virtual environment
```

## Python Path and Imports

### Add Source Directory to Python Path

In VS Code `settings.json`:

```json
{
  "python.analysis.extraPaths": ["${workspaceFolder}/src"]
}
```

This allows imports like:

```python
# Instead of: from ..src.module import function
# You can use:
from module import function
```

### Create Python Modules

Structure your code in `src/`:

```
src/
├── __init__.py
├── data/
│   ├── __init__.py
│   ├── load.py
│   └── transform.py
├── models/
│   ├── __init__.py
│   ├── train.py
│   └── evaluate.py
└── utils/
    ├── __init__.py
    ├── helpers.py
    └── constants.py
```

Use in notebooks:

```python
from data.load import load_data
from models.train import train_model
from utils.helpers import process_features
```

## Package Management

### Adding Packages

```bash
# Add specific version
poetry add pandas==2.0.0

# Add with version constraint
poetry add "pandas>=2.0,<3.0"

# Add multiple at once
poetry add numpy pandas matplotlib scikit-learn

# Add with extras (additional features)
poetry add jupyter[all]
poetry add sqlalchemy[postgresql]

# Add as dev dependency only
poetry add --group dev pytest sphinx
```

### Updating Packages

```bash
# Update all packages to latest compatible versions
poetry update

# Update specific package
poetry update numpy

# Show outdated packages
poetry show --outdated
```

### Dependency Constraints

In `pyproject.toml`, use standard version specifiers:

```toml
python = "^3.14"              # >=3.14.0, <4.0.0
numpy = "~1.26"               # >=1.26.0, <1.27.0
pandas = ">=2.0,<3.0"         # Exact range
scipy = "*"                   # Any version
```

## Jupyter Lab Advanced Usage

### Notebook Organization

```bash
# Create notebooks directory
mkdir -p notebooks

# Create project notebook
poetry run jupyter lab

# In Jupyter, create: notebooks/01-data-exploration.ipynb
```

### Jupyter Extensions

Install useful extensions:

```bash
# Enable extension manager
poetry run jupyter labextension list

# Install extensions (if using older Jupyter)
poetry run pip install jupyterlab-git
poetry run pip install jupyterlab-lsp
```

### Export and Sharing

```bash
# Export to HTML (for presentations/sharing)
poetry run jupyter nbconvert --to html --no-input notebook.ipynb

# Export to PDF (requires nbconvert + pandoc)
poetry run jupyter nbconvert --to pdf notebook.ipynb

# Export to Markdown (for documentation)
poetry run jupyter nbconvert --to markdown notebook.ipynb

# Export to Python script
poetry run jupyter nbconvert --to script notebook.ipynb
```

### Jupyter Configuration

Create `~/.jupyter/jupyter_notebook_config.py`:

```python
# Auto-save every 30 seconds
c.ContentsManager.autosave_interval = 30

# Line numbers by default
c.NotebookApp.nbserver_extensions = {'jupyterlab': True}

# Default cell type
c.NotebookApp.default_cell_type = 'code'
```

## Testing and Quality

### Running Tests

```bash
# Run all tests
poetry run pytest

# Run specific test file
poetry run pytest tests/test_module.py

# Run with coverage
poetry run pytest --cov=src tests/

# Run with verbose output
poetry run pytest -v

# Run and show print statements
poetry run pytest -s
```

### Code Formatting

```bash
# Format code with Black
poetry run black src/ notebooks/

# Check formatting without changes
poetry run black --check src/

# Format with custom line length
poetry run black --line-length 100 src/
```

### Linting and Type Checking

```bash
# Lint with Pylint
poetry run pylint src/

# Lint with Ruff (faster)
poetry run ruff check src/

# Fix linting issues automatically
poetry run ruff check --fix src/

# Type checking with mypy
poetry run mypy src/

# Type checking with strict mode
poetry run mypy --strict src/
```

## Working with Data

### Common Data Science Workflow

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

# Load data
df = pd.read_csv('data/raw/dataset.csv')

# Explore
print(df.info())
print(df.describe())

# Visualize
plt.figure(figsize=(10, 6))
sns.heatmap(df.corr(), annot=True)
plt.show()

# Preprocess
X = df.drop('target', axis=1)
y = df['target']
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2)

# Train model
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

# Evaluate
y_pred = model.predict(X_test)
print(classification_report(y_test, y_pred))
```

### Save/Load Models

```python
import pickle
import joblib

# Save model
joblib.dump(model, 'models/model.pkl')

# Load model
model = joblib.load('models/model.pkl')

# Save data processing pipeline
joblib.dump(scaler, 'models/scaler.pkl')
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

## VS Code Tips & Keyboard Shortcuts

### Essential Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + Shift + P` | Command Palette (search anything) |
| `Ctrl + K Ctrl + S` | Keyboard Shortcuts reference |
| `Ctrl + ,` | Settings |
| `Ctrl + `` | Toggle terminal |
| `Ctrl + Shift + `` | New terminal |
| `Ctrl + /` | Toggle line comment |
| `Ctrl + Shift + /` | Toggle block comment |
| `Ctrl + F` | Find |
| `Ctrl + H` | Find and Replace |
| `Ctrl + J` | Toggle panel (output/terminal) |
| `Ctrl + B` | Toggle Explorer sidebar |
| `Ctrl + Shift + X` | Extensions |
| `Ctrl + Shift + D` | Debug/Run |
| `F5` | Start/Continue debugging |
| `F10` | Step over |
| `F11` | Step into |
| `Shift + F11` | Step out |
| `Shift + Enter` | Run cell (Jupyter) |
| `Ctrl + Enter` | Run current line as code |

### Python-Specific Commands

```bash
# Format document
Ctrl + Shift + I

# Organize imports
Ctrl + Shift + O

# Quick fix
Ctrl + .

# Run Python file
Ctrl + F5

# Go to definition
Ctrl + Click (or F12)

# Find all references
Ctrl + Shift + F10

# Rename symbol
F2

# Extract method/function
Ctrl + Shift + R
```

### VS Code Python Profile

Create `.vscode/keybindings.json` for custom Python shortcuts:

```json
[
  {
    "key": "ctrl+shift+b",
    "command": "python.runSelectionInTerminal",
    "when": "editorTextFocus && editorLangId == 'python'"
  },
  {
    "key": "ctrl+shift+f5",
    "command": "python.debugAll",
    "when": "editorTextFocus && editorLangId == 'python'"
  }
]
```

### Useful VS Code Extensions (Already Installed)

**Python Development:**
- **Python** (ms-python.python) - Core Python support
- **Pylance** (ms-python.vscode-pylance) - Advanced IntelliSense
- **Jupyter** (ms-toolsai.jupyter) - Interactive notebooks
- **Pylint** (ms-python.pylint) - Code linting

**Code Quality:**
- **Black Formatter** (ms-python.black-formatter) - Auto-formatting
- **Even Better TOML** (tamasfe.even-better-toml) - pyproject.toml support

**Git & Version Control:**
- **Git Graph** (mhutchie.git-graph) - Visual git history
- **GitLens** (eamodio.gitlens) - Git annotations

**Productivity:**
- **Markdown All in One** (ms-vscode.markdown-all-in-one) - Markdown support
- **Thunder Client** (thunderclient.thunderclient) - API testing

### Debugging Python in VS Code

1. Set breakpoint (click line number → red dot appears)
2. Press F5 or `Ctrl + Shift + D` → "Run and Debug"
3. Select Python environment (should auto-detect Poetry venv)
4. Use Debug Console to inspect variables:
   ```python
   >>> variable_name  # Show variable value
   >>> type(obj)      # Check type
   >>> len(data)      # Check size
   ```
5. Step through code with F10 (step over), F11 (step into)

### Running Jupyter Cells in VS Code

With Jupyter extension installed:

1. Create or open `.ipynb` notebook
2. Click "Select Kernel" → choose "Python (data-science)"
3. Run individual cells with Shift + Enter
4. View outputs inline
5. Use terminal integration with the notebook

### Remote Development (Optional)

Connect to remote machines or WSL 2:

1. Install **Remote - WSL** extension
2. Install **Remote - SSH** extension
3. Open Command Palette → "Remote-Containers: Reopen in Container"

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

### Step 1: Verify Complete Installation

```bash
# Test all components
poetry show                          # List packages
poetry run python --version          # Python version
poetry run jupyter --version         # Jupyter version

# Test key packages
poetry run python -c "import numpy; print(f'NumPy: {numpy.__version__}')"
poetry run python -c "import pandas; print(f'Pandas: {pandas.__version__}')"
poetry run python -c "import sklearn; print(f'Scikit-learn: {sklearn.__version__}')"
```

### Step 2: Create Your First Analysis Notebook

```bash
# Launch Jupyter Lab
poetry run jupyter lab

# In Jupyter Lab:
# 1. File → New → Notebook
# 2. Select "Python (data-science)" kernel
# 3. Create analysis notebook
```

**Example first notebook cell:**

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Create sample data
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Score': [85, 92, 78, 95]
}
df = pd.DataFrame(data)

# Display
print(df)
print(f"\nMean score: {df['Score'].mean():.2f}")

# Plot
df.plot(x='Name', y='Score', kind='bar')
plt.title('Student Scores')
plt.show()
```

Run cells with `Shift + Enter`.

### Step 3: Organize Your Code

Create a modular project structure:

```bash
# Create src module structure
mkdir -p src/data src/models src/utils

# Create __init__.py files
touch src/__init__.py src/data/__init__.py src/models/__init__.py src/utils/__init__.py

# Create example modules
cat > src/data/load.py << 'EOF'
"""Data loading utilities."""
import pandas as pd

def load_dataset(filepath):
    """Load CSV dataset."""
    return pd.read_csv(filepath)

def info_summary(df):
    """Print dataset summary."""
    print(f"Shape: {df.shape}")
    print(f"\nColumns: {df.columns.tolist()}")
    print(f"\nData types:\n{df.dtypes}")
    print(f"\nMissing values:\n{df.isnull().sum()}")
EOF

cat > src/utils/helpers.py << 'EOF'
"""Utility helper functions."""

def normalize(data):
    """Normalize data to 0-1 range."""
    return (data - data.min()) / (data.max() - data.min())

def describe_stats(series):
    """Print statistics for a series."""
    stats = {
        'mean': series.mean(),
        'std': series.std(),
        'min': series.min(),
        'max': series.max()
    }
    return stats
EOF
```

Use in notebooks:

```python
from data.load import load_dataset, info_summary
from utils.helpers import normalize, describe_stats

# Load data
df = load_dataset('data/raw/dataset.csv')
info_summary(df)

# Process
df['normalized'] = normalize(df['value'])
stats = describe_stats(df['value'])
```

### Step 4: Set Up Version Control Workflow

```bash
# Create feature branch for your analysis
git checkout -b feature/initial-analysis

# Work on notebooks and code
# ... edit files, run experiments ...

# Stage changes
git add notebooks/ src/ data/processed/

# Commit with clear message
git commit -m "feat: Add initial data exploration and visualization"

# Switch back to main
git checkout main

# Merge feature branch
git merge feature/initial-analysis

# View history
git log --oneline --graph
```

### Step 5: Install Additional Packages As Needed

Common additions for data science:

```bash
# Machine Learning
poetry add scikit-learn xgboost lightgbm

# Deep Learning
poetry add tensorflow  # or pytorch

# Visualization
poetry add plotly seaborn folium

# Database
poetry add sqlalchemy psycopg2-binary pymongo

# APIs & Web
poetry add requests httpx

# Data manipulation
poetry add openpyxl xlrd  # Excel
poetry add python-dotenv  # Environment variables

# Testing
poetry add --group dev pytest-cov pytest-mock

# Documentation
poetry add --group dev sphinx sphinx-rtd-theme
```

### Step 6: Advanced Jupyter Usage

**Export notebook for presentation:**

```bash
# Remove code cells (show results only)
poetry run jupyter nbconvert --to html --no-input notebook.ipynb --output presentation.html

# Create PDF
poetry run jupyter nbconvert --to pdf notebook.ipynb

# Create slide presentation
poetry run jupyter nbconvert --to slides notebook.ipynb
```

**Jupyter Lab shortcuts:**

- `Shift + Enter` - Run cell and move to next
- `Ctrl + Enter` - Run cell and stay
- `Alt + Enter` - Run cell and insert new
- `Ctrl + /` - Toggle comment
- `Ctrl + ]` - Indent
- `Ctrl + [` - Dedent

### Step 7: Development Workflow Best Practices

**Use `.python-version` for consistency:**

```bash
# Create in project root
echo "3.14.2" > .python-version

# Poetry will use this version if available
```

**Create pre-commit hooks:**

```bash
# Install pre-commit framework
poetry add --group dev pre-commit

# Create .pre-commit-config.yaml
cat > .pre-commit-config.yaml << 'EOF'
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml

  - repo: https://github.com/psf/black
    rev: 23.11.0
    hooks:
      - id: black
        language_version: python3.14

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.5
    hooks:
      - id: ruff
        args: [--fix]
EOF

# Install pre-commit hooks
poetry run pre-commit install

# Run on all files
poetry run pre-commit run --all-files
```

**Use type hints:**

```python
from typing import List, Dict, Tuple
import pandas as pd

def process_data(
    df: pd.DataFrame,
    columns: List[str],
    fill_value: float = 0.0
) -> Tuple[pd.DataFrame, Dict[str, int]]:
    """Process dataframe and return results."""
    df_filled = df[columns].fillna(fill_value)
    stats = {col: df_filled[col].count() for col in columns}
    return df_filled, stats
```

### Step 8: Quick Daily Workflow

```bash
# Morning: Start development environment
cd ~/code/data-science
poetry shell                          # Activate virtual environment

# Run tests
poetry run pytest -v

# Format code
poetry run black src/ notebooks/

# Lint
poetry run ruff check --fix src/

# Open IDE
code .                                # Open in VS Code

# Launch Jupyter
poetry run jupyter lab

# ... work on analysis ...

# Evening: Commit your work
git add -A
git commit -m "day: Feature development progress"
git push origin main

# Exit poetry shell
exit
```

### Step 9: Collaboration & Sharing

**Share requirements:**

```bash
# Export dependencies
poetry export -f requirements.txt --output requirements.txt

# Team member can install
pip install -r requirements.txt
```

**Create project snapshot:**

```bash
# Jupyter notebook becomes standalone export
poetry run jupyter nbconvert --to html notebook.ipynb

# Share HTML file with non-technical stakeholders
```

**Docker deployment (advanced):**

Create `Dockerfile`:

```dockerfile
FROM python:3.14-slim

WORKDIR /app

# Copy project files
COPY pyproject.toml poetry.lock ./
COPY src/ ./src/
COPY data/ ./data/

# Install Poetry
RUN pip install poetry

# Install dependencies
RUN poetry config virtualenvs.create false && \
    poetry install --no-dev

# Launch Jupyter
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root"]
```

Build and run:

```bash
docker build -t data-science .
docker run -p 8888:8888 data-science
```

---

## Optional: Request Admin Access for Docker & WSL 2

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
