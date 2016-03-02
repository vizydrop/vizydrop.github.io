---
title: Introduction
tags: [getting_started]
audience: developers
type: first_page
homepage: true
---

## Overview 

This site provides documentation and other notes for integrating with and developing custom applications for Vizydrop - a data visualization platform brought to you by the folks behind [Targetprocess](http://www.targetprocess.com/).

The instructions here are geared towards developers and systems analysts.  If you are looking for documentation regarding the use of Vizydrop, you won't find that here.

## Brief Introduction

All communication between third party applications and Vizydrop's internal servers are done via standard hypertext protocols, whether they be HTTP or HTTPS.  All third party applications are expected to adhere to a particular API format as outlined in this documentation.  The underlying technologies used to develop these third party applications are up to the individual developer, though the Vizydrop team officially provides [software development kits (SDKs)](sdk/summary.md) in the following languages:

- [Python 3](../vizydrop/vizydrop_python_sdk.html) utilizing [Tornado](http://tornado-web.org)'s asynchronous HTTP server

All communication with third party services is done via Vizydrop's Applications Gallery, codenamed <a href="#" data-toggle="tooltip" data-original-title="{{site.data.vizydrop.vizydrop_glossary.hermione}}">Hermione</a>.  Users may register their applications with Vizydrop by providing a HTTP or HTTPS URI for their service.  The service must be accessible from the internet in order for the applications gallery to successfully communicate with the service.  It is _highly recommended_ that service providers consider utilizing HTTPS for all endpoints and limit access to these services only to IP addresses known to be from Vizydrop's <a href="#" data-toggle="tooltip" data-original-title="{{site.data.vizydrop.vizydrop_glossary.hermione}}">Hermione</a> service (see [technical specifications](tech-spec.md) and [security specifications](security.md) for more information).

In essence, Vizydrop's <a href="#" data-toggle="tooltip" data-original-title="{{site.data.vizydrop.vizydrop_glossary.hermione}}">Hermione</a> applications gallery service acts as a proxy between other Vizydrop services and the third party provider with some added logic for account and filter storage and validation.
