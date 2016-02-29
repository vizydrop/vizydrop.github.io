---
title: GET /logo - Application Logos
tags: [api_spec]
summary: "This simple endpoint provides a logo for connected applications."
---

The `/logo` endpoint is used to provide a SVG representation of a connected application's logo.  This endpoint is entirely optional.  Valid responses are a HTTP 200 response with a `image/svg+xml` content type, a HTTP 204 (No Content) response if there is no logo, or a 302 redirect to another URI containing the logo.  If no logo is provided, or an error occurs, the application will be represented with our default app logo.

*Note*: if you are using the [Python SDK](../vizydrop/vizydrop_sdk_python.html), you can get your logo integrated by putting it in a file called `logo.svg` in your application's module directory.  The SDK will handle the `/logo` endpoint automatically for you.