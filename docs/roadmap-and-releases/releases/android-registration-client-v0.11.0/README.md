# Android Registration Client v0.11.0

**Release version**: v0.11.0

**Support**: Stable Release

**Release Date**: 9th April, 2025

### **Overview** <a href="#overview" id="overview"></a>

The Android Registration Client is a tablet application designed to provide a mobile version of the existing desktop [Registration Client](https://docs.mosip.io/1.2.0/modules/registration-client).  It has been developed to ensure accessibility on all Android devices and to meet the mobility needs of countries implementing MOSIP.

Version 0.11.0 of the Android Registration Client is the beta release, covering features such as Operator Onboarding, Update Operator Onboarding, and the dashboard.

This release includes new features from the [Android Registration Client 0.11.0-beta.1](https://docs.mosip.io/1.2.0/releases/android-registration-client-0.11.0-beta.1) release and the precedent releases.

Below is the list of added features:

#### **1. Adding** [**handles** ](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/id-repository/custom-handle#what-is-a-handle)**during New registration**

When an Operator registers a resident while filling in the demographic details section, one of the mandatory fields will be marked as “handle”. This mandatory field, which is marked as the handle, has to be unique for each resident. For a detailed description of this feature, please refer to [point number 12](../../../id-lifecycle-management/identity-issuance/android-registration-client/overview/features.md).

#### **2. Authentication using** [**handles**](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/id-repository/custom-handle#what-is-a-handle)

Once the resident is registered and the handle attribute is duly entered, the resident can use that attribute to authenticate themselves.

{% hint style="info" %}
**Note**: Compatible with[ ](https://docs.mosip.io/1.2.0/releases/release-notes)[1.2.0.2 - Reg Processor & ID Repo](https://docs.mosip.io/1.2.0/releases/1.2.0.2-reg-processor-and-id-repo).
{% endhint %}

Only compatible with the below versions of Packet Manager, ID repo, and Registration processor.

#### **Repository Released** <a href="#repository-released" id="repository-released"></a>

| Repositories                | Tags Released                                                                |
| --------------------------- | ---------------------------------------------------------------------------- |
| android-registration-client | [v0.11.0](https://github.com/mosip/android-registration-client/tree/v0.11.0) |

#### **Compatible Modules** <a href="#compatible-modules" id="compatible-modules"></a>

The following table outlines the tested and certified compatibility of [1.2.0.2 - Reg Processor & ID Repo](https://docs.mosip.io/1.2.0/releases/1.2.0.2-reg-processor-and-id-repo) with other modules.

| Repositories            | Tags Released                                                     |
| ----------------------- | ----------------------------------------------------------------- |
| mosip-config            | [v1.2.3.0](https://github.com/mosip/mosip-config/tree/v1.2.3.0)   |
| id-repository           | [v1.2.2.0](https://github.com/mosip/id-repository/tree/v1.2.2.0)  |
| packet-manager          | [v1.2.0.2](https://github.com/mosip/packet-manager/tree/v1.2.0.2) |
| registration            | [v1.2.0.2](https://github.com/mosip/registration/tree/v1.2.0.2)   |
| bio-utils/biometric-api | [v1.2.0.3](https://github.com/mosip/bio-utils/tree/v1.2.0.3)      |

#### **Build and Deploy** <a href="#build-and-deploy" id="build-and-deploy"></a>

To access the build and read through the deployment instructions, please refer to the[ Developer Guide](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-developer-guide).

#### **Configurations** <a href="#configurations" id="configurations"></a>

For details related to Android Registration Client configurations, refer to the[ Configuration Guide](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-configuration).

#### **User Guide** <a href="#user-guide" id="user-guide"></a>

To learn more about the available features, processes, and user interface, please refer to the[ Android Registration User Guide](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-user-guide) for further information.

#### **Known Issues** <a href="#known-issues" id="known-issues"></a>

To view the list of known issues, refer [here](https://mosip.atlassian.net/issues/RCF-1138?jql=project%20IN%20%28%22Registration%20Client%20Flutter%22%2C%20MOSIP%29%20AND%20labels%20%3D%20ARC_release_0.11.0).

#### Documentation

[QA Report](https://docs.mosip.io/1.2.0/releases/android-registration-client-v0.11.0/test-report)
