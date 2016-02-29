---
title: API Specification Overview
tags: [getting_started, overview, api_spec]
---

All communication between Vizydrop and connected applications occurs over a REST API, as specified and outlined in this chapter. All third party applications are expected to adhere to a particular API format as outlined in this documentation.  The underlying technologies used to develop these third party applications are up to the individual developer.

## REST Endpoints

Below are a list of the HTTP endpoints expected in a Vizydrop connector:

*Required*

- [GET /](../vizydrop/vizydrop_api_schema_info.html): returns app and schema information
- [POST /](../vizydrop/vizydrop_api_schema_fetch.html): actual gathering of external source
- [POST /validate](../vizydrop/vizydrop_api_schema_validation.html): performs validation of accounts

*Optional*

- [POST /datalist](../vizydrop/vizydrop_api_schema_datalist.html): gathers possible options for filter fields
- [GET /logo](../vizydrop/vizydrop_api_schema_logo.html): returns an image/svg+xml representation of the application's logo
- [GET /oauth1](../vizydrop/vizydrop_api_oauth1.html): begins OAuth (v1) authentication by retrieving redirect URI
- [POST /oauth1](../vizydrop/vizydrop_api_oauth1.html): finalizes OAUth (v1) authentication by processing token request
- [GET /oauth2](../vizydrop/vizydrop_api_oauth2.html): begins OAuth (v2) authentication by retrieving redirect URI
- [POST /oauth2](../vizydrop/vizydrop_api_oauth2.html): finalizes OAUth (v2) authentication by processing token request
