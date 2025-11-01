# Partner Management System Revamp 1.2.2.2 (Patch)

**Release Name**: Partner Management System Revamp 1.2.2.2 (Patch)

**Release Number**: v1.2.2.2

**Release Date**: 5th July 2025

### Overview

We are pleased to announce the release of **PMS Revamp v1.2.2.2**, a patch focused on resolving key issues related to backward compatibility with earlier versions of the MOSIP Platform.

This release builds upon PMS v1.2.2.0 and **extends the enhancements delivered in v1.2.2.1**, introducing further compatibility fixes — particularly for the following KeyManager versions: v1.1.5, v1.2.0.1, v1.2.1.0, v1.3.0-beta.1 and 1.3.0-beta.2.

These updates enhance platform interoperability and ensure smoother integration across supported MOSIP modules.

### Key Manager configurations to turn PMS backward compatible

New configurations are now available for backward compatibility with different versions of MOSIP platform. Set these configurations as below:

**For 1.1.5.5-P3 Key Manager**:

```
pmp.partner.certificaticate.upload.rest.uri=${mosip.kernel.keymanager.url}/v1/keymanager/v2/uploadPartnerCertificate
```

```
mosip.pms.ca.signed.partner.certificate.available=false
mosip.pms.oidc.client.available=false
mosip.pms.root.and.intermediate.certificates.available=false
```

**For 1.2.0.1 Key Manager**:

```
mosip.pms.ca.signed.partner.certificate.available=false
mosip.pms.oidc.client.available=true
mosip.pms.root.and.intermediate.certificates.available=false
```

**For 1.2.1.0 Key Manager**:

```
mosip.pms.ca.signed.partner.certificate.available=true
mosip.pms.oidc.client.available=true
mosip.pms.root.and.intermediate.certificates.available=false
```

**For 1.3.0-beta.1 Key Manager**:

```
mosip.pms.ca.signed.partner.certificate.available=false
mosip.pms.oidc.client.available=true
mosip.pms.root.and.intermediate.certificates.available=false
```

**For 1.3.0-beta.2 Key Manager**:

```
mosip.pms.ca.signed.partner.certificate.available=true
mosip.pms.oidc.client.available=true
mosip.pms.root.and.intermediate.certificates.available=true
```

### **Bug Fixes**

<table><thead><tr><th width="263.8046875">Bug ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41629">MOSIP-41629</a></td><td>For non-valid PMS partners, when required attributes are missing in Keycloak (but roles are present), PMS portal returns a <code>User ID not found</code> error on login.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41628">MOSIP-41628</a></td><td>For valid PMS partners with missing Keycloak attributes in Keycloak (but required role mappings present), the PMS dashboard does not display all expected cards and the user profile shows incomplete details.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41594">MOSIP-41594</a></td><td>Compatibility configurations have been enabled ( <code>true</code> by default) in the <code>release-1.2.2.x</code> GitHub branch. Country-specific deployments can disable these settings as needed. The README has also been updated with relevant configuration details.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41592">MOSIP-41592</a></td><td>In screens where a feature is not supported, the info note now displays the feature name in <em>italics</em> for better visual distinction.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41445">MOSIP-41445</a></td><td>Automation failures observed in API test rigs caused by issues with Key Manager, OIDC authentication, and partner certificate retrieval.</td></tr></tbody></table>


### **Known Issues**

<table><thead><tr><th width="176.47869873046875">JIRA ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41707">MOSIP-41707</a></td><td>The '<strong>Account Setup Required</strong>' popup does not currently support RTL layout for Arabic language users. This issue will be addressed in the develop branch and is planned for delivery in an upcoming release.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41719">MOSIP-41719</a></td><td>When attributes are missing in Keycloak, the user profile currently displays '<strong>Not available</strong>' without any actionable next steps. A design enhancement is under consideration to better handle scenarios involving missing attributes.</td></tr></tbody></table>

### **Repositories Released**

| Repository Released         | Version  |
| --------------------------- | -------- |
| partner-management-services | [v1.2.2.2](https://github.com/mosip/partner-management-services/tree/v1.2.2.2) |
| partner-management-portal   | [v1.2.2.2](https://github.com/mosip/partner-management-portal/tree/v1.2.2.2) |

### Compatible Modules

The following table outlines the tested and certified compatibility of PMS 1.2.2.2 with other backward compatible modules.

| Module/ Repo          | 1.1.5.x versions                                                             | 1.2.2.0 versions                                                        |
| --------------------- | ---------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Key Manager**       | [v1.1.5.5-P3](https://github.com/mosip/keymanager/tree/v1.1.5.5-P3)             | [v1.3.0-beta.2](https://github.com/mosip/keymanager/tree/v1.3.0-beta.2) |
| **auth manager**      | [1.1.5.5-P2](https://github.com/mosip/mosip-openid-bridge/tree/v1.1.5.5-P2)  | [v1.2.0.1](https://github.com/mosip/mosip-openid-bridge/tree/v1.2.0.1)  |
| **artifactory**       | [1.1.5.5-P2](https://github.com/mosip/artifactory-ref-impl/tree/v1.1.5.5-P2) | [v1.2.0.2](https://github.com/mosip/artifactory-ref-impl/tree/v1.2.0.2) |
| **IDA**               | [1.2.0.1-B4](https://github.com/mosip/id-authentication/tree/v1.2.0.1-B4)    | [v1.2.1.0](https://github.com/mosip/id-authentication/tree/v1.2.1.0)    |
| **eSignet**           | NA                                                                           | [v1.4.1](https://github.com/mosip/esignet/tree/v1.4.1)                  |
| **Reg Proc**          | [v1.1.5.5-P5](https://github.com/mosip/registration/tree/v1.1.5.5-P5)        | [v1.2.0.1](https://github.com/mosip/registration/tree/v1.2.0.1)         |
| **Notifier (Kernel)** | [1.1.5.3](https://github.com/mosip/commons/tree/v1.1.5.3/kernel)             | [v1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel)       |
| **Audit manager**     | [1.1.5.5](https://github.com/mosip/audit-manager/tree/1.1.5.5)               | [v1.2.0.1](https://github.com/mosip/audit-manager/tree/v1.2.0.1)        |
| **ID Repo**           | [v1.1.5.5-P2](https://github.com/mosip/id-repository/tree/v1.1.5.5-P2)       | [v1.2.1.0](https://github.com/mosip/id-repository/tree/v1.2.1.0)        |
| **datashare**         | [1.1.5.3-P2](https://github.com/mosip/durian/tree/v1.1.5.3-P2)               | [v1.2.0.1](https://github.com/mosip/durian/tree/v1.2.0.1)               |
| **Keycloak**          | [mosipid/mosip-keycloak:9.0.0](https://github.com/mosip/keycloak)            | [v1.2.0.1](https://github.com/mosip/keycloak/tree/v1.2.0.1)             |
| **config-server**     | [1.1.0](https://github.com/mosip/mosip-config/tree/v1.1.0)                   | [v1.1.2](https://github.com/mosip/mosip-config/tree/v1.1.2)             |
| **Websub**            | NA                                                                           | [v1.2.0.1](https://github.com/mosip/websub/tree/v1.2.0.1)   

### Documentation

* [Feature Documentation](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/functional-overview/auth-partner/features)
* [End User Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/functional-overview)
* [Services Deployment Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/build-and-development-guide)
* [UI Developer’s Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/ui-developers-guide)
* [Backend Developer’s Guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/pms-revamp/technical-overview/backend-developers-guide)
* [API Documentation](https://mosip.stoplight.io/docs/partner-management-portal-revamp)
* [Test Report](https://github.com/mosip/test-management/tree/master/PMS%20Revamp/1.2.2.2)
