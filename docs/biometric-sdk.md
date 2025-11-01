# Biometric SDK

## Overview

![](\_images/sdk.png)

## Applications

* Registration Client.
* Backend quality check.
* Biometric authentication during onboarding (internal auth).
* ID Authentications.

## Biometric SDK library

The library is used by [Registration Client](registration-client.md) to perform 1:N match, segmentation, extraction etc. For more information on integration with Registration Client, refer to [Registration Client Biometric SDK Integration Guide](registration-client-sdk-integration.md).

A simulation of this library is available as [Mock BioSDK](https://github.com/mosip/mosip-mock-services/tree/release-1.2.0/mock-sdk). The same is installed in the [MOSIP sandbox](sandbox-details.md).

## Biometric SDK service

For 1:1 match and quality check of biometrics at the MOSIP backend, the BioSDK must be running as a service that can be accessed by [Registration Processor](registration-processor.md) and [IDA Internal Services](id-authentication-services.md#internal-services). The service exposes REST APIs specified [here](biometric-sdk.md#api).

A [simulation (mock) service](https://github.com/mosip/biosdk-services/tree/release-1.2.0) has been provided. The mock service loads [mock BioSDK](https://github.com/mosip/mosip-mock-services/tree/release-1.2.0/mock-sdk) internally on the startup and exposes the endpoints to perform 1:N match, segmentation, extraction as per [IBioAPI](https://github.com/mosip/commons/blob/release-1.2.0/kernel/kernel-biometrics-api/src/main/java/io/mosip/kernel/biometrics/spi/IBioApi.java).

The service may be packaged as a docker running inside [MOSIP Kubernetes cluster](https://github.com/mosip/mosip-infra/blob/release-1.2.0/deployment/v3/cluster/README.md) or running separately on a server. It is important that the scalability of this service is taken care depending on the load on the system, i.e., the rate of enrolment and ID authentication.

## API

1. BioSDK library: [IBioAPI](https://github.com/mosip/commons/blob/release-1.2.0/kernel/kernel-biometrics-api/src/main/java/io/mosip/kernel/biometrics/spi/IBioApi.java).
2. BioSDK service: TBD.

## Testing kit

BioSDK server request/response may be tested using [BioSDK testing kit](https://github.com/mosip/biosdk-testing-kit.git).

## Configuration

The following properties in [`application-default.properties`](biometric-sdk.md) needs to be updated to integrate the BioSDK library and service with MOSIP.

```
mosip.fingerprint.provider=io.mosip.kernel.bioapi.impl.BioApiImpl
mosip.face.provider=io.mosip.kernel.bioapi.impl.BioApiImpl
mosip.iris.provider=io.mosip.kernel.bioapi.impl.BioApiImpl
mosip.ida.biosdk-service.url=http://mock-biosdk-service.default:80
mosip.regproc.biosdk-service.url=http://mock-biosdk-service.default:80
mosip.idrepo.biosdk-service.url=http://mock-biosdk-service.default:80
```


<!--



Ticket ID - https://mosip.atlassian.net/browse/MOSIP-41464

https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/biometrics/biometric-sdk



Normal Packets


All biometric modalities are successfully captured and present in the packet.

Partial Exceptions

One or more modalities containing exceptions.  Sample is give only for eyes. The same format applies to fingers as well.

Total Exceptions

The entire modality being marked as an exception in a packet. Sample is give only for eyes. The same format applies to fingers as well.

Corresponding sample files(SampleRequests&Responses.zip) are attached for reference and must be included in the documentation accordingly.

In the response payload, if the biometric extraction is successful, the values for the following fields should be updated accordingly:

"level": "PROCESSED"

"purpose": "VERIFY"

These changes reflect the successful completion of the extraction process and should be documented appropriately.

If the SDK encounters an error, it should return the error details in the following structured format:

"errors": [
  {
    "code": "ERR001",
    "message": "Invalid request data"
  }
]


-->