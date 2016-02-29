---
title:  Brute Force Attacks
tags: [publish, security]
---

Since all third-party applications are HTTP services that are publicly available on the internet, one should always be mindful of the possibility of brute-force attacks.  While brute-force attacks are unlikely due to the "security through obscurity" obtained by running your application service on a non-standard HTTP port, they should not be disregarded as a possibility.  Brute-force attacks can be used against the `POST /validate` endpoint to perform brute-force attempts at cracking login credentials for the services and/or platforms that you integrate with.  This poses a major security concern, especially if your application handles confidential, privileged, or otherwise sensitive information.

In order to mitigate these risks, it is recommended that application developers only accept requests from valid Vizydrop servers.  All requests coming from Vizydrop's applications gallery will contain a `Server` header similar to `Vizydrop-Hermione/v.1.0.0`.  However, because these headers are easily spoofed, we recommend that developers utilize other means to help combat this risk, such as:

- Rate Limiting
- Allowing only Vizydrop IP addresses

Rate limiting is the least recommended of these two methods as they still leave your application susceptible to denial of service (DOS) attacks.  This is the same reason why we recommend performing IP-address validation using a firewall, rather than in the application itself.  Linux servers can take advantage of the `/etc/hosts.deny` file (or your favorite flavor's equivalent).  Enterprise-class firewalls, however, are the preferred method.