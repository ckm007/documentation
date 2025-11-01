# API changes with PMS Revamp

This document captures all the changes that have been made in the API endpoints during the PMS Revamp Releases. These changes include addition of new endpoints, deprecation of a few endpoints and also some other changes.

# PMS API Endpoints Documentation

## /oauth/client (GET)

**Description:** This endpoint retrieves a list of all OAuth clients created by the Auth Partners. It supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the PARTNER_ADMIN role, then it will fetch all the OAuth clients created by all the partners associated with the logged in user only. If the token used to access this endpoint, has PARTNER_ADMIN role, then it will fetch all the OAuth clients created by all the partners. It is configured for **PARTNER_ADMIN** and **AUTH_PARTNER** roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, partnerId, orgName, policyGroupName, policyName, clientName, status

## /oauth/client (POST)

**Description:** This endpoint is used for creating OIDC Client.

**Changes done in release 1.2.2.0:** 
1. Added validation to check the partner id in the request body belongs to the user who's token is being used to access this endpoint. This will ensure that PMS user can create OIDC client only for the partner id which belongs to the user. This validation is skipped if the user's role is **PARTNER_ADMIN**.

2. Added validation to check if the **Partner ID** used in the request body is active. This will ensure that OIDC client cannot be created for an inactive partner. ([MOSIP-34276](https://mosip.atlassian.net/browse/MOSIP-34276))

3. If multiple policy requests were created by the partner for a policy, then while creating the OIDC client, this endpoint was checking the status of only the first policy request. So even if there was an approved policy request, it was still throwing an error. Fixed this bug ([MOSIP-34599](https://mosip.atlassian.net/browse/MOSIP-34599))

4. Improved JWK validation for the public key by adding validation that n value (modulus value) of the JWK must be unique ([MOSIP-36219](https://mosip.atlassian.net/browse/MOSIP-36219))

5. Updated client name to be a JSON string to support client name language map ([ES-836](https://mosip.atlassian.net/browse/ES-836))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /oauth/client/{client_id} (GET)

**Description:** This endpoint retrieves the OIDC client details by client id

**Changes done in release 1.2.2.0:** 
1. Added validation to check the partner id in the request belongs to the user who's token is being used to access this endpoint. This will ensure that PMS user can access OIDC client only for the partner id which belongs to the user. This validation is skipped if the user's role is **PARTNER_ADMIN**.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /oauth/client/{client_id} (PUT)

**Description:** This endpoint is used for updating OIDC Client based on client id

**Changes done in release 1.2.2.0:** 
1. Added validation to check the partner id in the request body belongs to the user who's token is being used to access this endpoint. This will ensure that PMS user can update OIDC client only for the partner id which belongs to the user. This validation is skipped if the user's role is **PARTNER_ADMIN**.

2. Added validation to check if the **Partner ID** used in the request body is active. This will ensure that OIDC client cannot be updated for an inactive partner. This validation is skipped if the user's role is **PARTNER_ADMIN** and status in the request is changed to **INACTIVE**. ([MOSIP-34276](https://mosip.atlassian.net/browse/MOSIP-34276))

3. If the status in the request is changed to **INACTIVE**, only the status is updated in the database other fields remain unchanged. This will ensure that PUT endpoint can be used to deactivate the OIDC client.

4. Added a bypass for a user with **PARTNER_ADMIN** role. If the user with **PARTNER_ADMIN** role is used to access this endpoint, then it will deactivate the OIDC client for any partner ID, even if the partner ID is deactivated.

5. Added a validation to check if the OIDC client is already deactivated.([MOSIP-34108](https://mosip.atlassian.net/browse/MOSIP-34108))

6. Updated client name to be a JSON string to support client name language map ([ES-836](https://mosip.atlassian.net/browse/ES-836))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail (GET)

**Description:** This endpoint retrieves a list of all the Devices across all the Device Providers in PMS. It supports pagination, sorting, and filtering. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, partnerId, orgName, deviceType, deviceSubType, status, make, model, sbiId, sbiVersion, deviceId

## /devicedetail (PUT)

**Description:** Service to update Device Detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail (POST)

**Description:** Service to save Device Detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST /securebiometricinterface/{sbiId}/devices endpoint

This ensures that a device will always be created for a SBI and not without one.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail (PATCH)

**Description:** Service to approve/reject Device Detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST devicedetail/{id}/approval endpoint

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail/{deviceId} (PATCH)

**Description:** This endpoint deactivates a Device based on the Device Id. It is configured for the roles **DEVICE_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: deviceId, status

## /devicedetail/{id}/approval (POST)

**Description:** This endpoint is for the Partner Admin user to approve or reject a Device and activate the mapping between the Device and the SBI. It is configured for the role **PARTNER_ADMIN**

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sbiId, partnerId, deviceId, status

## /devicedetail/deviceSubType/filtervalues (POST)

**Description:** Service to filter Device Sub Types

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail/deviceType/filtervalues (POST)

**Description:** Service to filter Device Types

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail/deviceType/search (POST)

**Description:** Service to search Device Types

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail/filtervalues (POST)

**Description:** Service to filter Device Detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /devicedetail endpoint

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /devicedetail/search (POST)

**Description:** Service to search Device Detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /devicedetail endpoint

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail (GET)

**Description:** This endpoint retrieves a list of all FTM Chip details created by all the FTM Providers associated with the logged in user. It is configured for the roles **FTM_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added an optional query parameter expiryPeriod

## /ftpchipdetail (PUT)

**Description:** Service to update ftp chip detail

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail (POST)

**Description:** Service to save ftp chip detail

**Changes done in release 1.2.2.0:** 
1. Improved the validation check by trimming extra spaces in make and model to prevent duplicate entries. ([MOSIP-35788](https://mosip.atlassian.net/browse/MOSIP-35788))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail (PATCH)

**Description:** Service to approve/reject ftp chip detail

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail/{ftmId} (PATCH)

**Description:** This endpoint deactivates the ftp chip detail based on the ftp chip detail Id. It is configured for the roles **FTM_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail/{ftmId}/certificate-data (GET)

**Description:** This endpoint fetches both the CA signed certificate uploaded by the FTM Chip Provider and the MOSIP signed certificate generated by PMS. It is configured for the roles **FTM_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following field: ftmId

## /ftpchipdetail/getPartnerCertificate/{ftpChipDetailId} (GET)

**Description:** Service to get certificate of ftp chip

**Changes done in release 1.2.2.0:** Improved Key Manager error handling, to capture the correct error code from Key Manager and send it in the endpoint's response.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail/search (POST)

**Description:** Service to search ftp chip details

**Changes done in release 1.2.2.0:** 
1. This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /ftpchipdetail/v2 endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail/uploadcertificate (POST)

**Description:** Service to upload certificate of ftp chip

**Changes done in release 1.2.2.0:** 
1. Added validation to allow certificate upload only if the FTM chip details certificate status is **APPROVED** or **PENDING_CERT_UPLOAD**.([MOSIP-36283](https://mosip.atlassian.net/browse/MOSIP-36283)). So for Rejected or Deactivated FTM, a certificate cannot be uploaded.

2. Improved Key Manager error handling, to capture the correct error code from Key Manager and send it in the endpoint's response.

3. Set isActive to false after certificate re-upload. This will ensure that after cert is reuploaded, partner admin will have to approve the FTM again. ([MOSIP-36285](https://mosip.atlassian.net/browse/MOSIP-36285))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /ftpchipdetail/v2 (GET)

**Description:** This endpoint retrieves a list of all FTM Chip details created by all the FTM Providers. Also supports pagination, sorting, and filtering. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: ftmId, status

## /admin-partners (GET)

**Description:** This endpoint retrieves a list of all Partners. Also supports pagination, sorting, and filtering. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

- Disabled sorting on the email_id column due to encryption-related limitations.

- Modified filtering behavior for the email_id column: now supports only exact match filtering; partial or "contains" search is no longer supported.

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, partnerId, partnerType, orgName, emailAddress, certificateUploadStatus, policyGroupName

## /admin-partners/{partnerId} (GET)

**Description:** This endpoint retrieves all the details of the Partner based on Partner Id. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following field: partnerId

## /partner-api-keys (GET)

**Description:** This endpoint retrieves a list of all the API keys created by the Auth Partners. Also supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the **PARTNER_ADMIN** role, then it will fetch all the API keys created by all the partners associated with the logged in user only. If the token used to access this endpoint, has **PARTNER_ADMIN** role, then it will fetch all the API keys created by all the partners.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** 
1. This endpoint has been deprecated since the release-1.3.0-beta.2. It has been replaced by the new GET /partner-api-keys/v2 endpoint.

2. Also added input regex validation for the following fields: sortFieldName, sortType, partnerId, apiKeyLabel, orgName, status, policyName, policyGroupName

## /partner-api-keys/v2 (GET)

**Description:** This endpoint retrieves a list of all the API keys created by the Auth Partners. Also supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the **PARTNER_ADMIN** role, then it will fetch all the API keys created by all the partners associated with the logged in user only. If the token used to access this endpoint, has **PARTNER_ADMIN** role, then it will fetch all the API keys created by all the partners.

**Changes done in release 1.2.2.0:** -

**Changes done in release 1.3.0-beta.1:** -

**Changes done in release 1.3.0-beta.2:** 
1. Newly added in release 1.3.0-beta.2

2. Also added input regex validation for the following fields: sortFieldName, sortType, partnerId, apiKeyLabel, orgName, status, policyName, policyGroupName

## /partner-policy-requests (GET)

**Description:** This endpoint fetches list of all the policy requests made by the partners. Also supports pagination, sorting, and filtering based on optional query parameters. If the token used to access this endpoint, does not have the **PARTNER_ADMIN** role, then it will fetch all the policy requests made by all the partners associated with the logged in user only.If the token used to access this endpoint, has **PARTNER_ADMIN** role, then it will fetch all the policy requests made by all the partners.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, partnerId, partnerComment, orgName, status, policyId, policyName, policyGroupName, partnerType

## /partners (GET)

**Description:** Service to get partner details

**Changes done in release 1.2.2.0:** 
1. This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId} (PATCH)

**Description:** Service to activate/de-activate partner

**Changes done in release 1.2.2.0:** 
1. Added a check to verify if the **partner** is already deactivated. If yes, partner cannot be deactivated again. ([MOSIP-37017](https://mosip.atlassian.net/browse/MOSIP-37017))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/apikey/{apikey} (GET)

**Description:** Service to get policy for given API key

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/apikey/{apikey}/policies (PUT)

**Description:** Service to update policies against to API key

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/policy/{policyId}/apikey/status (PATCH)

**Description:** Service to activate/de-activate partner API key

**Changes done in release 1.2.2.0:** 
1. If the API key is already deactivated, it cannot be deactivated again.([MOSIP-34430](https://mosip.atlassian.net/browse/MOSIP-34430))

2. Added a validation to check if the **Partner ID** used in the request body is active. This will ensure that API cannot be deactivated if partner has been deactivated. This validation is skipped if the user's role is **PARTNER_ADMIN**. ([MOSIP-34430](https://mosip.atlassian.net/browse/MOSIP-34430))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/apikey (GET)

**Description:** Service to get API key requests

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/apikey/{apikey} (GET)

**Description:** Service to get API key request

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/policy/{mappingkey} (PUT)

**Description:** Service to approve/reject partner policy mapping

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/v2 (GET)

**Description:** Service to get partner details

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /trust-chain-certificates (GET)

**Description:** This endpoint retrieves a list of all the Trust Certificates uploaded by the Partner Admin. Also supports pagination, sorting, and filtering. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, caCertificateType, certificateId, partnerDomain, issuedTo, issuedBy

## /trust-chain-certificates/{certificateId}/certificateFile (GET)

**Description:** This endpoint will download p7b file for a CA / Intermediate CA certificate along with the trust chain based on Certificate Id. It is configured for the role **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following field: certificateId

## /partners (POST)

**Description:** partner self registration

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId} (GET)

**Description:** Service to get details of partner

**Changes done in release 1.2.2.0:** Corrected the version in the response body

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId} (PUT)

**Description:** Service to update details of partner

**Changes done in release 1.2.2.0:** 

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/apikey/request (GET)

**Description:** Service to get API key requests of partner

**Changes done in release 1.2.2.0:** Corrected the version in the response body

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/certificate (GET)

**Description:** Service to get partner certificate

**Changes done in release 1.2.2.0:** 
1. Added a check to verify if the partner id in the request exists in the database.([MOSIP-37017](https://mosip.atlassian.net/browse/MOSIP-37017))

2. Added validation to check if the certificate has been uploaded previously.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/certificate-data (GET)

**Description:** This endpoint retrieves both the CA signed certificate uploaded by the partner and the MOSIP-signed certificate generated by PMS. It is configured for role any of the partner type or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following field: certificateId

## /partners/{partnerId}/contact/add (POST)

**Description:** Service to add additional contact deatils of partner

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/generate/apikey (PATCH)

**Description:** To generate API Key for approved policies

**Changes done in release 1.2.2.0:** Added a check to remove extra spaces in the API key label before saving to the database, preventing the creation of duplicate API key labels with extra spaces.([MOSIP-35788](https://mosip.atlassian.net/browse/MOSIP-35788))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/policy/map (POST)

**Description:** To request for policy mapping

**Changes done in release 1.2.2.0:** Updated error messages to indicate if the policy is already mapped and its status is **Approved** or **In Progress**.([MOSIP-33803](https://mosip.atlassian.net/browse/MOSIP-33803))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/{partnerId}/policygroup/{policygroupName} (PUT)

**Description:** Service to update the policy group for partner

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/apikey/request/filtervalues (POST)

**Description:** Service to filter API key requests

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/apikey/request/search (POST)

**Description:** Service to search API key requests

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/apikey/search (POST)

**Description:** Service to search API key

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-api-keys endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/certificate/ca/upload (POST)

**Description:** Service to upload ca certificate

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/certificate/upload (POST)

**Description:** Service to upload partner certificate

**Changes done in release 1.2.2.0:** 
1. Added a validation to check if the **Partner ID** used in the request body is active. This will ensure that certificate cannot be uploaded if partner has been deactivated. ([MOSIP-34498](https://mosip.atlassian.net/browse/MOSIP-34498))

2. If domain is **FTM**, do not call the uploadOtherDomainCertificate endpoint of KeyManager.([MOSIP-35797](https://mosip.atlassian.net/browse/MOSIP-35797))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/email/verify (PUT)

**Description:** Service to verify partner email

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/filtervalues (POST)

**Description:** Service to filter partner details

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

- Support for email_id**, contact_no**, and address fields has been removed due to encryption constraints.

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/partner-certificates-details (GET)

**Description:** This endpoint retrieves a list of all Partner Certicates uploaded by the logged in user

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /partners/partnerType/search (POST)

**Description:** Service to search partner types

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## partners/search (POST)

**Description:** Service to search partner details

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

- Support for email_id**, contact_no**, and address columns has been removed due to encryption constraints.

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## partners/v2 (POST)

**Description:** Registers partner details

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## partners/v2/{partnerId} (PUT)

**Description:** Service to update details of partner

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** Handled encryption and decryption for PII columns([MOSIP-38061](https://mosip.atlassian.net/browse/MOSIP-38061))

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## partners/v3 (GET)

**Description:** This endpoint retrieves a list of Partners associated with the logged in user, based on the query parameters. It is configured for role any of the partner type or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: status, partnerType

## /roles (GET)

**Description:** Service to get required roles

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface (GET)

**Description:** This endpoint retrieves a list of all SBIs created by the Device Providers. Also supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the **PARTNER_ADMIN** role, then it will fetch all SBIs created by all the partners associated with the logged in user only. If the token used to access this endpoint, has **PARTNER_ADMIN** role, then it will fetch all the SBIs created by all the partners.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** 
1. Added input regex validation for the following fields: sortFieldName, sortType, partnerId, orgName, sbiId, sbiVersion, status, sbiExpiryStatus

2. Included an optional query parameter expiryPeriod

## /securebiometricinterface (PUT)

**Description:** Service to update SecureBiometricInterface

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface (POST)

**Description:** Service to save SecureBiometricInterface details

**Changes done in release 1.2.2.0:** Added a check to remove extra spaces in the SBI version before saving to the database, preventing the creation of duplicate SBI versions with extra spaces.([MOSIP-35788](https://mosip.atlassian.net/browse/MOSIP-35788))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface (PATCH)

**Description:** Service to approve/reject SecureBiometricInterface

**Changes done in release 1.2.2.0:** Added separate error codes for cases when SBI is already **approved** or **rejected**.([MOSIP-38973](https://mosip.atlassian.net/browse/MOSIP-38973))

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface/{sbiId} (PATCH)

**Description:** This endpoint deactivates an SBI along with associated Devices. It is configured for the roles **DEVICE_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sbiId, status

## /securebiometricinterface/{sbiId}/devices (GET)

**Description:** This endpoint fetches the list of Devices associated with a given SBI Id. It is configured for the roles **DEVICE_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following field: sbiId

## /securebiometricinterface/{sbiId}/devices (POST)

**Description:** This endpoint adds a new Device and creates an inactive mapping between the device and the given SBI. It is configured for the roles **DEVICE_PROVIDER** or **PARTNER_ADMIN**.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sbiId, id, make, model, deviceTypeCode, deviceSubTypeCode

## /securebiometricinterface/devicedetails/map (PUT)

**Description:** Service to map device details with sbi

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST /securebiometricinterface/{sbiId}/devices endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface/devicedetails/map/remove (PUT)

**Description:** Service to remove mapped device details with sbi

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface/devicedetails/map/search (POST)

**Description:** Service to search mapped device details and SecureBiometricInterface details

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface/{sbiId}/devices endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface/filtervalues (POST)

**Description:** Service to filter SBI's

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /securebiometricinterface/search (POST)

**Description:** Service to search SecureBiometricInterface details

**Changes done in release 1.2.2.0:** This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface endpoint.

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /system-config (GET)

**Description:** This endpoint fetches the configurations for PMS and sends them to the UI. No roles are required for access.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /users (POST)

**Description:** Service to register user

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /users/user-consent (GET)

**Description:** This endpoint fetches the user's consent related to the data captured by PMS. The consent is requested only once after the user's first login, and won't be asked again if already given. It is configured for all Partner Type roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /users/user-consent (POST)

**Description:** This endpoint saves the user's consent related to data captured by the PMS portal, which is requested only once after the user's first login. Once provided, the consent will not be asked again. It is configured for all Partner Type roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /users/{userId}/notifications-seen-timestamp (GET)

**Description:** This endpoint which will get the status and timestamp of when the notifications were last viewed by the user in the PMS portal.

**Changes done in release 1.2.2.0:** -

**Changes done in release 1.3.0-beta.1:** Newly added in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /users/{userId}/notifications-seen-timestamp (PUT)

**Description:** This endpoint which will update the status and timestamp of when the notifications were last viewed by the user in the PMS portal.

**Changes done in release 1.2.2.0:** -

**Changes done in release 1.3.0-beta.1:** Newly added in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /notifications (GET)

**Description:** This endpoint will get all the notifications from the pms.notifications table. Also supports pagination, sorting, and and filtering based on optional query parameters.

**Changes done in release 1.2.2.0:** -

**Changes done in release 1.3.0-beta.1:** Newly added in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: notificationStatus, notificationType, certificateId, expiryDate, issuedBy, issuedTo, partnerDomain, createdFromDate, createdToDate, ftmId, make, model, apiKeyName, policyName, sbiId, sbiVersion

## /notifications/{notificationId} (PATCH)

**Description:** This endpoint will be used to handle the dismiss action by the user.

**Changes done in release 1.2.2.0:** -

**Changes done in release 1.3.0-beta.1:** Newly added in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: notificationId, notificationStatus

---

# Policy Management Service Endpoints

## /policies (GET)

**Description:** Service to get policies

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies (POST)

**Description:** Service to create a new authentication, data sharing, or credential policy.

**Changes done in release 1.2.2.0:** Handled missing 'Empty Array and Empty String' Schema Validation

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/{policyId} (GET)

**Description:** Service to retrieve the details of a specific policy by its ID.

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/{policyId} (PUT)

**Description:** Service to update policy details

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/{policyId} (PATCH)

**Description:** This endpoint deactivates a policy based on the Policy Id. It checks if any policy requests are associated with the policy: it can be deactivated if there are no requests or if there are rejected requests. It cannot be deactivated if there are approved or pending requests, returning error codes PMS_POL_063 or PMS_POL_064, respectively. This endpoint is configured for the **POLICYMANAGER** or **PARTNER_ADMIN** roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: policyId, status

## /policies/{policyId}/group/{policygroupId}/publish (POST)

**Description:** Service to publish policy

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/active/group/{groupName} (GET)

**Description:** Service to get active policy details for policy group name

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/group/{policygroupId} (GET)

**Description:** Service to get policy group

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/group/{policyGroupId} (PATCH)

**Description:** Service for Partner Admin users to deactivate a Policy Group based on the Policy Group Id. It is configured for the **POLICYMANAGER** or **PARTNER_ADMIN** roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: policyGroupId, status

## /policies/group/new (POST)

**Description:** Service to create a new policy group

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/group/search (POST)

**Description:** Service to search policy group

**Changes done in release 1.2.2.0:** No changes made in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/policy-groups (GET)

**Description:** Service to retrieve details about all active Policy Groups

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** No changes made in release 1.3.0-beta.2

## /policies/v2 (GET)

**Description:** Service to retrieve the list of all Policies. It is configured for the **POLICYMANAGER** or **PARTNER_ADMIN** roles.

**Changes done in release 1.2.2.0:** Newly added in release 1.2.2.0

**Changes done in release 1.3.0-beta.1:** No changes made in release 1.3.0-beta.1

**Changes done in release 1.3.0-beta.2:** Added input regex validation for the following fields: sortFieldName, sortType, policyType, policyId, policyName, policyDescription, policyGroupName, status














<!--

Partner Management Service:

<table><thead><tr><th width="109.49713134765625">API Path</th><th width="80.49932861328125">Method</th><th width="246.69384765625">Description</th><th width="215.2449951171875">Changes done in release 1.2.2.0</th><th>Changes done in release 1.3.0-beta.1</th></tr></thead><tbody><tr><td>/oauth/client</td><td>GET</td><td>This endpoint retrieves a list of all OAuth clients created by the Auth Partners. It supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the PARTNER_ADMIN role, then it will fetch all the OAuth clients created by all the partners associated with the logged in user only. If the token used to access this endpoint, has PARTNER_ADMIN role, then it will fetch all the OAuth clients created by all the partners. It is configured for <strong>PARTNER_ADMIN</strong> and <strong>AUTH_PARTNER</strong> roles.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/oauth/client</td><td>POST</td><td>This endpoint is used for creating OIDC Client.</td><td><ol start="1"><li>Added validation to check the partner id in the request body belongs to the user who’s token is being used to access this endpoint. This will ensure that PMS user can create OIDC client only for the partner id which belongs to the user. This validation is skipped if the user’s role is <strong>PARTNER_ADMIN</strong>.</li><li>Added validation to check if the <strong>Partner ID</strong> used in the request body is active. This will ensure that OIDC client cannot be created for an inactive partner. (<a href="https://mosip.atlassian.net/browse/MOSIP-34276">MOSIP-34276</a>)</li><li>If multiple policy requests were created by the partner for a policy, then while creating the OIDC client, this endpoint was checking the status of only the first policy request. So even if there was an approved policy request, it was still throwing an error. Fixed this bug (<a href="https://mosip.atlassian.net/browse/MOSIP-34599">MOSIP-34599</a>)</li><li>Improved JWK validation for the public key by adding validation that n value (modulus value) of the JWK must be unique (<a href="https://mosip.atlassian.net/browse/MOSIP-36219">MOSIP-36219</a>)</li><li>Updated client name to be a JSON string to support client name language map (<a href="https://mosip.atlassian.net/browse/ES-836">ES-836</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/oauth/client/{client_id}</td><td>GET</td><td>This endpoint retrieves the OIDC client details by client id</td><td><ol start="1"><li>Added validation to check the partner id in the request belongs to the user who’s token is being used to access this endpoint. This will ensure that PMS user can access OIDC client only for the partner id which belongs to the user. This validation is skipped if the user’s role is <strong>PARTNER_ADMIN</strong>.</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/oauth/client/{client_id}</td><td>PUT</td><td>This endpoint is used for updating OIDC Client based on client id</td><td><ol start="1"><li>Added validation to check the partner id in the request body belongs to the user who’s token is being used to access this endpoint. This will ensure that PMS user can update OIDC client only for the partner id which belongs to the user. This validation is skipped if the user’s role is <strong>PARTNER_ADMIN</strong>.</li><li>Added validation to check if the <strong>Partner ID</strong> used in the request body is active. This will ensure that OIDC client cannot be updated for an inactive partner. This validation is skipped if the user’s role is <strong>PARTNER_ADMIN</strong> and status in the request is changed to <strong>INACTIVE</strong>. (<a href="https://mosip.atlassian.net/browse/MOSIP-34276">MOSIP-34276</a>)</li><li>If the status in the request is changed to <strong>INACTIVE</strong>, only the status is updated in the database other fields remain unchanged. This will ensure that PUT endpoint can be used to deactivate the OIDC client.</li><li>Added a bypass for a user with <strong>PARTNER_ADMIN</strong> role. If the user with <strong>PARTNER_ADMIN</strong> role is used to access this endpoint, then it will deactivate the OIDC client for any partner ID, even if the partner ID is deactivated.</li><li>Added a validation to check if the OIDC client is already deactivated.(<a href="https://mosip.atlassian.net/browse/MOSIP-34108">MOSIP-34108</a>)</li><li>Updated client name to be a JSON string to support client name language map (<a href="https://mosip.atlassian.net/browse/ES-836">ES-836</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail</td><td>GET</td><td>This endpoint retrieves a list of all the Devices across all the Device Providers in PMS. It supports pagination, sorting, and filtering. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail</td><td>PUT</td><td>Service to update Device Detail</td><td>This endpoint has been deprecated since the release-1.2.2.0.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail</td><td>POST</td><td>Service to save Device Detail</td><td><p>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST /securebiometricinterface/{sbiId}/devices endpoint</p><p>This ensures that a device will always be created for a SBI and not without one.</p></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail</td><td>PATCH</td><td>Service to approve/reject Device Detail</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST devicedetail/{id}/approval endpoint</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/{deviceId}</td><td>PATCH</td><td>This endpoint deactivates a Device based on the Device Id. It is configured for the roles <strong>DEVICE_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/{id}/approval</td><td>POST</td><td>This endpoint is for the Partner Admin user to approve or reject a Device and activate the mapping between the Device and the SBI. It is configured for the role <strong>PARTNER_ADMIN</strong></td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/deviceSubType/filtervalues</td><td>POST</td><td>Service to filter Device Sub Types</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/deviceType/filtervalues</td><td>POST</td><td>Service to filter Device Types</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/deviceType/search</td><td>POST</td><td>Service to search Device Types</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/filtervalues</td><td>POST</td><td>Service to filter Device Detail</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /devicedetail endpoint</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/devicedetail/search</td><td>POST</td><td>Service to search Device Detail</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /devicedetail endpoint</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail</td><td>GET</td><td>This endpoint retrieves a list of all FTM Chip details created by all the FTM Providers associated with the logged in user. It is configured for the roles <strong>FTM_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail</td><td>PUT</td><td>Service to update ftp chip detail</td><td>This endpoint has been deprecated since the release-1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail</td><td>POST</td><td>Service to save ftp chip detail</td><td><ol start="1"><li>Improved the validation check by trimming extra spaces in make and model to prevent duplicate entries. (<a href="https://mosip.atlassian.net/browse/MOSIP-35788">MOSIP-35788</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail</td><td>PATCH</td><td>Service to approve/reject ftp chip detail</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/{ftmId}</td><td>PATCH</td><td>This endpoint deactivates the ftp chip detail based on the ftp chip detail Id. It is configured for the roles <strong>FTM_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/{ftmId}/certificate-data</td><td>GET</td><td>This endpoint fetches both the CA signed certificate uploaded by the FTM Chip Provider and the MOSIP signed certificate generated by PMS. It is configured for the roles <strong>FTM_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/getPartnerCertificate/{ftpChipDetailId}</td><td>GET</td><td>Service to get certificate of ftp chip</td><td>Improved Key Manager error handling, to capture the correct error code from Key Manager and send it in the endpoint’s response.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/search</td><td>POST</td><td>Service to search ftp chip details</td><td><ol start="1"><li>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /ftpchipdetail/v2 endpoint.</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/uploadcertificate</td><td>POST</td><td>Service to upload certificate of ftp chip</td><td><ol start="1"><li>Added validation to allow certificate upload only if the FTM chip details certificate status is <strong>APPROVED</strong> or <strong>PENDING_CERT_UPLOAD</strong>.(<a href="https://mosip.atlassian.net/browse/MOSIP-36283">MOSIP-36283</a>). So for Rejected or Deactivated FTM, a certificate cannot be uploaded.</li><li>Improved Key Manager error handling, to capture the correct error code from Key Manager and send it in the endpoint’s response.</li><li>Set isActive to false after certificate re-upload. This will ensure that after cert is reuploaded, partner admin will have to approve the FTM again. (<a href="https://mosip.atlassian.net/browse/MOSIP-36285">MOSIP-36285</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/ftpchipdetail/v2</td><td>GET</td><td>This endpoint retrieves a list of all FTM Chip details created by all the FTM Providers. Also supports pagination, sorting, and filtering. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/admin-partners</td><td>GET</td><td>This endpoint retrieves a list of all Partners. Also supports pagination, sorting, and filtering. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td><p>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</p><ul><li>Disabled sorting on the email_id column due to encryption-related limitations.</li><li>Modified filtering behavior for the email_id column: now supports only exact match filtering; partial or "contains" search is no longer supported.</li></ul></td></tr><tr><td>/admin-partners/{partnerId}</td><td>GET</td><td>This endpoint retrieves all the details of the Partner based on Partner Id. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partner-api-keys</td><td>GET</td><td>This endpoint retrieves a list of all the API keys created by the Auth Partners. Also supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the <strong>PARTNER_ADMIN</strong> role, then it will fetch all the API keys created by all the partners associated with the logged in user only. If the token used to access this endpoint, has <strong>PARTNER_ADMIN</strong> role, then it will fetch all the API keys created by all the partners.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partner-policy-requests</td><td>GET</td><td>This endpoint fetches list of all the policy requests made by the partners. Also supports pagination, sorting, and filtering based on optional query parameters. If the token used to access this endpoint, does not have the <strong>PARTNER_ADMIN</strong> role, then it will fetch all the policy requests made by all the partners associated with the logged in user only.If the token used to access this endpoint, has <strong>PARTNER_ADMIN</strong> role, then it will fetch all the policy requests made by all the partners.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners</td><td>GET</td><td>Service to get partner details</td><td><ol start="1"><li>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.</li></ol></td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/{partnerId}</td><td>PATCH</td><td>Service to activate/de-activate partner</td><td><ol start="1"><li>Added a check to verify if the <strong>partner</strong> is already deactivated. If yes, partner cannot be deactivated again. (<a href="https://mosip.atlassian.net/browse/MOSIP-37017">MOSIP-37017</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/apikey/{apikey}</td><td>GET</td><td>Service to get policy for given API key</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/apikey/{apikey}/policies</td><td>PUT</td><td>Service to update policies against to API key</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/policy/{policyId}/apikey/status</td><td>PATCH</td><td>Service to activate/de-activate partner API key</td><td><ol start="1"><li>If the API key is already deactivated, it cannot be deactivated again.(<a href="https://mosip.atlassian.net/browse/MOSIP-34430">MOSIP-34430</a>)</li><li>Added a validation to check if the <strong>Partner ID</strong> used in the request body is active. This will ensure that API cannot be deactivated if partner has been deactivated. This validation is skipped if the user’s role is <strong>PARTNER_ADMIN</strong>. (<a href="https://mosip.atlassian.net/browse/MOSIP-34430">MOSIP-34430</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/apikey</td><td>GET</td><td>Service to get API key requests</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/apikey/{apikey}</td><td>GET</td><td>Service to get API key request</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/policy/{mappingkey}</td><td>PUT</td><td>Service to approve/reject partner policy mapping</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/v2</td><td>GET</td><td>Service to get partner details</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/trust-chain-certificates</td><td>GET</td><td>This endpoint retrieves a list of all the Trust Certificates uploaded by the Partner Admin. Also supports pagination, sorting, and filtering. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/trust-chain-certificates/{certificateId}/certificateFile</td><td>GET</td><td>This endpoint will download p7b file for a CA / Intermediate CA certificate along with the trust chain based on Certificate Id. It is configured for the role <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners</td><td>POST</td><td>partner self registration</td><td>No changes made in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/{partnerId}</td><td>GET</td><td>Service to get details of partner</td><td>Corrected the version in the response body</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/{partnerId}</td><td>PUT</td><td>Service to update details of partner</td><td></td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/{partnerId}/apikey/request</td><td>GET</td><td>Service to get API key requests of partner</td><td>Corrected the version in the response body</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/certificate</td><td>GET</td><td>Service to get partner certificate</td><td><ol start="1"><li>Added a check to verify if the partner id in the request exists in the database.(<a href="https://mosip.atlassian.net/browse/MOSIP-37017">MOSIP-37017</a>)</li><li>Added validation to check if the certificate has been uploaded previously.</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/certificate-data</td><td>GET</td><td>This endpoint retrieves both the CA signed certificate uploaded by the partner and the MOSIP-signed certificate generated by PMS. It is configured for role any of the partner type or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/contact/add</td><td>POST</td><td>Service to add additional contact deatils of partner</td><td>No changes made in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/{partnerId}/generate/apikey</td><td>PATCH</td><td>To generate API Key for approved policies</td><td>Added a check to remove extra spaces in the API key label before saving to the database, preventing the creation of duplicate API key labels with extra spaces.(<a href="https://mosip.atlassian.net/browse/MOSIP-35788">MOSIP-35788</a>)</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/policy/map</td><td>POST</td><td>To request for policy mapping</td><td>Updated error messages to indicate if the policy is already mapped and its status is <strong>Approved</strong> or <strong>In Progress</strong>.(<a href="https://mosip.atlassian.net/browse/MOSIP-33803">MOSIP-33803</a>)</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/{partnerId}/policygroup/{policygroupName}</td><td>PUT</td><td>Service to update the policy group for partner</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/apikey/request/filtervalues</td><td>POST</td><td>Service to filter API key requests</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/apikey/request/search</td><td>POST</td><td>Service to search API key requests</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-policy-requests endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/apikey/search</td><td>POST</td><td>Service to search API key</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partner-api-keys endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/certificate/ca/upload</td><td>POST</td><td>Service to upload ca certificate</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/certificate/upload</td><td>POST</td><td>Service to upload partner certificate</td><td><ol start="1"><li>Added a validation to check if the <strong>Partner ID</strong> used in the request body is active. This will ensure that certificate cannot be uploaded if partner has been deactivated. (<a href="https://mosip.atlassian.net/browse/MOSIP-34498">MOSIP-34498</a>)</li><li>If domain is <strong>FTM</strong>, do not call the uploadOtherDomainCertificate endpoint of KeyManager.(<a href="https://mosip.atlassian.net/browse/MOSIP-35797">MOSIP-35797</a>)</li></ol></td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/email/verify</td><td>PUT</td><td>Service to verify partner email</td><td>No changes made in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>/partners/filtervalues</td><td>POST</td><td>Service to filter partner details</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.</td><td><p>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</p><ul><li>Support for email_id<strong>,</strong> contact_no<strong>,</strong> and address fields has been removed due to encryption constraints.</li></ul></td></tr><tr><td>/partners/partner-certificates-details</td><td>GET</td><td>This endpoint retrieves a list of all Partner Certicates uploaded by the logged in user</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/partners/partnerType/search</td><td>POST</td><td>Service to search partner types</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>partners/search</td><td>POST</td><td>Service to search partner details</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /partners/v3 endpoint.</td><td><p>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</p><ul><li>Support for email_id<strong>,</strong> contact_no<strong>,</strong> and address columns has been removed due to encryption constraints.</li></ul></td></tr><tr><td>partners/v2</td><td>POST</td><td>Registers partner details</td><td>No changes made in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>partners/v2/{partnerId}</td><td>PUT</td><td>Service to update details of partner</td><td>No changes made in release 1.2.2.0</td><td>Handled encryption and decryption for PII columns(<a href="https://mosip.atlassian.net/browse/MOSIP-38061">MOSIP-38061</a>)</td></tr><tr><td>partners/v3</td><td>GET</td><td>This endpoint retrieves a list of Partners associated with the logged in user, based on the query parameters. It is configured for role any of the partner type or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/roles</td><td>GET</td><td>Service to get required roles</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface</td><td>GET</td><td>This endpoint retrieves a list of all SBIs created by the Device Providers. Also supports pagination, sorting, and and filtering based on optional query parameters. If the token used to access this endpoint, does not have the <strong>PARTNER_ADMIN</strong> role, then it will fetch all SBIs created by all the partners associated with the logged in user only. If the token used to access this endpoint, has <strong>PARTNER_ADMIN</strong> role, then it will fetch all the SBIs created by all the partners.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface</td><td>PUT</td><td>Service to update SecureBiometricInterface</td><td>This endpoint has been deprecated since the release-1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface</td><td>POST</td><td>Service to save SecureBiometricInterface details</td><td>Added a check to remove extra spaces in the SBI version before saving to the database, preventing the creation of duplicate SBI versions with extra spaces.(<a href="https://mosip.atlassian.net/browse/MOSIP-35788">MOSIP-35788</a>)</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface</td><td>PATCH</td><td>Service to approve/reject SecureBiometricInterface</td><td>Added separate error codes for cases when SBI is already <strong>approved</strong> or <strong>rejected</strong>.(<a href="https://mosip.atlassian.net/browse/MOSIP-38973">MOSIP-38973</a>)</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/{sbiId}</td><td>PATCH</td><td>This endpoint deactivates an SBI along with associated Devices. It is configured for the roles <strong>DEVICE_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/{sbiId}/devices</td><td>GET</td><td>This endpoint fetches the list of Devices associated with a given SBI Id. It is configured for the roles <strong>DEVICE_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/{sbiId}/devices</td><td>POST</td><td>This endpoint adds a new Device and creates an inactive mapping between the device and the given SBI. It is configured for the roles <strong>DEVICE_PROVIDER</strong> or <strong>PARTNER_ADMIN</strong>.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/devicedetails/map</td><td>PUT</td><td>Service to map device details with sbi</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new POST /securebiometricinterface/{sbiId}/devices endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/devicedetails/map/remove</td><td>PUT</td><td>Service to remove mapped device details with sbi</td><td>This endpoint has been deprecated since the release-1.2.2.0.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/devicedetails/map/search</td><td>POST</td><td>Service to search mapped device details and SecureBiometricInterface details</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface/{sbiId}/devices endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/filtervalues</td><td>POST</td><td>Service to filter SBI's</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/securebiometricinterface/search</td><td>POST</td><td>Service to search SecureBiometricInterface details</td><td>This endpoint has been deprecated since the release-1.2.2.0. It has been replaced by the new GET /securebiometricinterface endpoint.</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/system-config</td><td>GET</td><td>This endpoint fetches the configurations for PMS and sends them to the UI. No roles are required for access.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/users</td><td>POST</td><td>Service to register user</td><td>No changes made in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/users/user-consent</td><td>GET</td><td>This endpoint fetches the user's consent related to the data captured by PMS. The consent is requested only once after the user's first login, and won't be asked again if already given. It is configured for all Partner Type roles.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/users/user-consent</td><td>POST</td><td>This endpoint saves the user's consent related to data captured by the PMS portal, which is requested only once after the user's first login. Once provided, the consent will not be asked again. It is configured for all Partner Type roles.</td><td>Newly added in release 1.2.2.0</td><td>No changes made in release 1.3.0-beta.1</td></tr><tr><td>/users/{userId}/notifications-seen-timestamp</td><td>GET</td><td>This endpoint which will get the status and timestamp of when the notifications were last viewed by the user in the PMS portal.</td><td>-</td><td>Newly added in release 1.3.0-beta.1</td></tr><tr><td>/users/{userId}/notifications-seen-timestamp</td><td>PUT</td><td>This endpoint which will update the status and timestamp of when the notifications were last viewed by the user in the PMS portal.</td><td>-</td><td>Newly added in release 1.3.0-beta.1</td></tr><tr><td>/notifications</td><td>GET</td><td>This endpoint will get all the notifications from the pms.notifications table. Also supports pagination, sorting, and and filtering based on optional query parameters.</td><td>-</td><td>Newly added in release 1.3.0-beta.1</td></tr><tr><td>/notifications/{notificationId}</td><td>PATCH</td><td>This endpoint will be used to handle the dismiss action by the user.</td><td>-</td><td>Newly added in release 1.3.0-beta.1</td></tr></tbody></table>

Policy Management Service:

| API Path                                           | Method | Description                                                                                                                                                                                                                                                                                                                                                                                                                              | Changes done in release-1.2.2.0                                  | Changes done in release 1.3.0-beta.1    |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | --------------------------------------- |
| /policies                                          | GET    | Service to get policies                                                                                                                                                                                                                                                                                                                                                                                                                  | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies                                          | POST   | Service to create a new authentication, data sharing, or credential policy.                                                                                                                                                                                                                                                                                                                                                              | Handled missing 'Empty Array and Empty String' Schema Validation | No changes made in release 1.3.0-beta.1 |
| /policies/{policyId}                               | GET    | Service to retrieve the details of a specific policy by its ID.                                                                                                                                                                                                                                                                                                                                                                          | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/{policyId}                               | PUT    | Service to update policy details                                                                                                                                                                                                                                                                                                                                                                                                         | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/{policyId}                               | PATCH  | This endpoint deactivates a policy based on the Policy Id. It checks if any policy requests are associated with the policy: it can be deactivated if there are no requests or if there are rejected requests. It cannot be deactivated if there are approved or pending requests, returning error codes PMS\_POL\_063 or PMS\_POL\_064, respectively. This endpoint is configured for the **POLICYMANAGER** or **PARTNER\_ADMIN** roles. | Newly added in release 1.2.2.0                                   | No changes made in release 1.3.0-beta.1 |
| /policies/{policyId}/group/{policygroupId}/publish | POST   | Service to publish policy                                                                                                                                                                                                                                                                                                                                                                                                                | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/active/group/{groupName}                 | GET    | Service to get active policy details for policy group name                                                                                                                                                                                                                                                                                                                                                                               | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/group/{policygroupId}                    | GET    | Service to get policy group                                                                                                                                                                                                                                                                                                                                                                                                              | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/group/{policyGroupId}                    | PATCH  | Service for Partner Admin users to deactivate a Policy Group based on the Policy Group Id. It is configured for the **POLICYMANAGER** or **PARTNER\_ADMIN** roles.                                                                                                                                                                                                                                                                       | Newly added in release 1.2.2.0                                   | No changes made in release 1.3.0-beta.1 |
| /policies/group/new                                | POST   | Service to create a new policy group                                                                                                                                                                                                                                                                                                                                                                                                     | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/group/search                             | POST   | Service to search policy group                                                                                                                                                                                                                                                                                                                                                                                                           | No changes made in release 1.2.2.0                               | No changes made in release 1.3.0-beta.1 |
| /policies/policy-groups                            | GET    | Service to retrieve details about all active Policy Groups                                                                                                                                                                                                                                                                                                                                                                               | Newly added in release 1.2.2.0                                   | No changes made in release 1.3.0-beta.1 |
| /policies/v2                                       | GET    | Service to retrieve the list of all Policies. It is configured for the **POLICYMANAGER** or **PARTNER\_ADMIN** roles.                                                                                                                                                                                                                                                                                                                    | Newly added in release 1.2.2.0                                   | No changes made in release 1.3.0-beta.1 |




-->