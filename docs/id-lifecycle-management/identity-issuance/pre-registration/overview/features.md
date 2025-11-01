# Features

Pre-registration offers a comprehensive suite of capabilities that simplify and optimize the identity registration journey. By enabling residents to complete few essential steps online—such as entering demographic details and uploading documents to initiate pre-registration—the module reduces wait times and improves data accuracy. Integrated verification mechanisms and secure data handling ensure both user convenience and system integrity.
These set of features collectively address challenges like manual data entry, appointment scheduling bottlenecks, and fragmented communication, resulting in a streamlined, secure, and user-friendly onboarding process for residents.

## Core Features

### 1. Login and Pre-Registration
Residents can access the Pre-registration portal using login methods based on email or mobile number, ensuring flexibility and convenience for application creation.

#### Login
Login allows residents to securely log in and initiate pre-registration for identity issuance using email or mobile number.

- **Multi-channel Registration**: Create accounts using email or mobile number.
- **OTP-based Verification**: Secure account verification via OTP sent to email or SMS, with retry options.
- **CAPTCHA Security**: Prevents automated bot registrations.

#### Pre-Registration
Pre-registration enables residents to initiate identity applications online by entering details, uploading documents, and booking appointments before visiting registration centers.

- **User Consent Management**: Explicit consent for data processing and acceptance of terms.
- **Session Management**: Secure sessions with configurable timeout.
- **Easy Application Creation**: The resident can navigate to the application creation page, enters the required details, reviews the information for accuracy, and submits the application.
- **Document Upload**: Upload supporting documents (e.g., Proof of Address, Birth Certificate).
- **Pre-registration ID Generation**: Each application is assigned a unique Application ID (AID), formerly known as PRID (Pre Registration ID), for secure tracking and reference.
- **Multiple Applicant Support**: Register multiple family members or individuals in a single session.
- **Add Applicant Functionality**: Easily add new applicants during the registration process.

#### Application Management and Status Tracking
Manage and track pre-registration applications with a user-friendly dashboard, status indicators, and lifecycle controls.

**Application Status Management**
Efficiently manage and track the status of pre-registration applications throughout their lifecycle. The system tracks each application's progress through distinct status.

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

A centralized dashboard for residents to view, manage, and track all their pre-registration applications and statuses in one place.

- **Chronological Sorting**: Applications are sorted by creation date, with the newest first.
- **Visual Status Indicators**: Each application displays a clear status.
- **Bulk Operations**: Select multiple applicants for group actions.
- **Persistent Storage**: Expired and cancelled applications remain visible for reference and re-booking.

**Application Lifecycle Management**

Efficiently manage the entire lifecycle of pre-registration applications, from creation and modification to tracking and deletion.

- **Create New Applications**: Generate multiple applications as needed.
- **Data Modification**: Edit demographic data and documents before booking an appointment.
- **Application Preview**: Residents can review all entered information—including demographic details and uploaded documents before final submission to ensure accuracy.
- **Version Control**: Maintain a history of changes to application data, allowing users and administrators to track modifications and preserve data integrity throughout the application lifecycle.
- **Delete Applications**: Permanently delete applications.


## 2. Appointment Booking
The Appointment Booking allows users to select a registration center using criteria such as postal code or geo-location. Once a center is chosen, available time slots are displayed for scheduling. Users also have the flexibility to cancel or re-book appointments as needed.


### Registration Center Discovery
Discover and select registration centers using postal code, location-on-map, or search criteria for convenient appointment booking.

- **Recommended Centers**: Automatically suggests centers based on demographic details (e.g., postal code).
- **Location-based Search**: Find centers using geo-location with a "Nearby" option.
- **Search Functionality**: Search centers by name, address, or other criteria.
- **Center Information Display**: View details such as working hours and available services for each center.
- **Distance Estimation**: Can display a map with nearby registration center indicators on it.

### Time Slot Management
Efficiently manage and book available time slots for identity registration appointments with real-time updates and capacity controls.

- **Calendar Interface**: User-friendly calendar displays available dates and booking counts.
- **Time Categorization**: Slots are organized by morning and afternoon sessions (configurable).
- **Real-time Availability**: Live display of available time slots.
- **Capacity Management**: Slot availability is managed based on center capacity.
- **Multi-applicant Booking**: Book appointments for multiple applicants in a single session.

### Appointment Flexibility
Appointment Flexibility empowers users to easily reschedule or cancel appointments, ensuring adaptability to changing schedules.

- **Rescheduling**: Modify appointment date/time easily, with a notice period which is configurable (e.g., 48 hours).
- **Cancellation**: Cancel appointments and automatically release slots for others.
- **Booking Confirmation**: Receive instant confirmation with unique appointment details.
- **Time Restrictions**: Minimum time between booking and appointment is configurable.
- **Booking or Re-Booking**: While booking or re-booking, only the current or future date and time is displayed.


### 3. Notification and Acknowledgment System
The Notification and Acknowledgment System ensures residents receive timely updates about their pre-registration status and appointments through email and SMS. Upon successful booking, users are provided with an acknowledgment that includes their AID and a QR code, which can be printed or presented digitally at registration centers for efficient processing.

#### Multi-channel Notifications
Stay informed with instant, multi-channel notifications and acknowledgments for every step of your pre-registration journey.

- **Email Notifications**: Receive appointment confirmations, reminders, and updates via email.
- **SMS Alerts**: Get critical updates and appointment reminders through SMS.

#### Comprehensive Acknowledgment Features
A single, unified system for delivering secure, real-time notifications and digital acknowledgments to residents throughout the pre-registration process.

- **Multiple Delivery Options**:
  - Print acknowledgment directly from the portal.
  - Download acknowledgment as a PDF.
  - Send acknowledgment via registered email.
  - Send acknowledgment via SMS to the registered mobile numbers.
- **Complete Information Package**: Acknowledgment includes AID and relevant application details.

#### Notification Types
The Notification and Acknowledgment System delivers timely updates and confirmations to residents throughout the pre-registration process via email and SMS.

- **Booking Confirmations**: Immediate notification upon successful appointment booking, re-booking and cancellation.
- **Status Updates**: Alerts for changes in application status.
- **OTP Notifications**: OTPs for login.


### 4. Registration Centers Data Integration and Synchronization

At the registration center, residents present their AID or QR code, allowing staff to quickly retrieve and pre-fill registration forms with pre-registration data. This seamless integration streamlines the enrollment process and reduces manual data entry.

#### Registration Center Integration
Pre-registration integrates directly with the [Registration Client](../../../identity-issuance/registration-client/overview/README.md), allowing registration centers to securely access and download resident data for scheduled appointments. This streamlines registration and minimizes manual data entry.

- **Data Download**: Registration centers can securely download pre-registration data for scheduled appointments.
- **Offline Support**: Enables access to pre-registration data even when the registration center is offline.
- **Data Pre-filling**: Automatically populates registration forms with resident data from pre-registration, reducing manual entry.

#### Master Data Integration
Integrates real-time master data to ensure accurate, up-to-date information for location selection, center details, and appointment scheduling.

- **Dynamic Dropdowns**: Utilizes real-time data from the Master Data service to populate location and center selection fields.
- **Center Information**: Provides up-to-date details on registration centers, including capacity and availability.
- **Holiday Management**: Integrates with holiday calendars to manage appointment slot availability and prevent bookings on non-working days.

## Security and Privacy Features
The following section describes the security and privacy measures that protect resident data throughout the pre-registration process.

### 1. Data Protection
Pre-registration enables secure and efficient online identity onboarding.

- **Encryption**: All PI data is protected with end-to-end encryption throughout the registration process.
- **Audit Logging**: Every user action is recorded to provide a comprehensive audit trail for security and compliance.

### 2. Privacy Controls
Pre-registration ensures secure, privacy-focused handling of resident data with robust consent and anonymization controls.

- **Consent Management**: Users provide granular consent for data usage, ensuring transparency and compliance.
- **Data Anonymization**: Personal data is anonymized as per regulatory requirements, ensuring that sensitive information is masked or removed when not needed for processing. This protects resident privacy and supports compliance with data protection standards.
- **Right to Deletion**: Residents can request deletion of their personal data in accordance with applicable privacy regulations.

## Advanced User Experience Features

### 1. Smart Recommendations
- **Automatic Center Suggestions**: As mentioned above with [Registration Center Discovery](#registration-center-discovery), Pre-reg can also let a user find the recommended registration centers based on postal code and demographic information. This enhances user experience by eliminating the need to manually search in the portal for registration centers.
- **Locate-On-Map**: Users can easily find the nearest registration centers on an interactive map.
- **Safe Date Selection while Booking and Re-booking**: The system prevents users from selecting past dates during booking or re-booking, reducing manual errors.