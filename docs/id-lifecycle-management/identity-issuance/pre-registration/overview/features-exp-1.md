# Features

## Overview

The Pre-registration module simplifies the identity registration journey by enabling residents to complete key steps online prior to visiting registration centers. This approach minimizes wait times, improves data quality, and delivers a more convenient experience.

This is broadly achieved through the following key user workflow:

* User enters demographic details and upload supporting documents.
* Book appointments for themselves or multiple applicants by selecting preferred registration centers and time slots.
* Receive notifications about appointment status and updates.
* Reschedule or cancel appointments as needed.

![Pre-Registration Process](../../../../.gitbook/assets/pre-reg-process.png)

After completing these steps, resident data is securely transferred to the chosen registration center ahead of the appointment, expediting the enrollment process. <!-- The module supports multiple languages and offers backend APIs, along with a customizable reference implementation of the [pre-registration portal](#pre-registration-portal). -->


## Core Features

### 1. Login/Account and Application Creation
Residents can access the Pre-registration portal using various login methods, including email or mobile number, ensuring flexibility and convenience for account and application creation. The application creation process includes secure verification and document upload, with each application assigned a unique [AID](../../../identity-management/identifiers.md#rid-aid) for tracking.

#### Application Creation

- **Multi-channel Registration**: Create accounts using email or mobile number.
- **OTP-based Verification**: Secure account verification via OTP sent to email or SMS, with retry options.
- **CAPTCHA Security**: Prevents automated bot registrations.
- **User Consent Management**: Explicit consent for data processing and acceptance of terms.
- **Session Management**: Secure sessions with configurable timeout.
- **Easy Application Creation**: The resident can navigate to the application creation page, enters the required details, reviews the information for accuracy, and submits the application.
- **Document Upload**: Upload supporting documents (e.g., Proof of Address, Birth Certificate).
- **Pre-registration ID Generation**: Each application receives a unique AID for reference.  
  _Note_: The AID was formerly called PRID in the pre-registration context.

#### Family/Group Registration

- **Multiple Applicant Support**: Register multiple family members or individuals in a single session.
- **Add Applicant Functionality**: Easily add new applicants during the registration process.

#### Application Management and Status Tracking

**Application Status Management**

The system tracks each application's progress through distinct status states:

- **Incomplete**: Only demographic details are filled.
  - *Action Required*: Upload documents and book an appointment.
- **Pending Appointment**: Demographic details and documents are completed.
  - *Action Required*: Book an appointment.
- **Booked**: Application is complete with a scheduled appointment.
  - *Action Required*: Visit the registration center on the appointment date and time.
- **Expired**: Appointment date has passed.
  - *Action Required*: Re-book an appointment.
- **Cancelled**: Appointment has been cancelled by the user.
  - *Action Required*: Re-book an appointment.


**Application Dashboard**

- **Chronological Sorting**: Applications are sorted by creation date, with the newest first.
- **Visual Status Indicators**: Each application displays a clear status.
- **Bulk Operations**: Select multiple applicants for group actions.
- **Persistent Storage**: Expired and cancelled applications remain visible for reference and re-booking.

**Application Lifecycle Management**

- **Create New Applications**: Generate multiple applications as needed.
- **Data Modification**: Edit demographic data and documents before booking an appointment.
- **Application Preview**: Review all entered information before final submission.
- **Version Control**: Track changes to maintain data integrity throughout the application lifecycle.


## 2. Appointment Booking
The Appointment Booking allows users to select a registration center using criteria such as postal code or geo-location. Once a center is chosen, available time slots are displayed for scheduling. Users also have the flexibility to cancel or re-book appointments as needed.


### Registration Center Discovery

- **Recommended Centers**: Automatically suggests centers based on demographic details (e.g., postal code).
- **Location-based Search**: Find centers using geo-location with a "Nearby" option.
- **Search Functionality**: Search centers by name, address, or other criteria.
- **Center Information Display**: View details such as working hours and available services for each center.
- **Distance Calculation**: Shows the distance from the user's location to registration centers.
- **Configurable Recommendations**: Customizable location hierarchy for center recommendations.

### Time Slot Management

- **Calendar Interface**: User-friendly calendar displays available dates and booking counts.
- **Time Categorization**: Slots are organized by morning and afternoon sessions (configurable).
- **Real-time Availability**: Live display of available time slots.
- **Capacity Management**: Slot availability is managed based on center capacity.
- **Multi-applicant Booking**: Book appointments for multiple applicants in a single session.

### Appointment Flexibility

- **Rescheduling**: Modify appointment date/time easily, with a configurable minimum notice period (e.g., 48 hours).
- **Cancellation**: Cancel appointments and automatically release slots for others.
- **Booking Confirmation**: Receive instant confirmation with unique appointment details.
- **Time Restrictions**: Minimum time between booking and appointment is configurable.


### 3. Notification and Acknowledgment System

The Notification and Acknowledgment System ensures residents receive timely updates about their pre-registration status and appointments through email and SMS. Upon successful booking, users are provided with an acknowledgment that includes their AID and a QR code, which can be printed or presented digitally at registration centers for efficient processing.

#### Multi-channel Notifications
- **Email Notifications**: Receive appointment confirmations, reminders, and updates via email.
- **SMS Alerts**: Get critical updates and appointment reminders through SMS.

#### Comprehensive Acknowledgment Features
- **Multiple Delivery Options**:
  - Print acknowledgment directly from the portal.
  - Download acknowledgment as a PDF.
  - Send acknowledgment via email to specified addresses.
  - Send acknowledgment via SMS to mobile numbers.
- **Complete Information Package**: Acknowledgment includes PRID/AID and relevant application details.

#### Notification Types
- **Booking Confirmations**: Immediate notification upon successful appointment booking.
- **Status Updates**: Alerts for changes in application status.
- **Document Updates**: Notifications for document upload and validation status.


### 4. Registration Centers Data Integration and Synchronization

At the registration center, residents present their AID or QR code, allowing staff to quickly retrieve and pre-fill registration forms with pre-registration data. This seamless integration streamlines the enrollment process and reduces manual data entry.

#### Registration Center Integration
- **Data Download**: Registration centers can securely download pre-registration data for scheduled appointments.
- **Offline Support**: Enables access to pre-registration data even when the registration center is offline.
- **Data Pre-filling**: Automatically populates registration forms with resident data from pre-registration, reducing manual entry.
- **Status Synchronization**: Ensures bi-directional updates between the pre-registration portal and registration centers for accurate application status tracking.

#### Master Data Integration
- **Dynamic Dropdowns**: Utilizes real-time data from the Master Data service to populate location and center selection fields.
- **Center Information**: Provides up-to-date details on registration centers, including capacity and availability.
- **Holiday Management**: Integrates with holiday calendars to manage appointment slot availability and prevent bookings on non-working days.


## Advanced User Experience Features

### 1. Application Management Operations
- **Discard Applications**: Permanently remove unwanted applications from the dashboard.
- **Cancel Appointments**: Cancel scheduled appointments while retaining the associated application data for future use.
- **Modify Applications**: Edit demographic details and uploaded documents prior to booking or attending appointments.
- **Bulk Selection**: Select and manage multiple applicants simultaneously for group actions such as booking or cancellation.

### 2. Smart Recommendations
- **Automatic Center Suggestions**: Receive recommended registration centers based on postal code and demographic information.
- **Intelligent Slot Management**: View availability patterns and popular time slots to optimize appointment scheduling.


## Security and Privacy Features

### 1. Data Protection

- **Encryption**: All sensitive data is protected with end-to-end encryption throughout the registration process.
- **Audit Logging**: Every user action is recorded to provide a comprehensive audit trail for security and compliance.
- **Data Retention**: Data retention policies are configurable to meet country-specific legal and regulatory requirements.

### 2. Privacy Controls

- **Consent Management**: Users provide granular consent for data usage, ensuring transparency and compliance.
- **Data Anonymization**: The system supports anonymization of personal data where required.
- **Right to Deletion**: Residents can request deletion of their personal data in accordance with applicable privacy regulations.


By allowing residents to submit demographic information and documents online before their appointment, the Pre-registration module streamlines the registration process and reduces the need for manual data entry at registration centers. This not only shortens wait times for individuals but also helps registration centers efficiently manage crowds and resources, particularly during high-volume national ID campaigns.









<!--



### QR Code Generation and Management

#### QR Code Features

- **Unique QR Code**: Each application is assigned a unique QR code containing the pre-registration ID.
- **Comprehensive Data Encoding**: The QR code encodes appointment details and relevant application information for secure and efficient processing.
- **Registration Center Integration**: QR codes can be scanned at registration centers to quickly retrieve and pre-fill resident data.
- **Printable Format**: Acknowledgment documents include an embedded QR code for easy printing and presentation at registration centers.
- **Multi-format Support**: QR codes are available in printable, digital, and shareable formats to suit various user needs.


-->




<!--
## 1. Operation Modes

### Self-Service Mode

The Pre-registration portal supports Self-Service Mode to enhance accessibility and user experience:
- **Independent Registration**: Residents can complete pre-registration themselves using computers, tablets, or smartphones.

### Assisted Mode - <!-- Varaniya - Remove this

- **Operator Assistance**: Trained operators help residents through the registration process.
- **Dual-language Support**: Operators can use the portal in one language while capturing resident data in another.
- **Accessibility Features**: Designed to support users with disabilities or those needing extra assistance.

-->





<!--

## 12. Administrative Features

### Configuration Management

- **UI Specifications**: Configure form fields and document categories using JSON.
- **Business Rules**: Set booking restrictions (e.g., minimum notice period for appointments).

# Varaniya - Remove this
- **Location Hierarchy**: Define center recommendations based on postal codes.
- **Language Settings**: Manage mandatory and optional languages per country requirements.
- **Time Slot Configuration**: Admin controls for appointment slot management.


### System Administration

- **Center Management**: Manage registration center details and capacity.
- **Slot Management**: Monitor and adjust appointment slot availability in real time.
- **Workflow Configuration**: Customize application workflows and approval processes.

### Reporting and Analytics

- **Application Statistics**: Report on application volumes and trends.
- **Center Utilization**: Analyze registration center usage and capacity.
- **Performance Metrics**: Track system performance and user experience.
- **Status Analytics**: Monitor application status distribution and completion rates.




13. Technical Features (Architecture and Integration)

### Microservices Architecture

- **Application Service**: Manages core application workflows and data.
- **Booking Service**: Handles appointment scheduling and management.
- **Datasync Service**: Synchronizes data between the portal and registration centers.
- **Captcha Service**: Provides security verification to prevent automated bot access.
- **Batchjob Service**: Executes background processing and maintenance tasks.

### Integration Capabilities

- **Master Data Integration**: Fetches real-time location and center data from the Master Data service.
- **Registration Center Integration**: Enables bi-directional data synchronization for application status and details.
- **API Gateway Integration**: Facilitates seamless connectivity within the MOSIP ecosystem.
- **Third-party Integrations**: Supports extensibility for connecting with external systems.

### Scalability and Performance

- **Load Balancing**: Ensures high availability and distributes traffic efficiently.
- **Caching**: Implements intelligent caching for faster response times.
- **Database Optimization**: Utilizes optimized data access patterns for improved performance.
- **Resource Management**: Maximizes efficient use of system resources.

### Monitoring and Maintenance

- **Health Checks**: Monitors system health and service availability.
- **Performance Metrics**: Tracks real-time system performance.
- **Error Handling**: Provides robust error detection and recovery mechanisms.
- **Backup and Recovery**: Supports data backup and disaster recovery processes.

-->









<!-- Varaniya - Repeating content

### Application Management Workflow

- **Create Multiple Applications**: Add family members or multiple applicants in one session.
- **Modify Applications**: Edit details before booking an appointment.
- **Cancel/Reschedule**: Manage appointments flexibly, subject to time restrictions.
- **Status Tracking**: Monitor application progress through the dashboard.
- **Discard/Delete**: Remove unwanted applications as needed.

-->


<!-- Keshav - Use this may be in Overview section

## Benefits

### For Residents

- **Convenience**: Complete pre-registration from home or any location.
- **Time Savings**: Reduced waiting time at registration centers.
- **Flexibility**: Schedule appointments at convenient times.
- **Transparency**: Real-time status tracking and notifications.

### For Registration Centers / Operators

- **Efficiency**: Pre-filled forms reduce data entry time.
- **Capacity Planning**: Improved resource allocation and queue management.
- **Data Quality**: Enhanced data accuracy through validation.
- **Reduced Workload**: Less manual data entry and verification.

The Pre-registration module is designed to minimize data updates during registration by enabling residents to submit demographic data in advance. This reduces time spent at registration centers and supports effective crowd management, especially during large-scale national ID drives.

-->


<!--

# Overview
Pre-registration module enables a resident to:

* enter demographic data and upload supporting documents,
* book an appointment for one or many users for registration by choosing a suitable registration center and a convenient time slot,
* receive appointment notifications,
* reschedule and cancel appointments.

Once the resident completes the above process, their data is downloaded at the respective registration centers before their appointment, thus, saving enrollment time. The module supports multiple languages.

MOSIP provides backend APIs for this module along with a reference implementation of [pre-registration portal](#pre-registration-portal).

## Pre-registration process

![Pre-Registration Process](../../../../.gitbook/assets/pre-reg-process.png)

### Create an application

* User provides consent
* The user provides demographic information
* User uploads supporting documents (Proof of Address, Birth certificate, etc.)
* A pre-registration request ID known as [AID](../../../identity-management/identifiers.md#rid-aid) is generated and provided to the user.

_Note_: The AID was formerly called PRID in the pre-registration context.

### Book an appointment

* The user selects a registration center based on postal code, geo-location, etc.
* The available slots are displayed
* An option to cancel and re-book the appointment is made available

### Receiving acknowledgement notifications

* An acknowledgment is sent via email/SMS
* The user can print the acknowledgment containing AID and QR code.
* This QR code can be scanned at the in-person registration centers.

### Download of pre-registration data at registration centers

* The user provides the AID/ QR code at the registration center.
* The registration form gets pre-filled with the pre-registration data.

## Pre-registration module

The relationship of the pre-registration module with other services is explained here.&#x20;

{% hint style="info" %}
**NOTE:** The numbers do not signify a sequence of operations or control flow.
{% endhint %}

![](../../../../.gitbook/assets/pre-reg-entity.png)

1. Fetch [ID Schema](../../../../id-schema) details with the help of Syncdata service.
2. Fetch a new OTP for the user on the login page.
3. Log all events.
4. Pre-Registration interacts with Keycloak via [`kernel-auth-adapater`](https://github.com/mosip/mosip-openid-bridge/tree/release-1.2.0). The Pre-Reg module communicates with endpoints of other MOSIP modules. However, to access these endpoints, a token is required. This token is obtained from Keycloak.
5. The database used by pre-reg.
6. Generate a new AID for the application.
7. Send OTP in the email/SMS to the user.
8. Registration Processor uses reverse sync to mark the pre-reg application as consumed.
9. Registration clients use the [Datasync service](https://github.com/mosip/pre-registration/tree/release-1.2.0/pre-registration/pre-registration-datasync-service) to get the pre-reg application details for a given registration center, booking date, and AID.
10. Request data from the MasterData service to get data for dropdowns, locations, consent forms etc.


## Services

Pre-registration module consists of the following services:

* [Application](https://github.com/mosip/pre-registration/tree/release-1.2.0/pre-registration/pre-registration-application-service)
* [Booking](https://github.com/mosip/mosip-ref-impl/tree/release-1.2.0/pre-registration-booking-service)
* [Batchjob](https://github.com/mosip/pre-registration/tree/release-1.2.0/pre-registration/pre-registration-batchjob)
* [Datasync](https://github.com/mosip/pre-registration/tree/release-1.2.0/pre-registration/pre-registration-datasync-service)
* [Captcha](https://github.com/mosip/pre-registration/tree/release-1.2.0/pre-registration/pre-registration-captcha-service)

For more details, refer to the [Pre-registration repo](https://github.com/pjoshi751/pre-registration/tree/develop).

## Pre-registration portal

MOSIP provides a **reference** implementation of the pre-registration portal that may be customized as per country needs. The sample implementation is available at the [reference implementation repository](https://github.com/mosip/mosip-ref-impl). For getting started with the pre-registration, refer to the [Pre-registration user guide](../test/pre-registration-user-guide.md)

## Build and deploy

To access the build and read through the deployment instructions, refer to the [Pre-registration repo](https://github.com/mosip/pre-registration/tree/release-1.2.0).

## Configurations

For details related to Pre-registration configurations, refer to [Pre-registration configuration](https://github.com/mosip/pre-registration/blob/release-1.2.0/docs/configuration.md).

## Developer Guide

To know more about the developer setup, read the [Pre-registration Developers Guide](https://docs.mosip.io/1.2.0/modules/pre-registration/pre-registration-developer-setup).

## API

Refer to [API Documentation](https://mosip.github.io/documentation/1.2.0/1.2.0.html).

## Source code

[Github repo](https://github.com/mosip/pre-registration/tree/release-1.2.0).

-->










