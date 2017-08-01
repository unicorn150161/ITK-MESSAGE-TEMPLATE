---
title: Messaging Interactions
keywords:  messaging, interactions
tags: [fhir,messaging,interactions]
sidebar: foundations_sidebar
permalink: explore_interactions.html
summary: "ITK Distribution Interactions"
---

{% include custom/search.warnbanner.html %}

{% include custom/messaging_overview.svg %}

## ITK Distribution Interactions Overview ##
This section provides ITK3 implementers with the information required to utilise the ITK Distribution Interactions.

The ITK Distribution provides a consistent standardised approach to message headers, whilst also providing a message handling specification to control the use of infrastructure and business acknowledgement responses through the use of flags.


**Note 1:** When using MESH, additional MESH acknowledgements and responses will be available.  The MESH acknowledgements and responses are not defined in this specification

**Note 2:** Messages are structured in eXtensible Markup Language (XML) only.

The ITK Distribution is based on the [HL7 FHIR STU3 Messaging Implementation] Messaging Implementation and supports multiple interactions. 

----------

## Message Handling Flags ##

Acknowledgement responses can be requested using the message handling as follows:

- *Key* - INFACK / BUSACK
- *Value* - true or false

**Note: When sending a payload bundle the acknowledgement type should be set to "true".**

The following additional message handling specifications are supported:

- *Key* - PID / INTID / SNDSRVC
- *Value* - string

These flags are configured within the [ITK-MessageHeader-1]

---

## RSP-ITK-Send-Message-Payload-1 Interaction ##

This is a generic ITK interaction which may be used when sending payloads for which no specific interaction is defined.

- *Sender:* Sending System
- *Receiver:* Recipient System
- *Message: Wire Format:* [ITK-SendMessagePayload-1]

---

## RSP-ITK-Infrastructure-Acknowledgement-Response-1 Interaction ##

The sending system may request an infrastructure acknowledgement by setting the message handling key to "INFACK" and the value to "true". The recipient system should construct an infrastructure acknowledgement response and return it to the sending system.

- *Sender:* Sending System
- *Receiver:* Recipient System
- *Message: Wire Format:* [ITKInfAckresponse-1]

----------

## RSP-ITK-Business-Acknowledgement-Response-1 Interactions ##

The sending system may request a business acknowledgement by setting the message handling key to "BUSACK" and the value to "true". The recipient system should construct a business acknowledgement response and return it to the sending system.

- *Sender:* Sending System
- *Receiver:* Recipient System
- *Message: Wire Format:* [ITKBusinessAckresponse-1]

----------

## ITK Interaction Diagram ##

This diagram below shows the possible ITK FHIR distribution payload and acknowledgement interactions:

<img src="images/explore/ITKFHIRInteractions.png" style="width:75%;max-width: 75%;">

Note: The arrows only indicate that an interaction may be exchanged based on local or business rules and do not imply any interoperability or connectivity between the systems.

## Example Usage Of Interactions ##

##  Scenario 1 - Incorrectly Formed Payload - Example Interactions ##

This diagram shows an eDischarge document sent from a Hospital system to a GP practice. On receipt of the eDischarge document, the GP system detects a structural error caused by a missing mandatory value in the eDischarge document.  The GP system sends an ITK Infrastructure Acknowledgement Response carrying a code for a "fatal-error" to the Hospital System.  This alerts the hospital that the original eDischarge document was rejected because of some of the content in it, and there is no point in resending it without making the appropriate changes.

<img src="images/explore/ITKFHIRStructuralErrorInteractions.png" style="width:75%;max-width: 75%;">

## Scenario 2 - Patient Not Registered at the GP Practice - Example Interactions ##

The diagram shows the eDischarge document sent from a Hospital system to a GP practice.  On receipt of this eDischarge document, the GP system sends an ITK Infrastructure Acknowledgement Response carrying a code of "OK" to the hospital system, this indicates that the message was delivered to the GP practice. Later that day, the GP system cross checks the details of the patient in that eDischarge Document against it's list of registered patients and detects that the patient's NHS number is not known, indicating that the patient is not registered at this practice. The GP system sends an ITK Business Acknowledgement Response message, containing a series of error codes to inform the Hospital System of the problem, the ITK Business Acknowledgement Response message may carry information such as:  

- A code (error) to indicate the issue is sufficiently important to cause the action to fail.
- A code (business-rule) to indicate the operation failed to pass some business rule, and so could not proceed.
- A code ("41002") describing that the "patient not known here" (indicating "patient record not present in system").
- Text (this patient is not registered at this GP practice) - A human-readable description of the issue.

The hospital system, on receipt of this ITK Business Acknowledgement Response, sends an ITK Infrastructure Acknowledgement Response, to advise the GP practice that the hospital has received the information from the GP practice concerning the fact that the patient is not registered with the GP Practice.

<img src="images/explore/ITKFHIRBusinessErrorInteractions.png" style="width:75%;max-width: 75%;">

[ITK-MessageHeader-1]: ../Profile.ITKSendPayload\itk-messageheader-1.html
[ITKBundle-1]: ../Profile.ITKBundle\Profile.ITKBundle.html
[ITKInfAckResponse-1]: ../Profile.ITKInfAckResponse\Profile.ITKInfAckResponse.html
[ITKBusinessAckResponse-1]: ../Profile.ITKBusinessAckResponse\Profile.ITKBusinessAckResponse.html








