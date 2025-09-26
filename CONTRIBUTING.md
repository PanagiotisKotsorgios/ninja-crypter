# Contributing to Ninja Crypter

Thank you for contributing to the NinjaApp repository! This is a **private, commercial project**. Only authorized developers from [Your Company Name] are permitted to access and contribute to this repository.  

By contributing, you agree to maintain confidentiality and follow company policies regarding security and intellectual property.

---

## 1. Getting Started
1. **Access**: Only authorized personnel may clone or fork this repository.  
2. **Development Environment**: Use the approved Java version (e.g., Java 17+) and follow company IDE configurations.  
3. **Dependencies**: Use `libs/` for local JARs or manage dependencies via Gradle/Maven as configured.

---

## 2. Branching Strategy
- **main**: Production-ready code, only updated via pull requests after review.  
- **develop**: Integration branch for all ongoing features.  
- **feature/<name>**: New features.  
- **bugfix/<name>**: Fixes to issues.  
- **hotfix/<name>**: Urgent production fixes.

---

## 3. Commit Guidelines
- Follow the format:  

**Types:**  
- `feat`: New feature  
- `fix`: Bug fix  
- `refactor`: Code restructuring  
- `docs`: Documentation  
- `test`: Adding or fixing tests  
- Include detailed descriptions in the commit body if necessary.  
- Never include sensitive keys, credentials, or confidential data in commits.

---

## 4. Coding Standards
- **Package Naming**: `com.ninjaapp.<module>`  
- **Class Naming**: PascalCase  
- **Method/Variable Naming**: camelCase  
- **Documentation**: Use Javadoc for all public classes and methods  
- **Code Style**: Follow company style guide in `docs/CodingGuidelines.md`  
- **Unit Testing**: Write tests for all new functionality. Place tests in `src/test/java/com/ninjaapp/unit/`.

---

## 5. Security & Confidentiality
- Do not expose **encryption keys, credentials, or sensitive user data** in code, commits, or logs.  
- Any external connections (API, database, analytics) must follow company security guidelines.  
- Code that handles user data must **encrypt, anonymize, or otherwise protect sensitive information**.  

---

## 6. Pull Requests (PRs)
- Open a PR from your feature/bugfix branch into `develop`.  
- PR must include:  
- Description of changes  
- Screenshots or test results if applicable  
- References to related issues or tasks  
- PRs must be **reviewed by at least one other authorized developer**.  
- Merge PRs only after all **tests pass** and security checks are verified.

---

## 7. Issue Tracking
- Report bugs, feature requests, or security issues using the templates in `.github/ISSUE_TEMPLATE/`.  
- Always reference relevant issues in your PR.

---

## 8. Code of Conduct
All contributors must adhere to the **[Code of Conduct](CODE_OF_CONDUCT.md)**, maintaining professionalism and confidentiality at all times.

---

## 9. Acknowledgment
By contributing to this repository, you confirm that you:  
- Are an authorized developer of [Your Company Name]  
- Have read and agreed to follow the **LICENSE.md**, **Code of Conduct**, and internal security guidelines.
