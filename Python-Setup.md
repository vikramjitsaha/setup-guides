# Python Setup Guide: Limited Access (No Admin Rights)

This guide provides a walkthrough for installing and configuring Python 3.12 on a Windows machine where you do not have administrative privileges.

---

## 🛠️ Step 1: Download Python

Since you cannot run a standard `.exe` installer without admin rights, use the **Windows embeddable package**.

* **Download Link:** [Python 3.12.9 (64-bit) Embeddable Zip]()
* **Action:** Extract the contents of the ZIP file to a local directory, for example:
`C:\Opt\python-3.12.9-embed-amd64`

---

## 🌐 Step 2: Configure Environment Variables

You need to tell Windows where Python is located without modifying system-wide settings.

1. Search for **"Edit environment variables for your account"** in the Start menu.
2. Under **User variables**, find the **Path** variable and select **Edit**.
3. Add the following two new entries:
* `C:\Opt\python-3.12.9-embed-amd64`
* `C:\Opt\python-3.12.9-embed-amd64\Scripts`


4. Click **OK** to save.

---

## 📦 Step 3: Enable Site-Packages

The embeddable version of Python is isolated by default. To allow it to use installed packages (like `pip`), you must modify the configuration.

1. Navigate to your Python folder: `C:\Opt\python-3.12.9-embed-amd64`.
2. Open the file `python312._pth` in Notepad.
3. Locate the line `#import site` and **remove the `#**` to uncomment it.
4. **Save** and close the file.

---

## 🐍 Step 4: Install Pip

1. Download the `get-pip.py` script from [bootstrap.pypa.io]().
2. Open your terminal (PowerShell or CMD) and navigate to the folder where you saved the script.
3. Run the following command to install `pip` while bypassing potential firewall restrictions:

```bash
python get-pip.py --trusted-host pypi.org --trusted-host files.pythonhosted.org

```

---

## 🏗️ Step 5: Virtual Environment Setup

It is best practice to use virtual environments to manage project-specific dependencies.

### 1. Install Virtualenv

```bash
python -m pip install virtualenv

```

### 2. Create an Environment

Navigate to your project codebase folder and run:

```bash
python -m virtualenv .venv

```

### 3. Activate the Environment

**PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1

```

**Command Prompt:**

```cmd
.\.venv\Scripts\activate.bat

```

---

## 📥 Step 6: Install Dependencies

Once the virtual environment is active, you can install your project requirements:

```bash
pip install -r requirements.txt

```

> **Note:** If you encounter SSL errors during installation, append `--trusted-host pypi.org --trusted-host files.pythonhosted.org` to your pip command.
