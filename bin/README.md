# Ninja Crypter — `bin` Folder Overview

## Purpose

The `bin` folder contains **compiled binaries, executable scripts, and launchers** for Ninja Crypter.  

This folder is primarily for:

- **End Users:** run the app by **double-clicking the desktop or Start Menu icon** (no CLI needed)  
- **Developers / QA / IT Staff:** test, deploy, or troubleshoot builds  

> End users **should never need to open scripts or a terminal**. The app is designed to be fully GUI-driven.

---

## Folder Contents

| File / Folder | Description |
|---------------|-------------|
| `NinjaCrypter.jar` | The main compiled Java application (cross-platform). |
| `ninja.bat` | Windows launcher script (used internally by desktop/Start Menu shortcuts). |
| `ninja.sh` | Linux/macOS launcher script (used internally by desktop shortcuts). |
| `tools/` | Optional CLI or developer utilities (scripts, SDK helpers, key generators). |
| `libs/` | External libraries or dependencies required at runtime (JARs). |

---

## Usage Instructions (GUI-Only)

**Windows / macOS / Linux:**

1. Locate the **desktop or Start Menu/Application shortcut** for Ninja Crypter.  
2. **Double-click the shortcut**.  
3. The **first-run setup wizard** will launch automatically:
   - Master Key (MK) generation  
   - Initialization of Data Key storage, metadata, and audit logs  
   - Optional configuration for user authentication and policies  

> No terminal commands are required for end users.

---

## Optional CLI / Developer Usage

For testing, automation, or IT deployment:

```bash
# Cross-platform Java command
java -jar NinjaCrypter.jar <command> [options]

# Example encryption command
java -jar NinjaCrypter.jar encrypt -i myfile.txt -o myfile.enc --recipients user1

    These are internal or developer-facing only. End users should never use CLI commands.

Notes & Best Practices

    The bin folder does not store keys or sensitive data. All keys are stored in encrypted local storage managed by the app.

    Desktop and Start Menu shortcuts should always point to the launcher scripts.

    Only authorized developers or IT personnel should add new binaries or update scripts.

    Maintain clean builds: remove old versions to prevent conflicts.

    Digitally sign all JARs and scripts for secure distribution.

Folder Layout Example for End Users

Desktop/
└─ Ninja Crypter.lnk  (Windows shortcut)
Applications/
└─ Ninja Crypter.app   (macOS launcher)
Program Files/
└─ NinjaCrypter/
   ├─ bin/
   │  ├─ NinjaCrypter.jar
   │  ├─ ninja.bat       <-- used internally by shortcut
   │  └─ ninja.sh        <-- used internally by shortcut
   ├─ resources/         <-- icons, GUI assets, config templates
   └─ encrypted_volume/  <-- secure key and file storage

    End users only interact with the desktop or Start Menu shortcuts. All app functionality is accessible through the GUI.


---

This version:

- Highlights **click-and-run experience**  
- Differentiates **end user vs developer/IT files**  
- Includes **first-run wizard explanation**  
- Shows **recommended folder layout for commercial deployment**  

