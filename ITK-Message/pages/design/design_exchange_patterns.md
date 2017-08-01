---
title: Exchange Patterns
keywords: design, build
tags: [design, build]
sidebar: foundations_sidebar
permalink: design_exchange_patterns.html
summary: "The Exchange Patterns introduce the three ways of exchanging FHIR Resources using RESTful API, messaging and documents."
---

{% include custom/search.warnbanner.html %}

## Exchange Paradigms ##

This section has been included to show the types of exchange patterns and how these ways of exchanging FHIR resources relates to Information Sharing Patterns.

The exchange patterns are complimentary, each having it's strengths and weaknesses. The best solution will probably to use a combination of pattern.

**Note: for ITK3 only Messaging or Documents can be used.  **

## RESTful API


Manipulate data held in a remote system while avoiding direct coupling to remote procedures.

Many web services use messages to form their own domain-specific APIs. These messages incorporate common logical commands like Create, Read (i.e. Get), Update, or Delete (CRUD). Also across the health and social care domain, we have many common entities such as Patient, Practitioner, Organisation, etc. For example, many systems will implement an API that allows you to search for Patients by their NHS Number, maybe called GetPatient, QueryPatient, CreatePatient, etc.

Rather than implementing a system specific API, we could utilise standards defined in the HTTP specification (i.e. GET, POST, etc) and standarise how we return the payload.

So rather than a wide variety of GetPatient, QueryPatient we have:

<table width="60%">
    <tr>
        <td>
            <b>GET Request</b>
        </td>
        <td>
            <b>Response (server)</b>
        </td>
    </tr>
    <tr>
        <td>
            URI
        </td>
        <td>
            FHIR Resource <br> E.g. Patient
        </td>
    </tr>
</table>

<table width="60%">
    <tr>
        <td>
            <b>POST/PUT Request</b>
        </td>
        <td>
            <b>Response (server)</b>
        </td>
    </tr>
    <tr>
        <td>
            URI + FHIR Resource <br> Patient
        </td>
        <td>
            FHIR Resource <br> E.g. OperationOutcome
        </td>
    </tr>
</table>

<table width="60%">
    <tr>
        <td>
            <b>DELETE Request</b>
        </td>
        <td>
            <b>Response (server)</b>
        </td>
    </tr>
    <tr>
        <td>
            URI
        </td>
        <td>
            FHIR Resource <br> E.g. OperationOutcome
        </td>
    </tr>
</table>


This type of interface may also be called as **ResourceAPI** and is useful for real time applications and mobile/web based access.

**Benefits**
- Mobile and web application friendly, can be reused for messaging simplifying interfacing.
- Quick to develop
- Real Time Systems
- Uses modern web technologies
- Can be used with modern security and consent technologies ([OAuth2](https://oauth.net/2/), [OpenID](http://openid.net/what-is-openid/), [SMART on FHIR](http://docs.smarthealthit.org/))

**Concerns**
- Less suitable for large transfers of data between organisations and large systems.

### Information Sharing Patterns ###

<table width="80%">
<tr>
<td>
  <a href="http://developer.nhs.uk/library/architecture/integration-patterns/portal/"><img class="alignnone size-full wp-image-9872" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-Portal-e1422958326475.jpg" alt="tn_Portal" width="251" height="72" /></a>
</td>
<td></td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/registry-repository/"><img class="alignnone size-full wp-image-9922" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-RegistryRepository-e1422959886826.jpg" alt="tn_RegistryRepository" width="250" height="72" /></a>
</td>
<td>Consider using Messaging to populate the Repository</td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/shared-repository/"><img class="alignnone size-full wp-image-9912" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-Repository-e1422959862898.jpg" alt="tn_Repository" width="250" height="72" /></a>
</td>
<td>Consider using Messaging to populate the Repository</td>
</tr>
<tr>
<td>
 <a href="http://developer.nhs.uk/library/architecture/integration-patterns/store-and-notify/"><img class="alignnone size-full wp-image-9832" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-StoreAndNotify-e1422958493685.jpg" alt="tn_StoreAndNotify" width="251" height="72" /></a>
</td>
<td></td>
</tr>
<tr>
<td><a href="http://developer.nhs.uk/library/architecture/integration-patterns/publish-subscribe/"><img class="alignnone size-full wp-image-16992" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn_PubSub_250.jpg" alt="tn_PubSub_250" width="250" height="72" /></a></td>
<td></td>
</tr>
</table>

## Messaging ##
There are many scenarios where messaging can't be driven entirely by the service owner. This is especially true in large organisations or in scenarios where health and social care organisations need to exchange data. In these situations we need an API that recognises a set of related resources but does not tie them into specific procedures, this may also be called a **MessagingAPI**.

For example a Referral Request will typically contain supporting information such as a referral letter, images/scans, or other resources relevant to the referral. How the Referral Request and other resources are handled is down to the service. The service handler may block (synchronous) while waiting for a response but typically the response will be generated later (asynchronously).


<table width="30%">
    <tr>
        <td>
            <b>Request (FHIR Bundle)</b>
        </td>
    </tr>
    <tr>
        <td>
            ITK DistributionHeader
        </td>
    </tr>
    <tr>
        <td>
            Main FHIR Resource <br> (e.g. ReferralRequest)
        </td>
    </tr>
    <tr>
        <td>
            Other FHIR Resources
        </td>
    </tr>
</table>


**Benefits**
- Established and mature pattern in Health and Social Care domain
- Process isolation, useful for communication between organisations and large systems.

**Concerns**
- Not suitable mobile or browser use
- Information Governance concerns especially when used with broadcast pattern.
- Messages need handling, this may be unnecessary for small transactions

### Information Sharing Patterns ###

<table width="80%">
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/message-broker/"><img class="alignnone size-full wp-image-9902" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-Broker-e1422958425684.jpg" alt="tn_Broker" width="250" height="72" /></a>
</td>
<td></td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/broadcast-point-to-point-sharing/"><img  src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-PointToPoint-e1422958448799.jpg" alt="tn_PointToPoint" width="249" height="72" /></a>
</td>
<td>
</td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/registry-repository/"><img class="alignnone size-full wp-image-9922" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-RegistryRepository-e1422959886826.jpg" alt="tn_RegistryRepository" width="250" height="72" /></a>
</td>
<td>
To store resources in the Repository
<br>Use API to retrieve the resources
</td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/shared-repository/"><img class="alignnone size-full wp-image-9912" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-Repository-e1422959862898.jpg" alt="tn_Repository" width="250" height="72" /></a>
</td>
<td>To store resources in the Repository
<br>Use API to retrieve the resources
</td>
</tr>
<tr>
<td>
 <a href="http://developer.nhs.uk/library/architecture/integration-patterns/store-and-notify/"><img class="alignnone size-full wp-image-9832" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-StoreAndNotify-e1422958493685.jpg" alt="tn_StoreAndNotify" width="251" height="72" /></a>
</td>
<td>To store resources in the repository
<br>and provide Notification
<br>Use API to retrieve the resources</td>
</tr>
<tr>
<td><a href="http://developer.nhs.uk/library/architecture/integration-patterns/publish-subscribe/"><img class="alignnone size-full wp-image-16992" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn_PubSub_250.jpg" alt="tn_PubSub_250" width="250" height="72" /></a></td>
<td></td>
</tr>
</table>

## 4. Documents ##

Send documents to remote systems while avoiding direct coupling to remote procedures.

A **DocumentAPI** is an extension of the **MessagingAPI** which provides a set of coherent information that is a statement of healthcare information, including clinical observations and services. A document is an immutable set of resources with a fixed presentation that is authored and/or attested by humans, organizations and devices.

<table width="30%">
    <tr>
        <td>
            <b>Request (FHIR Bundle)</b>
        </td>
    </tr>
    <tr>
        <td>
            FHIR Composition
        </td>
    </tr>
    <tr>
        <td>
            Other FHIR Resources
        </td>
    </tr>
</table>


**Benefits**
- Formatted for human readability using structured headings [PRSB](http://theprsb.org/)
- Static coherent statement of health care at fixed point in time.
- Can be generated on demand to provide a current statement of Patient care.

**Concerns**
- More complex to develop

### Information Sharing Patterns ###

<table width="80%">
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/message-broker/"><img class="alignnone size-full wp-image-9902" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-Broker-e1422958425684.jpg" alt="tn_Broker" width="250" height="72" /></a>
</td>
<td></td>
</tr>
<tr>
<td>
<a href="http://developer.nhs.uk/library/architecture/integration-patterns/broadcast-point-to-point-sharing/"><img  src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-PointToPoint-e1422958448799.jpg" alt="tn_PointToPoint" width="249" height="72" /></a>
</td>
<td>
</td>
</tr>
<tr>
<td>
 <a href="http://developer.nhs.uk/library/architecture/integration-patterns/store-and-notify/"><img class="alignnone size-full wp-image-9832" src="http://developer.nhs.uk/wp-content/uploads/2015/02/tn-StoreAndNotify-e1422958493685.jpg" alt="tn_StoreAndNotify" width="251" height="72" /></a>
</td>
<td>To populate the repository. <br>Use Message or API for the notification<br>Use API to retrieve the document
</td>
</tr>
</table>


