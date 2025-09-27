# Ninja Crypter — Project Overview

**Ninja Crypter** is a high-security, enterprise-grade file encryption software currently in **pre-development**. It is designed to protect sensitive company data across multiple platforms and operating systems, including Windows, macOS, and Linux, and will be implemented in **Java** for maximum portability and maintainability. The software will provide comprehensive capabilities to encrypt and decrypt all types of files, including text, binary, and large datasets, ensuring confidentiality, integrity, and authenticity even if files are intercepted, exfiltrated, or compromised.  

The application will support multiple **modern cryptographic algorithms** such as AES-256-GCM, XChaCha20-Poly1305 for symmetric encryption, RSA-OAEP and ECIES for asymmetric key wrapping, as well as authenticated signing using Ed25519 or RSA-PSS. Each file will use a **unique data key**, securely managed and wrapped by a **master key** stored in a Hardware Security Module (HSM) or enterprise Key Management System (KMS) such as HashiCorp Vault, AWS KMS, or Azure Key Vault.  

Ninja Crypter will include both a **graphical user interface (GUI)**, designed with JavaFX for cross-platform usability, and a **command-line interface (CLI)** for automation and scripting. Additionally, a **Java SDK** will provide programmatic access to encryption, decryption, key management, and audit functionality. Users will be able to perform secure file sharing with access control, expiration, and revocation policies, while all operations are **logged for auditing** and **tamper detection**.  

Other enterprise-focused features will include **key rotation, offline and online operational modes, batch encryption, streaming support for very large files, secure wipe of originals, compliance options (FIPS), configurable policies, telemetry, and optional corporate SSO or multi-factor authentication**. Ninja Crypter aims to serve as a **complete, secure, and auditable solution** for protecting top-secret company files and critical data, ensuring that sensitive information remains inaccessible to unauthorized parties under any circumstances.  

As the project is currently in pre-development, the design and architecture are being finalized to incorporate **best-practice cryptography, modern software engineering standards, and enterprise-grade security policies** to ensure the final product meets the highest levels of security, usability, and maintainability.



# Ninja Crypter — Application Analysis

## 1. Overview

**Ninja Crypter** is a top-secret, enterprise-grade file encryption tool designed to secure both content and binary files. It ensures that even if files are exfiltrated, they cannot be decrypted without authorized keys. The application supports:

- GUI (cross-platform, JavaFX recommended)
- CLI for automation and scripting
- Programmatic APIs / Java SDK
- Enterprise key management
- Secure file sharing
- Auditability
- Compliance with cryptographic best practices

### High-Level Goals

- Ensure confidentiality, integrity, and authenticity of files
- Provide strong cryptography with multiple algorithm options
- Enable enterprise features such as RBAC, key rotation, and tamper detection
- Support both offline and online modes
- Facilitate secure collaboration and sharing within the organization

---

## 2. High-Level Capabilities

| Feature | Description |
|---------|-------------|
| Symmetric Encryption | Strong symmetric file encryption using AEAD (AES-GCM, XChaCha20-Poly1305) |
| Hybrid Encryption | Combines symmetric + asymmetric encryption for secure key sharing |
| Algorithm Flexibility | AES-GCM, XChaCha20-Poly1305, RSA-OAEP, ECIES |
| Per-File Unique Keys | Data keys (DK) per file, wrapped by Master Key (MK) |
| Key Management | Integration with Java Keystore, HSMs, KMS (Vault, AWS KMS, Azure Key Vault) |
| GUI & CLI | Full-featured graphical interface + command-line automation |
| Enterprise Features | RBAC, audit logs, secure sharing, revocation, remote wipe, versioning, key rotation |
| Offline & Online Modes | Encrypt/decrypt without network, optional centralized policy and telemetry |
| Tamper Detection | Authenticated metadata and integrity checks |
| Secure Updates | Code signing and secure application updates |
| Compliance Options | FIPS mode for regulatory compliance |
| Testing | Unit, integration, fuzzing, crypto regression tests |

---

## 3. Cryptography Primitives

### Symmetric Encryption

- **AES-256-GCM**: Primary AEAD for authenticated encryption
- **XChaCha20-Poly1305**: Alternative AEAD for systems without AES-NI
- **Mode Details**:
  - AES-GCM: 96-bit random IV
  - XChaCha20: random nonce per file

### Asymmetric / Key Wrapping

- **RSA-OAEP (SHA-256)**: For wrapping data keys; 4096+ bit recommended
- **ECIES (X25519/Curve25519 + AEAD)**: Ephemeral key exchange for sharing

### Key Derivation & Hashing

- **HKDF (SHA-256 / SHA-512)**: Deriving subkeys
- **Argon2id**: Password-based key derivation (secure passwords)
- **PBKDF2-HMAC-SHA256**: Legacy password option (high iteration counts)
- **HMAC-SHA256**: Additional authentication when required

### Signing / Authenticity

- **Ed25519 / RSA-PSS**: File and release signing
- Private signing keys protected via HSM/KMS

### Security Notes

- AEAD required; no unauthenticated modes
- Metadata must be authenticated: version, algorithm, timestamps

---

## 4. Key Management & Secrets

| Key Type | Description |
|----------|-------------|
| Master Key (MK) | Stored in HSM or KMS, never exported in plaintext |
| Data Key (DK) | Random per-file key, used for file encryption, wrapped by MK or recipient public key |
| Key Wrapping | AES-KW + RSA-OAEP/ECIES/HKDF as appropriate |
| Key Rotation | Rewrap DKs or re-encrypt files in batch |
| Key Access | RBAC enforced, multi-person approval for sensitive keys |
| Secure Storage | Java Keystore, Vault, HSM, PKCS#11 support |
| Zeroization | Keys zeroed in memory after use |
| Audit | Creation, rotation, deletion, and export events logged |

---

## 5. Threat Model

- **Adversary**: Local disk access, network eavesdropping, stolen backups
- **Exclusions**: Private HSM keys are assumed secure
- **Assumptions**: OS/endpoint may be compromised
- **Mitigations**:
  - HSM integration
  - Secure boot
  - Tamper detection
- **Design Constraints**:
  - No plaintext keys or secrets in code/repo/logs
  - Fail closed on errors
  - Strict input validation and size limits

---

## 6. Core Application Features (Detailed)

### A. File Encryption / Decryption

- **Encrypt File (single file)**  
  - Encrypts any file type (text/binary) → outputs `.ninja` or `.enc` package  
  - Includes authenticated metadata: algorithm, version, original name (optional encrypted), timestamp, file hash, signer info  

- **Encrypt Directory**  
  - Recursive encryption with preserved folder structure  

- **Decrypt File / Directory**  
  - Requires valid unwrapping keys  

- **Streaming Support**  
  - Chunked AEAD with sequence numbers for very large files  
  - Optional partial decrypt for requested ranges  

- **Secure Wipe**  
  - Configurable overwrite policy for originals after encryption  

---

### B. File Format

- Containerized format:  
  `Header + Metadata + Encrypted Data + Auth Tag + Optional Signature`  
- Versioned for algorithm upgrades  
- Support for multiple recipients (each with wrapped DK entry)  

---

### C. Sharing & Access Control

- Share files to users by wrapping DK with recipient public key(s)  
- Expiration: enforce time-limited access  
- Revocation: support immediate revocation (online)  
- Access tokens: short-lived tokens for authenticated online decryption  

---

### D. Authentication & Authorization

- Local OS user authentication  
- Optional corporate SSO (SAML / OIDC)  
- Multi-factor authentication for sensitive operations  
- RBAC for file operations and key management  

---

### E. GUI Features (JavaFX recommended)

- **Main Window**  
  - Drag & drop for files/folders  
  - Quick actions: Encrypt, Decrypt, Share, Verify, Settings  

- **Wizard Flows**  
  - Encrypt wizard: select files → recipients / password → algorithm → advanced → execute  
  - Decrypt wizard: detect available keys → show metadata → decrypt  

- **Key Manager UI**  
  - List keys, import/export, request from KMS, rotation interface  

- **Activity / Audit Log Viewer**  
  - Local + server-side logs (filterable)  

- **Policy / Settings**  
  - Default algorithms, overwrite policy, retention, telemetry opt-in  

- **Dialogs**  
  - Error & warning dialogs, Help & Docs integration  

---

### F. CLI Features

- Example commands:

```bash
ninja encrypt -i in -o out --recipients user1,user2 --alg AES-GCM --chunked
ninja decrypt -i file --output-dir dir
ninja share --file file --user user@company.com --expire 2026-01-01
ninja key rotate --master-key-id id
ninja audit --since "2025-01-01" --format json
```
Scripting-friendly: exit codes, machine-readable output

G. API & SDK

Java SDK Classes (examples)

```java
Encryptor.encrypt(File file, EncryptionOptions options);
Decryptor.decrypt(File file, KeyProvider keyProvider);
KeyManager.wrapKey(DataKey dk, RecipientPublicKey pk);
KeyManager.rotateMasterKey(String masterKeyId);
AuditLogger.query(LocalDate since, Format format);

```


Support for internal REST endpoints for policy/telemetry


7. Testing & Compliance

Unit, integration, fuzzing, crypto regression tests

CI/CD integration for automated testing

Optional FIPS / compliance mode

Secure updates & code signing verification

8. Summary

Ninja Crypter is designed as a secure, enterprise-ready encryption platform with:

Strong, modern cryptography

Comprehensive key management

GUI + CLI + programmatic access

Enterprise sharing, audit, and revocation features

Offline and online operational modes

Full testing, compliance, and secure development lifecycle

