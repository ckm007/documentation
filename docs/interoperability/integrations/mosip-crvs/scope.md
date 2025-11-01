# Scope

#### **Overview** <a href="#overview" id="overview"></a>

This section defines the scope of integration between Civil Registration and Vital Statistics (CRVS) systems and Modular Open-Source Identity Platform (MOSIP). The integration supports a comprehensive set of use cases, including birth and death registrations, demographic updates, and other vital events such as marriage and divorce.

#### **Use Cases Supported Through CRVS-MOSIP Integration** <a href="#use-cases-supported-through-crvs-mosip-integration" id="use-cases-supported-through-crvs-mosip-integration"></a>

This integration currently supports the following use cases:

1. [Birth registration](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-crvs-integration/scope#id-1.-birth-registration)
   1. [Birth registration is initiated by the CRVS system](scope.md#id-1.1-birth-registration-initiated-by-crvs-system)
   2. [Duplicate and/or repeated infant birth registration requests initiated by the CRVS system](scope.md#id-1.2-duplicate-and-or-repeated-infant-birth-registration-requests-initiated-by-crvs)
   3. [Failure handling](scope.md#id-1.3-failure-handling)
2. [Death registration ](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-crvs-integration/scope#id-2.-death-registration)
   1. [New death registration initiated by CRVS](scope.md#id-2.1-new-death-registration-initiated-by-crvs)
   2. [Duplicate and/or repeated requests for death registration](scope.md#id-2.2-duplicate-and-or-repeated-requests-for-death-registration)
   3. [Failure handling](scope.md#id-2.3-failure-handling)
3. [Demographic data update](https://docs.mosip.io/1.2.0/interoperability/integrations/mosip-crvs-integration/scope#id-3.-demographic-data-update-initiated-by-crvs-system)&#x20;
   1. [Infant demo data update request initiated by CRVS](scope.md#id-3.1-infant-demo-data-update-request-initiated-by-crvs)
   2. [Duplicate and/or repeated infant demo data update requests](scope.md#id-3.2-duplicate-and-or-repeated-infant-demo-data-update-requests)
   3. [Adult demo data update request initiated by CRVS](scope.md#id-3.3-adult-demo-data-update-request-initiated-by-crvs-system)

{% hint style="info" %}
**Note**: These are the currently supported scenarios. Additional use cases will be introduced as the integration evolves and expands based on country-specific requirements and feedback.
{% endhint %}

#### **1. Birth Registration:** <a href="#id-1.-birth-registration" id="id-1.-birth-registration"></a>

#### **1.1 Birth Registration Initiated by CRVS System**

When a birth (of an infant) is registered in the CRVS system, the CRVS system shares the demographic data with MOSIP, which then creates an ID for the newborn. This ID can be issued as a credential, granting immediate access to services requiring identity verification, like healthcare and education.

#### **Approach**

For newborns who do not yet possess a national ID, the CRVS system can initiate a national ID registration request on their behalf. This request is initiated by a guardian, parent, or another authorized individual, referred to in MOSIP as the **“Introducer”** or an **“Informant”** in the CRVS system. The introducer must already be registered in MOSIP and have a valid national ID, which is used for authentication through **eSignet** to ensure the legitimacy of the registration.

To further enhance security and data accuracy, the CRVS system utilizes MOSIP’s authentication mechanisms to verify the identities of parents or informants during the birth registration process. This helps prevent fraudulent registrations and strengthens overall data quality and system integrity.

Once the request is submitted, the CRVS system shares the birth data with MOSIP. MOSIP then processes the birth registration request based on the flow defined below, and generates a unique national ID for the newborn. This process closely mirrors the standard new registration flow in MOSIP, with the key difference being that the request is initiated by CRVS rather than through the Registration Client.

{% hint style="info" %}
Note: MOSIP typically defines infants as individuals aged between 0 to 5 years. However, this classification is configurable based on the specific legal or administrative definitions of the implementing country. Anyone above the configured age threshold is categorized as either a minor or an adult.
{% endhint %}

A high-level workflow diagram for this process is provided below.

**High-Level Workflow:**

<figure><img src="../../../.gitbook/assets/Infant_birth_registration.png" alt=""><figcaption><p>Infant Birth Registration</p></figcaption></figure>

Steps and required information are provided below:

#### **Step 1: Operator Login & Authentication**

1. The CRVS operator logs into the CRVS portal and enters the required details for the newborn and the parent/introducer.
2. The introducer’s identity (VID/UIN) is authenticated via **eSignet**.
3. Upon successful authentication, the request proceeds for further processing.

**Required Information for MOSIP to Process the Request:**\
**Newborn Information** (Additional fields can be included based on country needs)

1. Name
2. Gender
3. Date of Birth (DOB)

**Introducer/Informant Information** (Additional fields can be included based on country needs)

1. Introducers' VID/UIN
2. eSignet User Info Token

**Step 2: Packet Creation**

CRVS creates a registration packet by calling the **Packet Manager API**, using:

1. Access Token
2. Client ID
3. ID Schema Version
4. Unique Registration ID (RID)

The packet is stored in the **Object Store** for further processing.

**Step 3: Workflow Trigger & Notification**

1. CRVS calls the **Trigger API** to initiate the processing workflow.
2. Once the packet reaches a "Completed" state, MOSIP publishes an event to a **WebSub topic**, notifying subscribers.

**Step 4: Identity Credential Sharing**\
Upon successful processing:

1. The newborn’s demographic data is updated in MOSIP.
2. A notification is sent to the registered email/phone number.
3. The update event with identity credentials is published to the subscribed **WebSub topic**.
4. CRVS receives this update and can proceed with issuing the birth certificate.

#### **1.2 Duplicate and/or Repeated Infant Birth Registration Requests Initiated by CRVS**

Duplicate and/or repeated requests may arise under the following conditions:

1. **Repeated Requests- Same RID Used In Multiple Requests:**&#x20;
   1. When multiple requests are made using the same RID (Request ID) for the birth registration of the same infant (with the same or different data).
   2. Currently, the request will be processed even if the same RID is used in multiple requests.
   3. MOSIP will overwrite the existing data with the **most recent values** provided in the latest request.
2. **Duplicate Requests - Same Infant Demographic Data with Different RIDs:**
   1. Multiple requests are made using identical infant demographic data but with different RIDs.
   2. Currently, the request will be processed, and an additional UIN will be issued for the infant for the additional RID.

{% hint style="info" %}
**Note**: MOSIP relies on CRVS to perform deduplication and treats CRVS as the source of truth. While MOSIP has its internal deduplication mechanism to detect and reject duplicate packets, the above scenarios are not currently handled for rejection of duplicate and/or repeated requests.
{% endhint %}

#### **1.3 Failure Handling**

1. **Technical Failures**
   1. There is a possibility that some requests may fail due to failure caused by **internal MOSIP** technical problems during processing.
   2. In case of internal processing issues within MOSIP, a **retry mechanism** automatically attempts reprocessing of failed requests.
2. **Validation Failures**
   1. This includes requests failing due to:
      1. Missing or invalid data
      2. Uniqueness conflicts
      3. Schema mismatches
   2. MOSIP will publish a **failure event** to the **WebSub topic**, detailing the rejection reason.
   3. CRVS must subscribe to the WebSub topic to receive and act on such notifications.

#### 2. Death Registration <a href="#id-2.-death-registration" id="id-2.-death-registration"></a>

#### **2.1 New Death Registration Initiated by CRVS:**

When a death (infant or adult) is registered in the CRVS system, the information is shared with MOSIP, including the deceased’s National ID number. Once received, the individual’s ID undergoes a regulated update process. This ensures timely updates to social security systems and other related services, promoting consistency across systems and easing administrative burdens for bereaved families.

This integrated approach to ID lifecycle management supports the accuracy of records within the national ID system, enabling secure and uninterrupted access to essential services throughout an individual's life.

**Approach**

A death registration request is initiated by the CRVS system based on the informant reporting the deceased. For MOSIP, the informant must be a registered user with a valid national ID. This ID is authenticated using eSignet. During the death registration, MOSIP marks the individual as deceased using a status flag, without deactivating the ID. The date of death declaration is recorded in the system.

To facilitate this process, the following fields can be added to the ID schema:

1. declaredAsDeceased
2. deceasedDeclarationDate
3. typeOfDeath
4. deceasedInformer

It is up to each country to determine which fields should be included in the ID schema, based on their specific use case.

**High-Level Workflow:**

<figure><img src="../../../.gitbook/assets/death_registration.png" alt=""><figcaption><p>Death Registration</p></figcaption></figure>

Steps and required information are provided below:

**Step 1: Registration Initiation & Authentication:**

1. The informant visits the CRVS Registration Centre.
2. Provides necessary details.
3. The CRVS system verifies the informant's identity via eSignet.
4. On successful authentication, CRVS adds the eSignet user info token to the ID schema and proceeds.

**Required Information for MOSIP to Process the Request:**

1. **Deceased Information** (Extendable as per country needs):
   1. Name
   2. Date & Time of Death
   3. UIN/VID
2. **Informant Information** (Extendable as per country needs):
   1. Informant's UIN/VID
   2. eSignet User Info Token

**Step 2: Packet Creation:**

1. CRVS sends a request to the Packet Manager API.
2. Includes access token, client ID, ID schema version, and RID.
3. The packet is stored in the object store.

**Step 3: Workflow Trigger:**

1. CRVS triggers the registration workflow by calling the "trigger" API using the access token.
2. This ensures the death registration is processed within MOSIP.

**Step 4: Validation:**

1. MOSIP checks the UINs/VIDs' current status to determine if it was previously marked as deceased.
2. If not, MOSIP updates the death declaration flag to "Y - YES".

**Step 5: Notifications:**

1. Once the packet is processed and approved, a notification is sent to the registered email and phone number regarding the update.
2. Update is also shared with CRVS through a WebSub event.

#### **2.2 Duplicate and/or Repeated Requests for Death Registration:**

1. A request is considered a duplicate under the following conditions:
   1. **Repeated Requests - Same AID Used for Multiple Requests:**
      1. Multiple requests are made using the same AID for the same deceased individual.
      2. Currently, the request will be processed even if the same AID is used in multiple requests.
      3. MOSIP will overwrite the existing data with the **most recent values** provided in the latest request.
   2. **Duplicate Requests - Same Data with Different AIDs:**
      1. Multiple requests are made for the same individual using identical data but with different AIDs.
      2. Currently, the request will be processed, and data will be updated based on the latest request.

{% hint style="info" %}
**Note**: MOSIP relies on CRVS to perform deduplication and treats CRVS as the source of truth. While MOSIP has its internal deduplication mechanism to detect and reject duplicate packets, the above scenarios are not currently handled for rejection of duplicate and/or repeated requests.
{% endhint %}

#### 2.3 **Failure Handling:**

1. **Technical Failures**
   1. Failures due to internal MOSIP issues.
   2. MOSIP includes a retry mechanism to reprocess such requests.
2. **Validation Failures**
   1. Failures due to data validation errors or uniqueness conflicts.
   2. MOSIP returns a failure response and rejects the request if required fields are missing or data is incomplete.
   3. MOSIP will publish a **failure event** to the **WebSub topic**, detailing the rejection reason.
   4. CRVS must subscribe to the WebSub topic to receive and act on such notifications.

#### 3. Demographic Data Update Initiated by CRVS System <a href="#id-3.-demographic-data-update-initiated-by-crvs-system" id="id-3.-demographic-data-update-initiated-by-crvs-system"></a>

Demographic data updates may be required due to life events such as marriage, divorce, changes in guardianship (in cases of adoption into a family), or corrections to previously submitted data. Regardless of the specific scenario, such cases follow the standard update flow. This integration between the CRVS system and MOSIP enables CRVS to submit demographic update requests to MOSIP on behalf of individuals when these life events occur.\
\
The integration supports updates for the following fields:

1. Name
2. Date of Birth (DOB)
3. Gender
4. Parent's / Guardian's Name

{% hint style="info" %}
**Note:** Updates to biometrics or any other data beyond the fields listed above are not supported via CRVS. For such changes, individuals must visit the National ID department and initiate the request directly through the National ID system (MOSIP).
{% endhint %}

**High-Level Workflow:**

<figure><img src="../../../.gitbook/assets/Infant_Demo _Data_Update.png" alt=""><figcaption><p>Infant Demo Data Update</p></figcaption></figure>

The various scenarios for demographic data updates are outlined below, along with the basic workflow and the expected behavior from MOSIP in each case.

#### **3.1 Infant Demo Data Update Request Initiated by CRVS**

This includes scenarios such as:

1. Corrections to inaccurate information submitted during birth registration
2. Changes resulting from life events like adoption or a change in guardianship

Steps and required information are provided below:

1. **Step 1: Update Request Initiation & Authentication**
   1. The parent, guardian, or introducer visits the CRVS registration centre and provides updated demographic details.
   2. CRVS authenticates the individual's identity using their national ID via eSignet.
   3. Upon successful authentication, the request is sent to MOSIP along with the eSignet user info token.

**Required Information for MOSIP to Process the Request:**

1. **Individual’s Update Information** (Any or all of the following fields):
   1. Name
   2. Date of Birth (DOB)
   3. Gender
   4. Address
2. **Informant Information** (Extendable as per country needs):
   1. eSignet User Info Token

**Step 2: Packet Creation**

1. CRVS creates a registration packet by calling the Packet Manager API with an access token, client ID, ID schema version, and RID.
2. The packet is stored in the Object Store.

**Step 3: Workflow Trigger:**

1. CRVS triggers processing by calling the "trigger" API with the access token.
2. This ensures the update packet is processed within MOSIP.

**Step 4: Update & Notification:**

1. Once approved, the demo data is updated in MOSIP.
2. Notifications are sent to the registered email and phone number.
3. Update status is also shared with CRVS via a WebSub event.

#### **3.2 Duplicate and/or Repeated Infant Demo Data Update Requests**

An update request is considered a duplicate under the following conditions:

1. **Repeated Requests - Same RID Used for Multiple Requests:**
   1. Multiple requests are made using the same RID (Request ID) for the update of the same individual.
   2. Currently, the request will be processed even if the same RID is used in multiple requests.
   3. MOSIP will overwrite the existing data with the **most recent values** provided in the latest request.

{% hint style="info" %}
**Note**: MOSIP relies on CRVS to perform deduplication and treats CRVS as the source of truth. While MOSIP has its internal deduplication mechanism to detect and reject duplicate packets, the above scenarios are not currently handled for rejection of duplicate/repeated requests.
{% endhint %}

2. **Duplicate Requests - Multiple Update Requests with Different RIDs for the Same Infant (with Same or Different Demo Data):**
   1. When MOSIP receives multiple update requests for the same infant with different RIDs, whether the demographic data fields contain the same values or have been modified, each request is treated as a new submission.
   2. Currently, the request will be processed, and data will be updated based on the latest request.

#### **3.3** **Adult Demo Data Update Request Initiated by CRVS System**

While adults may experience life events (e.g., marriage or divorce) that require updates to name or address, MOSIP does not support adult demographic data updates via CRVS. For such requests, individuals must visit the National ID department and initiate the request directly through the National ID system (MOSIP).

#### **Integration Limitations** <a href="#integration-limitations" id="integration-limitations"></a>

Although the integration scope includes scenarios for birth, death, and updates, there are still some cases where limitations exist. While some of these limitations have been outlined above as part of the scope, this section will cover all current limitations of the integration.

1. **No Support for New Adult Birth Registrations**:\
   MOSIP does not support new adult birth registrations when the request comes from CRVS.
2. **Integration for Birth and Death Registrations**:\
   The integration works seamlessly for birth and death registrations. However, updates to demographic data are still a work in progress.
3. **Duplicate Request Rejection**:\
   Since the CRVS system is considered the source of truth, MOSIP currently does not reject duplicate birth/death registration requests received from the CRVS system. This can result in multiple UINs for the same infant or an update of the death flag for the same deceased. Deduplication is expected to be handled by CRVS.
4. **No Support for Rejected Packets, Status Updates, and Reason**\
   If a request fails due to validation issues in MOSIP, there is currently no mechanism to send detailed rejection reasons back to CRVS.
5. **No support for Offline Integration**:\
   This integration works only when online connectivity is available. Offline (no-connectivity) support is under development.
6. **Use of VID/UIN for Death Registration**:\
   Only VID or UIN can be used to register a death. Currently, MOSIP does not support death updates with any other identifier.

While these are the currently supported scenarios, additional use cases will be introduced as the integration evolves and expands based on country-specific requirements and feedback.

In summary, by embracing open-source principles, MOSIP remains committed to transparency, collaboration, and adaptability. The integration of CRVS systems with MOSIP marks a significant step toward the global adoption of Open Standards, promoting interoperability and flexibility across diverse digital ecosystems. Through these efforts, we aim to advance societal well-being and expand equitable access to essential services at scale.
