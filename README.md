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

If you've had previous installations of Intel graphics drivers containing `IntelArcControl.exe` (not the `IntelArcControl.msi`), you can often find it by checking:
`C:\ProgramData\Package Cache`

You'll need to browse through the subfolders within `Package Cache` to find the specific driver version. To check its version, open a PowerShell terminal (PowerShell 7.* or later is recommended for best compatibility) and use the following command, replacing `{Unique-Identifier-Serial}` with the actual folder name:

```powershell
(Get-Item 'C:\ProgramData\Package Cache\{Unique-Identifier-Serial}\IntelArcControl.exe').VersionInfo.FileVersion
