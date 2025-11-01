# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of :

* Deployability&#x20;
* Functionality (Automation API Testrig & DSLs) and Reg Client sanity

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software is also assessed. This ensures readiness of software for use in multiple countries. Since MOSIP is an “API First” product platform, Verification scope required comprehensive automation testing for all the MOSIP APIs. An automation Test Rig is created for the same.

## Test Approach

Reference docs: [https://github.com/mosip/infra/tree/release-0.1.0](https://github.com/mosip/infra/tree/release-0.1.0)  &#x20;

* Deployability&#x20;
* Functionality (Automation API Testrig & DSLs) and Reg Client UI

The verification methods may differ based on how the need was addressed.&#x20;

MOSIP Test Rig covers the end to end test execution and reporting. The end to end functional test scenarios are written starting from pre-registration, to creation of packet in registration center, processing the packet through the registration processor, generating UIN and authenticating identity using IDA through various permutation and combinations of cases being covered. MOSIP Test Rig will be an open source artifact which can also be enhanced and used by countries to validate the SI deliveries before going live.

Environment name: mod.mosip.net

Rapid deployment test completed on date: 07<sup>th</sup> Oct 2025. \


## Time taken for deployment

| Component                                                                                       | Time taken | Time taken |
| ----------------------------------------------------------------------------------------------- | ---------- | ---------- |
| RDT2                                                                                            | RDT1       |            |
| Terraform plan/apply                                                                            | 25m 45s    | 25m 34s    |
| Helmsman External services of MOSIP using Helmsman                                              | 15m 59s    | 12m 31s    |
| Helmsman Deploy MOSIP services of MOSIP using Helmsman                                          | 52m 7s     | 47m 57s    |
| <p>Helmsman Testrigs of MOSIP using Helmsman</p><p>(API Testrig -full run and DSL - Sanity)</p> | 2h 55m 49s | 3h 5m 40s  |

## Rapid Deployment - Check List

<table data-header-hidden><thead><tr><th></th><th valign="bottom"></th></tr></thead><tbody><tr><td>Check List - Description </td><td valign="bottom">RDT1 &#x26; RDT2 envs</td></tr><tr><td>Are all environment variables correctly set?</td><td valign="bottom">Yes</td></tr><tr><td>Is the correct version of the application deployed?</td><td valign="bottom">Yes - MOSIPID</td></tr><tr><td>Are dependencies (libraries, services, databases) properly configured?</td><td valign="bottom">Yes</td></tr><tr><td>Are all services (APIs, databases, third-party integrations) up and running?</td><td valign="bottom">Yes</td></tr><tr><td>Can the application connect to required services without errors?</td><td valign="bottom">Yes</td></tr><tr><td>Do core features work as expected in the deployed environment?</td><td valign="bottom">Yes</td></tr><tr><td>Are there any broken links, missing assets, or UI glitches?</td><td valign="bottom">No</td></tr><tr><td>Are security configurations (SSL, authentication, authorization) correctly applied?</td><td valign="bottom">Yes</td></tr><tr><td>Are sensitive endpoints protected?</td><td valign="bottom">Yes</td></tr><tr><td>Is the application responsive?</td><td valign="bottom">Yes</td></tr><tr><td>Are there any slow-loading pages or timeouts?</td><td valign="bottom">No</td></tr><tr><td>Are logs being generated and stored correctly? </td><td valign="bottom">Yes</td></tr><tr><td>Are user roles and permissions correctly applied?</td><td valign="bottom">Yes</td></tr><tr><td>Can users log in and perform expected actions?</td><td valign="bottom">Yes</td></tr><tr><td>Run a quick set of tests to validate critical flows.</td><td valign="bottom">Yes - Validated</td></tr></tbody></table>

## Main features tested   &#x20;

* Deployment&#x20;
* Basic functionality - by automation (API testrig and DSLs)

Out of scope:

Docker compose testing

* Real device testing
* Manual verification of modules
* Upgrade testing
* UI automation

## Limitations:

1. eSignet is not part of deployment.
2. Resident audit failures are because of some missing indexes which will be delivered later.
3. Rid generator configurations are tweaked and no of UIN's and VID's to be generated is reduced to 10k only to reduce start-up time, later expect a patch to fix the same.
4. Captcha will be disabled as part of testrig run.
5. Add mosip-testrig-client on top of existing configuration etc
6. Partner onboarding manual intervention is required
7. Terraform apply fails when branch protection rule is enabled
8. ErrImagePull: error due to Docker Hub's unauthenticated pull rate limit.

## Test execution statistics

### Automation test results

Below are the test metrics by performing functional testing using mock MDS, mock Auth and mock ABIS. The process followed was black box testing which based its test cases on the specifications of the software component under test. Functional test was performed in combination of individual module testing as well as integration testing. Test data were prepared in line with the user stories. Expected results were monitored by examining the user interface. The coverage includes System testing, End-To-End flows across multiple languages and configurations. The testing cycle included simulation of multiple identity schema and respective UI schema configurations.

&#x20;Here is the detailed breakdown:

**RTD1 Env 7th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 588  | 2    | 1    | 5       | 16           |
| PMS                | 509   | 481  | 0    | 1    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 315  | 0    | 1    | 78      | 20           |
| Resident           | 1142  | 581  | 535  | 14   | 0       | 12           |
| Master Data Ara    | 945   | 895  | 0    | 0    | 15      | 35           |
| Master Data eng    | 945   | 922  | 0    | 1    | 0       | 22           |
| Master Data french | 945   | 907  | 0    | 0    | 15      | 23           |
| DSL                | 204   | 159  | 0    | 6    | 12      | 27           |

&#x20;**RTD1 Env - 8th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 563  | 6    | 22   | 5       | 16           |
| PMS                | 509   | 480  | 0    | 2    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 315  | 0    | 1    | 78      | 20           |
| Resident           | 1142  | 575  | 535  | 20   | 0       | 12           |
| Master Data Ara    | 945   | 895  | 0    | 0    | 15      | 35           |
| Master Data eng    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data french | 945   | 907  | 0    | 0    | 15      | 23           |
| DSL                | 204   | 155  | 0    | 10   | 12      | 27           |

**RTD1 Env - 9th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 591  | 0    | 0    | 5       | 16           |
| PMS                | 509   | 481  | 0    | 1    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 581  | 535  | 14   | 0       | 12           |
| Master Data Ara    | 945   | 895  | 0    | 0    | 15      | 35           |
| Master Data eng    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data french | 945   | 907  | 0    | 0    | 15      | 23           |
| DSL                | 204   | 162  | 0    | 3    | 12      | 27           |

**RTD1 Env - 10th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 505  | 68   | 18   | 5       | 16           |
| PMS                | 509   | 480  | 0    | 2    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 581  | 535  | 14   | 0       | 12           |
| Master Data Ara    | 945   | 895  | 0    | 0    | 15      | 35           |
| Master Data eng    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data french | 945   | 907  | 0    | 0    | 15      | 23           |
| DSL                | 204   | 157  | 0    | 8    | 12      | 27           |

**RTD2 Env 7th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 589  | 0    | 2    | 5       | 16           |
| PMS                | 509   | 480  | 0    | 2    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 581  | 535  | 14   | 0       | 12           |
| Master Data Ara    | 945   | 922  | 0    | 1    | 0       | 22           |
| Master Data eng    | 945   | 907  | 0    | 0    | 15      | 23           |
| Master Data french | 945   | 895  | 0    | 0    | 15      | 35           |
| DSL                | 204   | 158  | 0    | 7    | 12      | 27           |

**RTD2 Env - 8th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 590  | 0    | 1    | 5       | 16           |
| PMS                | 509   | 480  | 0    | 2    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 577  | 535  | 18   | 0       | 12           |
| Master Data Ara    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data eng    | 945   | 907  | 0    | 0    | 15      | 23           |
| Master Data french | 945   | 895  | 0    | 0    | 15      | 35           |
| DSL                | 204   | 153  | 0    | 12   | 12      | 27           |

**RTD2 Env - 9th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 591  | 0    | 1    | 5       | 16           |
| PMS                | 509   | 481  | 0    | 1    | 15      | 12           |
| Pre-reg            | 509   | 481  | 0    | 1    | 15      | 12           |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 582  | 535  | 13   | 0       | 12           |
| Master Data Ara    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data eng    | 945   | 907  | 0    | 0    | 15      | 23           |
| Master Data french | 945   | 895  | 0    | 0    | 15      | 35           |
| DSL                | 204   | 151  | 0    | 14   | 12      | 27           |

**RTD2 Env - 10th Oct 2025**

| Module             | Total | Pass | Skip | Fail | Ignored | Known Issues |
| ------------------ | ----- | ---- | ---- | ---- | ------- | ------------ |
| Auth               | 612   | 591  | 0    | 0    | 5       | 16           |
| PMS                | 509   | 481  | 0    | 1    | 15      | 12           |
| Pre-reg            | 288   | 277  | 0    | 0    | 2       | 9            |
| Idrepo             | 414   | 316  | 0    | 0    | 78      | 20           |
| Resident           | 1142  | 583  | 535  | 12   | 0       | 12           |
| Master Data Ara    | 945   | 923  | 0    | 0    | 0       | 22           |
| Master Data eng    | 945   | 907  | 0    | 0    | 15      | 23           |
| Master Data french | 945   | 895  | 0    | 0    | 15      | 35           |
| DSL                | 204   | 157  | 0    | 8    | 12      | 27           |

Click[ here ](https://github.com/mosip/test-management/tree/master/Platform%20release/Rapid%20Deployment%20Testing-0.1.0-Beta)to view the detailed test report.
