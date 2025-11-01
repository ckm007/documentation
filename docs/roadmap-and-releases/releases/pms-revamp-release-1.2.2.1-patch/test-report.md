---
hidden: true
---

# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of&#x20;

* Functionality
* Deployability
* Configurability
* Customizability

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software is also assessed. This ensures the readiness of software for use in multiple countries. Since MOSIP is an “API First” product platform, Verification scope required comprehensive automation testing for all the MOSIP APIs. An automation Test Rig is created for the same.

The Partner Management System Revamp testing scope revolves around the following flows:

* Features: Authentication Partner, Device Partner, FTM Partner, Partner Admin Certificate Trust Store, Partners, Policies, Partner-Policy Linking, SBI-Device, FTM Chip, Authentication Services, User Profile, User Dashboard, Accept Terms & Conditions/ Consent.
* Multilingual (English/Arabic/French)
* Multi-browser testing: Using Edge, Firefox, and Chrome browsers (Windows/ Mac, Tablet, Extra-large screen)
* Partner Management System Revamp End to End testing
* Regression Testing
* Integration Testing

## Test Approach

Persona based approach has been adopted to perform the IV\&V, by simulating test scenarios that resemble a real-time implementation.

A Persona is a fictional character/user profile created to represent a user type that might use a product/or a service in a similar way. Persona based testing is a software testing technique that puts software testers in the customer's shoes, assesses their needs from the software and thereby determines use cases/scenarios that the customers will execute. The persona needs may be addressed through any of the following.

* Functionality
* Deployability
* Configurability
* Customizability

The verification methods may differ based on how the need was addressed.

For regression check, “MOSIP Test Rig” - an automation testing suite - which is indigenously designed and developed for supporting persona-based testing. MOSIP Test Rig covers the end-to-end test execution and reporting. The end-to-end functional test scenarios are written starting from creation of packet in registration center, processing the packet through the registration processor, generating UIN and authenticating identity using IDA through various permutation and combinations of cases being covered. MOSIP Test Rig will be an open-source artifact which can also be enhanced and used by countries to validate the SI deliveries before going live. Persona classes include positive personas.

## Verified configuration

Verification is performed on various configurations as mentioned below

* Default configuration with verified configuration for 3 Lang (English/Arabic/French)

## Browser compatibility evaluations

* Browser versions tested on desktop/laptop

<table><thead><tr><th width="100.73651123046875" valign="top">Sl.No</th><th width="302.328857421875" valign="top">Browser</th><th valign="top">Versions</th></tr></thead><tbody><tr><td valign="top">1</td><td valign="top">Chrome</td><td valign="top">Version 133.0.6943.127</td></tr><tr><td valign="top">2</td><td valign="top">Firefox</td><td valign="top">Version 135.0.1</td></tr><tr><td valign="top">3</td><td valign="top">Edge</td><td valign="top">Version 133.0.3065.82</td></tr><tr><td valign="top">4</td><td valign="top">Safari</td><td valign="top">Version 18.3</td></tr></tbody></table>



* Browser versions tested on tablet device

<table data-header-hidden><thead><tr><th width="112.37359619140625" valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Sl.No</td><td valign="top">Browser</td><td valign="top">Versions</td></tr><tr><td valign="top">1</td><td valign="top">Chrome</td><td valign="top">Version 133.0.6943.121</td></tr><tr><td valign="top">2</td><td valign="top">Firefox</td><td valign="top">Version 135.0.1</td></tr><tr><td valign="top">3</td><td valign="top">Edge</td><td valign="top">Version 133.0.3065.82</td></tr></tbody></table>



* Browser versions tested on extra-large screens

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Sl.No</td><td valign="top">Browser</td><td valign="top">Versions</td></tr><tr><td valign="top">1</td><td valign="top">Chrome</td><td valign="top">Version 133.0.6943.127</td></tr><tr><td valign="top">2</td><td valign="top">Firefox</td><td valign="top">Version 135.0.1</td></tr><tr><td valign="top">3</td><td valign="top">Edge</td><td valign="top">Version 133.0.3065.82</td></tr><tr><td valign="top">4</td><td valign="top">Safari</td><td valign="top">Version 18.3</td></tr></tbody></table>

&#x20;

## Screen sizes used for UI responsiveness validation

* Laptop/Desktop: 1920x1080
* Tablet: 1280X800
* Extra-large screens: 3840x2160
* Mac book: 2560 x 1664

## Feature Health

## Test execution statistics

### Functional test results by modules

Below are the test metrics by performing functional testing. The process followed was black box testing which based its test cases on the specifications of the software component under test. The functional test was performed in combination with individual module testing as well as integration testing. Test data were prepared in line with the user stories. Expected results were monitored by examining the user interface. The coverage includes GUI testing, System testing, End-To-End flows across multiple languages and configurations. The testing cycle included simulation of multiple identity schema and respective UI schema configurations.

Manual Verification (UI):

<table><thead><tr><th valign="top">Total</th><th valign="top">Passed</th><th valign="top">Failed</th><th valign="top">Skipped (N/A)</th></tr></thead><tbody><tr><td valign="top">4103</td><td valign="top">4033</td><td valign="top">39</td><td valign="top">31</td></tr><tr><td valign="top">Test Rate: 99% with Pass Rate: 99%</td><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>

Note: NA - 31 Test Cases which are descoped scenarios/not developed feature

Manual Verification (API):

<table><thead><tr><th valign="top">Total</th><th valign="top">Passed</th><th valign="top">Failed</th><th valign="top">Skipped (N/A)</th></tr></thead><tbody><tr><td valign="top">542</td><td valign="top">532</td><td valign="top">2</td><td valign="top">8</td></tr><tr><td valign="top">Test Rate: 98% with Pass Rate: 98%</td><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>

Note: NA - 8 Test Cases which are descoped scenarios/not developed feature



API Test Rig:

<table><thead><tr><th width="208.2698974609375" valign="top">Total</th><th width="82.30755615234375" valign="top">Passed</th><th width="81.102294921875" valign="top">Failed</th><th width="118.6527099609375" valign="top">Skipped (N/A)</th><th width="115.8394775390625" valign="top">Ignored</th><th valign="top">Known issues</th></tr></thead><tbody><tr><td valign="top">509</td><td valign="top">497</td><td valign="top">0</td><td valign="top">0</td><td valign="top">0</td><td valign="top">12</td></tr><tr><td valign="top">Test Rate: 98% with Pass Rate: 98%</td><td valign="top"></td><td valign="top"></td><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>



{% hint style="warning" %}
Note - API flow is tested through automation for both positive and negative scenarios, while test cases that are not automated are tested manually.
{% endhint %}

### Detailed Test metrics

Below are the detailed test metrics by performing Manual/automation testing. The project metrics are derived from Defect density, Test coverage, Test execution coverage, test tracking and efficiency.

The various metrics that assist in test tracking and efficiency are as follows:

* Passed Test Cases Coverage: It measures the percentage of passed test cases. (Number of passed tests / Total number of tests executed) x 100
* Failed Test Case Coverage: It measures the percentage of all failed test cases. (Number of failed tests / Total number of test cases executed) x 100

### Tested with components:

<table><thead><tr><th valign="top">Module/Repo</th><th valign="top">Compatible Version</th></tr></thead><tbody><tr><td valign="top">partner-management-portal</td><td valign="top">mosipqa/pmp-revamp-ui:1.2.2.x</td></tr><tr><td valign="top">partner-management-services</td><td valign="top">mosipqa/partner-management-service:1.2.2.x</td></tr><tr><td valign="top">Policy Management service</td><td valign="top">mosipqa/policy-management-service:1.2.2.x</td></tr><tr><td valign="top">Key-manager</td><td valign="top">mosipqa/kernel-keymanager-service:1.3.x</td></tr><tr><td valign="top">IDA Auth</td><td valign="top">mosipid/authentication-service:1.2.1.0</td></tr><tr><td valign="top">Artifactory</td><td valign="top">mosipid/artifactory-server:1.2.0.2</td></tr><tr><td valign="top">eSignet</td><td valign="top">mosipid/esignet:1.4.1</td></tr><tr><td valign="top">Notifier (Kernel)</td><td valign="top">mosipid/kernel-notification-service:1.2.0.1</td></tr><tr><td valign="top">Audit manager</td><td valign="top">mosipid/kernel-auditmanager-service:1.2.0.1</td></tr><tr><td valign="top">ID Repro</td><td valign="top">mosipid/id-repository-identity-service:1.2.1.0</td></tr><tr><td valign="top">datashare</td><td valign="top">mosipid/data-share-service:1.2.0.1</td></tr><tr><td valign="top">Keycloak</td><td valign="top">mosipid/mosip-artemis-keycloak:1.2.0.1</td></tr><tr><td valign="top">config-server</td><td valign="top">mosipid/config-server:1.1.2</td></tr><tr><td valign="top">Websub</td><td valign="top">mosipid/websub-service:1.2.0.1</td></tr><tr><td valign="top">postgres</td><td valign="top">bitnami/postgresql:15.4.0-debian-11-r10</td></tr></tbody></table>

### Sonar Report

* Partner-Management-Service:
* Partner-Management-Portal:

