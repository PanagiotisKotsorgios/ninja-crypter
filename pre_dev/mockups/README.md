# Ninja Crypter — GUI & Workflow Mockups

**Project Status:** Pre-Development  
**Purpose:** Collect and organize all GUI and workflow mockups for Ninja Crypter.  
This document helps visualize user interactions, window layouts, wizards, and functional workflows before implementation.

---

## 1. Main Application Window

**Description:**  
The main window serves as the starting point for all user interactions. It includes a drag & drop area, quick action buttons, and navigation to settings, logs, and key management.

**Elements:**
- Drag & drop area for files and folders
- Quick actions: Encrypt, Decrypt, Share, Verify Signature
- Navigation panel:
  - Home
  - Key Manager
  - Audit Logs
  - Policy / Settings
- Status bar: current user, last activity, telemetry status

**Mockup Placeholder:**  
![Main Window Mockup](images/main_window_mockup.png)

---

## 2. Encrypt Wizard

**Description:**  
Guides the user step-by-step through encrypting files or directories.

**Steps:**
1. Select file(s) or folder(s)
2. Choose recipients (user or password-protected)
3. Select encryption algorithm (AES-GCM, XChaCha20, etc.)
4. Advanced options: chunking, metadata, secure wipe
5. Execute and view progress

**Mockup Placeholder:**  
![Encrypt Wizard Mockup](images/encrypt_wizard_mockup.png)

---

## 3. Decrypt Wizard

**Description:**  
Guides the user through decrypting files or directories.

**Steps:**
1. Select file(s) or folder(s)
2. Detect available keys
3. Display file metadata
4. Confirm decryption options
5. Execute and view progress

**Mockup Placeholder:**  
![Decrypt Wizard Mockup](images/decrypt_wizard_mockup.png)

---

## 4. Key Manager UI

**Description:**  
Interface to view, import/export, and manage keys.

**Elements:**
- List of Master Keys (MK) and Data Keys (DK)
- Key import/export options
- Request key from KMS
- Key rotation interface
- RBAC view for permissions

**Mockup Placeholder:**  
![Key Manager Mockup](images/key_manager_mockup.png)

---

## 5. Audit / Activity Logs

**Description:**  
Shows all local and server-side audit events. Filterable by date, user, event type, and severity.

**Elements:**
- Table of events: timestamp, user, action, file, outcome
- Filters panel: date range, event type, user
- Export logs: CSV / JSON

**Mockup Placeholder:**  
![Audit Logs Mockup](images/audit_logs_mockup.png)

---

## 6. Settings & Policy Panel

**Description:**  
Interface to configure defaults and advanced policies.

**Sections:**
- Default encryption algorithms
- Overwrite policy after encryption
- Retention / versioning
- Telemetry opt-in / opt-out
- Compliance / FIPS mode
- Multi-factor authentication settings

**Mockup Placeholder:**  
![Settings Panel Mockup](images/settings_panel_mockup.png)

---

## 7. CLI Workflow Mockups

**Description:**  
Illustrates example commands and expected outputs for automation.

**Examples:**

Encrypt a file for multiple recipients

ninja encrypt -i input.txt -o output.ninja --recipients alice,bob --alg AES-GCM
Decrypt a file

ninja decrypt -i output.ninja --output-dir ./decrypted
Share a file

ninja share --file output.ninja --user alice@company.com

--expire 2026-01-01
Rotate master key

ninja key rotate --master-key-id mk-1234
View audit logs

ninja audit --since "2025-01-01" --format json


**Notes:**  
- CLI should provide **machine-readable outputs** (JSON/CSV) for automation scripts.

---

## 8. Optional Mockups / Future Work

- Mobile or tablet interface mockups (optional)
- Additional wizards: Batch encryption, Key import/export wizard
- Interactive diagrams for key wrapping, DK/MK relationships
- Telemetry and policy sync visualizations

---

## 9. Summary

This document serves as a **central reference for GUI, CLI, and workflow mockups**. All images and diagrams should be added to the `images/` folder in the repository.  
Developers and designers must refer to this file before implementing UI elements, wizards, or CLI commands to
