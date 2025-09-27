# Ninja Crypter GUI — Full Navigation / Menu Structure

## Top-Level Window

**Title:** Ninja Crypter  

**Main layout:** Menu Bar (top) + Toolbar (optional quick actions) + Workspace (file drag-drop, logs, status) + Status Bar  

---

## 1. Menu Bar Structure

### File
- **Encrypt File…** → opens Encrypt Wizard  
- **Encrypt Folder…** → folder encryption wizard  
- **Decrypt File…** → decrypt wizard  
- **Decrypt Folder…** → decrypt directory wizard  
- **Secure Wipe…** → wipe selected files/folders  
- **Open Encrypted File** → preview metadata (optional secure viewer)  
- **Recent Files** → list of recently encrypted/decrypted files  
- **Exit** → closes application  

### Edit
- **Preferences / Settings…** → opens main settings popup  
- **Encryption Options…** → algorithm selection, chunk size, streaming mode  
- **Key Management…** → launch Key Manager popup  
- **Manage Recipients / Shares…** → user & access management  

### View
- **Activity Log** → opens popup/window with audit log  
- **Progress / Status** → show ongoing tasks  
- **Notifications / Alerts** → security or system alerts  

### Tools
- **Key Manager** → GUI for master/data key management  
- **Import / Export Public Keys**  
- **Rotate Master Key**  
- **Generate Data Key**  
- **Rewrap Data Keys**  
- **Key Backup / Restore**  
- **Batch Encrypt / Decrypt** → bulk operations for directories  
- **Share / Revoke Access…**  
  - Share file/folder with recipients  
  - Set expiration  
  - Revoke existing shares  
- **Integrity Check / Verify Signature…** → verify encrypted files or signatures  
- **Secure Update / Check for Updates** → update the application safely  

### Security
- **Encryption Algorithms…** → select primary and fallback algorithms  
- **Password Protection / Argon2 Options** → optional password-based encryption  
- **Policy Manager / Access Control** → RBAC settings  
- **Tamper Detection Settings** → enable/disable alerts and logging  

### Window
- **Show/Hide Toolbar**  
- **Show/Hide Status Bar**  
- **Tile / Cascade windows** (if multiple internal frames for logs / key manager)  

### Help
- **User Guide…** → opens integrated guide  
- **Developer Guide…** → for internal devs, optional password-protected  
- **About…** → version info, license, cryptography library info  
- **Check for Updates** → alternative place for updates  

---

## 2. Toolbar / Quick Actions (Optional)
- Encrypt File  
- Encrypt Folder  
- Decrypt File  
- Decrypt Folder  
- Key Manager  
- Share File  
- View Activity Log  

---

## 3. Settings / Preferences Popup

**Tabs:** General | Encryption | Keys | Network | Audit | UI | Advanced  

### 3.1 General
- Default output folder  
- Overwrite policy (ask / overwrite / skip)  
- Language / Locale  
- Theme: Light / Dark / Custom  

### 3.2 Encryption
- Default algorithm (AES-GCM / XChaCha20-Poly1305)  
- Key size  
- Chunk size / streaming mode  
- Include metadata (yes/no)  
- Sign files by default (Ed25519 / RSA-PSS)  
- Enable tamper detection  

### 3.3 Keys
- Default key storage (Keystore / Vault / HSM)  
- Master key selection  
- Automatic key rotation schedule  
- Import / Export keys  
- Multi-recipient sharing defaults  

### 3.4 Network
- Policy / telemetry server settings  
- Proxy configuration  
- Enable online revocation / shares  
- Audit sync frequency  

### 3.5 Audit / Logging
- Enable local audit logging  
- Enable server-side audit logging  
- Log level: Info / Warn / Error / Debug  
- Tamper alert notifications  

### 3.6 UI
- Show toolbar / status bar  
- Drag-and-drop options  
- Recent files count  
- Popup confirmations (on overwrite, delete, wipe)  

### 3.7 Advanced
- Enable FIPS mode  
- Enable developer mode  
- Debug / verbose logging  
- Enable experimental algorithms  
- Zeroization behavior  
- HSM / KMS integration options  

---

## 4. Encrypt / Decrypt Wizards

### Encryption Wizard
1. Select File / Folder → drag-drop or file chooser  
2. Select Recipients / Password Protection → multi-user selection + password  
3. Select Algorithm / Options → AES-GCM / XChaCha20 / hybrid mode  
4. Advanced Options  
   - Chunked mode  
   - Streaming encryption  
   - Sign file  
   - Include metadata  
5. Output & Overwrite Policy → choose folder, filename pattern  
6. Summary & Execute → show estimated time & progress bar  

### Decryption Wizard
1. Select Encrypted File / Folder  
2. Select Key / Password  
3. Verify Integrity / Signature → optional check  
4. Output Folder & Overwrite Policy  
5. Summary & Execute → progress bar, cancel option  

---

## 5. Popups / Dialogs
- **Confirmation Dialogs** → overwrite, wipe, delete, key rotation, revocation  
- **Error / Warning Dialogs** → encryption/decryption failure, missing keys, tampered file  
- **Progress Dialog** → streaming encryption/decryption  

### Key Manager Popups
- Generate / Import / Export keys  
- View key metadata  
- Rotate master key  

### Share File / Folder Dialog
- Select recipients  
- Set expiration & access level  
- Display share token  

### Audit Log Viewer
- Filter by date, file, user, operation  
- Export logs to CSV / JSON  

### About Dialog
- Application version  
- Libraries used  
- License info  

### Update Dialog
- Show current version  
- Show update details  
- Progress bar & install  

---

## 6. Status Bar
- Current user / role  
- Encryption / decryption progress  
- Active operation (e.g., "Encrypting file XYZ…")  
- Notifications / errors
