---
title: Messages 
keywords:  messaging
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_messages.html
summary: "ITK Distribution Messages"
---

{% include custom/search.warnbanner.html %}

{% include custom/messaging_overview.svg %}

## ITK Send Payload ##

This message is a generic message for sending any payload.

The Bundle consists of the following FHIR Resource Profiles.

- **ITK-Message-Bundle-1** - A NHS Digital Profile of the FHIR Bundle resource.
- **ITK-MessageHeader-1** - A NHS Digital Profile of the FHIR MessageHeader resource.	
- **CareConnect-Practitioner-1** - A CareConnect Profile of the FHIR Practitioner resource 
- **CareConnect-Location-1** - A CareConnect Profile of the FHIR Location resource.
- **CareConnect-Organization-1** - A CareConnect Profile of the FHIR Organization resource.
- **Payload** - Any Resource or Profile. 
- 
## ITK Send Payload Bundle Diagram ##

The diagram shows the referencing between the profiles in the bundle which make up the Send Payload Message.

<img src="images/explore/send_payload_message.png" style="width: 75%;max-width: 75%;"> 

## ITK Send Payload Example ##

<script src="https://gist.github.com/unicorn150161/4cc76d52e3a93ce529efdffcaa487396.js"></script>

## ITK Infrastructure Acknowledgement Response ##

This response message allows systems to acknowledge that a message was received without error at the infrastructure layer or to send infrastructure error information back to the sender of a message. When a message is received without error at the infrastructure layer it may subsequently error later at the business layer.

The Bundle consists of the following FHIR Resource Profiles.

- **ITK-Message-Bundle-1** - A NHS Digital Profile of the FHIR Bundle resource.
- **ITK-MessageHeader-1** - A NHS Digital Profile of the FHIR MessageHeader resource.	
- **CareConnect-Practitioner-1** - A CareConnect Profile of the FHIR Practitioner resource 
- **CareConnect-Location-1** - A CareConnect Profile of the FHIR Location resource.
- **CareConnect-Organization-1** - A CareConnect Profile of the FHIR Organization resource.
- **ITK-OperationOutcome-1** - A NHS Digital Profile of the OperationOutcome resource


## ITK Infrastructure Acknowledgement Bundle Diagram ##
The diagram shows the referencing between the profiles in the bundle which make up the Infrastructure Acknowledgement Response message.

<img src="images/explore/ack_message.png" style="width: 75%;max-width: 75%;"> 

## ITK Infrastructure Acknowledgement Bundle Success Example ##

<script src="https://gist.github.com/unicorn150161/8894acb45610bdebae8b7f18bffea35c.js"></script>

## ITK Business Acknowledgement Response ##

This response message allows systems to acknowledge that a message was received and processed at the business layer without error or to send business error information back to the sender of a message. 

The Bundle consists of the following FHIR Resource Profiles.

- **ITK-Message-Bundle-1** - A NHS Digital Profile of the FHIR Bundle resource.
- **ITK-MessageHeader-1** - A NHS Digital Profile of the FHIR MessageHeader resource.	
- **CareConnect-Practitioner-1** - A CareConnect Profile of the FHIR Practitioner resource 
- **CareConnect-Location-1** - A CareConnect Profile of the FHIR Location resource.
- **CareConnect-Organization-1** - A CareConnect Profile of the FHIR Organization resource.
- **ITK-OperationOutcome-1** - A NHS Digital Profile of the OperationOutcome resource


## ITK Business Acknowledgement Bundle Diagram ##
The diagram shows the referencing between the profiles in the bundle which make up the Business Acknowledgement Response message.

<img src="images/explore/ack_message.png" style="width: 75%;max-width: 75%;"> 


## ITK Business Acknowledgement Bundle Success Example ##

<script src="https://gist.github.com/unicorn150161/6d74aac6b6e7305814f56188ea9b9baa.js"></script>



[ITK Send Payload]: ../Profile.ITKSendPayload/Profile.ITKSendPayload.html
[ITK Infrastructure Acknowledgement Response]: ../Profile.ITKInfAckResponse/Profile.ITKInfAckResponse.html
[ITK Business Acknowledgement Response]: ../Profile.ITKBusinessAckResponse/Profile.ITKBusinessAckResponse.html
