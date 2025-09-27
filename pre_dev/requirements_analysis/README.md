# Ninja Crypter — Requirements Analysis

## 1. Project Overview

**Ninja Crypter** is an enterprise-grade, cross-platform file encryption tool currently in **pre-development**, designed to securely encrypt and decrypt content and binary files. The software ensures that sensitive company data remains confidential, tamper-proof, and auditable, even if files are intercepted or exfiltrated. It will support **GUI (JavaFX), CLI, and Java SDK** for programmatic access, and will integrate with enterprise **HSM/KMS systems** for secure key management.  

---

## 2. Functional Requirements

### 2.1 Core Features

1. **File Encryption & Decryption**
   - Encrypt single files or directories recursively
   - Support for large files using streaming / chunked AEAD
   - Optional partial decryption for file ranges
   - Secure wipe option after encryption with configurable overwrite policy

2. **File Formats**
   - Containerized: `Header + Metadata + Encrypted Data + Auth Tag + Optional Signature`
   - Versioned for future algorithm upgrades
   - Support multiple recipients per file

3. **Key Management**
   - Data Keys (DK) per file, Master Key (MK) stored in HSM/KMS
   - AES-KW, RSA-OAEP, ECIES wrapping
   - Key rotation and re-encryption capabilities
   - RBAC-based access control
   - Audit logs for all key events

4. **Sharing & Access Control**
   - Share files securely using recipient public keys
   - Expiration and revocation policies
   - Short-lived online access tokens
   - Multi-person approval for sensitive keys

5. **Authentication**
   - Local OS user authentication
   - Optional corporate SSO (SAML / OIDC)
   - Multi-factor authentication for critical operations

6. **GUI Features**
   - Drag & drop for files/folders
   - Quick actions: Encrypt, Decrypt, Share, Verify, Settings
   - Wizard flows for encrypt/decrypt
   - Key Manager interface
   - Audit log viewer with filtering
   - Policy & Settings configuration

7. **CLI Features**
   - Full command-line access for encryption, decryption, key rotation, sharing, and auditing
   - Scripting-friendly with exit codes and machine-readable outputs

8. **API / SDK**
   - Java SDK providing programmatic access to core features
   - REST endpoints (internal) for telemetry and policy enforcement

---

### 2.2 Cryptography Requirements

1. **Symmetric Encryption**
   - AES-256-GCM (Primary AEAD)
   - XChaCha20-Poly1305 (Alternative AEAD)
   - Random IV/nonce per file

2. **Asymmetric Encryption / Key Wrapping**
   - RSA-OAEP (SHA-256), ≥4096-bit keys
   - ECIES (Curve25519/X25519 + AEAD)

3. **Key Derivation & Hashing**
   - HKDF (SHA-256 / SHA-512)
   - Argon2id for password-based key derivation
   - PBKDF2-HMAC-SHA256 (legacy option)
   - HMAC-SHA256 for additional authentication

4. **Signing**
   - Ed25519 or RSA-PSS for file and release signing

5. **Metadata**
   - Authenticated: version, algorithm, timestamps
   - Support for multiple recipients and DK entries

---

### 2.3 Non-Functional Requirements

- **Security**
  - AEAD mandatory
  - Fail-closed on errors
  - Keys never stored in plaintext in memory or disk
  - Zeroization of keys after use
  - Tamper detection on files and application

- **Performance**
  - Efficient encryption/decryption for large files
  - Streaming support to minimize memory footprint
  - Multi-threading for batch operations

- **Cross-Platform**
  - Must work on Windows, macOS, Linux
  - GUI using JavaFX

- **Audit & Logging**
  - Local and optional centralized logging
  - Filterable audit events

- **Compliance**
  - Optional FIPS mode
  - Secure updates with code signing

---

## 3. Technical Requirements

### 3.1 Programming Languages

- **Java 17+** (cross-platform)
- Optional scripting integration via CLI

### 3.2 IDE / Tools

- IntelliJ IDEA / Eclipse / VSCode (Java support)
- Maven or Gradle for build and dependency management
- Git for version control
- GitHub / GitLab repository

### 3.3 Libraries & Dependencies

- **Cryptography**
  - BouncyCastle (for advanced crypto primitives)
  - Google Tink (optional AEAD wrapper)
- **GUI**
  - JavaFX (Scene Builder optional)
- **JSON / Config**
  - Jackson or Gson for metadata and configuration
- **Logging**
  - SLF4J + Logback
- **Networking**
  - Apache HttpClient / Java 11+ HttpClient
- **Testing**
  - JUnit 5
  - Mockito for mocking
  - Fuzzing libraries for crypto testing

### 3.4 Platform / Runtime

- Java 17+ runtime
- Cross-platform support (Windows, macOS, Linux)
- Optional Docker container for CI/CD or testing

---

## 4. Development Requirements

- **Version Control**
  - Git branching: main, dev, feature/*, hotfix/*
  - GitHub / GitLab CI pipelines

- **CI/CD**
  - Build automation (Maven/Gradle)
  - Automated testing: unit, integration, regression, fuzz
  - Code signing and secure release pipeline

- **Documentation**
  - Developer guide
  - API/SDK documentation (Javadoc)
  - Security guidelines and coding standards

- **Team Roles**
  - Cryptography engineers
  - Java GUI developers
  - DevOps / CI/CD engineers
  - QA / Test engineers

---

## 5. Hardware / Infrastructure Requirements

- Development machines: modern desktops/laptops with 8+ GB RAM
- HSM / KMS access for key management testing
- Test environment for large files and multi-OS compatibility
- Optional servers for telemetry, policy enforcement, and secure sharing

---

## 6. Security & Compliance Requirements

- HSM / KMS integration for master key protection
- Zeroization of sensitive memory
- Tamper detection and integrity checks
- FIPS 140-2/3 compliance mode (optional)
- Audit logging with role-based access
- Multi-factor authentication for sensitive operations
- Secure update mechanism with code signing

---

## 7. Deliverables

1. Fully functional cross-platform Ninja Crypter GUI
2. CLI for automation and scripting
3. Java SDK for programmatic access
4. Complete unit, integration, and fuzz tests
5. Developer documentation, API documentation, and user guides
6. Secure CI/CD pipeline with automated testing
7. Deployment-ready packages for Windows, macOS, and Linux

---

## 8. Summary

This requirements analysis defines all **functional, non-functional, technical, development, and security requirements** for the Ninja Crypter project. It ensures that the development team has a clear specification for building a **secure, enterprise-grade file encryption application** that is cross-platform, auditable, and capable of protecting top-secret files while supporting GUI, CLI, and programmatic access.

