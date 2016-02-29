---
title: DataSource Class
tags: [sdk, python]
---

The `DataSource` class is very similar to the `Account` class described above.  Subclasses of this base class include a `Meta` inner-class, field information defining the underlying data source (if required) defined in a `Schema` inner-class, and a single to handle the retrieval of data:

```python
class TrelloCardSource(DataSource):
    class Meta:
        identifier = "cards"
        name = "Cards"
        tags = ["Kanban", "Cards", ]
        description = "List of cards"
        filter = TrelloCardSourceFilters

    class Schema(SourceSchema):
        id = TextField(description="Card ID")
        name = TextField(name="Name", description="Name of the card")
        # ...

    @classmethod
    def get_data(cls, account, source_filter):
    	# ...
```

The `filter` object within the `DataSource.Meta` class refers the SDK to the `vizydrop.sdk.source.SourceFilter` subclass that contains and handles filter information (see below).  The `SourceSchema` inner-class contains all `vizydrop.fields` that define the underlying data schema.  This information is not required; if it is not provided then Vizydrop will attempt to automatically determine the source schema based on the data provided by the TPA.

The `get_data` class method is the single most important function in an entire TPA.  This is the function that actually performs the gathering of data from the datasource represented by the TPA.  The `account` and `source_filter` arguments will be instances of the `Account` and `SourceFilter` subclasses defined elsewhere in your application.
