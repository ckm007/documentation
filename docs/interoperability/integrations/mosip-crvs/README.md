# MOSIP - CRVS

### Introduction to MOSIP CRVS Integration

Imagine a world where a child's digital identity is created the moment they are born. Through each life milestone, from their first day of school to entering the workforce, this national digital ID ensures seamless access to essential services tailored to their evolving needs. Even at the end of life, the ID is securely managed to ensure that only the entitled beneficiaries receive the rightful government support. This careful management helps make sure that benefits are distributed fairly and accurately, contributing to the overall well-being of society.

Achieving this vision has proven to be a challenge, as civil registration systems often operate in isolation, rarely sharing data with other critical platforms such as digital identity systems. This lack of integration leads to fragmented data systems and inefficiencies in data collection, hindering efficient service delivery.

In an increasingly digital world, integrating Civil Registration and Vital Statistics (CRVS) systems with national digital identity platforms like MOSIP represents a foundational shift in how countries can manage identity and vital statistics. This synergy allows for the seamless management of an individual's identity across life events, starting from birth registration, through education and employment, to end-of-life verification.

<div align="right"><figure><img src="../../../.gitbook/assets/CRVS (1).png" alt=""><figcaption><p>Birth and Death Registration</p></figcaption></figure></div>

#### Why Integration Matters

Civil registration systems record vital life events such as births, deaths, marriages, and divorces. Meanwhile, national ID systems provide legal and verifiable identities. When these systems operate in isolation, it leads to administrative inefficiencies, fragmented data, and challenges in service access.

Through integration with MOSIP (Modular Open Source Identity Platform), CRVS systems can enable:

* Real-time updates between registration and ID issuance
* Automated processes to reduce duplication
* Improved service delivery with more accurate citizen records
* Enhanced data-driven governance and policy-making

#### Vision and Impact

The combined capabilities of MOSIP and CRVS systems have the potential to demonstrate a transformative impact across countries. Together, they can provide a holistic framework for:

* **Recognition** – Establishing a secure, legal identity from birth
* **Protection** – Ensuring privacy, security, and proper authentication mechanisms
* **Provision** – Enabling access to services through a Unique Identification Number (UIN)

This vision further aligns with global Sustainable Development Goals (SDGs), including the UN’s SDG Target 16.9: “Provide legal identity for all, including birth registration, by 2030.”

#### Key Objectives of the Integration

#### **Objectives** <a href="#objectives" id="objectives"></a>

The integration of MOSIP with CRVS systems is designed to achieve several key objectives aimed at enhancing the efficiency, security, and accuracy of national identity and civil registration systems. These objectives include:

1. **Streamlining Processes and Enhancing Information Exchange**\
   The integration will create a seamless flow of information between MOSIP and CRVS systems, reducing administrative burdens and enabling faster, more efficient processing of civil registration events.
2. **Establishing Secure and Reliable Data Verification Mechanisms**\
   A central goal of this integration is to establish robust verification protocols, ensuring that data exchanged between the systems is accurate, reliable, and trustworthy, thereby preventing errors and enhancing security.
3. **Issuance of Unique Identity Numbers Linked to Birth Certificates**\
   The integration will facilitate the issuance of unique identification numbers (UINs) linked directly to birth certificates, providing individuals with a verified, digital identity that is consistently updated as they undergo significant life events.
4. **Improving Accuracy in Identification and Reducing Data Duplication**\
   By linking civil registration events to the national identity system, the integration will eliminate the risk of duplicate records, ensuring that every individual has a single, verified identity across all government systems.
5. **Maintaining Accurate Records of Deceased Individuals**\
   One of the core aims of the integration is to ensure that the identity system is promptly updated with the status of deceased individuals, preventing identity fraud or the misuse of personal data for illicit purposes.
6. **Establishing and Maintaining Accurate Spousal and Marital Status Information**\
   The integration will enable accurate recording of spousal relationships by linking marriage registrations with national identity records. This ensures that marital status information is consistently updated and maintained, resulting in more reliable and up-to-date personal identity data for married individuals.
7. **Enhancing Data Quality, Integrity, and Reliability for Better Governance**\
   The integration will improve the accuracy, completeness, and timeliness of vital event records across systems, enhancing overall data quality and integrity. This reliable data foundation will support better governance by equipping authorities with accurate statistics for more informed, data-driven decision-making.
8. **Ensuring Strong Security and Privacy Protections**\
   The integration will adhere to stringent data protection and cybersecurity standards, ensuring that personal information is safeguarded throughout the data exchange process. Privacy-by-design principles will be embedded to prevent unauthorized access, misuse, or breaches, thereby building public trust and protecting individual rights.

#### Integration Architecture and Guidelines

The following is a list of guiding principles for this integration.

#### **Guidelines**&#x20;

1. **Data Verification and Trust:**
   1. The initiation of the request with the data will be from CRVS to MOSIP
   2. Data transmitted from CRVS to MOSIP will undergo thorough data/document verification and deduplication before any request is initiated for MOSIP to process.
   3. MOSIP will trust all information provided by CRVS and honor the received requests. MOSIP will ensure that the technical and logical validations are all in place for packet processing.
   4. The integration should define the mandatory attributes to be exchanged between the two systems. It is crucial to agree upon these attributes to ensure consistent and accurate data exchange.
2. **Data consistency:**
   1. It is imperative to maintain consistency in data across both platforms, MOSIP and CRVS. This ensures that accurate and up-to-date data is shared between the systems.
3. **Fallback mechanism:**
   1. CRVS should initiate the request by calling the create packet API if the failure occurs during creation, CRVS should be able to retry to create the packet.
   2. In the event of technical failures on the MOSIP side during packet processing, reprocessing of the packet should be in place to ensure that the packet is marked appropriately as rejected or approved.
4. **Proof of Authentication:**
   1. For any request submitted to MOSIP, it is essential to include the biometric data of the informant or applicant, whenever feasible, to ensure the accurate verification of the individual initiating the request and confirm their legitimacy.
   2. For cases where biometric data is not collected by CRVS, it is recommended for CRVS to use eSignet for the applicant or introducer authentication. Post-authentication user info token should be shared with MOSIP for validation and auditing purposes.
5. **Identity Credential Sharing & Packet status**
   1. The identity credential sharing and packet status updates are two separate MOSIP integration points for any CRVS.
   2. MOSIP will generate and share identity credentials for new registration cases via WebSub. Any partner configured according to the policy will receive these notifications automatically.
   3. By default, MOSIP recommends sharing the PSUT token as part of the identity credential returned to CRVS. However, the system also supports sharing UIN, VID, or the PSUT token, based on the country’s specific requirements.
   4. MOSIP will publish packet status updates to a separate WebSub. Any credential partner subscribed to this WebSub topic can filter and track specific packets based on their status.
6. **Multiple CRVS Systems:**
   1. If a country deploys multiple CRVS systems, each system will be treated as a separate partner for MOSIP. This allows for independent management and integration with each CRVS system.
   2. Credentials generated/update messages from MOSIP will be sent to all the configured credential partners subscribed to the websub as per policy. It is the responsibility of the country and CRVS systems to manage the sharing of information across multiple CRVS systems

#### About the Platforms

**MOSIP** is an open-source, modular identity platform designed for scalability, interoperability, and compliance with global standards. It allows countries to customize identity systems tailored to their governance needs. To learn more about MOSIP, click [here](https://docs.mosip.io/1.2.0/id-lifecycle-management).\
\
**Civil Registration and Vital Statistics (CRVS)** systems are essential for documenting key life events such as births, deaths, marriages, and divorces. These systems provide individuals with legal recognition and play a vital role in ensuring access to rights and services. Additionally, CRVS systems generate important demographic data that supports effective policy-making, governance, and resource planning.\
\
In summary, this integration represents a significant stride in building resilient, citizen-centric digital infrastructure. By combining the strengths of CRVS and MOSIP, countries can ensure inclusive access to public services and rights, starting from birth and extending throughout every life milestone.

{% hint style="info" %}
Refer here for details on the MOSIP-CRVS integration [scope](scope.md) and [approach](approach/).
{% endhint %}

{% hint style="info" %}
Amongst the various CRVS systems, MOSIP has integrated with [**OpenCRVS**](https://documentation.opencrvs.org/), a digital civil registration solution. To know more about this integration, click here. (Link to be updated)
{% endhint %}

**Assumption:** This approach assumes that the CRVS system is recognized as the authoritative source of vital event data and is legally authorized to issue official birth and death certificates in accordance with the laws of the country.
