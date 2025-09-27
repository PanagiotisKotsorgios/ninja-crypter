# Ninja Crypter — Version 1.0 Release Notes

**Release Date:** 2026-03-01

## Overview
- Enterprise-ready release.
- GUI and CLI fully functional.
- Encrypted storage initialized automatically.
- Master Key (MK) and per-file Data Keys (DK) managed securely.
- Audit logging and tamper detection implemented.
- Secure file sharing and revocation available.
- Installer ready with desktop/Start Menu shortcuts.

## New Features
- Full AEAD encryption support: AES-GCM, XChaCha20-Poly1305
- Hybrid key wrapping: RSA-OAEP, ECIES
- Key rotation and secure storage
- GUI wizards for encrypt/decrypt/share operations
- CLI commands for scripting and automation

## Known Limitations
- Remote policy sync (planned for v2.0)
- Multi-user RBAC (planned for v2.0)
