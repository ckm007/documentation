# Features

The key features of the Authentication Partner and the Partner Management System are below.

### Ease of Use and Usability Enhancements

### Self-registration

A Partner can self-register with much of the process as automated with the least manual intervention.

### Interface / User Experience

For its user part, the new interface of PMP has undergone a complete revamp not only on UI but the UX been worked upon from the ground up. The select few points from the UX enhancements are as below:

* Card view presentation – You now get ‘Partner User Dashboard’ and this offers a Card view presentation for each functionality with a brief/one-liner description to help you understand the services offered in:
* User Profile - The user can view his organization name and username on the top right, the user dropdown on the top right- has two options: User Profile and Logout.

### Partner Admin Features

#### Admin dashboard

Refreshed new user experience to the Admin dashboard which now has structured the high-level functionalities with the help of cards that are ordered logically on the dashboard.

* The dashboard displays the cards for **Certificate Trust Store**, **Partners, Policies**, **Parter Policy-Linking**, **SBI-Device**, **FTM Chip,** and **Authentications Services**.
* It also displays the pending requests count for Partner Policy-Linking, SBI-Device, and FTM Chip.

Note: For devices that are orphaned without an associated SBI, the partner admin will only have the option to Reject.


#### Certificate Trust Store

Upload, Download, or View (List View and Detailed view) of Root and Intermediate Certificates.

#### Partners

Download (Original & MOSIP Signed Certificate), Deactivate Partner or View (List and Detailed View)

#### Policies

You can use this section for Policy Group and Policy related operations enlisted here:

* Create **Policy Group**
* Create **Policy**
  * Authentication Policy
  * Datashare Policy
* **Clone Policy** in Different Policy Groups
* **Publish** Policy in draft status
* **Edit** Policy in draft status
* **View**
  * **List View**
  * **Detail View**
* **Deactivate** Policy Group (if no active policy is linked)
* **Deactivate** Policy (if no active partner policy mappings)

#### Partner Policy Linking

Approve / Reject or View (List View and Details View)

#### Partner Certificate

* Upload and Re-upload: Easily upload or re-upload Certificate Authority (CA) signed Partner Certificate.
* Download: Download CA signed Partner Certificate and corresponding MOSIP Signed Certificate.

Note:

* API Key gets auto deactivated after its expiry.

* API Key expiration duration can be configured : Newly generated API keys should be set to 100 years of expiration duration by default, since the time of its creation. But an admin-level configuration (via config file) allows setting the API key expiration duration in days (such that it can accommodate months/years too). But please note that existing API keys (created before this feature) remains unaffected.

### Partner Type Feature

#### User Access Features

* Login: Existing Partner who has already registered can login to the portal with email/username and password.
* Retrieve Password / Forgot Password: Partner will have the option to reset the password using the Forget Password option.

#### Key Feature of Authentication Partner

Features discussed here are provided only for Partner Type which is Authentication Partner.

* Policies - Request Policy, View, Select Policy Group
* Enable Authentication mechanisms for approved policies
* API Key:
  * Generate API Key: Create API Keys for approved policies.
  * View API Key Details: View a tabular list and individual details of submitted API Keys.
  * Deactivate: Deactivate API Keys when necessary.
* OIDC Client
  * Create OIDC Client: Create OIDC Clients for approved policies.
  * View OIDC Details: Access a tabular list and individual views of submitted OIDC Client details, including OIDC Client IDs.
  * Edit: Edit existing OIDC Client details.
  * Deactivate: Deactivate OIDC Client whenever needed.

#### The key features of the Device Provider

* **Partner Certificate**
  * **Upload and Re-upload:** Easily upload or re-upload Certificate Authority (CA) signed Partner Certificate.
  * **Download:** Download CA signed Partner Certificate and corresponding MOSIP Signed Certificate.
* **Device Provider Services**
  * **SBI - Device Creation:** Add SBI, Add Devices associated to an SBI. SBI / Device submissions will go to Partner Admin for approval.
  * **Deactivate:** Deactivate SBI or Deactivate mapped devices
  * **View** SBI and its associated devices

Note: SBI gets auto deactivated along with its associated devices after SBI expiry.

#### The key features of FTM Chip Provider

* **Partner Certificate**
  * **Upload and Re-upload:** Easily upload or re-upload Certificate Authority (CA) signed Partner Certificate.
  * **Download:** Download CA signed Partner Certificate and corresponding MOSIP Signed Certificate.
* **FTM Chip Services**
  * **FTM Chip details:** Add FTM details, and deactivate FTM details.
  * **FTM Chip Certificate:** Upload, Re-upload, or download certificate.

### Receive Notifications via PMS portal and email

Users receive timely notifications through both the PMS portal and email regarding the upcoming expiry of certificates (Root/ Intermediate CA Certificate, Partner Certificate, FTM Chip Certificate), API Key and SBI linked to the Partner Management System (PMS).

#### Notification Details

* **Notification Channels**
  * Email
  * PMS Portal notifications
* **Recipients**
  * **Partner Admins**
    * Receive notifications about the expiry of all **Root / Intermediate CA certificates** (regardless of who uploaded them) which is set to expire in next 30 days.
    * Receive a **weekly summary** listing partners whose partner certificates, FTM Chip Certificates, API Keys and SBIs are expiring in the next 7 days.
    * Receive individual notifications before the expiry of:
      * Root CA Certificates
      * Intermediate CA Certificates
  * **Partner Users**
    * Receive notifications for partner certificates they personally uploaded.
    * Notifications are specific to their uploaded partner certificates or corresponding MOSIP signed certificates expiring within the next 30 days.
    FTM Chip Providers receive notifications for FTM Chip Certificates they have personally uploaded that are expiring within the next 30 days.
  * Device Providers receive notifications for SBIs they have created that are expiring within the next 30 days.
  * Authentication Partners receive notifications for API Keys they have generated that are expiring within the next 30 days.

#### Notification Schedule

* **For Individual Certificate (Root CA/ Intermediate CA/ Partner Certificate / FTM Chip Certificate, API Key and SBI) Expirations:**
  * 30 days before expiry
  * 15 days before expiry
  * Daily reminders starting from 10 days before expiry up to the expiry date (i.e., from Day - 10 to Day 0).
* **For Weekly Summary Notifications (for Partner Admins)**
  * Sent every 7 days.
  * Lists all partner certificates expiring within the next 7 days.
  * The next weekly notification triggers only after another 7 days.

#### Notification Language Handling

* **Email Notifications**
  * Sent in the language selected by the user during registration (partner/partner admin).
* **PMS Portal Notifications**
  * Displayed in the language selected at the time of login, regardless of the user’s registration language preference.

#### Notification Retention

* Notifications in the PMS portal older than **60 days** are **automatically deleted**.

### Audit Logging for Certificates, API Key, SBI Expiry Notifications

To enhance traceability, PMS now captures audit logs for all certificate expiry-related notifications, including those shown on the portal and sent via email. Notifications for Root CA, Intermediate CA, Partner, FTM Chip Certificates & API Keys, SBIs—as well as the Weekly Summary of partner certificates, FTM Chip Certificates, SBIs, API Keys sent to Partner Admins—are tracked for both success and failure events. Each event is recorded in the audit.app_audit_log table with a unique event ID and reference details. The logs include metadata such as module name, notification ID, and type. The feature ensures greater transparency and accountability in certificate lifecycle communication.

In case of weekly summary notifications, audit logs are generated regardless of whether any partner-specific items—such as FTM Chip Certificates, SBI, Partner Certificates, or API Keys—are expiring (or not) in a given week. This includes logging events where no expiry notifications are triggered, ensuring consistent traceability for all weekly notification cycles, even if the system determines that there are no expiring items for the period.

## Browser Support

* Complete support on Chrome, Firefox, Edge, and Safari ensures a seamless user experience across these popular browsers.

## Language Support

* Currently supports English, French, and Arabic with plans to incorporate additional languages in future releases.

## Compatibility

* Optimized for standard browser sizes (laptop/desktop/extra large screen) with responsive UI design for laptop/desktop views.
