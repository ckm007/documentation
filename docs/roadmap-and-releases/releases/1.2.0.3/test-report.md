# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of &#x20;

●      Functionality &#x20;

●      Deployability &#x20;

●      Configurability &#x20;

●      Customizability

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software is also assessed. This ensures readiness of software for use in multiple countries. Since MOSIP is an “API First” product platform, Verification scope required comprehensive automation testing for all the MOSIP APIs. An automation Test Rig is created for the same.&#x20;

## Test Approach

Persona based approach has been adopted to perform the IV\&V, by simulating test scenarios that resemble a real-time implementation.&#x20;

&#x20;A Persona is a fictional character/user profile created to represent a user type that might use a product/or a service in a similar way. Persona based testing is a software testing technique that puts software testers in the customer's shoes, assesses their needs from the software and thereby determines use cases/scenarios that the customers will execute. The persona needs may be addressed through any of the following:

●      Functionality &#x20;

●      Deployability &#x20;

●      Configurability &#x20;

●      Customizability

&#x20;

The verification methods may differ based on how the need was addressed.&#x20;

&#x20;For regression check, “MOSIP Test Rig” - an automation testing suite - which is indigenously designed and developed for supporting persona based testing. MOSIP Test Rig covers the end to end test execution and reporting. The end to end functional test scenarios are written starting from pre-registration, to creation of packet in registration center, processing the packet through the registration processor, generating UIN and authenticating identity using IDA through various permutation and combinations of cases being covered. MOSIP Test Rig will be an open source artifact which can also be enhanced and used by countries to validate the SI deliveries before going live. Persona classes include both negative and positive personas. Negative persona classes include users like Bribed Registration Office, Malicious Insider etc. The needs of positive persona classes must be met, whereas the needs of negative persona classes must be effectively restricted by the software.

## Verified configuration

Verification is performed on various configurations as mentioned below :

▪       Default configuration - with 3 Languages (English/Arabic/French)

## Main features tested:

Performed sanity testing and bug verification across the following modules: PreReg, Admin, RegClient, RegProc, IDRepo, IDA, and Resident.

## Test execution statistics

## Automation test results

Below are the test metrics by performing functional testing using mock MDS, mock Auth and mock ABIS. The process followed was black box testing which based its test cases on the specifications of the software component under test. Functional test was performed in combination of individual module testing as well as integration testing. Test data were prepared inline with the user stories. Expected results were monitored by examining the user interface. The coverage includes System testing, End-To-End flows across multiple languages and configurations. The testing cycle included simulation of multiple identity schema and respective UI schema configurations.

Here is the detailed breakdown:

| Module            | Total | Passed | Failed | Skipped | Ignored | Known issues |
| ----------------- | ----- | ------ | ------ | ------- | ------- | ------------ |
| PreReg            | 288   | 277    | 0      | 0       | 2       | 9            |
| Master Data (Eng) | 945   | 923    | 0      | 0       | 0       | 22           |
| Master Data (Ara) | 945   | 896    | 0      | 0       | 15      | 34           |
| Master Data (Fra) | 945   | 907    | 0      | 0       | 15      | 23           |
| IDRepo            | 414   | 316    | 0      | 0       | 78      | 20           |
| IDA               | 612   | 591    | 0      | 0       | 5       | 16           |
| Resident          | 1142  | 1130   | 0      | 0       | 0       | 12           |

### DSL - End to end scenarios results:

<table data-header-hidden><thead><tr><th valign="bottom"></th><th></th></tr></thead><tbody><tr><td valign="bottom">End to end scenarios</td><td></td></tr><tr><td valign="bottom">Total</td><td>204</td></tr><tr><td valign="bottom">Pass</td><td>165</td></tr><tr><td valign="bottom">Fail</td><td>0</td></tr><tr><td valign="bottom">Skipped</td><td>0</td></tr><tr><td valign="bottom">Ignored</td><td>12</td></tr><tr><td valign="bottom">Known issues</td><td>27</td></tr></tbody></table>

&#x20;Click [here](https://github.com/mosip/test-management/tree/master/Platform%20release/1.2.0.3-Performance-fixes%20) to refer the full test report
