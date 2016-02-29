---
title: Implementing OAuth v1
tags: [api_spec, oauth]
summary: "This article provides information regarding integration with OAuth v1 applications."
---

## Starting the OAuth Flow

The `GET /oauth1` endpoint performs the initial setup for OAuth version 1 accounts.  Included with the request is a single query argument, `callback_uri`, which is the redirect URL that the user should be expected to be redirected to upon successful authentication with the third-party service.  Return body should at least include a `redirect_uri` that the user should be forwarded to in order to complete setup.  Replies are then POST'ed to this endpoint (see below).

```javascript
// GET /oauth1
{
    "redirect_uri": "https://trello.com/1/OAuthAuthorizeToken?oauth_token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&name=TrelloIntegration"
}
```

*Note:* The OAuth implementation requires the account identifier to be `oauth` for OAuth version 1.

## Finalizing accounts after user authorization

The `POST /oauth1` endpoint performs the final setup and validation of OAuth version 1 accounts.  Information as received from the third party upon redirection to the previously posted `callback_uri` are sent to this endpoint, with other applicable account information, for final setup.  The account is then validated and, if successful, the account is returned; if there is an error, it is to be raised appropriately.