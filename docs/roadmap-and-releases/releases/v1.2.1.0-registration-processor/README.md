# v1.2.1.0 - Registration Processor

**Release Version** : v1.2.1.0 - Registration Processor

**Release Date**: 16th April, 2025

**Overview**

We’re excited to announce the release of [Registration Processor v1.2.1.0](https://github.com/mosip/registration/tree/1.2.1.0), designed to make external system integration easier and more efficient than ever. This version introduces support for packet creation from external sources, empowering any external system to integrate seamlessly with MOSIP’s registration ecosystem.

#### What’s new?

* A new API has been added to the [registration processor module](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-processor/overview) to trigger packet processing
* Support for packet creation from external systems by leveraging the existing create packet API of the [packet manager module](https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/packet-manager).

#### **Major Highlights** <a href="#major-highlights" id="major-highlights"></a>

1. [**New API in Registration Processor Module:**](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-opencrvs-integration/approach/technical-details#id-9.-sync-and-trigger-api-workflow-manager-service)\
   Introduced a new API to trigger workflow execution when a packet is pushed from any external system, enabling seamless third-party integration.
2. [**Role-Based API Access for External Systems:**](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-opencrvs-integration/approach/technical-details#id-1.-create-client-id-role-for-the-crvs)\
   Added support for **role-based access control** for APIs exposed to external systems, ensuring secure integrations.
3. **VID & UIN-Based Updates:**\
   Enhanced flexibility by enabling support to **update individual details using VID or UIN**, improving usability across various ID scenarios.

{% hint style="info" %}
Access to third-party integrators should be limited only to these new APIs using firewall check&#x73;**.**
{% endhint %}

#### **User Stories Released** <a href="#user-stories-released" id="user-stories-released"></a>

| **Jira Issue**                                                | **Summary**                                                                              |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [MOSIP-39781](https://mosip.atlassian.net/browse/MOSIP-39781) | Infant(birth) credential generation in MOSIP when request is coming from external system |
| [MOSIP-40838](https://mosip.atlassian.net/browse/MOSIP-40838) | Deceased death flag update in MOSIP when the request is coming from an external system   |

#### **Key Known Issues** <a href="#key-known-issues" id="key-known-issues"></a>

| **Jira Issue**                                                | **Summary**                                                                    |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [MOSIP-40982](https://mosip.atlassian.net/browse/MOSIP-40982) | Credential request is not getting generated for VID during the Update UIN flow |
| [MOSIP-40984](https://mosip.atlassian.net/browse/MOSIP-40984) | Exception is thrown while updating handle field in Update UIN flow             |

Please refer to [this link](https://mosip.atlassian.net/issues/MOSIP-41091?filter=-4\&jql=labels%20%3D%20CRVS_Integration%20and%20issuetype%20%3D%20Bug) for the list of all known issues.

#### **Repositories Released** <a href="#repositories-released" id="repositories-released"></a>

| **Repository Released** | **Tags**                                                         |
| ----------------------- | ---------------------------------------------------------------- |
| **registration**        |  [v1.2.1.0](https://github.com/mosip/registration/tree/1.2.1.0)  |
| **mosip-config**        |  [v1.2.4.0](https://github.com/mosip/mosip-config/tree/v1.2.4.0) |

#### **Compatible Modules** <a href="#compatible-modules" id="compatible-modules"></a>

| **Module/Repo**             | **Compatible Version**                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------------------ |
| ID Authentication           | [1.2.1.0](https://github.com/mosip/id-authentication/tree/v1.2.1.0)                              |
| ID Repository               | [1.2.1.0](https://github.com/mosip/id-repository/tree/v1.2.1.0)                                  |
| packet-manager              | [1.2.0.2](https://github.com/mosip/packet-manager/tree/v1.2.0.2)                                 |
| key-manager                 | [1.2.1.0](https://github.com/mosip/keymanager/tree/v1.2.1.0)                                     |
| kernel - core               | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-core)                     |
| kernel-notification-service | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-notification-service)     |
| kernel-idgenerator-service  | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-idgenerator-service)      |
| kernel-auth-adaptor         | [1.2.0.1](https://github.com/mosip/mosip-openid-bridge/tree/v1.2.0.1/kernel/kernel-auth-adapter) |
| kernel-auth-service         | [1.2.0.1](https://github.com/mosip/mosip-openid-bridge/tree/v1.2.0.1/kernel/kernel-auth-service) |
| kernel-otp-manager          | [1.2.0.1](https://github.com/mosip/otp-manager/tree/v1.2.0.1/kernel/kernel-otpmanager-service)   |

### **Config Changes** <a href="#config-changes" id="config-changes"></a>

Please refer to [this](../../../id-lifecycle-management/identity-issuance/registration-processor/deploy/configurations-details.md) link to know more about the config properties added.

#### **Documentation** <a href="#documentation" id="documentation"></a>

1. [API Documentation](https://mosip.stoplight.io/docs/registration-processor/branches/main/d56c892cfa950-create-workflow-instance-for-packet-processing)
2. [Integration Guides](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-opencrvs-integration)
3. [QA Report](test-report.md)
