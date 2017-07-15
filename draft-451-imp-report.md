---
title: Implementation Report for HTTP Status Code 451 (RFC 7725)
abbrev: 451ImpReport
docname: draft-451-imp-report-00
date: 2017-07-15
category: info

ipr: trust200902
area: General
workgroup: Human Rights Protocol Considerations Research Group
keyword: Internet-Draft

stand_alone: yes
pi: 
  rfcedstyle: yes
  toc: yes
  tocindent: yes
  sortrefs: yes
  symrefs: yes
  strict: yes
  comments: yes
  inline: yes
  text-list-symbols: -o*+

author:
-
      ins: S. Abraham
      name: Sunil Abraham
      organization: CIS India
      email: sunil@cis-india.org

-
     ins: MP. Canales
     name: Maria Paz Canales
     organization: Derechos Digitales
     email: mariapaz@derechosdigitales.org

-
     ins: J. Hall
     name: Joseph Lorenzo Hall
     organization: CDT
     email: joe@cdt.org

-
     ins: N. ten Oever
     name: Niels ten Oever
     organization: ARTICLE 19
     email: niels@article19.org

-
     ins: C. Runnegar
     name: Christine Runnegar
     organization: ISOC
     email: runnegar@isoc.org

normative:

informative:

   RFC7725:

   Censys:
     title: "80.http.get.status_code: 451 - Censys"
     date: 2017
     author:
        - ins: Z. Durumeric
        - ins: D. Adrian
        - ins: A. Mirian 
        - ins: M. Bailey
        - ins: J.A. Halderman
     target: https://www.censys.io/ipv4?q=80.http.get.status_code%3A+451

--- abstract

This report describes implementation experience between various components working with the HTTP Status Code 451 {{RFC7725}}.

--- middle

Introduction
============

This document aims to evaluate the usage of HTTP status code 451, which was approved by the IETF in February 2016 {{RFC7725}}. This implementation report aims to illuminate whether the status code does what it set out to do ("provide transparency in circumstances where issues of law or public policy affect server operations"), the different ways it is being used, positive and negative impacts of the standard and we end with suggestions for improvement of the standard. 

Vocabulary
==========

Blocking 
: The act of making an HTTP resource inaccessible to a class of users.

Resource 
: A top-level information object served by an HTTP server (e.g., HTML page).

Subresource 
: An information object served within the context of a top-level Resource (e.g., JavaScript, Image, etc.)

Server Operator 
: An entity or an individual operating an HTTP server.

HTTP status 
: For each response, HTTP servers return a numerical status code (e.g., 400 (OK), 403 (unauthorized), etc.) described by IANA https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml.

 Response 
: When an HTTP Server responds to a request, it sends a Response, made up of header fields and a body (See: https://tools.ietf.org/html/rfc7725#section-3 

 Legal demand 
: A verbal or written request grounded in law or regulation from an Authority to a Server Operator to Blocking a Resource.

 Authority 
: A government or government-licensed entity mandating blocking of a resource directly or that may institute laws that indirectly require blocking of a resource.

 Complainant 
: A party making a Legal demand; may or may not be an Authority (e.g., the US DMCA allows a copyright holder to demand takedown).

Target audiences
================

# Who is likely to implement the 451 status code?

## Server operators 
Server operators that are being confronted with an order from a legal authority can use the HTTP status code to communicate to third parties why the content is not available on the server.

## Intermediaries 
Intermediaries such as Internet Service Providers, Content Distribution Networks and other might be obligated by a legal authority in their operational jurisdiction to filter certain content. The HTTP status code would add transparency to this practice.

# Who is likely to use the 451 status code data?

## Browser vendors 
Browser vendors might implement functionality to communicate the presence of a HTTP status code 451 to a user.

## End users
End users will be informed about why the information they are trying to access is not available, instead of merely concluding that the content is not available due to other reasons (e.g., 404 unavailable). 

## Researchers 
Researchers might want to scan for the prevalence of blocking, as well as trends in blocking behavior. 

## Civil society
Civil society may want to use instances of HTTP status code 451 to highlight censorship and censorship trends, to challenge blocking.

## Governments
Governments might want to verify compliance with blocking orders and use HTTP status code 451 to do so on the networks in their jurisdiction.

Current Usage
=============

# Overview

In the majority of cases in which HTTP status code 451 is being deployed {{Censys}}, the status code reads as follows - "451 Unavailable For Legal Reasons" or "451" or "451 Unknown Error" or "451 Error" or "451 Unavailable For Legal Reasons (burned)" or "451 OK". The Page Title could say "404 Not Found" or "Blocked" or "451 -" or "Restricted access" or "Bloqueado por ordem judicial" ("Blocked by judicial order") or "Sito censurato" ("Censored site") or "Доступ ограничен" ("Access is restricted") or "Зелёная точка - доступ к запрашиваемому ресурсу ограничен" ("Zelenaya tochka" - Internet and TV provider - access to the requested resource is restricted")or "Violazione del bispensiero" or "Please report sexual abuse against children to the Swedish National  Bureau of Investigation!" or "Copyright Notice" or "451 RKN Redirect" (RKN is likely Russia's Roskomnadzor) or "ATTENZIONE!! - POLIZIA POSTALE E DELLE COMUNICAZIONI - PAGINA BLOCCATA" ("Attention! - Postal and Communications Policy - Blocked Page") or "451 Unavailable For Legal Reasons 本网站由于国家政策而不可用" (Chinese: "This site is not available due to national policy").   

The hosts that were observed implementing the status code are located in Russia, United States of America, Singapore, Czech Republic, Thailand, Netherlands, Portugal, Spain, Italy, Greece, Bulgaria, Hungary, Germany, France, United Kingdom, Ukraine, Norway, Finland, Kazakhstan, United Arab Emirates, Japan, China, Philippines and Australia. In some cases - the visitor to the website is provided some context for the block -- for example, a take-down notice for copyright infringment -- in other cases the visitor is encouraged to  cooperate with law enforcement agencies. The page title may have information that does not always make sense in the context of the error code, for example when the title says "404 Not Found" but the page is a 451 response body. These observations are based an examination of the search results from Censys.io on 15 July 2017 which featured 526 IPv4 Hosts of which 17 were included in the list of "Top Million Websites".

# Trends and observations

- The majority of instance of HTTP status code 451 provide no explanation in the response body.

- There have been found several cases of servers serving HTTP status code 451 with redirect another server with a central warning message of a blocking authority.

- A registrar serves HTTP status code 451 when a registrant did not pay their domain fees.

- There are significant observations of server serving HTTP status code 451 based on geoIP (especially for gambling sites).

- There are different understandings of the 'blocked-by' field as defined in RFC7725. Some people interpret is as the entity that is doing the blocking, others are interpreting it at the authority responsible for ordering the blocking.

- HTTP Status Code 451 is thusfar only served by hosts, not by intermediaries.

Potential negative or positive impacts
======================================

- {{RFC7725}} specifies a status code for web resources that are blocked for legal reasons. The HTTP status code 451 is designed to enable content providers and intermediaries (including ISPs and search engines) to notify users that their access to specific web resources has been blocked for legal reasons. The standard also recommends that the notification include an explanation. This is important because this is the detail the user needs to be able to understand why access has been blocked, and if desired, to take action to challenge the blocked access. It also helps content servers and intermediaries who have been required to block access to notify users who directed that access by blocked.

- Also, as the 451 status code is machine-readable, researchers and others could use web crawlers to identity which blocked URLs or sub-resources use error code 451. This data could be used to produce a searchable open repository of all known error code 451 instances. This information could then be used to map the blocked Web and to analyze the explanations, looking for trends and anomalies. For example, one day there might be an answer to the question – “how much content is blocked for IPR reasons?”

- The 451 status code can also be used for encrypted webpages, which is significant as encryption on the Web becomes more and more prevalent. A user should be able to see the error code irrespective of whether they try to access the content via HTTP or HTTPS.

- This standard is a prime example of an Internet protocol enabling common policy objectives (in this case, transparency) to be implemented across the world. However, as with all IETF standards, the implementation of the 451 status code is voluntary.  So, how widely it is used will likely depend on a number of factors, including a legal/political regime that does not penalize transparency, the willingness to be transparent and the capability to implement. 

- It is possible that status code 451 code could be used for other purposes (e.g. to mislead users as to the reason for the content being blocked), especially as “legal reasons” is not defined. 

- It is also possible that content providers and intermediaries who are required to block content for legal reasons to be asked or compelled to use another status code (e.g. 404). In these circumstances, content providers and intermediaries should include information in their transparency reports to indicate whether this is happening, by, for example, stating: “We have/have not been required to replace 451 by other status codes.”

- There may be a temptation in some cases of the implementation of status code 451 to include the ability to identify and/or track the users that visit a web resource that has been blocked. This raises significant privacy issues. 

- The usage of HTTP status code 451 might lead to an increase in blocking because it makes analyzing compliance easier. 

What are features of a blocking reporting infrastructure that would be useful?
==============================================================================

- The reporting format needs to cover information enough to satisfy transparency and offer insight about possible misuse of 451 error as a vehicle for censorship.

- Transparency requirement will be better served through standardization of fields and descriptions. Currently many implementations for HTTP status code 451 do not provide the reason for blocking. This could be attributed to the fact that the different needs are not sufficiently documented in RFC7725. This could be fixed by adding fields in the header. Useful categorization fields to accurately describe content blocked by legal reasons are:

-- Identification of the legal source on which the blocking request is based.

-- Identification of the complainant/requestor if is an institution (not if individual because of privacy concerns). It could be useful to identify in this field if the request comes from a private or public entity, and in if there is a judicial order involved, or a law enforcement or other type of governmental request.

-- Description of blocked content (example: 'Non-consensual sexually explicit imagery'). It could be helpful to have suggested fields that standardize type of content in order to make easier the analysis and the evaluation about eventual challenge of the use of error 451 for the specific content removal.

-- Determination of the geographical scope of the blocking. Increasingly blocks are being implemented at the level of the city or province. Therefore country codes may not be sufficient to describe the geographical scope.

-- Date of block order and time-period for which the block has to be enforced.

-- Date of start serving HTTP status code 451.

-- Link to the final decision (if available). Again this should only be the case when the complainant is not an individual.

-- Contact information for relevant authority for the purposes of verification of procedural stage and appeal or redress opportunities.


What features of blocking events are supported by the existing 451 status code, and what features do we need to add?
====================================================================================================================

- Guidance on the representation of HTTP status code for subresources in browsers

- Guidance on the implementation of HTTP status code 451 could lead to an increase in adoption. RFC7725 provides high level advice but still leaves space for interpretation. An implementation guide in conjunction with an adoption campaign might lead to increased adoption. 

- {{RFC7725}} does not clarify whether HTTP Status Code 451 is only meant for respones to GET/HEAD requests or also for POST/HEAD requests. 


Background: Legal Realities
===========================

In the light of the use cases outlined above underneath we are providing an overview of legal frameworks in a number of countries that could be used to make a blocking request. This is to show that a reference to a the description of blocked content, the legal source on which the blocking order or request is based and the authority that is makes the order or request is crucial in understanding the context and nature of the blockage.

# Russia

Blocking by the government:

## Federal Law of 27 July 2006
Law No. 149-FZ on Information, Information Technologies and Protection of Information and its amendments:

- “Blacklist” law 139-FZ (2012) – allowing to block websites if they appear to have dangerous information for children such as information about suicide and drugs. The blocking was often done by keyword so as a result one of the biggest wiki sites in Russia (Lukmore) was accused of drugs propaganda, an online encyclopedia (Absurdopedia) was accused of suicide propaganda and an online game was blocked because on it’s forum somebody used a word “drug”. 

- “Anti-pirate” law 187-FZ (2013) – easier way for the government to block access to websites if they are suspected in any wrongdoing. The amendment also allows blocking by IP address. Leads to the blockage of portals such as OpenSharing.org 

- The law 398-FZ on immediate blockage of websites at the request of Prosecutor General (2013).

- “Bloggers’ amendment” 97-FZ (2014)  – bloggers with more than 3000 need to register as mass media (“information distributors”) and have the same responsibilities (including on what their readers post in comments).

- Data localization law 242-FZ (2015) all companies collecting personal data of the Russian citizens must store that information on the servers within Russia

- The laws against extremism that have been updated throughout the past 5 years expanding the term “extremism” and making the punishment tougher (jail terms for posting and reposting) as well as blocking. These laws have been used widely after the conflict in Ukraine. Some people got jail sentences and resources were being blocked for spreading information sympathizing with the Ukrainian side. Such laws are particularly vague and “extremism” is very laxly defined. For example, “…extremist materials, as well as information propagating racial, national or religious hatred or enmity or hatred towards any social group.” 

## “Yarovaya laws” 
This law was approved by the Parliament and, if passed, will oblige messaging apps to store messaging history and decrypt messages at prosecutors’ request. 

# Chile

# India

## Blocking by the government 
Under Section 69A of Information Technology Act 2000, the executive branch of the government has "the power to issue directions for blocking for public access of any information through any computer Resource". According to the law, any person can send a block request to a Nodal Officer. These Nodal Officers should be designated in all government entities to deal with block requests. The request is then approved by the state or central Chief Secretary. This step is not required if the Nodal Officer has initiated the blocking procedure without any complainant. The request is then forward to the head of CERT-IN. If it is not a public emergency, the persons or intermediaries should be given 48 hours to respond. But this is not required if the emergency provision has been invoked, but the block list still has to be reviewed by "Committee for Examination of Request" within 48 hours after the block been issued. The block lists are usually issued directly to ISPs and are marked confidential and are implemented unevenly with some ISPs providing sparse details if users try to access the blocked resources and other ISPs returning a 404 Error Code. 

## Blocking by courts
Increasingly Indian courts are issuing ex-parte John Doe orders for website blocking. These orders can be issued by courts for any illegal content. There are around 30 different laws that place reasonable restrictions on the right to free speech in India. For example: The Scheduled Castes and the Scheduled Tribes (Prevention of Atrocities) Act, 1989, The Prenatal Diagnostic Techniques (Regulation and Prevention of Misuse) Act, 1994 and The Juvenile Justice Act, 2000. Some of these laws have multiple provisions that regulate speech for ex. the Information Technology Act has 6 sections and the Indian Penal Code has 10 sections. Once a court order has been obtained, the order can be sent to Secretary of the Department of Electronics and Information Technology who will then forward it to ISPs. Or alternatively complainants could also send court orders directly to ISPs without following the procedure described above.  

## Takedowns by web sites
Under Section 79 of the Information Technology Act 2000, both the government and private parties can send take-down notices to web sites. Intermediaries can ignore private party take-downs without losing immunity but take-down notices from the government have to be complied with. Under Section 52(1)(c) of the Indian Copyright Act, take-down notices can be sent to websites who are engaged in infringement but they need to be followed by court orders otherwise the content can be reinstated. 