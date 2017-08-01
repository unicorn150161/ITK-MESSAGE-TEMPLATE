---
title: Work flow
keywords: workflow
tags: [development,fhir,profiles]
sidebar: foundation_sidebar
permalink: explore_hand_spec.html
summary: "The ITK3 handling specification usage."
---

{% include custom/search.warnbanner.html %}

## Overview ##

There are a number of extensions added to the ITK messageHeader profile which are referred to as the handling specification. These extensions are used to control messaging behaviour such as when to send an acknowledgement. 

**Important Note 1: There is no default behaviour, therefore when the handling specification keys are not set by a sender , receiving systems should do nothing.**

## ITKMeassageHandling Extension ##

This is a complex extension which consists of a coded key using an extensible value set and an associated value which can be a boolean or a string. The table below shows the values which should be assigned to the key / value pairs. 

**Important Note 2: As this value set is extensible other keys and values may be used by local agreement.**


<table width="100%">
<tr>
<th>Key</th>
<th>Usage</th>
<th>Allowable Values</th>
<th>Example Value</th>
</tr>

<tr>
<td>BUSACK</td>
<td>Populated when sender requires a business acknowledgement to be returned</td>
<td>true or false</td>
<td>true</td>
</tr>

<tr>
<td>INFACK</td>
<td>Populated when sender requires a infrastructure acknowledgement to be returned</td>
<td>true or false</td>
<td>true</td>
</tr>

<tr>
<td>INTID</td>
<td>Informs the receiver of the interaction identifier associated with the message flow</td>
<td>Any valid interaction identifier</td>
<td>DOC-ToC-Primary-Recipient-eDischarge-1</td>
</tr>

<tr>
<td>PID</td>
<td>Informs the receiver of the message specification identifier and version that the sending system is built from or conforms to.</td>
<td>Any valid message profile identifier</td>
<td>eDischarge 1.0.0-alpha.1</td>
</tr>

<tr>
<td>SNDO</td>
<td>Informs the receiver of the message that this is a send only transaction i.e. this is an asynchronous message flow.</td>
<td>true</td>
<td>true</td>
</tr>
</table>


An example of how this works is for  when an infrastructure acknowledgement is required by a sender of a message. The sender would send a code of "INFACK" with a boolean value of "true".

<script src="https://gist.github.com/unicorn150161/62a30e5ce737c696494648c06b06c1e6.js"></script>
