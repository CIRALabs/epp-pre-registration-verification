---
title: "EPP Pre-Registration Verification"
abbrev: "EPP Pre-Registration Verification"
docname: draft-ietf-epp-pre-registration-verification-latest
category: std
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 0
area: AREA
workgroup: workgroup
keyword: Internet-Draft
pi: [toc, sortrefs, symrefs]

venue:
  group: WG
  type: Working Group
  mail: WG@example.com
  github: "CIRALabs/epp-pre-registration-verification"
  latest: "https://github.com/CIRALabs/epp-pre-registration-verification/blob/main/draft-ietf-epp-pre-registration-verification.html"

author:
 -
   ins: J. Latour
   name: Jacques Latour
   org: CIRA
   email: jacques.latour@cira.ca
 -
   ins: D. Slaunwhite
   name: Don Slaunwhite
   org: CIRA
   email: don.slaunwhite@cira.ca
 -
   ins: Tim Johnson
   name: Jacques Latour
   org: InternetNZ
   email: timj@internetnz.net.nz

normative:

informative:


--- abstract

This Internet Draft introduces an extension to the Extensible Provisioning Protocol (EPP) for top-level domain (TLD) registries, enabling registrars to submit pre-registration information for domain names. The extension facilitates quality verification by the registry, employing advanced Artificial Intelligence and Machine Learning (AI/ML) techniques. Pre-registrations are assigned a quality score based on the analysis of the submitted data, ranging from 0 for non-abusive registrations to 100 for potentially abusive ones. This extension addresses the critical need to proactively identify and mitigate abusive domain registrations within TLDs, contributing to a safer and more reliable internet environment. The document outlines the EPP command definitions, XML schemas, data flow, and security considerations necessary to implement this innovative quality assurance mechanism, thereby enhancing the integrity and trustworthiness of TLD registrations.

--- middle




# Introduction

## Problem Statement
The current EPP protocol lacks mechanisms for registrars to submit pre-registration data to the registry for quality verification. This gap leads to potential issues with abusive domain registrations, which can harm the integrity of the top-level domain (TLD).
## Use Case Description

A registrant wants to register domain names within a TLD registry via a registrar. To ensure the quality of registrations and prevent abusive domains, the registrar uses the proposed EPP extension to submit pre-registration data of the registrant to the registry. The registry, equipped with AI/ML techniques or services, analyzes this data to assign a registrant quality score back to the registrar. Based on this score, the registrar can decide whether to accept, reject or put on hold the registration request.

## Importance and Benefits
Addressing the quality of the registrant data before the actual registration process occurs brings many benefits.  Adding a pre-registration process benefits the domain registration ecosystem by:
- Potentially reducing the number of malicious registration and frauds and reducing operating costs to registrar and registry in responding to the abuse.
- Ensuring the quality of domain registrations is crucial to maintaining the trust and reputation of the TLD. Abusive registrations can lead to various issues, including spam, phishing, and other malicious activities.
- The proposed extension enables registries to proactively identify and block abusive registrations, thereby improving the overall quality of domain names within the TLD. This can lead to a safer and more reliable internet for end-users.
- And contributing to a safer internet.

## Scope of the Extension - Verification
This EPP extension focuses on enabling registrars to submit pre-registration data to the registry and receive a registrant quality score based on abuse AI/ML analysis. It does not address other aspects of domain registration, such as pricing or dispute resolution.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Terminology

**Pre-Registration Registrant Information**: This term refers to the data and details submitted by the registrar before the registration of a domain name. It typically includes information provided by the registrant, such as contact information and the intended use of the domain name, and is used for quality verification by the registry as part of the pre-registration process.

**Registrant**: RFC8499 defines the registrant as "an individual or organization on whose behalf a name in a zone is registered by the registry. A registrant is created in the registry after a successful registration with the registrar.

**AI/ML-Powered Domain Abuse Mitigation**: This term encompasses the use of Artificial Intelligence (AI) and Machine Learning (ML) technologies within the top-level domain (TLD) industry to identify, prevent, and mitigate abusive domain registrations. These technologies are employed to detect and combat various forms of domain abuse, such as spam, phishing, malware distribution, and other malicious activities, ultimately enhancing the security and integrity of domain name space.

**Quality Score**: Define a quality score as the numeric value assigned to a pre-registration registrant based on the AI/ML analysis of their pre-registration data. Mention that higher scores indicate potentially abusive registrations.

**EPP**: RFC 5730: Extensible Provisioning Protocol (EPP) (rfc-editor.org)

# Extension Overview and Command Definition

## Extension Overview

### EPP Protocol Extension Purpose
This extension is designed to enhance the Extensible Provisioning Protocol (EPP) by introducing mechanisms for registrars to submit pre-registration information to the registry, thus enabling the verification of the quality of domain name registrations using advanced Artificial Intelligence and Machine Learning (AI/ML) techniques. The primary objectives of this extension are as follows:

- Quality Assurance: To proactively assess the quality of domain name registrations and reduce the risk of abusive registrations within the top-level domain (TLD).
- Enhanced Trust: To improve the overall quality of domain names within the TLD, promoting a safer and more trustworthy internet environment.

### Integration with AI/ML Techniques

The extension integrates AI/ML techniques into the EPP framework, allowing the registry to analyze pre-registration data for signs of potential abuse. These techniques include data analysis, pattern recognition, and predictive modeling. The analysis results in a registrant quality score, which helps the registry make informed decisions regarding the acceptance or rejection of registration requests.

# EPP Command Definition

## New EPP Commands
This extension introduces new EPP commands to facilitate pre-registration data submission and quality verification. The following commands are defined within the extension:
### "create" Command Extension
Command Name: "create" (Extended)
Purpose: To create a new domain registration while including additional XML elements for registrars to submit pre-registration data. Registrars can provide information such as the intended use of the domain and other relevant details.
XML Element: `<pre-registration-data>` - This element encapsulates the pre-registration data submitted by the registrar.
Usage: Registrars initiate the "create" command with the pre-registration data, which is then stored by the registry for later analysis.
### "verify" Command

Command Name: "verify" (New)
Purpose: To trigger the quality verification process for pre-registration data that has been submitted. Registrars can initiate this command after an initial "create" request.
XML Element: N/A
Usage: After pre-registration data is submitted through the "create" command, registrars can use the "verify" command to request the registry's AI/ML analysis and obtain a registrant quality score.

## XML Schema Definitions

To support these new EPP commands, the extension defines the XML schema elements necessary for encapsulating pre-registration data, ensuring interoperability between EPP clients and servers.

TBD


# EPP Protocol Extension

## Extended "create" Command for Pre-Registration and Quality Verification

This section outlines the extension of the existing "create" EPP command to accommodate the pre-registration data submission and quality verification process. The extended "create" command enables registrars to provide additional information related to the intended use of the domain name, facilitating quality assurance within the top-level domain (TLD).

### Command Name

Command Name: "create" (Extended)

### Command Purpose
The extended "create" command serves the following purposes:
- To create a new domain registration within the TLD.
- To allow registrars to submit pre-registration data for quality verification.
- To enhance the quality assurance process by providing registrars the opportunity to convey relevant information about the domain's intended use.

### XML Element Extension

To enable registrars to submit pre-registration data, the "create" command is extended to include an optional XML element, `<pre-registration-data>`. This XML element is included within the "create" command's payload and encapsulates the pre-registration information provided by the registrar.

***XML Element:***

- `<pre-registration-data>` (Optional)

### Usage

Registrars initiate the extended "create" command in the following manner:

- The registrar includes the `<pre-registration-data>` XML element within the "create" command when submitting a domain registration request.
- The `<pre-registration-data>` element allows registrars to provide information related to the intended use of the domain, additional contact details, or any other relevant data.

Example "create" Command with Pre-Registration Data:

~~~ xml
<epp xmlns="urn:ietf:params:xml:ns:epp-1.0">
     <command>
       <create>
         <!-- Domain creation data -->
         <domain:create>
           <!-- Domain details -->
         </domain:create>
         <!-- Pre-Registration Data -->
         <pre-registration-data>
           <!-- Pre-registration information -->
         </pre-registration-data>
       </create>
     </command>
   </epp>
~~~


The inclusion of the `<pre-registration-data>` element within the "create" command allows registries to participate in the quality assurance process and ensures that additional data relevant to the domain's use is considered prior its potentially abusive registration.

Extended "create" Command: The existing "create" command will be extended to include an optional XML element for registrars to submit pre-registration data. This will enable registrars to provide additional information related to the intended use of the domain name.

## Introduction of New Verify EPP Commands

New "verify" Command: A new EPP command, "verify," will be introduced to trigger the quality verification process on the submitted pre-registration data. Registrars can use this command after the initial "create" request.
It’s important to note that the time to respond to the verify command is important to take in account, should be in the order of seconds and not minutes.

## Command Flow Overview

Command Flow: The process begins with a registrar initiating a "create" command with additional pre-registration data. The registry, upon receiving the request, stores the data for further analysis. Once the data is collected, the registrar can initiate the "verify" command to trigger the quality verification process, which results in the assignment of a quality score.
By mapping the EPP verify commands to the new registration process, it demonstrate how the new extension fits into the existing EPP framework and how it can facilitate the pre-registration data submission and quality verification.




# Pre-Registration and Verification Command Flow

## Pre-Registration Data Submission Flow

The command flow within the EPP protocol extension for pre-registration and quality verification is a series of interactions between the registrar and the registry. This section outlines the steps involved in submitting pre-registration data and initiating the quality verification process:

***Step 1: Registrar Initiates "create" Command***

The process begins when a registrar initiates a modified "create" command, extending the EPP protocol. This command is used to request the creation of a new domain registration.

***Step 2: Registrar Includes Pre-Registration Data***

Within the "create" command, the registrar includes the `<pre-registration-data>` XML element. This element encapsulates the pre-registration information, such as the intended use of the domain and any other relevant data.

***Step 3: Registry Receives and Stores Pre-Registration Data***

The registry, upon receiving the "create" command, stores the pre-registration data associated with the domain name in question. This data is queued for subsequent quality verification.

## Quality Verification Flow

After pre-registration data is successfully submitted through the "create" command, the quality verification process can be initiated by the registrar. Here's how the flow continues:

***Step 4: Registrar Initiates "verify" Command***

After the pre-registration data has been stored, the registrar initiates the "verify" command, a new EPP command introduced by this extension.

***Step 5: Registry Triggers Quality Verification***

Upon receiving the "verify" command, the registry's system is triggered to initiate the quality verification process. This process involves AI/ML analysis of the pre-registration data.

***Step 6: AI/ML Analysis and Quality Score Calculation***

The registry's AI/ML algorithms analyze the pre-registration data to assess its quality. This analysis considers factors such as the nature of the registration, the intended use of the domain, and other relevant data. Based on the analysis, the system calculates a registrant quality score.

***Step 7: Registry Provides Quality Score***

The registry sends the registrant quality score as part of the "verify" command response to the registrar. The score indicates the perceived quality of the registration, with values ranging from 0 for non-abusive registrations to 100 for potentially abusive ones.

***Step 8: Registrar Takes Action Based on Quality Score***

Depending on the quality score received, the registrar can make informed decisions regarding the acceptance, rejection, or further review of the domain registration request.

# Pre-Registration Quality Score ***Guidance***

This section provides a range of registrant quality scores with corresponding actionable actions for the proposed quality verification process, where 0 indicates a good registration and 100 signifies an absolutely malicious registration:

## Score 0 - 20 (Non-Abusive):

### Actionable Actions:
- The registration appears to be non-abusive and legitimate.
- The address and information provided by the registrant match and seem trustworthy.
- No immediate action required.


## Score 21 - 40 (Low Suspicion):

### Actionable Actions:

- The registration raises minimal suspicion.
- While the information appears consistent, there might be subtle irregularities.
- Regular monitoring and further review may be necessary.
- Regular monitoring and further review may be necessary.

## Score 41 - 60 (Moderate Suspicion):

## Actionable Actions:

- The registration raises moderate suspicion.
- Some elements in the registration data seem incongruent or questionable.
- Investigate further and consider additional verification steps.
- Suspend the registration at the Registry? (after Registrar registration)

## Score 61 - 80 (High Suspicion):

### Actionable Actions:

- The registration exhibits a high level of suspicion.
- Several aspects of the registration data appear inconsistent or potentially problematic.
- Immediate investigation and verification are necessary.
- Suspend the registration at the Registar

## Score 81 - 99 (Very High Suspicion):

### Actionable Actions:

- The registration is highly suspicious and raises significant concerns.
- Multiple elements in the registration data are irregular or seem malicious.
- Implement rigorous verification and consider delaying or rejecting the registration.

## Score 100 (Absolutely Malicious):

### Actionable Actions:

- The registration is deemed absolutely malicious and poses a severe threat.
- Clear evidence of fraudulent activity or malicious intent is present.
- Reject the registration and take appropriate measures to prevent abuse.

These quality score ranges and associated actions provide guidance for registrars and registries in evaluating the legitimacy of domain registrations. The specific actions to be taken can vary depending on the policies and procedures of the TLD registry and the severity of the suspicions raised by the quality score.

## Error Handling

TBD

## Registration Timing Considerations

This process has to be quick, if too slow a timer must be defined to mark the registration verification as incomplete, need a specific workflow



# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
