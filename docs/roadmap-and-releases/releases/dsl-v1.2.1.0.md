# DSL-V1.2.1.0

#### **Release Name:** DSL Orchestrator & Packet Creator <a href="#release-name-dsl-orchestrator-and-packet-creator" id="release-name-dsl-orchestrator-and-packet-creator"></a>

**Release Version:** 1.2.1.0

**Release Type:** Minor Release

**Release Date:** 5th September, 2025

### **Overview**

We are pleased to announce the release of **DSL Orchestrator & Packet Creator v**1.2.1.0, a patch update that brings significant enhancements to the MOSIP DSL testing pipeline. This release introduces biometric variation generation, adds new test scenarios, improves thread safety in both DSL and Packet Creator components, and reduces overall execution time. It also enhances emailable reporting by including known issues and ignored test cases, resulting in more efficient, reliable, and observable test executions.

In addition, the DSL codebase has been upgraded from Java 11 to Java 21 (LTS) for improved performance and maintainability, and the deprecated Auth Demo module for biometric generation has been removed, simplifying the system.

### **Major Highlights / Key Features:**

As part of this release we have executed major enhancements in DSL scripts such as:

* Migrated to JAVA 21 to enable support to the latest technologies
* Removal of dependency of auth-demo service
* Removal of mount volume which intern helps to enhance the storage capacity of the system reduce the overall DSL execution time

Refer below table to know more enhancements included in this release in addition to the key items listed above:

<table data-header-hidden><thead><tr><th width="168"></th><th width="266"></th><th></th></tr></thead><tbody><tr><td><strong>Key JIRA</strong></td><td><strong>Feature</strong></td><td><strong>Summary</strong></td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-29153">MOSIP-29153</a></td><td><strong>Biometric data provider</strong> <strong>Utility</strong></td><td>Generated packets will now be stored in <code>/tmp</code> within the Packet Creator pod, removing external folder dependency. Biometric data will be sourced from MDS, while other profile resources will be pulled from Git during startup. The Auth Demo Service is being modularized as a library. Scenario sheets will be Git-managed and synced to the Orchestrator, with a configmap controlling which scenarios to run.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-29306">MOSIP-29306</a></td><td><strong>Authentication &#x26; Biometric Handling</strong></td><td>Implemented biometric data extraction logic for Iris, Fingerprint, and Face post successful Demo KYC and OTP authentication. Enhanced the authentication flow to prevent extraction on failure, added test coverage for success and failure scenarios, and improved logging and error handling for better traceability.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41300">MOSIP-41300</a></td><td><strong>Scenario Management &#x26; DSL Orchestration</strong></td><td>Support for multiple execution modes has been introduced in the DSL Orchestrator to improve flexibility and control. The "full" mode runs the complete test suite without requiring any config map changes. The "smoke" mode is designed to validate only positive scenarios, while the "sanity" mode defaults to running scenario 2. To run a different scenario in sanity mode, the config map must be manually updated.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35914">MOSIP-35914</a></td><td><strong>Performance Optimization &#x26; DSL Stability</strong></td><td>Optimized the DSL execution framework by increasing thread utilization and enhancing stability under parallel loads. These improvements significantly reduce overall execution time while ensuring consistent and reliable test runs.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35402">MOSIP-35402</a></td><td><strong>System Profiling &#x26; Optimization</strong></td><td>Performed code profiling using JProfiler to identify performance bottlenecks in the Packet Utility. A significant number of HTTP calls were found to be triggered during parallel execution, primarily from the health check step in the orchestrator. Optimizations were implemented to reduce redundant ping health calls during concurrent execution, resulting in improved performance and reduced overhead.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-34512">MOSIP-34512</a></td><td><strong>Scenario Coverage – UPDATE Flow</strong></td><td>Added new scenario combinations to enhance coverage of the <strong>UPDATE</strong> flow in DSL, ensuring validation of edge cases and alternate paths in packet update processing.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-39771">MOSIP-39771</a></td><td><strong>Biometric variation Utility</strong></td><td>Biometric Variation Checks were implemented to validate the system’s ability to handle slight variations in biometric data during packet processing. This ensures that the DSL can accurately simulate real-world scenarios where biometric inputs may not be identical but still belong to the same individual. The enhancement improves test coverage for biometric matching logic and helps identify false rejections or unintended matches in the system.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35765">MOSIP-35765</a></td><td><strong>Migration to Java 21</strong></td><td>The DSL codebase has been upgraded from Java 11 to Java 21 (LTS), bringing improved performance, modern language features, and long-term support for better scalability and maintainability.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-29184">MOSIP-29184</a></td><td><strong>Auth Demo Removal</strong></td><td>The authentication demo module used for generating biometric data has been removed from the DSL codebase, simplifying the system and removing unused components.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41682">MOSIP-41682</a></td><td><strong>Reporting Improvements</strong></td><td>DSL reporting has been enhanced with a dedicated Known Issues [KI] bucket. Scenarios mapped to known issues are skipped, and associated bug details are captured in the definition file, providing clearer and more traceable test reports.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-26315">MOSIP-26315</a></td><td><strong>MockSMTP Integration</strong></td><td>MockSMTP has been integrated to generate and use OTPs, enabling simulation of real-time scenarios and improving the reliability of end-to-end test flows.</td></tr></tbody></table>

### **Bug Fixes**

<table data-header-hidden><thead><tr><th width="176"></th><th></th></tr></thead><tbody><tr><td><strong>Bug ID</strong></td><td><strong>Description</strong></td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-31750"><strong>MOSIP-31750</strong></a></td><td>Fixed an intermittent issue where biometric data generation via Mock MDS failed during parallel DSL executions.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-25639"><strong>MOSIP-25639</strong></a></td><td>Removed hardcoded email ID for OTP delivery in DSL properties to avoid conflicts during concurrent OTP scenarios.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41493"><strong>MOSIP-41493</strong></a></td><td>Resolved a validation failure where newly created packets were incorrectly flagged at the Biographic Verification stage due to potential biometric match errors.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41431"><strong>MOSIP-41431</strong></a></td><td>Addressed shared state issues in <code>createContainer</code> method that caused incorrect <code>machineId</code> and <code>centerId</code> values during multi-threaded test execution.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41128"><strong>MOSIP-41128</strong></a></td><td>Enabled packet signature verification by updating the <code>packetmanager.packet.signature.disable-verification</code> property and restarting the Packet Manager, ensuring correct signature checks in DSL sanity runs.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35631"><strong>MOSIP-35631</strong></a></td><td>Fixed an issue where thread count listener updates were not being considered during orchestrator execution.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35662"><strong>MOSIP-35662</strong></a></td><td>General automation issues were resolved to improve test stability and reliability.</td></tr></tbody></table>

### **Known Issues:**

Few intermittent issues observed which are still existing and will be fixed in the upcoming releases:

<table data-header-hidden><thead><tr><th width="177"></th><th></th></tr></thead><tbody><tr><td><strong>JIRA</strong></td><td><strong>Description</strong></td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-42878">MOSIP-42878</a></td><td>Intermittent packet processing failure with "Potential Demo Match Found – referenceId not found (in ABIS)"</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-42877">MOSIP-42877</a></td><td>Intermittent packet finalization failure with "Invalid Input Parameter - verifiedAttributes"</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-42865">MOSIP-42865</a></td><td>Demographic data name mismatch during Demo Authentication in Resident Walk-in Registration flow</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-42757">MOSIP-42757</a></td><td>Digital signature verification failed</td></tr></tbody></table>

### **Repositories Released**

| **Repository**                                                                           | **Version**                                                     |
| ---------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| <h4 id="dsl-orchestrator-and-packet-creator">DSL Orchestrator &#x26; Packet Creator</h4> | [v1.2.1.0](https://github.com/mosip/mosip-automation-tests.git) |

### **Compatibility:**

| **Modules**                 | **Version**                                                                    |
| --------------------------- | ------------------------------------------------------------------------------ |
|  id-authentication          |  [v1.2.1.0](https://github.com/mosip/id-authentication/tree/v1.2.1.0)          |
|  id-repository              |  [v1.2.2.2](https://github.com/mosip/id-repository/tree/v1.2.2.2)              |
| admin-services              | [v1.2.1.2](https://github.com/mosip/admin-services)                            |
| resident-services           | [v1.2.1.2](https://github.com/mosip/resident-services/tree/v1.2.1.2)           |
| partner-management-services | [v1.2.2.2](https://github.com/mosip/partner-management-services/tree/v1.2.2.2) |
| pre-registration            | [v1.2.0.2](https://github.com/mosip/pre-registration/tree/v1.2.0.2)            |

### **Documentation:**

[DSL Automation](https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/quality-manager/test-automation/dsl-test-rig-automation)
