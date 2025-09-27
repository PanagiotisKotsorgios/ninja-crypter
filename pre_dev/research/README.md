# Ninja Crypter — Research Notes

**Project Status:** Pre-Development  
**Purpose:** Collect and organize all research, references, and findings relevant to the Ninja Crypter encryption project.  

---

## 1. Cryptography Research

### 1.1 Symmetric Encryption
- **AES-256-GCM**  
  - Authenticated encryption (AEAD)  
  - Recommended for strong enterprise-grade encryption  
  - Uses 96-bit random IV per file  

- **XChaCha20-Poly1305**  
  - Alternative AEAD for platforms without AES-NI  
  - Streamable for large files  

- **Key Takeaways:**  
  - Always use AEAD; do not implement unauthenticated modes  
  - Random per-file keys improve security  

### 1.2 Asymmetric Encryption / Key Wrapping
- **RSA-OAEP (SHA-256)**  
  - Recommended key sizes: 4096+ bits  
  - Suitable for wrapping symmetric data keys  

- **ECIES (Curve25519 / X25519 + AEAD)**  
  - Ephemeral key exchange for secure file sharing  

- **Key Takeaways:**  
  - Hybrid encryption (symmetric + asymmetric) is needed for sharing  
  - Use AEAD for all wrapped keys  

### 1.3 Key Derivation & Hashing
- **HKDF (SHA-256 / SHA-512)** for subkey derivation  
- **Argon2id** for password-based encryption  
- **PBKDF2-HMAC-SHA256** as a legacy option  
- **HMAC-SHA256** for message authentication  

### 1.4 Signing & Integrity
- **Ed25519** for file signing  
- **RSA-PSS** for release signing  
- **Metadata authentication** (version, timestamps, algorithm, recipients)  

---

## 2. File Formats & Containers

- Containerized file format:  
  `Header + Metadata + Encrypted Data + Auth Tag + Optional Signature`  
- Versioned to support algorithm upgrades  
- Supports multiple recipients, each with wrapped data key  
- Streaming support for very large files  

---

## 3. Key Management & Storage

- **Master Key (MK)** stored in HSM or KMS (HashiCorp Vault, AWS KMS, Azure Key Vault)  
- **Data Key (DK)** generated per file, wrapped by MK or recipient public key  
- Key rotation strategies: rewrap DKs or re-encrypt files  
- RBAC-based key access policies  
- Audit logging for key events  
- Zeroization of keys in memory after use  

---

## 4. GUI & CLI Research

- **GUI**  
  - JavaFX recommended for cross-platform support  
  - Drag & drop functionality for files/folders  
  - Wizard flows for encryption and decryption  
  - Key Manager, Audit Log viewer, Policy & Settings panel  

- **CLI**  
  - Commands for encrypt, decrypt, share, rotate keys, and audit logs  
  - Scripting-friendly: exit codes, JSON output for automation  

- **API / SDK**  
  - Java SDK for programmatic encryption, decryption, and key management  
  - Internal REST endpoints for policy and telemetry  

---

## 5. Libraries & Tools Evaluation

| Library / Tool | Purpose | Notes |
|----------------|--------|------|
| BouncyCastle | Cryptography primitives | Strong, widely used in Java |
| Google Tink | AEAD wrapper | Optional for simplifying AEAD |
| JavaFX | GUI | Cross-platform UI |
| Jackson / Gson | JSON | For metadata and config |
| SLF4J + Logback | Logging | Enterprise-grade logging |
| Apache HttpClient | Networking | For optional telemetry and policy sync |
| JUnit 5 | Testing | Unit and integration testing |
| Mockito | Testing | Mocking components |

---

## 6. Security Considerations

- Always use AEAD encryption modes  
- Fail-closed on errors to prevent data leaks  
- Ensure zeroization of keys and sensitive memory  
- Tamper detection for both files and metadata  
- FIPS-compliant options if required  

---

## 7. Platform & Development Notes

- Java 17+ for cross-platform compatibility  
- Target OS: Windows, macOS, Linux  
- Build tools: Maven or Gradle  
- Version control: GitHub / GitLab  
- CI/CD pipelines for testing, building, and code signing  

---

## 8. References & Links

- [NIST AES-GCM specification](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf)  
- [XChaCha20-Poly1305 documentation](https://datatracker.ietf.org/doc/html/draft-irtf-cfrg-xchacha)  
- [RSA-OAEP standard](https://www.rsa.com/rsalabs/node.asp?id=2125)  
- [ECIES reference](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme)  
- [BouncyCastle Java library](https://www.bouncycastle.org/java.html)  
- [Google Tink](https://developers.google.com/tink)  

---

## 9. Summary

This document collects all **research, notes, and references** required for the Ninja Crypter project. It will guide developers and architects in selecting secure algorithms, implementing key management, designing file formats, and building both GUI and CLI components. As the project progresses, this file will be **updated continuously** with new research, evaluations, and best practices.
