---
title: POST /datalist - Options for Filter Fields
tags: [api_spec]
summary: "This endpoint provides options to available datalist fields."
---

This endpoint performs gathering datalists from filter fields as defined by the get_options function for the filter field.  Included are two query parameters: `source` and `field` denoting the source identifier and field name the datalist is to be grabbed for.

## Request

The POST body includes a JSON serialized authentication object formatted according to the authentication scheme provided in the initial `GET /` request:

```javascript
//POST BODY /datalist?source=supersource&field=country
{
  'auth': 'basic', // the identifier of the account type
  'username': 'Superman', // all fields
                          // according to the account format
  'password': 'annoyingj0k3r',
  /*...*/
}
```

The app should utilize these authentication credentials to gather possible values for the `field` provided.

## Response

The response from your API should be a JSON-serialized list of name-value objects:

```javascript
//POST /datalist?source=supersource&field=country
[
  {'name': 'United States', 'value': 'US'},
  {'name': 'Belarus', 'value': 'BY'},
  /*...*/
]
```

The `name` in each object is what is displayed to the end-user for each value in a combobox and the `value` is what is stored with the filter and what will be passed with subsequent requests that utilize the user-created filter.
