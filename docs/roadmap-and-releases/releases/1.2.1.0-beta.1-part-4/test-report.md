# Test Report

### Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of:

- **Functionality**
- **Deployability**
- **Configurability**
- **Customizability**

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence, configurability and extensibility of the software are also assessed. This ensures readiness of the software for use in multiple countries.

Since MOSIP is an **“API First”** product platform, the verification scope requires comprehensive automation testing for all MOSIP APIs. An automation Test Rig has been created for this purpose.


### Test Approach

A **persona-based approach** has been adopted to perform the IV&V, simulating test scenarios that resemble a real-time implementation.

A **persona** is a fictional character or user profile created to represent a user type that might use a product or service in a particular way. Persona-based testing is a software testing technique that puts testers in the customer's shoes, assesses their needs, and determines use cases/scenarios that customers will execute.

The persona needs may be addressed through any of the following:

- **Functionality**
- **Deployability**
- **Configurability**
- **Customizability**

The verification methods may differ based on how the need was addressed.

For regression checks, the **MOSIP Test Rig**—an automation testing suite designed and developed in-house—supports persona-based testing. It covers end-to-end test execution and reporting.

**Key aspects of MOSIP Test Rig:**

- End-to-end functional test scenarios written from pre-registration to:
  - Creation of packets at registration centers
  - Processing packets through the registration processor
  - Generating UIN
  - Authenticating identity using IDA with various permutations and combinations
- Open-source artifact enabling countries to validate SI deliveries before going live
- Includes both **positive personas** (e.g., genuine citizens) and **negative personas** (e.g., bribed registration officers, malicious insiders)
- The needs of positive personas must be met, while the needs of negative personas must be effectively restricted


### Verified Configuration

Verification was performed on the following configuration:

- **Default configuration** with 3 languages (English, Arabic, French)

**Main features tested:**

- Registration Client
- Master Data
- ID Authentication
- Key Manager


### Test Execution Statistics

**Functional Test Results**

Below are the test metrics from functional testing using mock MDS, mock Auth, and mock ABIS:

| Total | Passed | Failed | Skipped | Ignored |
|-------|--------|--------|---------|---------|
| 1967  | 1861   | 1      | 0       | 105     |

**Test Rate: 100%**  
**Pass Rate: 99.95%**

**Detailed Breakdown**

| Module              | Total | Pass | Fail | Skipped | Ignored |
|---------------------|-------|------|------|---------|---------|
| Master Data - Eng   | 945   | 945  | 0    | 0       | 0       |
| ID Repository       | 410   | 325  | 1    | 0       | 84      |
| ID Authentication   | 612   | 591  | 0    | 0       | 21      |
| **Overall**         | 1967  | 1861 | 1    | 0       | 105     |

> **Note:** In API-based testing, some test cases are marked as 'ignored' due to dependencies on other modules.


**DSL – End-to-End Scenarios Results**

| Total | Pass | Fail | Skipped |
|-------|------|------|---------|
| 205   | 165  | 11   | 29      |


### Detailed Test Metrics

The metrics derived from manual and automation testing include:

- **Defect Density**
- **Test Coverage**
- **Test Execution Coverage**
- **Test Tracking & Efficiency**

**Key indicators:**

- **Passed Test Case Coverage:**  
  `(Number of passed tests / Total number of tests executed) × 100`
- **Failed Test Case Coverage:**  
  `(Number of failed tests / Total number of tests executed) × 100`

  
