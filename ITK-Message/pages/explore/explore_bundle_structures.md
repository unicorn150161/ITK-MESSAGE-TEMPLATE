---
title: Bundles Structure
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_bundle_structures.html
summary: "The structures of the bundles used in the messages"
---

{% include custom/search.warnbanner.html %}

{% include custom/messaging_overview.svg %}

## Background ##
To enable a standardised structure to carry information regarding common end-to-end distribution requirements, two profiles have been defined, the ITK Message Bundle and the ITK Message Header that combine to make up the ITK Distribution Bundle. 

The ITK Distribution Bundle may be used to wrap any payload. This provides a lightweight structure to carry information relating to the end-to-end technical distribution of payloads.
The ITK Distribution Bundle is an autonomous and transport agnostic design, whilst enabling audit, access control and authentication as required by both sender and receivers. Some extensions have been added the the ITK Message Header profile to allow a similar functionality to the previous versions of ITK. 

This specification also defines an Infrastructure Acknowledgement and a Business Acknowledgement which may be used with the ITK Distribution Bundle.

## The ITK Distribution Bundle ##

The diagram below shows a schematic of the basic ITK Distribution Bundle structure.

<img src="images/explore/ITKBundle.png" style="width:50%;max-width: 50%;">

The ITK message bundle is the container for the ITK message header and any payload. The message header contains information that pertains to the payload content. The Payload can be anything.


## Example Payload Structures ##


## COFE Document Structure Example ##

The diagram below is an example of a ITK FHIR document payload that may be used with the ITK Distribution Bundle. When sending FHIR Documents the is a bundle of type document.

<img src="images/explore/ITKDocExample.png" style="width:50%;max-width: 50%;">

## Infrastructure Acknowledgement Example ##

The diagram below is an example of an Infrastructure Acknowledgement for a valid response. There is no actual payload as all the information is carried in the message header resource when there are no errors. When there are errors the structure is the same as the Business Acknowledgement. 
 
<img src="images/explore/INFExample.png" style="width:50%;max-width: 50%;">


## Business Acknowledgement Example ##

The diagram below is an example of a Business Acknowledgement that may be used with the ITK message bundle. 

<img src="images/explore/BUSExample.png" style="width:50%;max-width: 50%;">











