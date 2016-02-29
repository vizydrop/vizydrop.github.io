---
title: The Application Class
tags: [sdk, python]
---

The base class of all Vizydrop third-party applications written using the Python SDK extend the `vizydrop.sdk.application.Application` class.  This class contains no functions and only contains a single `Meta` inner-class to define the required information datapoints:

```python
class Trello(Application):
    class Meta:
        version = "1.0"
        name = "Trello"
        logo = None  # Optional
        website = "http://www.trello.com/"
        color = "#0076C0"
        description = "Infinitely flexible. Incredibly easy to use. Great mobile apps. It's free. " \
                      "Trello keeps track of everything, from the big picture to the minute details."
        tags = ['kanban', 'project management', ]

        authentication = [TrelloOAuth, TrelloTokenAuth, ]

        sources = [TrelloCardSource, ]
```

Within the `Meta` inner-class, the `authentication` and `sources` lists contain class names of classes that extend the `vizydrop.sdk.account.Account` and `vizydrop.sdk.source.DataSource` classes, respectively.

All Meta fields except `logo` are required.  The `logo` attribute can be used to specify a URI where a SVG logo for your application can be found.  Alternately, you can place your logo in a file called `logo.svg` in your application's main module directory (where you have your `Application` class).  If a logo file is provided, it will automatically be served by the SDK at `GET /logo`.
