---

copyright:
  years: 2018, 2020
lastupdated: "2020-03-10"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Web Application Firewall concepts
{: #waf-q-and-a}

The Web Application Firewall (WAF) protects against OSI Layer-7 attacks, which can be some of the most tricky. This document gives some details.
{: shortdesc}

## What is a Web Application Firewall?
{: #what-is-a-waf}

A WAF helps protect web applications by filtering and monitoring HTTP traffic between a web application and the internet. A WAF is an OSI protocol Layer-7 defense in the [OSI model](https://en.wikipedia.org/wiki/OSI_model){: external}, and it is not designed to defend against all types of attacks.

Deploying a WAF in front of a web application is like placing a shield between the web application and the internet. A proxy server protects a client machine’s identity by using an intermediary (for outgoing traffic), but a WAF is a type of reverse-proxy that protects the server from exposure by having the client's traffic pass through the WAF before reaching the server (for incoming traffic).

## Types of attacks WAF can prevent
{: #what-types-of-attacks-can-waf-prevent}

A WAF typically protects web applications from attacks such as cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection, among others. A WAF usually is part of a suite of tools, which together can create a holistic defense against a range of attack vectors.

## How a WAF works
{: #how-does-waf-work}

A WAF operates through a set of rules often called policies. These policies aim to protect against vulnerabilities in the application by filtering out malicious traffic.

The value of a WAF comes from the speed and ease with which its policy modifications can be implemented, thereby allowing a faster response to varying attack vectors. For example, during a [DDoS attack](https://en.wikipedia.org/wiki/Denial-of-service_attack){: external}, rate limiting can be implemented by modifying WAF policies.

## Key benefits of a {{site.data.keyword.cis_short_notm}} WAF
{: #key-benefits-of-cis-waf}

The {{site.data.keyword.cis_full}} WAF is an easy way to set up, manage, and customize security rules to protect your web applications from common web threats. See the following list for key features:

* **Easy setup** - The {{site.data.keyword.cis_short_notm}} WAF is part of our overall service, which takes just a few minutes to set up. After you redirect your DNS to us, you can switch on the WAF and set up the rules you need.

* **Detailed reporting** - See greater detail in the reporting, for example, threats blocked by rule/rule group.
