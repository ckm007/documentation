# Privacy

## Overview

The right to privacy is a fundamental right in many contexts. Privacy protection or preservation can be ensured in an application by adopting a privacy friendly design stance.

## What is privacy and privacy protection?

Privacy takes many forms. From an identity system perspective, the confidentiality of identity information and anonymity when using the identity offers privacy.

MOSIP views the identity system as a custodian of the individual's data. This data has to be protected in order to protect the individual from privacy and security risks. Privacy protection measures include [data protection](data-protection.md), transparency, user control, confidentiality, selective disclosure, user anonymity and intrusion protection.

## Privacy design elements

MOSIP addresses privacy design at four levels.

### 1. Functional Privacy

Functional Privacy ensures the system is designed to process and expose only the data necessary for a specific function. It embodies data minimization and protects individuals from unnecessary data collection and exposure.

By embedding this principle, MOSIP achieves:

- 📉 Minimal data exposure across system components
- 🔒 Robust protection against unauthorized access and misuse
- 🛡️ Compliance with privacy principles like data minimization and purpose limitation
- 🌐 Alignment with standards and specifications. (refer [here](https://docs.mosip.io/1.2.0/readme/standards-and-specifications) to know more about the standards and specification)

MOSIP achieves Functional Privacy through the following key mechanisms:

- Selective Disclosure
  - **What it is**  -Selective disclosure is the principle of limiting the data shared with different system components or relying parties to only what they strictly require.
  - **Purpose**  -To prevent over-sharing of personal data across services and ensure privacy at every step of the identity lifecycle.
  - **How MOSIP implements it**  -MOSIP’s modular architecture ensures that different modules (e.g., Registration, ID Authentication) only access and process the subset of identity data they need for their specific tasks. For example:
    - The Registration Client only collects demographic and biometric data required for enrolment.
    - Authentication services only verify the attributes requested by the relying party without exposing the full identity.

- Anonymization
  - **What it is**  -Anonymization removes or masks personal identifiers to make it impossible to link data back to an individual.
  - **Purpose**  -To ensure privacy in scenarios like analytics, system monitoring, and reporting where identification isn’t necessary.
  - **How MOSIP implements it**  -Audit logs and analytics data in MOSIP are anonymized by stripping or pseudonymizing personally identifiable information (PII), ensuring privacy even in post-processing environments.

- Need to Know
  - **What it is**  -This principle limits access to personal data only to the individuals, modules, or systems that require it for their roles.
  - **Purpose**  -To reduce the risk of unauthorized access and exposure of sensitive information.
  - **How MOSIP implements it**  -MOSIP enforces Role-Based Access Control (RBAC) and fine-grained permissions across modules. For example:
      - Biometric data is accessible only to the modules responsible for deduplication and authentication.
      - Administrative users can only view logs relevant to their operational scope.

- Encryption
  - **What it is**  -Encryption secures sensitive data by converting it into an unreadable format accessible only with the right cryptographic keys.
  - **Purpose**  -To safeguard sensitive identity data from unauthorized access, breaches, or interception during storage and transmission.
  - **How MOSIP implements it**
    - MOSIP uses encryption algorithms such as: RSA,Elliptic Curve Cryptography (EC),JSON Web Encryption (JWE) 
    - Secure key management is enforced through **Hardware Security Modules (HSMs)** for cryptographic key storage and usage.

- Tokenization
  - **What it is**  -Tokenization substitutes sensitive data elements with randomly generated tokens to reduce direct exposure of real identifiers during system operations.
  - **Purpose**  -To protect sensitive identifiers like UINs during processing and interaction between modules.
  - **How MOSIP implements it**  -In MOSIP, sensitive identifiers (such as UIN) are tokenized during authentication or API interactions to ensure the original identifiers are not exposed to external systems.

### 2. Security

Security is a foundational principle ensuring the protection of the system, user data, and transactions from unauthorized access, breaches, and malicious attacks.

By embedding strong security practices, MOSIP achieves:

- 🔒 Protection of sensitive identity data from external and internal threats
- 🧑‍💻 Resilience against cyberattacks and unauthorized system usage
- 🌐 Trust and confidence for governments, system integrators, and end-users
- 🛠️ Compliance with global security standards and frameworks

This robust security framework enables MOSIP to function as a reliable backbone for national ID systems deployed worldwide.

MOSIP implements its security framework through the following key sub-elements:

- Data Security
  - **What it is**  -Data security ensures that all data handled by MOSIP—whether in storage or while processing—is safeguarded against unauthorized access, tampering, or breaches.
  - **Purpose**  -To prevent data leaks, ensure confidentiality and integrity, and protect user identities throughout their lifecycle.
  - **How MOSIP implements it**  -MOSIP adopts a multi-layered security approach to protect sensitive data:
    - **Encryption & Decryption** – Encryption is achieved using algorithms such as RSA, EC, and JWE.
    - **Hashing** – Sensitive elements like biometric templates are hashed with secure algorithms.
    - **HSM-backed Key Management** – Cryptographic keys are securely managed using Hardware Security Modules.
    - **Database Security** – Role-based permissions and audit trails monitor access.
refer this [link](https://docs.mosip.io/1.2.0/readme/principles/privacy-and-security/data-protection) to know more about how MOSIP Identity Platform supports data security

- Trusted Applications
  - **What it is**  -Trusted applications refer to MOSIP’s mechanism to ensure that only verified and authorized software can interact with core modules and services.
  - **Purpose**  -To prevent unverified, potentially malicious applications from accessing sensitive APIs or data within MOSIP.
  - **How MOSIP implements it**  -MOSIP uses several mechanisms to ensure only authorized applications interact with the identity system:
    - **API Key Management** – Each external application accessing MOSIP APIs is registered and issued secure API keys.
    - **Digital Certificates** – Mutual TLS (mTLS) ensures both MOSIP and external applications verify each other’s identity.
    - **Sandbox Environments** – Applications are tested and validated in a sandbox before production deployment.

- Access Control
  - **What it is**  -Access control manages who can view, modify, or use specific data and system functions within MOSIP.
  - **Purpose**  -To ensure that only authorized personnel and system components can access sensitive data or perform privileged operations.
  - **How MOSIP implements it**  -MOSIP enforces strict access policies through:
    - **Role-Based Access Control (RBAC)** – Defines roles (e.g., admin, registrar, operator) with precise permissions.
    - **Principle of Least Privilege** – Grants users/modules only the minimum access necessary for their tasks.
    - **Audit Trails** – Tracks and logs all access attempts and changes for monitoring and compliance.
    - **Multi-Factor Authentication (MFA)** – Adds an additional layer of protection for administrative access.

### 3. User Centricity

User Centricity means putting individuals at the heart of the identity system. It ensures that users are empowered to control their data, understand how it’s used, and interact with the system in ways that are inclusive, usable, and respectful of their privacy.

By adopting user-centric principles, MOSIP achieves:

- 👤 Empowerment of individuals over their personal data
- ✅ Transparency and informed decision-making through consent
- 🌍 Inclusivity for diverse populations, including the marginalized
- 📱 Usability to support users with varying levels of digital literacy

This approach ensures MOSIP supports privacy rights and accessibility for all users, making identity systems fair and equitable.

MOSIP integrates User Centricity through the following sub-elements:

- User Control
  - **What it is**  -User Control means enabling individuals to manage how their identity data is collected, used, and shared within the system.
  - **Purpose**  -To empower users with autonomy over their data, preventing misuse or overreach by third parties.
  - **How MOSIP implements it**
    - Users can update certain attributes through designated update mechanisms. For example, if a user wishes to update their address, they can log in to the resident portal and make the change directly. If they require assistance, they may visit a registration center, where an operator will update the address on their behalf. Once the update is successful, the new information will be reflected in the user’s records.
    - Authentication requests disclose what data is being accessed, giving users the choice to proceed or decline.  

- Consent
  - **What it is**  -Consent is the process of obtaining explicit and informed agreement from individuals before accessing or using their personal data.
  - **Purpose**  -To respect individual privacy rights and comply with global data protection regulations.
  - **How MOSIP implements it**  -MOSIP integrates consent mechanisms at multiple stages:
    - **During registration** – Presents clear information about data usage and requires explicit consent before proceeding.
    - **During authentication** – Displays prompts specifying which identity attributes are being requested.
    - **User decision** – Individuals can approve or deny data-sharing requests before information is transmitted.
    - **Auditing** – Consent actions are securely recorded for transparency and accountability.

- Usability
  - **What it is**  -Usability ensures the system is designed to be simple, intuitive, and accessible to people of varying education levels and digital literacy.
  - **Purpose**  -To make MOSIP approachable and effective for all users, including those unfamiliar with technology.
  - **How MOSIP implements it**  
    - Multilingual support in registration and authentication modules.
    - Simple, clear UI/UX design in client applications.
    - Offline capabilities for areas with low connectivity.
    - Assisted user journeys for vulnerable individuals.
    - Incorporation of GenderMag principles to evaluate and improve usability across diverse cognitive styles and gender-inclusive perspectives  

- Inclusion
  - **What it is**  -Inclusion ensures that the identity system accommodates all segments of society, including marginalized groups, persons with disabilities, and those in remote areas.
  - **Purpose**  -To prevent exclusion and ensure equitable access to identity for every individual.
  - **How MOSIP implements it**  
    - Supports biometric exceptions for individuals unable to provide fingerprints.
    - Allows demographic-only registration when biometrics cannot be captured.
    - Provides accessibility features for people with disabilities.
    - Designed for multilingual, multi-cultural, and resource-constrained environments.

   You can refer to this [link](https://docs.mosip.io/1.2.0/readme/principles/inclusion) to know more about how MOSIP Identity Platform supports inclusivity


### 4. Transparency

Transparency ensures that all stakeholders—governments, system integrators, and end users—have clear visibility into how the system works, how decisions are made, and how data is handled.

By embedding transparency into its architecture and processes, MOSIP achieves:

- 🏛️ Trust through openness and accountability
- 📜 Verifiability of system behavior and outputs
- 👥 Governance structures that ensure fair and ethical use of the platform

This fosters confidence in MOSIP as a public good and aligns it with international best practices for open and transparent digital systems.

MOSIP enables Transparency through the following sub-elements:

- Openness
  - **What it is**  -Openness means making MOSIP’s design, codebase, and operational principles publicly accessible to encourage trust, collaboration, and innovation.
  - **Purpose**  -To promote community participation, allow peer review, and ensure the platform evolves securely and inclusively.
  - **How MOSIP implements it**  
    - **Open-source architecture** – Entire codebase is published under an open-source license on GitHub.
    - **Open APIs and standards** – API documentation and integration standards are freely available.
    - **Community engagement** – Feedback and contributions from global experts are encouraged.  

- Verifiability
  - **What it is**  -Verifiability ensures that the system’s actions and outputs can be independently audited for correctness and compliance.
  - **Purpose**  -To build stakeholder confidence that the system operates as intended without hidden processes or biases.
  - **How MOSIP implements it**
      - **Audit trails** – All critical system actions are logged for compliance and monitoring.
      - **Deterministic algorithms** – Processes yield consistent, predictable results for identical inputs.
      - **Third-party assessments** – Encourages independent audits of MOSIP deployments.  

- Governance
  - **What it is**  -Governance refers to the frameworks and policies defining how MOSIP is managed, maintained, and deployed responsibly.
  - **Purpose**  -To ensure fair, ethical, and lawful operation of MOSIP-based identity systems, protecting individuals’ rights.
  - **How MOSIP implements it**  
    - **Strong governance model** – Managed by IIIT-Bangalore for independence and neutrality.
    - **Advisory boards** – Include global experts guiding MOSIP’s evolution.
    - **Policy frameworks** – Guidance for governments on privacy, security, and ethical deployment.  

These design principles have resulted in features as well as development practices in MOSIP that enhance privacy protection. A typical example for a practice is how PII (Personally Identifiable Information) is dealt with when creating application or audit logs. An example of a feature is how our [Datashare policies](../../../id-lifecycle-management/support-systems/partner-management-services/partners.md#partner-policies) allow selective sharing of information.
