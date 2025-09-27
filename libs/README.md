
# Ninja Crypter — Libraries Folder

This folder contains **all third-party libraries and dependencies** used by the Ninja Crypter project.

## Folder Structure

- `core/` — Encryption algorithm libraries (AES-GCM, XChaCha20, ECIES, RSA)  
- `key-management/` — Vault, AWS KMS, Azure Key Vault SDKs, HSM libraries  
- `gui/` — JavaFX SDK, GUI utilities, icons, and visual assets  
- `network/` — Networking and JSON parsing libraries  
- `testing/` — Unit testing, mocking, and fuzzing tools  
- `legacy/` — Optional legacy libraries or algorithms  

## Usage

- Add all JARs in `libs/` to the **project classpath** during compilation and packaging.  
- **Do not modify** libraries without approval; keep them versioned and documented.  
- When adding a new library, **update this README** with the library name, version, and purpose.

> All libraries must be approved for **commercial use** and comply with licensing restrictions.
