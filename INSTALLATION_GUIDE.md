# Installation Guide for Intel Arc Control Standalone Scripts

This guide provides detailed steps for locating the necessary Intel Arc Control files and preparing your system before running the main installation script (`Install-IntelArcControl.ps1`).

## Prerequisites

To proceed, you **must already possess a specific version of the Intel Arc Graphics driver** that included Intel Arc Control. This typically means drivers released between roughly **2024 and mid-2025**.

**I do not recommend downloading software from unauthorized third-party sources**, as this carries significant risks. Please ensure you have obtained your driver files legally.

## Step 1: Locate Necessary Files

The `IntelArcControl.exe` and its dependencies are typically found within the extracted files of an Intel graphics driver installation package.

1.  **Find your driver package:**
    * If you have the original `.exe` installer for an older driver version, you might need to run it to extract its contents to a temporary location (often `C:\Users\YourUser\AppData\Local\Temp` or a similar folder) without completing the full installation.
    * A common location where Windows stores cached installation packages is `C:\ProgramData\Package Cache`. You will need to browse through the subfolders within `Package Cache` to find the specific driver version that contains `IntelArcControl.exe`.
        * **Note:** The exact subfolder name within `C:\ProgramData\Package Cache` (e.g., `{0416176c-517d-404f-bf20-ab563fe1313e}`) is a Globally Unique Identifier (GUID) and is unique to each specific driver installation package. You will need to manually browse through these folders to find the one containing your desired `IntelArcControl.exe`.

2.  **Identify core files:**
    * From this extracted package (or the `Package Cache` subfolder), you'll need `IntelArcControl.exe` and any other DLLs or resource files that are essential for it to run.
    * Common dependencies often include files like `igfxcm.dll`, `igfxext.dll`, and other `igfx*` DLLs found alongside `IntelArcControl.exe` or in the driver's `System32` subfolder within the package.
    * **Tip for identifying dependencies:** The easiest way to identify all required files is often to copy `IntelArcControl.exe` to a new, empty folder and then try to run it. Windows will usually pop up errors indicating missing DLLs. Copy those missing DLLs from the original driver package (or the `Package Cache` subfolder) into your new folder until `IntelArcControl.exe` launches successfully.

3.  **Verifying the File Version (Optional but Recommended):**
    Once you've located a potential `IntelArcControl.exe` file, you can verify its version programmatically using PowerShell. This helps ensure you have the correct version.

    * **Open PowerShell:** Search for "PowerShell" in the Start Menu and open it.
    * **Run the command:** Replace `PATH_TO_INTELARCCONTROL.EXE` with the actual path to the file you found.

    ```powershell
    (Get-Item 'PATH_TO_INTELARCCONTROL.EXE').VersionInfo.FileVersion
    ```
    For example, if your file is at `C:\ProgramData\Package Cache\{0416176c-517d-404f-bf20-ab563fe1313e}\IntelArcControl.exe`, the command would be:
    ```powershell
    (Get-Item 'C:\ProgramData\Package Cache\{0416176c-517d-404f-bf20-ab563fe1313e}\IntelArcControl.exe').VersionInfo.FileVersion
    ```
    This command will output the file version string, which you can then compare to known versions that included Arc Control.

## Step 2: Prepare Your Standalone Folder

1.  **Create a new, dedicated folder:** Choose a clean location on your system where you want to install the standalone Intel Arc Control. A good example is `C:\ArcControlStandalone` or `C:\Program Files\Intel\Intel Arc Control` (if you prefer a more traditional program files location).
2.  **Copy the core files:** Copy `IntelArcControl.exe` and *all identified essential DLLs/resource files* from your located driver package (from Step 1) into this new standalone folder. This folder will be the `SourcePath` for the `Install-IntelArcControl.ps1` script.

## Step 3: Download and Use the Scripts

1.  **Download this repository:** Download the entire repository (or just the `scripts` folder) to your computer.
2.  **Place scripts:** Copy the relevant scripts (e.g., `Install-IntelArcControl.ps1`, `Uninstall-IntelArcControl.bat`) into the `C:\ArcControlStandalone` folder, or a convenient location from where you want to manage them.

## Step 4: Install the Standalone Launcher (Windows)

This script will create a shortcut for easy access.

* **Open PowerShell as Administrator:** Right-click on the Start button, select "Command Prompt (Admin)" or "Windows PowerShell (Admin)".
* **Navigate to your folder:** `cd C:\ArcControlStandalone`
* **Run the installation script:**
    ```powershell
    .\Install-IntelArcControl.ps1
    ```
* The script will guide you through the installation process, including asking for confirmation and creating necessary shortcuts.

## Running Intel Arc Control

Once the `Install-IntelArcControl.ps1` script has completed, it will have created a shortcut for Intel Arc Control in your Start Menu.

* You can now launch **Intel Arc Control** directly from your Start Menu.
* **Important Note:** This standalone setup does **not** automatically run Arc Control with Windows startup. You will need to manually start it after each reboot from the Start Menu shortcut. Also, Intel Driver & Support Assistant (IDSA) might recognize this standalone Arc Control as an outdated component; you can safely ignore this notification.

## Uninstalling Intel Arc Control Standalone

The `Install-IntelArcControl.ps1` script also creates a dedicated uninstallation script (`Uninstall-IntelArcControl.bat`) and a shortcut for it in your Start Menu.

* To uninstall, simply find and run the **"Intel Arc Control Uninstall"** shortcut in your Start Menu.
* Alternatively, you can manually run the `Uninstall-IntelArcControl.bat` file that was created in your `C:\Program Files\Intel\Intel Arc Control` (or your chosen `InstallPath`) folder.
