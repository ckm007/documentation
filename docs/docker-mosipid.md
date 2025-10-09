# MOSIP (Modular Open Source Identity Platform)

**MOSIP** is an open-source, modular platform that enables governments and organizations to build secure, scalable, and interoperable digital identity systems. It promotes privacy, vendor neutrality, and open standards for foundational ID programs worldwide.

**Website:** [https://www.mosip.io](https://www.mosip.io)  
**Documentation:** [https://docs.mosip.io](https://docs.mosip.io)  
**Community:** [https://community.mosip.io](https://community.mosip.io)  
**License:**
* Core MOSIP modules – Mozilla Public License 2.0
* Reference modules – MIT License
---

## Getting Started
To explore MOSIP’s source code and architecture, visit our GitHub repositories and [MOSIP Documentation](https://docs.mosip.io) for setup, deployment, and contribution guides.  
Contribution process: [Contributor Guide](https://docs.mosip.io/1.2.0/community/code-contributions)

---

## Core Modules Overview

| **Module** | **Purpose / Highlights** | **GitHub** |
|-------------|--------------------------|-------------|
| **Pre-Registration** | Online appointment booking and data entry before visiting centers. | [mosip/pre-registration](https://github.com/mosip/pre-registration) |
| **Registration Client** | Captures demographic + biometric data (desktop + Android, offline-first). | [registration-client](https://github.com/mosip/registration-client) / [android-client](https://github.com/mosip/android-registration-client) |
| **Registration Processor** | Validates and deduplicates data using ABIS workflows. | [mosip/registration](https://github.com/mosip/registration) |
| **ID Repository** | Securely stores processed identity data and generates UINs/tokens. | [mosip/id-repository](https://github.com/mosip/id-repository) |
| **Authentication** | Provides identity verification (OTP, biometric, key-based). | [mosip/id-authentication](https://github.com/mosip/id-authentication) |
| **Resident Services** | Self-service portal for residents to manage UIN and credentials. | [resident-ui](https://github.com/mosip/resident-ui) / [resident-services](https://github.com/mosip/resident-services) |
| **Partner Management** | Onboards and certifies ecosystem partners and vendors. | [partner-management-services](https://github.com/mosip/partner-management-services) / [portal](https://github.com/mosip/partner-management-portal) |
| **Administration** | Manages master data, access roles, and operational parameters. | [admin-services](https://github.com/mosip/admin-services) / [admin-ui](https://github.com/mosip/admin-ui) |
| **Analytics & Reporting** | Provides anonymized metrics and monitoring insights. | [mosip/reporting](https://github.com/mosip/reporting) |

---

## Additional Resources
- **Configurations:** [mosip/mosip-config](https://github.com/mosip/mosip-config)  
- **Infrastructure & Deployment:** [mosip-infra](https://github.com/mosip/mosip-infra) , [k8s-infra](https://github.com/mosip/k8s-infra).
- **Licenses:** [MPL 2.0](https://www.mozilla.org/en-US/MPL/2.0/) and [MIT](https://mit-license.org/) (varies by repo)

---

## Contributing
We welcome community participation through bug fixes, feature development, and feedback.  
Refer to the [Contributor Guide](https://docs.mosip.io/1.2.0/community/code-contributions) for contribution standards.

---

## Governance
MOSIP is maintained by the **MOSIP Foundation**, in collaboration with governments, academic institutions, and open-source contributors worldwide.
