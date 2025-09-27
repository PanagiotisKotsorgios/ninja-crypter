# Ninja Crypter — Application Analysis

## 1. Overview

**Ninja Crypter** is a top-secret, enterprise-grade file encryption tool designed to secure both content and binary files. It ensures that even if files are exfiltrated, they cannot be decrypted without authorized keys. The application supports:

- GUI (cross-platform, JavaFX recommended)
- CLI for automation and scripting
- Programmatic APIs
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

## 6. Functional Modules

**Core Modules and Responsibilities:**

- **GUI**: Wizards, menus, key management interface, audit viewer
- **CLI**: Command-line equivalents for encrypt, decrypt, share, rotate keys
- **Core Engine**: File encryption/decryption, streaming, AEAD
- **Crypto**: Symmetric/asymmetric primitives, hashing, signing
- **Key Management**: Master/Data key lifecycle, wrapping/unwrapping, rotation
- **Sharing**: User-based sharing, expiration, revocation
- **Network**: Optional telemetry, online policy enforcement
- **Utilities**: Logging, error handling, metadata parsing

---

## 7. Testing & Compliance

- **Unit Tests**: Crypto primitives, file format, API coverage
- **Integration Tests**: Key management, KMS/HSM, multi-file scenarios
- **Fuzz Testing**: Malformed input files, headers, truncated data
- **Crypto Regression Tests**: Ensure cross-compatibility and AEAD correctness
- **Compliance**: Optional FIPS mode, secure code practices, secure update verification

---

## 8. Summary

Ninja Crypter is designed as a **secure, enterprise-ready encryption platform** with:

- Strong, modern cryptography
- Comprehensive key management
- GUI + CLI + programmatic access
- Enterprise sharing, audit, and revocation features
- Offline and online operational modes
- Full testing, compliance, and secure development lifecycle

This document serves as the **full application analysis** for developers, security auditors, and project leads.
