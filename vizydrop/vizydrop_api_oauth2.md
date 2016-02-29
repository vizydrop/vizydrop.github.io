---
title: Implementing OAuth v2
tags: [api_spec, oauth]
summary: "This article provides information regarding integration with OAuth v2 applications."
---

## Starting the OAuth2 Flow

The `GET /oauth2` endpoint performs the initial setup for OAuth version 2 accounts.  Included with the request is a single query argument, `callback_uri`, which is the redirect URL that the user should be expected to be redirected to upon successful authentication with the third-party service.  Return body should at least include a `redirect_uri` that the user should be forwarded to in order to complete setup.  Replies are then POST'ed to this endpoint (see below).

```javascript
// GET /oauth2
{
    "redirect_uri": "https://accounts.google.com/o/oauth2/token?scope=openid+profile+email&client_secret=xxxxxxxxxxx&grant_type=authorization_code&redirect_uri=something&code=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&client_id=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

*Note:* The OAuth implementation requires the account identifier to be `oauth2` for OAuth version 2.

## Finalizing accounts after user authorization

The `POST /oauth2` endpoint performs the final setup and validation of OAuth version 2 accounts.  Information as received from the third party upon redirection to the previously posted `callback_uri` are sent to this endpoint, with other applicable account information, for final setup.  The account is then validated and, if successful, the account is returned; if there is an error, it is to be raised appropriately.

**A note about refresh tokens:** prior to each use of an account, Vizydrop master will `POST /validate` to ensure that the account information is still valid.  If your OAuth v2 implementation uses refresh tokens, the token refresh should occur during validation and the new token and refresh token returned in the response.
