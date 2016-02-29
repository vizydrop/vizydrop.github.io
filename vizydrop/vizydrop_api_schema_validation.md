---
title:  POST /validate - Account Validation
tags: [api_spec]
summary: "This API endpoint performs validation of connected accounts."
---

This endpoint performs account validation when setting up an account for the TPA.  The incoming payload includes information about the account type to be validated and all fields required:

```javascript
{
	"id": "basic", //identifier for the account type
    "fields": { //list of field values to validate
                //according to schema
    	"username": "jonnyfunfun",
        "password": "z0mgt3hacc0unt5!",
        /*...*/
    }
}
```

If the account is valid, the TPA should return HTTP status 200 with a JSON object containing a friendly name for the account:

```javascript
{"name": "JonnyFunFun's Awesome Account"}
```

In the event that an account's details have been updated during the validation routine, such as is the case with OAuth v2 refresh tokens, the TPA should return a JSON object containing all fields that have been updated:

```javascript
{"token": "blurb", "refresh_token": "random stuff"}
```

If the account is invalid, the TPA should return HTTP status 401 (Not Authorized) with a simple JSON object containing an error message:

```javascript
{"error": "Your password is incorrect!"}
```

If desired, additional debug information can be included in this response, but it will not be parsed and returned to the end-user.
