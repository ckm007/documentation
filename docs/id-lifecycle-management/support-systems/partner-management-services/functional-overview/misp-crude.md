# MISP Partner Onboarding

Coming Soon

<!-

### Overview

This guide shows how Partner Admins can onboard a **MISP Partner** in PMS, manage their **Partner Certificates**, link a **Policy Group**, and generate/manage **MISP License Keys** from the **PMS portal**. Use this as the "how-to" that operators will follow on the live system.

### Prerequisites (Before you begin)

1. You must be logged in with **Partner Admin** credentials (role: PARTNER ADMIN).
2. Root and Intermediate CA certificates should already have been uploaded to the PMS **Certificate Trust Store** (these are required before uploading partner CA-signed certificates).
3. Policy Manager must have created the required **Policy Group** and MISP policies (so they can be selected later). See the Policy Group & MISP Policy creation docs- [Policy Manager](policy-manager#policies)

<!-- Change the links above -->


### Navigation where to start

1. Log into the PMS portal with your Partner Admin account.
2. From the left navigation panel or dashboard itself, click on **Partners** card. You will be redirected to 'List of Partners' page (tabular view).

![](../../../../.gitbook/assets/misp-image1.png)


### Create a new MISP Partner

1. On the _Partners_ tabular screen, click **Create Partner** button placed on top-right (if partner records already exist) or positioned at the centre of the screen (if no records exist)

![](../../../../.gitbook/assets/misp-image2.png)

2. In the **Create Partner** form:
   * Partner Type = MISP is already pre-selected.
   * Enter Address, Organization Name, Email Address, and other mandatory fields. Selecting a Policy Group is optional but highly recommended before proceeding.

> Note: Ensure the Organization name matches the one in the CA-signed certificate that will be uploaded later.

![](../../../../.gitbook/assets/misp-image3.png)

3. Click **Save/Submit**. A confirmation message appears on successful creation.

![](../../../../.gitbook/assets/misp-image4.png)

4. In the 'Success/Confirmation' screen, you are provided with an option to upload CA-Signed partner certificate or return to 'Home page'.

> ![](../../../../.gitbook/assets/misp-image5.png)



### 5. Upload CA-signed Partner Certificate (First time upload)

Either you can upload the partner certificate soon after MISP partner creation as per above steps or In the 'List of Partners' page, locate the newly created MISP Partner(inactive status) and choose **Upload Certificate** from the action menu.

![](../../../../.gitbook/assets/misp-image6.png)


1. The **Upload Partner Certificate** popup opens. Click the upload area and select the CA-signed certificate file from local folder in `.cer` or `.pem` format.

> ![](../../../../.gitbook/assets/misp-image7.png)

2. Verify the certificate details auto-populated (Issuer, Validity, etc.) and click **Submit**.

> ![](../../../../.gitbook/assets/misp-image8.png)

3. On success, admin receives a confirmation and the partner row should show the certificate upload date/status along with status= ACTIVE.
   1. ![](../../../../.gitbook/assets/misp-image9.png)



> **Note**:

* If Root/Intermediate CA is missing, the system will reject the upload --- ensure CA certificates are uploaded first. [MOSIP Docs](https://docs.mosip.io/1.2.0/id-lifecycle-management/support-systems/partner-management-services/functional-overview/partner-administration#certificate-trust-store)




### 6. Re-Upload Partner Certificate (Replacing an existing cert)

**Goal:** Replace previously uploaded certificate (e.g., when expiring or after re-issue).


1. From Partners table action menu, select **Re-Upload Certificate**.
   
<!-- Screenshot placeholder -->

2. Follow the same upload flow as in Step 5 and click **Submit**.
3. The new certificate details and updated certificate status is displayed in the Partners list.

<!-- Screenshot placeholder -->



### 7. Select Policy Group (one-time assignment)

Assign a Policy Group to the MISP Partner 

> Note: Recommended before generating license keys.

1. From the Partners action menu, choose **Select Policy Group** (if it wasn't set during creation).

> ![](../../../../.gitbook/assets/misp-image10.png)

2. The popup lists available Policy Groups; pick the appropriate one for the partner.

> ![](../../../../.gitbook/assets/misp-image11.png)

3. Click **Submit**

> Note: 

* The user will not be able to modify the policy group selection after submit.

* Selecting a policy group and policy is optional but strongly recommended prior to license key generation.



### 8. Partner Policy Linking (requesting and approving MISP policies)


1. Navigate to **Partner Policy Linking** (dashboard card or left menu).

> ![](../../../../.gitbook/assets/misp-image12.png)

2. Click on Request policy button to request for a relavant policy within an already selected policy group against the MISP partner ID.

> ![](../../../../.gitbook/assets/misp-image13.png)
>
> ![](../../../../.gitbook/assets/misp-image14.png)

3. After requesting policy, approve the requests

> ![](../../../../.gitbook/assets/misp-image15.png)

4. View details to inspect the mapping and comments before acting.

**Success check:** Approved partner-policy links will appear in the partner's policy list.




### 9. MISP Services --- Generate MISP License Key

**Goal:** Generate the MISP License Key for a selected policy and partner.


1. Open the **MISP Services** card (from dashboard) or navigate to **MISP Services → Generate MISP License Key**.

> ![](../../../../.gitbook/assets/misp-image16.png)
>
> ![](../../../../.gitbook/assets/misp-image17.png)

2. On the **Generate MISP License Key** page:
   * Select **Partner ID** (Dropdown shows only MISP partners with uploaded certificates).
   * Policy Group auto-populates (based on Partner ID).
   * Choose **Policy Name** (only approved & active policies show).
   * Enter **MISP License Key Name** (Unique, 1--128 chars).

> ![](../../../../.gitbook/assets/misp-image18.png)

3. Click **Submit**. A popup displays the newly generated MISP License Key (visible only once).
   * Copy the key (Use **Copy** button). The UI may show "Copied" briefly.

> ![](../../../../.gitbook/assets/misp-image19.png)

4. Close popup → success message screen appears. Use **Go Back** to view the tabular list.

**Important:** The license key value is displayed only once - ensure you copy and store it securely.


### 10. Tabular View - MISP License Keys (list and filters)

**Goal:** Review, sort, filter, and act on existing license keys.


1. Navigate to **MISP Services → Tabular View**.

> ![](../../../../.gitbook/assets/misp-image20.png)

2. Use **Filters** (Partner ID, Policy Group, Policy Name, Name, Status) to narrow results; **Reset Filter** clears filters.

> ![](../../../../.gitbook/assets/misp-image21.png)![](../../../../.gitbook/assets/misp-image22.png)

3. Columns include: Partner ID, Policy Group, Policy Name, License Key Name, Created Date, Status and Action
4. Click a row or **View** in the action menu to see details. (Deactivated records appear greyed out.)



### 11. Regenerate MISP License Key

**Goal:** Create a new license key in place of an existing one.


1. From the tabular view select the target license key and choose **Regenerate**.

> ![](../../../../.gitbook/assets/misp-image23.png)

2. A regeneration form opens with read-only fields and editable **Name** and **Validity**.

> ![](../../../../.gitbook/assets/misp-image24.png)

3. Submit → popup shows the new key (visible only once). Copy and store securely.

> ![](../../../../.gitbook/assets/misp-image25.png)



### 12. Deactivate License Key

**Goal:** Deactivate an active license key so it can no longer be used for authentication.


1. In the License Keys table, open the action menu for the active key and select **Deactivate**.

> ![](../../../../.gitbook/assets/misp-image26.png)

2. Confirm the deactivation on the popup.

> ![](../../../../.gitbook/assets/misp-image27.png)

3. On success, the row becomes **Deactivated** and is greyed out; only **View** remains in the action menu.



### 13. Deactivate Partner

**Goal:** Deactivate the entire MISP Partner (prevents future requests & license generation).


1. From Partners list, open the action menu → **Deactivate Partner**.

> ![](../../../../.gitbook/assets/misp-image28.png)

2. Confirm and note the consequences (partner cannot request policies or generate license keys).