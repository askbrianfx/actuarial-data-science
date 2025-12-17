# Ì∫Ä START HERE - Complete Python & Data Science Environment

## ‚è±Ô∏è Setup Time: ~20 minutes | No Admin Required

Welcome! This is your complete guide to setting up a professional data science environment on Windows.

---

## Ì≥å Quick Overview

This workspace includes:
- ‚úÖ **Git Bash** - Unix-like shell on Windows + version control
- ‚úÖ **Python 3.14+** - Latest scientific Python
- ‚úÖ **Poetry** - Dependency management
- ‚úÖ **VS Code** - Professional IDE with extensions
- ‚úÖ **Jupyter Lab** - Interactive notebooks
- ‚úÖ **Data Science Stack** - NumPy, Pandas, Scikit-learn, Matplotlib, etc.
- ‚úÖ **No Admin Required** - Everything is user-local

---

## ÌæØ Choose Your Path

### ÌøÉ **Path 1: Just Get Started (5 minutes)**

Read ‚Üí **[QUICK_START.md](QUICK_START.md)**

This one-page guide has:
- 5-step installation checklist
- 6-step project creation
- Common issues & solutions

‚úÖ **Perfect if:** You're in a hurry and want to work right away

---

### Ì≥ñ **Path 2: Complete Setup Guide (20-30 minutes)**

Read ‚Üí **[SETUP.md](SETUP.md)** 

This 2,000+ line comprehensive guide includes:
- **Part A:** Bash installation (steps 1-8, recommended)
- **Part B:** PowerShell installation (alternative)
- **Part C:** VS Code complete setup with extensions
- **Part D:** Python & Data Science environment
- **Part E:** Project scaffolding from scratch
- **Part F:** Workflows, testing, debugging, best practices
- **Part G:** Troubleshooting
- **Part H:** After setup - 9 daily workflows

‚úÖ **Perfect if:** You want complete understanding and professional setup

---

### Ì≥ã **Path 3: Find What You Need**

Read ‚Üí **[DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md)**

This index includes:
- Overview of all documentation files
- 5 navigation scenarios
- Statistics and what's included
- Links to external resources

‚úÖ **Perfect if:** You want to find specific information quickly

---

## ÌæÆ Installation in 3 Steps

### Step 1: Install 5 Tools (10 minutes)

```bash
# 1. Git Bash
# Download & install: https://git-scm.com/download/win

# 2. Python 3.14+
# Download & install: https://www.python.org/downloads/
# IMPORTANT: Check "Add Python to PATH"

# 3. Poetry (run in Git Bash)
curl -sSL https://install.python-poetry.org | python -
echo 'export PATH="$HOME/AppData/Roaming/Python/Scripts:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 4. VS Code
# Download & install: https://code.visualstudio.com/

# 5. VS Code Extensions (Ctrl + Shift + X)
# - Python (ms-python.python)
# - Pylance (ms-python.vscode-pylance)  
# - Jupyter (ms-toolsai.jupyter)
```

### Step 2: Create Your Project (5 minutes)

```bash
mkdir -p ~/code/data-science
cd ~/code/data-science
git init

poetry init -n --name "data-science"
poetry config virtualenvs.in-project true
poetry add numpy pandas matplotlib seaborn scikit-learn jupyter jupyterlab ipykernel
poetry add --group dev pytest black ruff
poetry install

poetry run python -m ipykernel install --user --name data-science --display-name "Python (data-science)"

mkdir -p notebooks data/{raw,processed} src tests models

git add -A
git commit -m "Initial project setup"
```

### Step 3: Start Working (1 minute)

```bash
poetry run jupyter lab
```

Browser opens ‚Üí Create notebook ‚Üí Select "Python (data-science)" kernel ‚Üí Start coding! Ìæâ

---

## Ì≥ö What You Get

### Tools
- Git 2.52.0+ (version control)
- Python 3.14.2+ (scientific computing)
- Poetry 2.2.1+ (dependency management)
- VS Code (IDE)
- Jupyter Lab (notebooks)

### Data Science Stack
- NumPy (numerical)
- Pandas (data analysis)
- Matplotlib (plotting)
- Seaborn (visualization)
- Scikit-learn (ML)
- SciPy (scientific)
- And more!

### IDE Features
- Syntax highlighting
- Code completion (IntelliSense)
- Linting (Pylint, Ruff)
- Formatting (Black)
- Debugging
- Jupyter support
- Git integration

---

## Ì≤° Key Commands

```bash
# Daily workflow
poetry shell                    # Activate environment
poetry run jupyter lab          # Launch Jupyter
poetry add package-name         # Add package
poetry run pytest               # Run tests
poetry run black src/           # Format code

# Jupyter shortcuts
Shift + Enter                   # Run cell
Ctrl + /                        # Comment
Ctrl + Shift + I                # Auto-format

# VS Code shortcuts
Ctrl + Shift + P                # Command palette
Ctrl + `                        # Terminal
Ctrl + ,                        # Settings
F5                              # Debug
```

---

## Ì∂ò Common Issues (Quick Fixes)

| Issue | Fix |
|-------|-----|
| Poetry not found | `source ~/.bashrc` |
| Kernel not available | `poetry run python -m ipykernel install --user --name data-science --force` |
| Wrong terminal in VS Code | `Ctrl + ,` ‚Üí search `terminal.integrated.defaultProfile.windows` ‚Üí set to `Git Bash` |
| Python not found | Close & reopen Git Bash to refresh PATH |
| Package install fails | Update Poetry: `poetry self update` |

---

## Ì≥ñ Documentation Files

| File | Size | Purpose |
|------|------|---------|
| **QUICK_START.md** | 4 KB | 5-minute reference |
| **SETUP.md** | 47 KB | Complete guide (2,000+ lines) |
| **DOCUMENTATION_INDEX.md** | 8 KB | Navigation guide |
| **ADMIN_REQUEST.md** | 7 KB | Request Docker/WSL 2 access |
| **bash-setup.md** | 19 KB | Bash details |
| **configuration.md** | 8 KB | PowerShell reference |
| **README.md** | 3 KB | Project overview |

---

## Ìæì Next Steps

1. **Now:** Follow one of the 3 paths above
2. **In 20 mins:** Have working environment
3. **Then:** Start working on your data science project
4. **Later:** Request admin access for Docker & WSL 2 (optional, see `ADMIN_REQUEST.md`)

---

## ‚ú® What Makes This Setup Great

- **No Admin Required** - Everything installs user-local
- **Reproducible** - Same setup on any Windows machine
- **Professional** - Bash (Unix shell) + VS Code + Poetry
- **Modern Stack** - Python 3.14+ with latest packages
- **Well Documented** - 7 guides totaling 90+ KB
- **Isolated** - Poetry venv keeps dependencies clean
- **Version Controlled** - Git integration from the start
- **IDE Ready** - VS Code with all needed extensions

---

## Ì∫Ä Ready to Go?

### Pick One:

**Fast Track (5 min):**  
‚Üí Read [QUICK_START.md](QUICK_START.md)

**Complete Guide (20 min):**  
‚Üí Read [SETUP.md](SETUP.md)

**Need Specific Help:**  
‚Üí Check [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md)

---

## Ì≥û Resources

- **Python:** https://docs.python.org/
- **Poetry:** https://python-poetry.org/docs/
- **Jupyter:** https://jupyter.org/
- **Git:** https://git-scm.com/
- **VS Code:** https://code.visualstudio.com/docs

---

**Status:** ‚úÖ Complete | **No Admin:** ‚úÖ Required | **Time:** ‚è±Ô∏è ~20 minutes

Let's build something amazing! ÌæØ
