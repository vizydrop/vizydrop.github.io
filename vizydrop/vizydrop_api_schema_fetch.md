---
title: POST / - Source Data Fetching
tags: [api_spec]
summary: "This endpoint performs actual data gathering from the source specified."
---

This endpoint performs actual data gathering from the source specified.  The incoming payload includes both account and filter information as provided by the end-user and gathered in accordance with the scheme information provided in the initial [GET /](../vizydrop/vizydrop_api_schema_info.html#source-schema-information) request (if specified):

```javascript

//POST /
//Request Body:
{
  "source": "supersource",  // identifier
	"account": {  //account information, formatted according to /info#account_schema
	    "identifier": "basic",  // identifier of this account type
    	"username": "jonnyfunfun",
        "password": "l33tx0r5!",
        /*...*/
    },
    "filter": { //filter field values according to /info#source/filter_fields
    	"ssn": "696969696",
        /*...*/
    }
}
```

In the event that the account information is incorrect, the TPA should return an HTTP status 401 (Unauthorized) and include a human-friendly error message.  In the event the information is incomplete, the TPA should return HTTP status 400 (Bad Request) and include a human friendly error message:

```javascript
// there's been an error!
{"error": "This is a friendly error message for you."}
```

Internal errors during the process should return HTTP status 500 (Internal Server Error) and include an error message similar to the one above.

If desired, additional debug fields (such as tracebacks) can be included in this response, but they will not be parsed and returned to the end-user.

OK responses should return an appropriate HTTP 2xx status code and be in any text-like format, serialized or not.  Because source schema information is not concrete and isn't necessarily provided to the master node, the return representation of the datapoints can be structured according to the underlying data model or arbitrarily defined by the implementer of the TPA.
