# Intel Arc Control Standalone Scripts

This repository provides scripts and methods to help users run Intel Arc Control as a more standalone application, separate from the full Intel graphics driver installation. This approach aims to offer more flexibility and potentially avoid conflicts with newer driver versions or other system components.

---

## IMPORTANT: Disclaimer and Copyright Information

This solution and associated scripts are provided for **EDUCATIONAL AND RESEARCH_PURPOSES_ONLY**.

* **No Software Distribution:** I, the creator of these scripts, **do not distribute, encourage the distribution of, or provide access to any software** (including drivers or parts thereof) protected by copyright. All necessary drivers must be legally downloaded from their official sources by the end-user.
* **No Reverse Engineering:** These scripts **do not provide instructions for, and do not encourage, "reverse engineering" or decompiling** any copyrighted software, including drivers.
* **At Your Own Risk:** The use of these scripts is **entirely at your own risk**. I take no responsibility for any damages, data loss, functionality issues, warranty voiding, or any other consequences that may arise from using this solution. It is your responsibility to ensure your usage complies with applicable laws and licensing agreements.
* **No Warranty:** This solution is provided "as is" without any warranties, express or implied, regarding functionality, reliability, or fitness for any particular purpose.

By using these scripts, you acknowledge that you have read and understood this disclaimer and agree to its terms.

---

## Project Goal

My primary goal is to empower users to utilize Intel Arc Control independently. While I am actively seeking official approval from Intel to distribute direct links to their official software, this repository serves as an interim solution. It allows me to share the methods and scripts without violating Intel's End User License Agreement (EULA) regarding the redistribution of their proprietary software.

### Why this approach?

The official `IntelArcControl.exe` installer typically integrates Arc Control as a Windows service and an autorun application. This can sometimes lead to:
* Installation of more components than strictly necessary.
* Potential interference with newer driver installations, updates, or the functionality of Intel Graphics Command Center (IGCC).

My scripts aim to provide a cleaner, less intrusive way to launch and use Arc Control, closer to a standalone application, without these deep system integrations.

## Prerequisites

To use these scripts, you **must already possess a specific version of the Intel Arc Graphics driver** that included Intel Arc Control. This typically means drivers released between roughly **2024 and mid-2025**.
If you've had previous installations of intel gfx drivers containing the IntelArcControl.exe (not the IntelArcControl.msi), you can find it using Explorer and check the version by lookingin:
 C:\ProgramData\Package Cache 

Search for Intel*.exe and check what version it is by right-clicking the file and clicking: Copy as path
Run a PowerShell terminal (I have not tested this with PowerShell below 7.*, I recommend you update yours, by store or Microsoft Update):

  PowerShell> (Get-Item 'C:\ProgramData\Package Cache\{Unique-Identifier-Serial}\IntelArcControl.exe').VersionInfo.FileVersion
  > 1.80.5684.2

The script provided might work with other versions, though this is the latest version and one I've successfully used. 

**I do not recommend downloading software from unauthorized third-party sources**, as this carries significant risks. Please ensure you have obtained your driver files legally.

## Getting Started

This section provides a quick overview of how to set up, run, and uninstall Intel Arc Control as a standalone application using the provided PowerShell script.
For detailed, step-by-step instructions on locating and preparing the necessary files, please refer to the dedicated [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) file.

### Installation

The main installation and setup is handled by the `Install-IntelArcControl.ps1` PowerShell script.

1.  **Prepare your files:** Follow the instructions in [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) to locate and copy the required `IntelArcControl.exe` and its dependencies into your chosen standalone folder (e.g., `C:\ArcControlStandalone`).
2.  **Download the script:** Download the `Install-IntelArcControl.ps1` script from the `scripts` folder in this repository and place it in the same standalone folder.
3.  **Execute the script:**
    * Open **PowerShell as Administrator**. You can do this by searching for "PowerShell" in the Start Menu, right-clicking, and selecting "Run as administrator."
    * Navigate to your standalone folder (e.g., `cd C:\ArcControlStandalone`).
    * Run the installation script:
        ```powershell
        .\Install-IntelArcControl.ps1
        ```
    * The script will guide you through the installation process, including asking for confirmation and creating necessary shortcuts.

### Running Intel Arc Control

Once the `Install-IntelArcControl.ps1` script has completed, it will have created a shortcut for Intel Arc Control in your Start Menu.

* You can now launch **Intel Arc Control** directly from your Start Menu.

### Uninstalling Intel Arc Control Standalone

The `Install-IntelArcControl.ps1` script also creates a dedicated uninstallation script and a shortcut for it in your Start Menu.

* To uninstall, simply find and run the **"Intel Arc Control Uninstall"** shortcut in your Start Menu.
* Alternatively, you can manually run the `Uninstall-IntelArcControl.bat` file that was created in your `C:\Program Files\Intel\Intel Arc Control` (or your chosen `InstallPath`) folder.

## Alternative Solutions

I understand that Intel Arc Control might not be for everyone, or that users might prefer other tools. I will also explore and potentially include information on alternative methods or software that can provide similar functionality, such as using features within **Microsoft Game Bar** or other third-party utilities for graphics configuration.

## Contributing

This project is currently maintained by me. If you have suggestions or improvements for the scripts, feel free to open an issue or pull request.

## License

This project's scripts are licensed under the MIT License. See the `LICENSE` file for details.
