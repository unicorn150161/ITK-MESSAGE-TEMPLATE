---
title: ITK 3 Error Codes
keywords: explore Reference
tags: [explore,fhir,error codes]
sidebar: overview_sidebar
permalink: explore_error_codes.html
summary: "Error codes, their associated elements and value sets."
---

{% include custom/search.warnbanner.html %}

## Overview ##

Error information in the Acknowledgement Response messages is carried in the MessageHeader Resource and the OperationOutcome Resource. There are several elements and their value sets used to carry error information in these resources. This page describes how error information is carried. The example fragments are used to illustrate the elements and value sets used and are not complete messages. 

## Elements And Value Sets Used To Carry Error Information ##


<table width="100%">
    <tr>
        <td>
            <b>Element</b>
        </td>
        <td>
            <b>Value Set</b>
        </td>
    </tr>
    <tr>
        <td>
            MessageHeader.response.code
        </td>
        <td>
            <a href="http://hl7.org/fhir/STU3/valueset-response-code.html" target="_blank">response-code</a>
        </td>
    </tr>
    <tr>
        <td>
            OperationOutcome.issue.severity.code
        </td>
        <td>
                 <a href="http://hl7.org/fhir/STU3/valueset-issue-severity.html" target="_blank">issue-severity</a>
        </td>
    </tr>
	<tr>
        <td>
            OperationOutcome.issue.code
        </td>
        <td>
                 <a href="http://hl7.org/fhir/STU3/valueset-issue-type.html" target="_blank">issue-type</a>
        </td>
    </tr>
	<tr>
        <td>
            OperationOutcome.issue.details
        </td>
        <td>
                 <a href="https://fhir.nhs.uk/ValueSet/itk-acknowledgement-1" target="_blank">itk-acknowledgement</a>
        </td>
    </tr>


</table>

## Examples of Responses ##

**Ok at infrastructure level**
This uses the MessageHeader resource to carry the code.

<script src="https://gist.github.com/unicorn150161/d70e5115e1bc1def9ac9111152674c09.js"></script>

**Ok at business level**

This use the MessageHeader and the OperationOutcome resources

<script src="https://gist.github.com/unicorn150161/8a49f03fa0fffffb5449b2863c6a27fb.js"></script>

**Error at business level due to patient not registered**

This use the MessageHeader and the OperationOutcome resources

<script src="https://gist.github.com/unicorn150161/1d1f6c626ed0676aab082fa53556906c.js"></script>


