# Ninja Crypter — Daily Development Log

**Project Status:** In Development  
**Planned End Date:** 2026-01-31

---

## Purpose

This document provides instructions for logging **daily development activities** for the Ninja Crypter project.  
Every developer must create a **daily `.txt` file** documenting their work. This ensures that all activities, files uploaded, and progress are properly logged for auditing and project tracking.

---

## Daily Log File Instructions

### 1. File Naming
- Name the file using the **current date** in `YYYY-MM-DD.txt` format.  
  Example: `2025-09-27.txt`

### 2. File Location
- Place the file inside the repository folder `daily_dev/`  
  Example path: `daily_dev/2025-09-27.txt`

### 3. File Structure
Each daily `.txt` file must include the following sections:

Date: YYYY-MM-DD
Developer: [Your Name]

Tasks Completed:

    [Task 1 description]
    [Task 2 description]
    [Task N description]

Files Uploaded / Modified:

    [src/.../FileName.java]
    [resources/.../FileName.fxml]
    [Other relevant files]
    

Summary:
[Brief overview of work done today, challenges, and next steps]

Commits / PR References:
    [Commit hash or PR link if applicable]


---

## Example Daily Log File

**File:** `daily_dev/2025-09-27.txt`

Date: 2025-09-27
Developer: Panagiotis Kotsorgios

Tasks Completed:

    Implemented AES-GCM encryption module
    Added metadata support to file container
    Initial GUI encrypt wizard layout

Files Uploaded / Modified:

    src/core/CryptoEngine.java
    src/gui/EncryptWizard.fxml
    resources/config/default_algorithms.json

Summary:
Completed core AES-GCM encryption implementation with authenticated metadata. Started GUI encrypt wizard layout. Next steps: integrate file selection and key wrapping.

Commits / PR References:

    Commit abc1234
    PR #45


---

## How It Works With the Repository

- **Individual Daily Logs (`daily_dev/YYYY-MM-DD.txt`)**
  - Each developer creates **one file per day**.
  - Tracks tasks, files, summaries, and commit references.
  - Supports auditing, progress tracking, and accountability.

---

## Best Practices

- Update your daily `.txt` file at the **end of each workday**.  
- Include **all relevant tasks and files** even if small.  
- Keep **summaries concise but detailed enough** to understand what was done.  
- Reference **commit hashes or pull requests** for accountability.  
- Ensure **daily files are committed** to the repository to maintain historical logs.  
- Use clear and consistent formatting for readability.

---

## Optional Enhancements

- If multiple developers are working on the same day, append the **developer name to the filename**:  
  `daily_dev/2025-09-27_Panagiotis.txt`  
- Consider adding **optional tags** for type of work: `[ENCRYPTION]`, `[GUI]`, `[KMS]`, `[TEST]`.

---

## Summary

This daily development log system ensures:

- Consistent tracking of **tasks, files, and progress**
- **Accountability** through commit references
- Easy **auditing and review** for project leads
- Clear visibility of **days remaining until project completion**
