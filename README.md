# learning-python

A comprehensive guide for setting up Python development environments in WSL (Ubuntu).

## Table of Contents
- [Installing Python on WSL (Ubuntu)](#installing-python-on-wsl-ubuntu)
- [Setting Up Virtual Environments](#setting-up-virtual-environments)
- [Managing Your Virtual Environment](#managing-your-virtual-environment)
- [Best Practices](#best-practices)

## Installing Python on WSL (Ubuntu)

### Step 1: Update System Packages
First, ensure your system packages are up to date:

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Python
Ubuntu usually comes with Python pre-installed. Check your Python version:

```bash
python3 --version
```

If Python is not installed or you want to install a specific version:

```bash
# Install Python 3 and pip
sudo apt install python3 python3-pip -y

# Install additional useful packages
sudo apt install python3-venv python3-dev build-essential -y
```

### Step 3: Verify Installation
Confirm Python and pip are installed correctly:

```bash
python3 --version
pip3 --version
```

### Step 4: Set Python3 as Default (Optional)
To use `python` instead of `python3`:

```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
```

## Setting Up Virtual Environments

### Step 1: Navigate to Your Project Directory
```bash
cd /path/to/your/project
# Example: cd ~/Documents/my-python-project
```

### Step 2: Create a Virtual Environment
Create a virtual environment named `venv` (you can use any name):

```bash
python3 -m venv venv
```

This creates a directory called `venv` containing:
- Python interpreter
- pip package manager
- Isolated package installation directory

### Step 3: Activate the Virtual Environment
```bash
source venv/bin/activate
```

After activation, your terminal prompt will change to show `(venv)` at the beginning:
```
(venv) user@hostname:~/project$
```

### Step 4: Verify Virtual Environment
Check that you're using the virtual environment's Python:

```bash
which python
# Should output: /path/to/your/project/venv/bin/python

python --version
pip --version
```

### Step 5: Install Packages
Now you can install packages that will be isolated to this project:

```bash
pip install package-name
# Example: pip install requests numpy pandas
```

### Step 6: Create Requirements File
Save your installed packages to a file:

```bash
pip freeze > requirements.txt
```

## Managing Your Virtual Environment

### Deactivating the Virtual Environment
When you're done working:

```bash
deactivate
```

### Reactivating Later
Navigate to your project directory and activate again:

```bash
cd /path/to/your/project
source venv/bin/activate
```

### Installing from Requirements File
When cloning a project or setting up on a new machine:

```bash
# Create and activate virtual environment first
python3 -m venv venv
source venv/bin/activate

# Install all dependencies
pip install -r requirements.txt
```

### Deleting a Virtual Environment
Simply delete the venv directory:

```bash
# Make sure it's deactivated first
deactivate

# Remove the directory
rm -rf venv
```

### Upgrading pip
Keep pip updated within your virtual environment:

```bash
pip install --upgrade pip
```

## Best Practices

### 1. Always Use Virtual Environments
- Create a separate virtual environment for each project
- Prevents dependency conflicts between projects
- Makes project dependencies explicit and reproducible

### 2. Add venv to .gitignore
Never commit your virtual environment to version control:

```bash
echo "venv/" >> .gitignore
echo "*.pyc" >> .gitignore
echo "__pycache__/" >> .gitignore
```

### 3. Document Dependencies
Always maintain an updated `requirements.txt`:

```bash
# Update after installing new packages
pip freeze > requirements.txt
```

### 4. Use Descriptive Names
If working with multiple Python versions:

```bash
python3.9 -m venv venv39
python3.11 -m venv venv311
```

### 5. Directory Structure
Recommended project structure:

```
my-project/
├── venv/                 # Virtual environment (not in git)
├── src/                  # Source code
│   └── main.py
├── tests/                # Test files
├── requirements.txt      # Dependencies
├── .gitignore           # Git ignore file
└── README.md            # Project documentation
```

### 6. Quick Setup Script
Create a `setup.sh` file for quick project setup:

```bash
#!/bin/bash
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
echo "Environment ready! Virtual environment activated."
```

Make it executable:
```bash
chmod +x setup.sh
./setup.sh
```

## Common Commands Cheat Sheet

```bash
# Create virtual environment
python3 -m venv venv

# Activate (Linux/WSL/Mac)
source venv/bin/activate

# Deactivate
deactivate

# Install package
pip install package-name

# Install specific version
pip install package-name==1.2.3

# Install from requirements
pip install -r requirements.txt

# Save current packages
pip freeze > requirements.txt

# List installed packages
pip list

# Uninstall package
pip uninstall package-name

# Upgrade package
pip install --upgrade package-name
```

## Troubleshooting

### Issue: `python3-venv` not found
```bash
sudo apt update
sudo apt install python3-venv -y
```

### Issue: Permission denied
Don't use `sudo` with pip inside virtual environments. If you see permission errors, ensure your virtual environment is activated.

### Issue: Command not found after activation
Make sure you're using `source` to activate:
```bash
source venv/bin/activate  # Correct
./venv/bin/activate       # Won't work in bash/zsh
```

### Issue: Different Python version needed
Install specific Python version:
```bash
sudo apt install python3.11 python3.11-venv
python3.11 -m venv venv
```

---

**Happy coding! 🐍**
