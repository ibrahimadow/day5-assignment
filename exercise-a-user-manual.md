# Creating and Activating a Python Virtual Environment and Installing a Package

**Purpose:** By the end of this procedure, you will have a project folder with its own isolated Python environment, the `requests` package installed inside it, and a `requirements.txt` file listing what you installed.

**What is a virtual environment?** It is a private copy of Python for one project. Packages you install stay inside it, so they never clash with other projects on your computer.

## Prerequisites

Before you start, make sure you have:

- A Windows 10 or 11 computer
- Python 3.10 or newer, installed with the **Add Python to PATH** option ticked
- Windows PowerShell (already included with Windows)
- An internet connection, needed to download the package
- About 10 minutes

## Procedure

**Step 1. Open PowerShell.**
Click the Start menu, type `PowerShell`, and press Enter.
**Expected result:** A window opens with a prompt that looks like `PS C:\Users\YourName>`.

**Step 2. Create a project folder.**
Type `mkdir python_setup_lab` and press Enter.
**Expected result:** PowerShell prints a small table showing a new directory named `python_setup_lab`.

**Step 3. Move into the project folder.**
Type `cd python_setup_lab` and press Enter.
**Expected result:** The prompt now ends with `python_setup_lab>`.

**Step 4. Check that Python is installed.**
Type `python --version` and press Enter.
**Expected result:** PowerShell prints a version number such as `Python 3.14.7`.

**Step 5. Create the virtual environment.**
Type `python -m venv venv` and press Enter.
**Expected result:** After a few seconds the prompt returns with no message. A new folder named `venv` now exists inside `python_setup_lab`. You can confirm by typing `dir`.

**Step 6. Activate the virtual environment.**
Type `.\venv\Scripts\Activate.ps1` and press Enter.
**Expected result:** The prompt now starts with `(venv)`. If you see red error text instead, go to the Troubleshooting section below.

**Step 7. Install the `requests` package.**
Type `pip install requests` and press Enter.
**Expected result:** Text scrolls by, and the last line begins with `Successfully installed` and includes `requests`.

**Step 8. Confirm the package is installed.**
Type `pip list` and press Enter.
**Expected result:** A table of package names and versions appears, and `requests` is one of the rows.

**Step 9. Save the package list to a file.**
Type `pip freeze > requirements.txt` and press Enter.
**Expected result:** The prompt returns with no message, and a file named `requirements.txt` now exists in the folder.

**Step 10. Deactivate the virtual environment.**
Type `deactivate` and press Enter.
**Expected result:** The `(venv)` label disappears from the start of the prompt.

## Screenshot

**Figure 1:** The PowerShell window after Step 6. The prompt begins with `(venv)`, followed by the folder path, for example `(venv) PS C:\Users\YourName\python_setup_lab>`. Look for `(venv)` at the very start of the line. If you can see it, the virtual environment is active and any package you install goes into it.

## Troubleshooting: "running scripts is disabled on this system"

**What you see:** After Step 6, the window shows red text: `File ...\venv\Scripts\Activate.ps1 cannot be loaded because running scripts is disabled on this system.`

**Why it happens:** Windows PowerShell blocks scripts from running by default as a safety measure. The activation file is a script, so PowerShell refuses to run it.

**How to fix it:**

1. Type `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` and press Enter.
2. If PowerShell asks you to confirm, type `Y` and press Enter.
3. Type the activation command again: `.\venv\Scripts\Activate.ps1`

**Expected result:** The red error does not appear, and the prompt now starts with `(venv)`.

This change applies only to your own user account, and it only allows scripts created on your own computer.