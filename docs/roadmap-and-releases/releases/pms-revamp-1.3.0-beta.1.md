# PMS Revamp 1.3.0-beta.1

**Release Name**: Partner Management System Revamp 1.3.0-beta.1

**Release Number**: v1.3.0-beta.1

**Release Date**: 24th July, 2025

## Overview

We are excited to announce the release of **PMS Revamp v1.3.0-beta.1**, featuring a **Java 21 upgrade** and the introduction of **Certificate Expiry Notifications** within Partner Management System (PMS). The feature enables proactive monitoring and timely alerts for expiring certificates- Root CA Certificate, Intermediate CA Certificate and Partner Certificate through both PMS Portal and email, helping partners and partner admins take necessary action in advance.

## Key Features

### I. Certificate Expiry Notifications:

**a) Notification Channels:**

* **PMS Portal:** In-application alerts via the notification bell icon.
* **Email:** Sent to the registered email address of the user.

**b) Recipients and Scope:**

<table><thead><tr><th width="263.8046875">Role</th><th>Notification Type</th></tr></thead><tbody><tr><td>Partner Admins</td><td>Expiry alerts for all Root / Intermediate CA certificates (irrespective of who uploaded them). Weekly summary of partner certificates expiring in the next 7 days.</td></tr><tr><td>Partner Users</td><td>Alerts for partner certificates uploaded by them or associated MOSIP-signed certificates.</td></tr></tbody></table>

**c) Notification Schedule:** **For Individual Certificates (Root CA / Intermediate CA / Partner Certificate):**

* 30 days before expiry
* 15 days before expiry
* Daily reminders from 10 days prior until expiry date

**d) Weekly Summary Notifications (Partner Admins only):**

* Sent every 7 days
* Lists all partner certificates expiring within the next 7 days

**e) Language Handling:**

<table><thead><tr><th width="263.8046875">Channel</th><th>Language Used</th></tr></thead><tbody><tr><td>Email</td><td>Based on the user's registration language</td></tr><tr><td>PMS Portal</td><td>Based on the language selected at login, overriding registration preferences</td></tr></tbody></table>

**f) Notification Retention Policy:**

* Notifications are retained for 60 days on the PMS portal.
* Notifications older than 60 days are automatically deleted.

### II. Audit Logs for Certificate Expiry Notifications

Audit logging has been implemented for all certificate expiry notifications (Root CA, Intermediate CA, Partner Certificates, and Weekly Summary) sent via PMS portal and email. Success and failure events are now recorded with unique event IDs in the audit.app\_audit\_log table, enhancing traceability and monitoring.

### Browser Support

* Complete support on Chrome, Firefox, Edge and Safari ensures a seamless user experience across all these popular browsers.

### Language Support

* The system offers multilingual support, with resource bundles available in three languages: English, Arabic, and French. Additional languages can be easily integrated by following the guidelines provided in the ['New Language Support'](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/develop/new-language-support) documentation.

### Compatibility

* Responsive UI design for laptop/desktop views, optimized for standard browser sizes (laptop/desktop/tablet/larger screens).

For a comprehensive and detailed description of all the features, refer to [Feature Documentation](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/functional-overview/auth-partner/features).

## User Stories

<table><thead><tr><th width="222.37713623046875">Feature</th><th>Sub-Feature</th><th>Jira ID</th></tr></thead><tbody><tr><td>Root CA Certificate Expiration</td><td>Notification displayed on notification panel in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39304">MOSIP-39304</a></td></tr><tr><td></td><td>Notification displayed in View all notification page in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40016">MOSIP-40016</a></td></tr><tr><td></td><td>Count of Root CA Certificate expiring is displayed as a dashboard badge</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40027">MOSIP-40027</a></td></tr><tr><td></td><td>Email notification</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39314">MOSIP-39314</a></td></tr><tr><td>Intermediate CA Certificate Expiration</td><td>Notification displayed on notification panel in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40037">MOSIP-40037</a></td></tr><tr><td></td><td>Notification displayed in View all notification page in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40057">MOSIP-40057</a></td></tr><tr><td></td><td>Count of Intermediate CA Certificate expiring is displayed as a dashboard badge</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40067">MOSIP-40067</a></td></tr><tr><td></td><td>Email notification</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40047">MOSIP-40047</a></td></tr><tr><td>Weekly Summary of Partner Certificate</td><td>Notification displayed on notification panel in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39400">MOSIP-39400</a></td></tr><tr><td></td><td>Notification displayed in View all notification page in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39844">MOSIP-39844</a></td></tr><tr><td></td><td>Email notification</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39419">MOSIP-39419</a></td></tr><tr><td></td><td>View list of partner IDs whose partner certificates are expiring in a given week via email</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-41058">MOSIP-41058</a></td></tr><tr><td></td><td>View list of partner IDs whose partner certificates are expiring in a given week on PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40639">MOSIP-40639</a></td></tr><tr><td>Partner Certificate Expiration</td><td>Notification displayed on notification panel in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39325">MOSIP-39325</a></td></tr><tr><td></td><td>Notification displayed in View all notification page in PMS portal</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40089">MOSIP-40089</a></td></tr><tr><td></td><td>Count of Partner Certificate expiring is displayed as a dashboard badge</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40079">MOSIP-40079</a></td></tr><tr><td></td><td>Email notification</td><td><a href="https://mosip.atlassian.net/browse/MOSIP-39335">MOSIP-39335</a></td></tr><tr><td>Audit Logs for notifications</td><td></td><td><a href="https://mosip.atlassian.net/browse/MOSIP-40807">MOSIP-40807</a></td></tr></tbody></table>

List of all user stories pertaining to this release are available [here](https://mosip.atlassian.net/issues/MOSIP-39314?filter=11933\&jql=project%20%3D%20MOSIP%20AND%20%22Epic%20Link%22%20%3D%20MOSIP-32075%20and%20status%20not%20in%20%28Canceled%29%20and%20issuetype%3D%20Story%20and%20%22Release%20Number%5BLabels%5D%22%20in%20%28PMS_Release_1.3.0-beta.1%29%20ORDER%20BY%20status%20ASC).

## **Known Issues**

<table><thead><tr><th width="176.47869873046875">JIRA ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-34109">MOSIP-34109</a></td><td>Length validation of OIDC Client name is not functioning as expected for lengthy names within the given range. This has a dependency with eSignet, where the column size needs to be increased.Its suggested that meaningful and reasonable length be utilised for OIDC Client name.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-39623">MOSIP-39623</a></td><td>Unable to select policy group in tablet and mac devices.This issue is found when more than 3000 Policy Groups are getting loaded into the Dropdown for selection. As a workaround, suggested to keep the create policy groups less than 3000.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-42374">MOSIP-42374</a></td><td>The UI Automation report for PMS Revamp is not stable and shows many failures. This will be fixed in upcoming release.</td></tr><tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-35343">MOSIP-35343</a></td><td>Error message is displayed when same Make and Model is entered for two different SBI versions.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-38958">MOSIP-38958</a></td><td>Able to Approve the Expired SBI which is in pending for approval status</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-39893">MOSIP-39893</a></td><td>(IDA Issue) Authentication is still Active from IDA even after deactivating the API key from the Partner Portal in PMS</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-38864">MOSIP-38864</a></td><td>(Platform Issue) Even after being deactivated by the Partner Admin, the Partner can still access and use previously created OIDC client, API key and trust Validation continues to work for the given partner.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-38383">MOSIP-38383</a></td><td>Still able to approve/reject the policy even after respective authentication partner is deactivated.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-34427">MOSIP-34427</a></td><td>On deactivating an API key from one browser , the status still remains 'Activated' on viewing the same API Key details in another browser.This is occurring due to caching. Hence user is expected to reload the tabular page of API Keys to see the latest status in View API Key screen.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-38890">MOSIP-38890</a></td><td>Partner domain dropdown items (AUTH/ DEVICE/ FTM) are in English and do not support multi-language.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41261">MOSIP-41261</a></td><td>The partner is still able to access the PMS portal even after the MOSIP-signed certificate has expired. Also Partner is able to create Policies, OIDC Client and API Key.</td></tr></tbody></table>

## **Repositories Released**

| Repository Released         | Version       |
| --------------------------- | ------------- |
| partner-management-services | [v1.3.0-beta.1](https://github.com/mosip/partner-management-services/tree/v1.3.0-beta.1) |
| partner-management-portal   | [v1.3.0-beta.1](https://github.com/mosip/partner-management-portal/tree/v1.3.0-beta.1) |
| mosip-openid-bridge         | [v1.3.0-beta.2](https://github.com/mosip/mosip-openid-bridge/releases/tag/v1.3.0-beta.2) |
| mosip-data                  | [v1.3.0-beta.2](https://github.com/mosip/mosip-data/tree/v1.3.0-beta.2) |

## Compatible Modules

The following table outlines the tested and certified compatibility of PMS 1.3.0-beta.1 with other backward compatible modules.

{% hint style="warning" %}
**Note**: We require KeyManager v1.3.0-beta.3 to ensure that notifications are generated for Root and Intermediate Certificate expiries, as the updated version includes the new endpoint used for this functionality. However, if deployed with an earlier KeyManager version, all other features will continue to work—except the Root and Intermediate Certificate expiry notifications.
{% endhint %}

| Module/ Repo          | Version                                                                 |
| --------------------- | ----------------------------------------------------------------------- |
| **Key Manager**       | [v1.3.0-beta.3](https://github.com/mosip/keymanager/tree/v1.3.0-beta.3) |
| **artifactory**       | [v1.2.0.2](https://github.com/mosip/artifactory-ref-impl/tree/v1.2.0.2) |
| **IDA**               | [v1.2.1.0](https://github.com/mosip/id-authentication/tree/v1.2.1.0)    |
| **eSignet**           | [v1.4.1](https://github.com/mosip/esignet/tree/v1.4.1)                  |
| **Reg Proc**          | [v1.2.0.2](https://github.com/mosip/registration/tree/v1.2.0.2)         |
| **Notifier (Kernel)** | [v1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel)       |
| **Audit manager**     | [v1.2.0.1](https://github.com/mosip/audit-manager/tree/v1.2.0.1)        |
| **ID Repo**           | [v1.2.2.0](https://github.com/mosip/id-repository/tree/v1.2.2.0)        |
| **datashare**         | [v1.2.0.1](https://github.com/mosip/durian/tree/v1.2.0.1)               |
| **Keycloak**          | [v1.2.0.1](https://github.com/mosip/keycloak/tree/v1.2.0.1)             |
| **config-server**     | [v1.1.2](https://github.com/mosip/mosip-config/tree/v1.1.2)             |
| **Websub**            | [v1.2.0.1](https://github.com/mosip/websub/tree/v1.2.0.1)               |

## Documentation

* [Feature Documentation](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/overview/features)
* [End User Guide](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/functional-overview/pms-notification)
* [Services Deployment Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/build-and-development-guide)
* [UI Developer’s Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/ui-developers-guide)
* [Backend Developer’s Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/backend-developers-guide)
* [API Documentation](https://mosip.stoplight.io/docs/partner-management-portal-revamp)
* [Test Report](https://github.com/mosip/test-management/tree/master/PMS%20Revamp/1.3.0-beta.1)
