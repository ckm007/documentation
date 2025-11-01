Ticket ID - https://mosip.atlassian.net/browse/MOSIP-41464

https://docs.mosip.io/1.2.0/id-lifecycle-management/supporting-components/biometrics/biometric-sdk



The documentation should include sample data illustrating capture request and responses exchanged with the BIOSDK partner. The following scenarios must be covered:





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



