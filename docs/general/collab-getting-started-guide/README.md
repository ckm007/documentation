---
icon: book
---

# Collab Environment Guides

Hello Partner!

Ready to delve deeper into the world of MOSIP? This expanded guide sheds light on the functionalities and benefits of each service and module available in the Collab environment. Explore, test, and build with confidence!

Let us dive deeper into MOSIP Collab: Modules in detail.

## Introduction <a href="#introduction" id="introduction"></a>

The Collab environment in [MOSIP](https://docs.mosip.io/1.2.0) offers a collaborative platform for partners and stakeholders to thoroughly test, collaborate, and validate their integrations, modules, and services. This environment is exclusively designed for partners and contributors involved in developing solutions on the MOSIP platform enabling them to perform comprehensive testing and seamless integration of their solutions with the latest platform code. To gain access to this environment, please click [here](https://collab.mosip.net/).

### Purpose <a href="#purpose" id="purpose"></a>

This guide has been created to offer a step-by-step overview of the fundamental procedures that as a partner, you must adhere to, to begin working with the Collab environment. By carefully following the setup and configuration process, which is outlined module by module within this guide, you will be able to effortlessly access the Collab environment, establish the necessary modules or services, and effectively demonstrate the application features as relevant.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before starting with the Collab environment, please ensure you have the following prerequisites in place:

* **UIN Credential (Unique Identification Number)** Issuance of [UIN](https://docs.mosip.io/1.2.0/id-lifecycle-management/identifiers#uin) as a demo credential will allow you to explore MOSIP's capabilities and experience seamless identity management firsthand.
  * Now you can self generate your own UIN Credential using the [Collab environment](https://collab.mosip.net/).
  * Click on the **Get UIN** button located at the top-right corner of the page. This will open the [Self Registration Form](https://self-register.collab.mosip.net/), You need to duly fill the self registration form. \
    Alternatively, you can also request UIN by opening this '[Form](https://docs.google.com/forms/d/e/1FAIpQLSc2I0CQqlYRIrEmcJ3J3tKlYOVNcYNj88YZe4MMwU2RZTrjOA/viewform)' and providing the required  details, The difference with this form is that the MOSIP team will evaluate your request and respond with a mail which will carry your UIN, this may take dew days.
  * On successful registration the UIN is sent to you over the email you used for registration, For more details you follow the [Generating Demo Credentials Guide](https://docs.mosip.io/1.2.0/general/collab-getting-started-guide/generating-demo-credentials).
* **MOCK SMTP** A mock SMTP server is a simulated email server used for testing and development purposes. In MOSIP, it is installed as part of the default installation and is utilized to mimic the behavior of a real SMTP server, allowing developers to test email functionality and interactions without sending actual emails. To set up a mock SMTP server for the message gateway during V3 installation, click.

Let’s Get Started!

**Step 1: Access the Collab Environment**

* Open your web browser and navigate to the Collab environment URL: [MOSIP Collab](https://collab.mosip.net/).
* In the Collab environment, click on the specific module/service that you want to access as a contributor.

**Step 2: Follow the module-specific guide to integrate with/ test the preferred application**

In MOSIP's Collab environment, the following components and services are available.

* Navigate to the [MOSIP Collab Portal](https://collab.mosip.net/).
* Select the module you wish to test for example and follow the step-by-step instructions for integrating and testing with your preferred application.

### Modules <a href="#modules" id="modules"></a>

#### Pre-registration - Optimize the Journey <a href="#pre-registration-optimize-the-journey" id="pre-registration-optimize-the-journey"></a>

* Pre-registration is a MOSIP module that allows residents to pre-register themselves by providing demographic data, uploading documents, and booking appointments before official registration at the registration center, thereby optimizing enrollment.
* To learn more about pre-registration click [here](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/pre-registration/overview).
* For the end-to-end process on how to set up the Pre-registration in the Collab environment, click on the [Pre-registration Setup Guide](https://docs.mosip.io/1.2.0/collab-getting-started-guide/collab-pre-registration-guide).
* For details on how to use the application, refer to our [end user guide](https://docs.mosip.io/1.2.0/modules/pre-registration/pre-registration-user-guide).

#### Registration Client - Efficient Enrollments <a href="#registration-client-efficient-enrollments" id="registration-client-efficient-enrollments"></a>

* Registering residents quickly and accurately is crucial. The Registration Client application in MOSIP enables agents to efficiently register residents by capturing their demographic and biometric data and managing tasks like onboarding, data synchronization, software upgrades, and packet management. Refer here to learn more about the [Registration client](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-client/overview).
* To know more about the installation and prerequisites for the same, click [here](https://docs.mosip.io/1.2.0/modules/registration-client/registration-client-installation-guide).
* For the end-to-end process on how to set up the Registration client in the Collab environment, click [here](https://docs.mosip.io/1.2.0/collab-getting-started-guide/collab-reg-client-setup-guide).
* For details on how to use the application, refer to our [user guide](https://docs.mosip.io/1.2.0/modules/registration-client/registration-client-user-guide).

#### Resident Portal - Empowering Users <a href="#resident-portal-empowering-users" id="resident-portal-empowering-users"></a>

* Imagine residents managing their identities with ease and convenience! Residents take center stage with the Resident Services module. This reference self-service portal empowers them to manage their Unique Identification Number (UIN), check their registration status, download documents, and access other essential services. Refer here to learn more about the Registration services.
* This web-based UI application provides residents of a country the services related to managing their Unique Identification Number (UIN).
* To learn more about Resident Services, click [here](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-management/resident-services/overview).
* For the end-to-end process of how to run Resident Services in our Collab env, click [here](https://docs.mosip.io/1.2.0/collab-getting-started-guide/collab-resident-portal-guide).
* For details on how to use the application, refer to the [end user guide](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-management/resident-services/test/resident-portal-user-guide).

#### Admin Portal - Master Data Management <a href="#admin-portal-master-data-management" id="admin-portal-master-data-management"></a>

* Behind the scenes, the Admin Portal empowers administrative personnel. This web-based platform helps manage master data, configure system settings, track user activity, and perform crucial operational tasks. Maintaining data accuracy, and optimizing platform efficiency necessitates a robust administrative infrastructure, and the Admin Portal fulfills this role effectively.
* To learn more about the Admin Portal, click [here](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/administration#overview).
* Admin portal access in Collab is limited, contact the [community forum](https://community.mosip.io/) for specific module needs.
* For details on how to use the application, refer to our [end user guide](https://docs.mosip.io/1.2.0/modules/administration/admin-portal-user-guide).

#### Partner Management System - Trust Made Easy <a href="#partner-management-system-trust-made-easy" id="partner-management-system-trust-made-easy"></a>

* MOSIP thrives on collaboration, and the Partner Management System facilitates it. This module handles partner onboarding and manages policy configurations, between partners and the platform. Building solutions together has never been easier! To learn more please refer [here](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/overview).
* MOSIP's Partner Management Services (PMS) module streamlines partner onboarding, policy management, and data sharing. It comprises Partner Management and Policy Management Services, providing essential support for effective collaboration within MOSIP.
* For the end-to-end process of how to run Partner Management in our collab environment, click [here](https://docs.mosip.io/1.2.0/collab-getting-started-guide/collab-pmp-guide).
* For details on how to use the application, refer to our [end user guide](https://docs.mosip.io/1.2.0/modules/partner-management-services/partner-management-portal).

#### Inji - Your Mobile Identity Wallet <a href="#inji-your-mobile-identity-wallet" id="inji-your-mobile-identity-wallet"></a>

* To fully explore the Inji Credentialing Stack and its features in the Collab environment, please refer to the [Inji Credentialing Stack Setup Guide](https://docs.mosip.io/inji/readme/try-it-out) provided within the Inji documentation.
* Please refer to the [Inji Credentialing Stack](https://docs.mosip.io/inji/readme/try-it-out) in our sandbox Collab environment to learn about setting up and configuring all modules. By following the steps outlined in each guide for different modules of Inji Stack, you will be able to smoothly utilize the individual features and functionalities of each module of Inji Stack. Whether you're a Developer, System Integrator, or an enthusiast eager to dive into the world of digital identity and verifiable credentials, these guides will provide you with the necessary information to get started with Inji Stack in our [Collab](https://collab.mosip.net/) environment.
* For the end-to-end process of how to set up the Inji Credentialing Stack in our Collab environment, click[ here](https://docs.inji.io/readme/try-it-out).
* **Inji Wallet** - To fully explore the [Inji Wallet](https://docs.mosip.io/inji/inji-mobile-wallet/overview) and its features in the Collab environment, please refer to the Inji Wallet [Try it out](https://docs.mosip.io/inji/inji-mobile-wallet/sandbox-details/inji-setup-guide) section provided within the Inji documentation.
* **Inji Web** - To fully explore the [Inji Web](https://docs.mosip.io/inji/inji-web/overview) and its features in the Collab environment, please refer to the Inji Web [Try it out](https://docs.mosip.io/inji/inji-web/try-it-out/inji-web-setup-guide) section provided within the Inji documentation.
* **Inji Verify** - To fully explore [Inji Verify](https://docs.mosip.io/inji/inji-verify/overview) and its features in the Collab environment, we kindly request you to refer to the Inji Verify [Try it out](https://docs.inji.io/inji-verify/releases-1/inji-verify-collab-guide) section provided within the Inji documentation.

#### eSignet - Simple and Secure Online Authentication <a href="#esignet-simple-and-secure-online-authentication" id="esignet-simple-and-secure-online-authentication"></a>

* Signing in online shouldn't be a hassle now. eSignet simplifies online authentication by allowing users to identify themselves and share profile information with just a few clicks. Secure and user-friendly, eSignet streamlines online interactions and protects user privacy.
* To learn more about eSignet, click [here](https://docs.esignet.io/overview).
* For the end-to-end process of how to run eSignet in our Collab environment, click [here](https://docs.mosip.io/1.2.0/collab-getting-started-guide/collab-esignet-setup-guide).
* For details on how to use the application, refer to our [end user guide](https://docs.esignet.io/esignet-end-user-guide).

**Step 3: Testing and Validation**

Once the setup and configuration are completed, you should proceed with testing and validation activities to ensure the smooth functioning of the modules or services. The testing process may include:

* Performing end-to-end tests for the integrated modules or services.
* Validating data exchange and interoperability between different components.
* Verifying the compliance of the modules or services with the specified requirements and standards.

**Step 4: Get in touch: Report issues and seek support**

We’re here to help! If you encounter any issues during the testing or integration process, please reach out to us through the support system below or navigate to the [Community](http://community.mosip.io/).

Continuous communication and collaboration between the MOSIP team and the community will aid successful integrations and help resolve any issues within the Collab environment.

_We thank you for your ongoing support and look forward to building MOSIP together!_
