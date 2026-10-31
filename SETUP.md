# 🛠️ Environment Setup Guide: Django Masterclass

Welcome to the **Complete Django Masterclass** environment setup guide! Before starting with **Day 1**, you need a fully configured development environment. This guide walks you through every step for **Windows (PowerShell / Command Prompt)**, **macOS**, and **Linux**.

---

## 📋 Table of Contents
1. [Installing Python](#1-installing-python)
2. [Installing Visual Studio Code & Extensions](#2-installing-visual-studio-code--extensions)
3. [Setting Up Your Project Workspace](#3-setting-up-your-project-workspace)
4. [Creating and Activating a Virtual Environment](#4-creating-and-activating-a-virtual-environment)
5. [Installing Django and Dependencies](#5-installing-django-and-dependencies)
6. [Creating Your First Django Project & Application](#6-creating-your-first-django-project--application)
7. [Running the Django Development Server](#7-running-the-django-development-server)
8. [Installing Django REST Framework (DRF)](#8-installing-django-rest-framework-drf)
9. [Setting Up MySQL (For Phase 6 & Day 29)](#9-setting-up-mysql-for-phase-6--day-29)
10. [Troubleshooting Common Setup Errors](#10-troubleshooting-common-setup-errors)

---

## 1. Installing Python

Django 5.x requires **Python 3.10, 3.11, or 3.12+**. 

### 🪟 Windows Installation:
1. Visit the official download page: [python.org/downloads](https://www.python.org/downloads/).
2. Download the latest Python 3 installer (e.g., Python 3.11 or 3.12).
3. **CRITICAL STEP:** In the installer wizard, check the box:
   > ☑️ **Add python.exe to PATH**
4. Click **Install Now**.
5. After installation, open PowerShell and verify:
   ```powershell
   python --version
   pip --version
   ```
   *Expected output:* `Python 3.11.x` (or newer) and `pip 24.x`.

### 🍎 macOS Installation:
Using [Homebrew](https://brew.sh/):
```bash
brew install python
python3 --version
pip3 --version
```

### 🐧 Linux (Ubuntu/Debian) Installation:
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv -y
python3 --version
```

---

## 2. Installing Visual Studio Code & Extensions

We strongly recommend **Visual Studio Code (VS Code)** for Django development.

1. Download and install VS Code from [code.visualstudio.com](https://code.visualstudio.com/).
2. Open VS Code and open the Extensions view (`Ctrl + Shift + X` on Windows/Linux or `Cmd + Shift + X` on macOS).
3. Install the following essential extensions:
   - **Python** (by Microsoft) – Language support, IntelliSense, linting, and debugging.
   - **Django** (by Baptiste Darthenay) – Syntax highlighting and autocompletion for Django templates and tags.
   - **Django View** – Quick navigation between views, models, and templates.
   - **SQLite Viewer** (by Florian Klampfer) – Explore SQLite databases directly inside VS Code.
   - **Thunder Client** or **Postman** – Testing REST APIs.

---

## 3. Setting Up Your Project Workspace

Create a dedicated folder for your Django practice:

### 🪟 Windows (PowerShell):
```powershell
mkdir C:\Users\$env:USERNAME\django_workspace
cd C:\Users\$env:USERNAME\django_workspace
```

### 🍎 macOS / 🐧 Linux:
```bash
mkdir -p ~/django_workspace
cd ~/django_workspace
```

---

## 4. Creating and Activating a Virtual Environment

A **virtual environment** isolates your Django packages from the global Python installation, preventing version conflicts between projects.

### Step 1: Create the Virtual Environment
```bash
# Windows
python -m venv venv

# macOS / Linux
python3 -m venv venv
```

### Step 2: Activate the Virtual Environment

**🪟 Windows (PowerShell):**
```powershell
.\venv\Scripts\Activate.ps1
```
> *Note for PowerShell users:* If you receive an `Execution_Policies` error, run:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```
> then re-run `.\venv\Scripts\Activate.ps1`.

**🪟 Windows (Command Prompt `cmd`):**
```cmd
venv\Scripts\activate.bat
```

**🍎 macOS / 🐧 Linux:**
```bash
source venv/bin/activate
```

*When activated, your terminal prompt will show `(venv)` prefix.*

### Step 3: Upgrading pip
```bash
python -m pip install --upgrade pip
```

---

## 5. Installing Django and Dependencies

With your virtual environment active, install Django:

```bash
pip install django
```

Verify the installation and check the version:
```bash
python -m django --version
```
*Expected output:* `5.1.x` (or latest stable version).

You can also run:
```bash
django-admin --version
```

---

## 6. Creating Your First Django Project & Application

### Step 1: Create a Django Project
Run `django-admin startproject` followed by your project name:
```bash
django-admin startproject myproject .
```
*(Notice the `.` at the end; this creates the project configuration inside the current directory without creating unnecessary nested folders).*

The generated project structure:
```text
myproject/
│── manage.py
└── myproject/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

### Step 2: Create a Django Application
A Django project is made of one or more modular **applications**:
```bash
python manage.py startapp core
```

Register `core` in `myproject/settings.py` under `INSTALLED_APPS`:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Custom apps
    'core',
]
```

---

## 7. Running the Django Development Server

Run initial database migrations (creates internal authentication and session tables):
```bash
python manage.py migrate
```

Start the built-in development web server:
```bash
python manage.py runserver
```

*Expected terminal output:*
```text
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
October 31, 2026 - 12:00:00
Django version 5.1.x, using settings 'myproject.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK (or CTRL-C).
```

Open your browser and navigate to:
👉 **`http://127.0.0.1:8000/`** or **`http://localhost:8000/`**

You should see the celebratory Django rocket welcome page: **"The install worked successfully! Congratulations!"**

To stop the server, press `Ctrl + C` in the terminal.

---

## 8. Installing Django REST Framework (DRF)

For Phase 5 (REST APIs) and Phase 6, install **Django REST Framework** and **SimpleJWT**:

```bash
pip install djangorestframework django-cors-headers djangorestframework-simplejwt
```

Add them to `INSTALLED_APPS` in `settings.py`:
```python
INSTALLED_APPS = [
    ...,
    'rest_framework',
    'rest_framework.authtoken',
    'corsheaders',
]
```

---

## 9. Setting Up MySQL (For Phase 6 & Day 29)

While SQLite is built-in and works out-of-the-box for learning, production systems typically use MySQL or PostgreSQL.

### Step 1: Install MySQL Server
- **Windows:** Download and run the [MySQL Community Server Installer](https://dev.mysql.com/downloads/installer/).
- **macOS:** `brew install mysql && brew services start mysql`
- **Linux:** `sudo apt install mysql-server -y && sudo systemctl start mysql`

### Step 2: Install the Python MySQL Client
```bash
pip install mysqlclient
```
*(If `mysqlclient` requires compilation tools on Windows, you can alternatively use `pip install pymysql` and install PyMySQL as demonstrated in Day 29).*

### Step 3: Create a Database
In your MySQL command line:
```sql
CREATE DATABASE djangodb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

---

## 10. Troubleshooting Common Setup Errors

### ❌ Error 1: `'python' is not recognized as an internal or external command`
- **Cause:** Python was installed without adding it to the system `PATH` variable.
- **Solution:** Re-run the Python installer, choose **Modify**, and check **Add Python to environment variables (PATH)**. Or search for "Environment Variables" in Windows and add `C:\Users\<YourUser>\AppData\Local\Programs\Python\Python3xx\` to `Path`.

### ❌ Error 2: `Execution of scripts is disabled on this system (PSSecurityException)`
- **Cause:** Windows PowerShell restricts script execution by default.
- **Solution:** Open PowerShell as Administrator or CurrentUser and run:
  ```powershell
  Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

### ❌ Error 3: `Port 8000 is already in use`
- **Cause:** Another process or Django instance is running on port 8000.
- **Solution:** Start the server on a different port:
  ```bash
  python manage.py runserver 8080
  ```

### ❌ Error 4: `ModuleNotFoundError: No module named 'django'`
- **Cause:** Django was installed globally or inside another environment, but your current terminal does not have the virtual environment activated.
- **Solution:** Activate your virtual environment first (`.\venv\Scripts\Activate.ps1` or `source venv/bin/activate`), then verify with `python -m django --version`.

---

🎉 **You are now completely set up!**  
Proceed to **[Day 01: Introduction to Django](../README.md)** to begin your learning journey!
