# Approach

MOSIP, as a modular identity platform, utilizes the [Registration Client](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-client) to collect essential information from individuals. This data is then used to generate a registration packet, which is uploaded to the [Registration Processor](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-processor/overview). Once the packet passes all required validations, a national ID is generated for the individual.

To enhance this process and support diverse entry points for national ID requests, including those from external systems such as CRVS platforms, MOSIP exposes a set of APIs through its [Packet Manager](https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/packet-manager) module. These APIs enable external systems to create and upload registration packets directly, bypassing the core registration workflow, and thus offering a streamlined integration pathway.

For every registration request, an [ID Schema](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-management/id-schema) must be defined. This schema, based on a standardized JSON structure, outlines the fields and data elements to be stored in MOSIP’s Identity Repository. It applies to all incoming requests from CRVS systems, such as birth registrations, demographic updates, or death notifications. The schema is flexible and can be customized to align with the specific needs of a country’s identity program.

## Pre-requisites

To successfully integrate with MOSIP’s registration process, external systems must fulfill certain prerequisites. These requirements ensure proper alignment, security, and functionality of the integration. Key pre-requisites include:

1.  **Create** a New Client and Assign a Role in Keycloak

    [**Keycloak**](https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/keycloak) is an identity and access management tool utilized by MOSIP. Use Keycloak, to create a new client for the external system (e.g., CRVS).

    1. Generate a unique client ID and client secret.
    2. Define a specific role (e.g., `CRVS_BIRTH_REGISTRATION_ROLE`) that reflects the intended function.
    3. Assign this role to the newly created client to enable permissioned access to relevant APIs.
2. **Obtain Access Token for API Calls**\
   Authenticate the CRVS system by calling the Keycloak token endpoint using the client credentials.
   * Retrieve a valid access token, which must be included in all subsequent API calls to MOSIP for authentication and authorization.
3. **Set Up a Registration Centre**\
   Define and register a unique Centre ID in the system.
   * This Centre ID should represent the CRVS registration location initiating the request.
   * It will be used to track and manage packet submissions by location.
4. **Register a Machine**\
   Create a unique Machine ID and corresponding key.
   * This ID will identify the hardware or system used for submitting requests to MOSIP.
   * The key ensures that only authorized machines can interact with MOSIP services.
5. **Create a Default Officer Profile**\
   Set up a default officer or operator ID who will be responsible for sending registration requests on behalf of the CRVS system.
   * This officer represents the actor initiating the transaction from the CRVS interface.
6. **Map Officer to Centre and Machine**\
   Establish mappings to link the created Officer ID with the relevant Centre ID and Machine ID.
   * This step ensures that the officer is correctly associated with a specific registration centre and the hardware device authorized to perform registrations.
7. **Generate and Use a Unique Application ID (AID)**\
   For each registration event (e.g., birth or death), the CRVS system must generate a unique **Application ID (AID).**
   * The AID should be included in the packet submitted to MOSIP.
   * It will serve as the reference ID for tracking the request and receiving response events via WebSub.

## Steps

Once the prerequisites are met, the integration between a CRVS system and MOSIP can be carried out by following these steps:

1. **Collect Vital Event Information**\
   The CRVS system should begin by capturing all necessary information related to the vital event (e.g., birth, death, marriage, or divorce). This includes personal identification details, event-specific data, and any required supporting documents.
2. **Submit Data Using Create Packet API**\
   Use MOSIP’s `Create Packet API` (provided by the Packet Manager module) to submit the collected information. This API call will initiate the creation of a packet containing the event data.
3. **Upload the Packet to MOSIP**\
   Ensure the packet is successfully uploaded to MOSIP’s registration system. The packet should include all required data elements to support identity issuance or event registration.
4. **Trigger Packet Processing**\
   Invoke the `Sync & Trigger API` from the Workflow Manager Service to start the validation and processing of the uploaded packet according to the configured workflow.
5. **Validate and Process the Packet**\
   MOSIP will subsequently perform validation checks to confirm that the packet is complete, consistent, and compliant with defined schema and business rules. Only validated packets will proceed further.
6. **Generate Identity Credentials**\
   On successful validation, MOSIP will generate the identity credentials (e.g., national ID) for the individual and/or update the required data. This ID will be linked to the vital event captured by the CRVS system.
7. **Listen for WebSub Event Publication**\
   MOSIP will publish an event to a pre-defined WebSub topic, indicating the status of the packet processing and including the generated national ID, if applicable.
8. **Subscribe and Monitor WebSub Updates**\
   Ensure the CRVS system is subscribed to the relevant WebSub topic. It should listen for and consume event notifications to receive real-time updates from MOSIP.
9. **Issue Certificates and Update Records**\
   Upon receiving the national ID and processing status, the CRVS system should proceed to issue the corresponding official certificate (e.g., birth, death, marriage). Additionally, update the national records to reflect the new identity credentials. This step ensures formal recognition and accurate documentation of the citizen's identity and vital event.

For detailed technical specifications, API documentation, and schema definitions, please refer to the subsequent section [here](technical-details.md). For details on configuration changes, please refer [here](../../../../id-lifecycle-management/identity-issuance/registration-processor/deploy/configurations-details.md).



## Other keys and certificates which are required for the integration

1. eSignet integration - If eSignet is used for authentication, refer here for detailed info on the onboarding process and the key required for onboarding to eSignet - [Integrate with eSignet](https://docs.esignet.io/esignet-authentication/test/try-it-out/integrate-with-e-signet).
2. Auth Partner Onboarding - (Certificates required Auth Partner Onboarding) - Refer to the [Partner Management Services - End User Guide](../../../../id-lifecycle-management/support-systems/partner-management-services/functional-overview/end-user-guide.md#authentication-partner-workflow).

<!-- 3. Cred partner onboarding - TBA - link - 3 - Varaniya -->






<!--

+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ### \[MOSIP-41820\] [Update the CRVS integration documentation to include the missing pre-requisites](https://mosip.atlassian.net/browse/MOSIP-41820) Created: 13/Jun/25  Updated: 28/Jul/25      |
+=================================================================================================+=================================================================================================+


## Task Details

---

### Task #1: Add Missing Pre-requisites to CRVS Integration Documentation

The [MOSIP CRVS Integration documentation](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-opencrvs-integration/approach) currently lacks information on the following pre-requisites. Please update the page to include these, along with the relevant documentation links:

| **Pre-requisite Missing**         | **Docs Link to be Added**                                                                                                                                    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Key for onboarding to eSignet     | [Integrate with eSignet](https://docs.esignet.io/test/try-it-out/integrate-with-e-signet)                                                                    |
| Auth partner onboarding - Certificates required | [Partner Management Services - End User Guide](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/functional-overview/end-user-guide) |
| Cred partner onboarding           | TBA                                                                                                                                                         |

---

### Task #2: Migrate Configuration Details Page

- **Current location:**  
   [Configuration details](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-processor/deploy/configurations-details)

- **New location:**  
   Create a new page under [Approach section of CRVS](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-opencrvs-integration/approach)

---

### Comments

> **Comment by [Rachik Sharma](https://mosip.atlassian.net/secure/ViewProfile.jspa?accountId=712020%3A46054c49-742c-483c-8c0b-9fc2069d4d73) [16/Jun/25]:**  
> Using this ticket to track the update on the CRVS related documentation.  
> cc [varaniya](https://mosip.atlassian.net/secure/ViewProfile.jspa?accountId=712020%3Aa354eedc-e17e-400c-b961-a8a3f716ad4f), [Keshav Singh](https://mosip.atlassian.net/secure/ViewProfile.jspa?accountId=712020%3A89022ae0-b73b-4f19-a5dc-8cf7cf3c67a7)

---

*Generated at Fri Aug 01 06:45:22 UTC 2025 by Keshav Singh using Jira 1001.0.0-SNAPSHOT#100287-rev:f621a79c61f778c46520a651f465e9980afc66a2.*


-->