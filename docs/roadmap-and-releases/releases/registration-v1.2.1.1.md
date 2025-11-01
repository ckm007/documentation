# Registration v1.2.1.1

**Release Version:** v1.2.1.1

**Release Type:** Patch Release

**Release Date:** 27th May, 2025

### Overview

This patch release focuses on critical bug fixes related to the Credential Requestor, Registration Processor, and Notification components in the MOSIP platform. The release addresses issues encountered during Update UIN workflows, packet processing, and email notifications. These fixes aim to enhance system stability, correctness in credential generation, and proper notification dispatch.

### Major Highlights/Features

* Ensures correct handling of signature validation during packet processing.
* Fixes issues in credential generation linked to VID in Update UIN workflows.
* Resolves failure in email notifications for CRVS\_DEATH events.

### Bug Fixes

The following bugs have been fixed in this release:

<table><thead><tr><th width="185.921142578125">Ticket ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-40982"><strong>MOSIP-40982</strong></a></td><td>Credential request was not generated for VID during Update UIN flow</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-40984"><strong>MOSIP-40984</strong></a></td><td>Exception was thrown while updating the handle field in Update UIN flow</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-31234"><strong>MOSIP-31234</strong></a></td><td>Packet processing notifications were not received in SMTP after uploading RCF packets</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41135"><strong>MOSIP-41135</strong></a></td><td>Packet signature validation skips during registration processing</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41276"><strong>MOSIP-41276</strong></a></td><td>Packets with invalid signatures were reprocessed instead of being marked as failed</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41277"><strong>MOSIP-41277</strong></a></td><td>Empty signature caused "Index 0 out of bounds" error during upload stage</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41403"><strong>MOSIP-41403</strong></a></td><td>Email notifications failed for CRVS_DEATH due to incorrect process type mapping</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-34070"><strong>MOSIP-34070</strong></a></td><td>Credential Requestor Generator delayed in responding to websub event delivery</td></tr></tbody></table>

### Known Issues

<table><thead><tr><th width="187.96307373046875">Jira Issue</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41556">MOSIP-41556</a></td><td>SMS notifications are not delivered via SMTP when handle is enabled for phone numbers with a '+' prefix.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-41564">MOSIP-41564</a></td><td>Packets with invalid/empty signatures are failing at UPLOAD_PACKET stage instead of the Packet Validation stage.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/MOSIP-28837">MOSIP-28837</a></td><td>Request OTP Notifications are coming in 3 languages, even when preferred lang is only one.</td></tr></tbody></table>

### Repository Released

| Repository     | Tag Released                                                      |
| -------------- | ----------------------------------------------------------------- |
| mosip-config   | [v1.2.4.1](https://github.com/mosip/mosip-config/tree/v1.2.4.1)   |
| id-repository  | [v1.2.2.1](https://github.com/mosip/id-repository/tree/v1.2.2.1)  |
| packet-manager | [v1.2.0.3](https://github.com/mosip/packet-manager/tree/v1.2.0.3) |
| registration   | [v1.2.1.1](https://github.com/mosip/registration/tree/v1.2.1.1)   |

### Compatible Modules

| Module/Repo                 | Compatible Version                                                                               |
| --------------------------- | ------------------------------------------------------------------------------------------------ |
| ID Authentication           | [1.2.1.0](https://github.com/mosip/id-authentication/tree/v1.2.1.0)                              |
| key-manager                 | [1.2.1.0](https://github.com/mosip/keymanager/tree/v1.2.1.0)                                     |
| kernel - core               | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-core)                     |
| kernel-notification-service | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-notification-service)     |
| kernel-idgenerator-service  | [1.2.0.1](https://github.com/mosip/commons/tree/v1.2.0.1/kernel/kernel-idgenerator-service)      |
| kernel-auth-adaptor         | [1.2.0.1](https://github.com/mosip/mosip-openid-bridge/tree/v1.2.0.1/kernel/kernel-auth-adapter) |
| kernel-auth-service         | [1.2.0.1](https://github.com/mosip/mosip-openid-bridge/tree/v1.2.0.1/kernel/kernel-auth-service) |
| kernel-otp-manager          | [1.2.0.1](https://github.com/mosip/otp-manager/tree/v1.2.0.1/kernel/kernel-otpmanager-service)   |

### Documentation

* [MOSIP Documentation](https://docs.mosip.io/1.2.0)
* [QA Report](https://github.com/mosip/test-management/tree/master/Platform%20release/1.2.1.1-PatchRelease)
