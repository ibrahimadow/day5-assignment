# Exercise A: User Manual Procedure
## Setting Up a Python Virtual Environment and Installing a Package

## Prerequisites

Before starting, make sure you have:

- A computer running Windows, macOS, or Linux
- Python 3.8 or later installed (check by opening a terminal and typing `python --version` or `python3 --version`)
- A terminal or command-line application (Command Prompt/PowerShell on Windows, Terminal on macOS/Linux)
- A code editor or text editor (e.g., VS Code) — optional but recommended
- Basic familiarity with navigating folders using `cd`

## Steps

1. Open your terminal application.
   **Expected result:** A blank command-line window appears with a prompt ready for input.

2. Navigate to the folder where you want to create your project by typing `cd path/to/your/folder`.
   **Expected result:** The prompt now shows your target folder as the current directory.

3. Create a virtual environment by typing `python -m venv venv` (use `python3` instead of `python` on macOS/Linux if needed).
   **Expected result:** A new folder named `venv` appears inside your project folder, with no error messages printed.

4. Activate the virtual environment:
   - Windows: type `venv\Scripts\activate`
   - macOS/Linux: type `source venv/bin/activate`
   
   **Expected result:** Your terminal prompt changes to show `(venv)` at the beginning of the line, indicating the environment is active.

5. Confirm the virtual environment is active by typing `pip list`.
   **Expected result:** A short list of only two or three default packages (such as `pip` and `setuptools`) is displayed, confirming you're in an isolated environment.

6. Install a package by typing `pip install requests` (or any package name you need).
   **Expected result:** Terminal output shows download and installation progress, ending with a line like "Successfully installed requests-x.x.x".

7. Verify the installation by typing `pip list` again.
   **Expected result:** The `requests` package (and its dependencies) now appears in the list.

8. When finished working, deactivate the environment by typing `deactivate`.
   **Expected result:** The `(venv)` prefix disappears from your terminal prompt, confirming you've returned to your system's global Python environment.

## Screenshot Description

**Screenshot to include:** A terminal window captured immediately after Step 4 (activation). It should clearly show the command that was typed (`source venv/bin/activate` or the Windows equivalent) on one line, followed by the next line showing the prompt with `(venv)` prepended — for example: `(venv) user@laptop project-folder %`. This visually confirms to the reader exactly what a successful activation looks like, since this is the step beginners most often aren't sure has worked.

## Troubleshooting Note

**Most common error:** On Windows, running the activation command in Step 4 sometimes fails with a message like "execution of scripts is disabled on this system," caused by PowerShell's default security policy blocking script execution. To fix this, open PowerShell as Administrator and run `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`, then confirm with "Y" when prompted. After this one-time fix, retry Step 4.