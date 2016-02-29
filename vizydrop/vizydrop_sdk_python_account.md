---
title: Account Class
tags: [sdk, python]
---

# Base Account Class

The `Account` class, similar to the `Application` class contains a `Meta` inner-class with meta information (used to build scheme information provided via the `GET /` endpoint).  Also included in the class are `vizydrop.fields` objects that correspond to the fields required for an account to operate.  Classes extending the `Account` base class must implement some functions for account validation, generation of a `tornado.httpclient.HTTPRequest`, and friendly name generation:

- `self.get_request(self, url, method='GET', body=None)` - generate a `HTTPRequest` object with current field values for the url and method provided
- `self.validate(self)` - returns a tuple (bool, str) indicating if the account is valid and, if not, a string representation of errors
- `self.get_friendly_name(self)` - returns a friendly name (str) for the account; this is the default name of an account object when displayed to the end-user

Here is an example of an `Account` subclass without these functions (import statements excluded for brevity):

```python
class TrelloTokenAuth(Account):
    class Meta:
        identifier = "token"
        name = "Token Authentication"
        description = "Authentication via a manually-generated and" \
        " supplied authentication token retrieved from Trello"

    token = TextField(name="Authentication Token",
    description="Auth token retrieved from Trello")

    token_link = LinkField(name="Token Page",
        default="https://trello.com/1/authorize?key={}&name=Vizydrop" \
            "&response_type=token".format(TRELLO_API_APP_KEY),
        description="Navigate here to retrieve your access token:")
```

# Subclasses and Helpers

There are a series of `Account` subclasses that provide helper functionality for HTTP Basic and OAuth-style authentication classes:

- `AppHTTPBasicAuthAccount` - automatically includes username and password fields for HTTP-basic style authentication, as well as extends the `get_request` function to automatically include a standards-compliant `Authorization: Basic` HTTP header.
- `AppOAuthv1Account` - automatically includes standard OAuth-v1 fields, such as access_token and access_secret, as well as extends the `get_request` function to automatically include standards-compliant OAuth query argument, header, or body elements for authentication.
- `AppOAuthv2Account` - similar to the `AppOAuthv1Account` class, only utilizing OAuth-v2.
