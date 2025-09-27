# Ninja Crypter — Encrypted Local Storage

**Project Status:** Pre-Development  
**Purpose:** Define how Ninja Crypter will securely store all cryptographic material, metadata, and audit logs **entirely within encrypted disk storage on company machines**, and how the application itself handles configuration and access.

---

## 1. Overview

All sensitive data for Ninja Crypter will reside in a **dedicated encrypted volume or container** on local machines. This includes:

- Master Keys (MK)  
- Data Keys (DK)  
- File Metadata  
- Audit / Activity Logs  
- Application configuration and policies  

The system is designed to be **offline, fully local, and initially configured entirely from the application itself**. Later, advanced settings may be edited from the GUI or CLI.

---

## 2. Encrypted Storage Strategy

### 2.1 Storage Method

- **Create a dedicated encrypted volume/container via the app:**
  - **Windows:** BitLocker-encrypted VHD/VHDX  
  - **Linux:** LUKS-encrypted volume  
  - **macOS:** Encrypted APFS volume or FileVault container
- **Mounting/unmounting**:
  - Managed automatically by the application at startup  
  - Unmounted after operations to prevent unauthorized access
- **Authentication**:
  - Strong password/passphrase configured from the application
- **Initial Configuration Flow**:
  1. User launches Ninja Crypter for the first time  
  2. Application prompts to **create and encrypt the storage volume**  
  3. Master Key is generated and stored inside the volume  
  4. Default DK storage, metadata, and audit folders are created  

### 2.2 Later Editable Configuration

- Advanced users or administrators can:
  - Change **volume mount location**  
  - Configure **backup paths**  
  - Adjust **encryption algorithms for DKs or metadata**  
  - Enable **tamper detection settings**  
- All modifications are **performed through GUI settings panel or CLI commands**  
- Application ensures **consistency and integrity** after edits

---

## 3. Java Application Interaction

The Java application interacts with the encrypted storage as follows:

### Option 1 — File-Based Volume Access
- Volume mounted by the application at a known path
- Java reads/writes DKs, metadata, and logs directly:

```java
Path dkPath = Paths.get("/mnt/ninja_secure/keys/file123.dk");
byte[] wrappedKey = Files.readAllBytes(dkPath);
byte[] dataKey = KeyManager.unwrapKey(wrappedKey, masterKey);

Option 2 — Encrypted Database Inside Volume

    Store DKs, metadata, and audit logs in an encrypted database

    Example folder structure:

/mnt/ninja_secure/
├─ keys/          # Wrapped DKs
├─ metadata/      # Encrypted JSON metadata
├─ audit/         # Encrypted logs
└─ db/ninja.db    # Encrypted SQLite/H2 database

    Java JDBC example:

String url = "jdbc:sqlite:/mnt/ninja_secure/db/ninja.db?cipher=aes-256-cbc&key=StrongPassphrase";
Connection conn = DriverManager.getConnection(url);
PreparedStatement stmt = conn.prepareStatement(
    "INSERT INTO keys(key_id, wrapped_key) VALUES (?, ?)"
);
stmt.setString(1, "file123");
stmt.setBytes(2, wrappedKey);
stmt.executeUpdate();

KeyManager Responsibilities

    Generate MK/DK

    Wrap/unwarp DK

    Store keys securely inside the encrypted volume

    Zeroize keys in memory after use

4. Security Measures

    Encryption at Rest: Volume encryption (AES-256 or OS-native)

    Access Control: Only authorized application processes and users can mount volume

    Zeroization: Keys cleared from memory after use

    Tamper Detection: Signed or hashed metadata and logs

    Offline Operation: Fully functional without network

    Backups: Encrypted and signed copies of the volume

5. Application-First Configuration Advantages

    Ensures consistent and secure setup without requiring manual disk encryption

    Reduces risk of misconfiguration by users

    All master and data keys are created and stored automatically during initial setup

    Later edits via GUI or CLI preserve security while allowing customization

6. Optional Enhancements

    Multi-factor authentication for volume mounting

    Digital signatures/HMAC for all files in the volume

    Versioned encrypted backups

    Support for multiple encrypted volumes for separate projects or user roles

7. Summary

Ninja Crypter’s approach:

    Initial setup is fully controlled by the application to ensure correct encryption and key handling

    Later GUI or CLI edits allow advanced configuration without compromising security

    Master Keys, Data Keys, metadata, and logs are always stored encrypted

    Offline, local operation ensures maximum protection for company-sensitive files
