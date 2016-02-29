---
title: GET / - Schema Information
tags: [api_spec]
summary: "This API endpoint provides application and schema information to Vizydrop"
---

## Overview

This endpoint is the main endpoint that returns information about the TPA that this endpoint provides.  Responses should be valid JSON similar to the following:

```javascript
{
  "version": "1.0",  //string representing the versionof your app
	"name": "My Super Application",  //title of the app
	"tags": ["super", "all your base"],  //OPTIONAL: list of tags
	"color": "#000000",  //OPTIONAL: background color
	"description": "All your base are belong to us!", //long description
	"site": "www.vizydrop.com",  //OPTIONAL: website, if you've got one
	"authentication": [...] //list of account schema information
	"sources": [...] //list of source info, see below
}
```

The `/` endpoint passes all schema information to the master node, including information about what datapoints are required for account setup, as account information is still stored locally within the master node.  Fields that *must* be included are:

- version
- name
- description
- authentication
- sources

## Authentication Information

The `authentication` object includes all account schema information.  This informs the Vizydrop front-end how to build forms for the end-user to input account information.  This option is required, even if your application does not require authentication.  At least one account object must be present in the array.

```javascript
"authentication": [
    {
    	"id": "basic", //identifier, lowercase, only letters and numbers
        "name": "Basic Authentication", //user-friendly title
        "description": "Just using a username and password", //description
        "fields": [  //list of fields to be filled
        	{
            	"id": "username",  //field identifier
                "title": "Username",  //friendly name
                "description": "Your username, duh!",  //description
                "type": "text",  //field type (text, password, number, etc.)
                "required": true,  // is this field required?
                "choices": ['Batman', 'Superman', 'Green Lantern', 'Aquaman, lol']  //list of possible choices, leave null if not applicable
            },
            /* ... */
        ]
    }
]
```

For authentication types that do not require any user input, such as is the case with applications that require no authentication at all, the `fields` array may be omitted.  For more information about fields and for a list of field types, please refer to (Fields)[fields.md].  Multiple account types and schemas may be specified.

*Important note:* if your app provides OAuth capabilities for authentication, the authentication identifiers _must_ be `oauth` and `oauth2` for OAuth v1 and OAuth v2, respectively.  Only one authentication type per OAuth version is currently supported.

## Source Schema Information

Source information is included in the overall `GET /` response in a format also similar to authentication schema information:

```javascript
"sources": [
	{
    	"id": "supersource", //identifier
        "name": "Super Data Source",  //friendly name
        "description": "Use data here to take over the world.", //description
        "tags": ['super', 'world domination'],  //tags
        "fields": {}, // schema object
        "filter": [ // list of fields used for filter
          {
              "id": "ssn",  //field identifier
              "title": "Social Security Number",  //friendly name
              "description": "Filter by your victim's socialized surf number",  //description
              "type": "number",  //field type (text, password, number, etc.)
              "required": false,  // is this a required field?
              "choices": [1, 2, 3]  //list of possible choices, leave null if not applicable
          },
          /*...*/
        ]
    }
]
```

For source objects, the `fields` object helps the Vizydrop services understand what type of data it should expect to receive from the third-party provider.  In most cases, this information is not required and the `fields` object can be omitted from the sources object.  In this case, Vizydrop will attempt to automatically determine the format and schema of the source based on the data provided.  If you experience issues with chart suggestions or bad type-mapping for your data fields, a source schema may be required.

## Source Filter Information

The `filter` object is used to help the user choose which data to filter.  Just like other field-like objects, the `filter` object is not required.  If none is provided, users will not be able to filter data received from the app.

For more information about fields and for a list of field types, please refer to [Fields](../vizydrop/vizydrop_fields.html).
