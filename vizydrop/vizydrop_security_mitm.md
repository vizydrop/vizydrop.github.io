---
title: Man In The Middle (MITM) Attacks
tags: [publish, security]
---

Because all communication between Vizydrop services and third-party applications is done via standard hypertext protocols, the same security considerations that you would expect for a publicly available web application are applicable to Vizydrop third-party applications.  Because the default communication for the system is HTTP, developers should be mindful that all communication - including sensitive information such as login credentials or contidential/proprietary information in data sources - are transmitted via plain text.  While unlikely, a man-in-the-middle (MITM) attack could allow unauthorized parties to access sensitive information.

Implementing HTTPS in place of HTTP greatly diminishes the risk of sensitive information being intercepted and read while in transit between your third-party application and Vizydrop's servers.  This can be done either in your implementation or can be achieved by placing a SSL load balancer and/or proxy between the internet and your third-party application.  Common solutions for a SSL load balancer and/or proxy include software solutions such as HAProxy or stunnel.