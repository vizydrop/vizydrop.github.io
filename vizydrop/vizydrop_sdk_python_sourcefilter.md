---
title: SourceFilter Class
tags: [sdk, python]
---

The `SourceFilter` class simply defines fields that can be used to generate a filter for the data provided by the `DataSource` class.  These classes may also optionally provide datalist functions that return options available for particular filter fields.  This class does _not_ include any `Meta` or `Schema` inner classes as we have previously seen in the SDK.

```python
class TrelloCardSourceFilters(SourceFilter):
    def get_board_options(account, **kwargs):
        client = AsyncHTTPClient()
        req = account.get_request("https://api.trello.com/1/members/me/boards")
        response = yield client.fetch(req)
        options = json.loads(response.body.decode('utf-8'))
        ret = []
        for option in options:
            ret.append({"value": option['id'], "title": option['name']})
        return ret

    boards = MultiListField(name="Board", description="Trello board",
        optional=False, get_options=get_board_options)
```

In this example we see that the user can filter on a field called `boards`, which is not optional and provides a `get_options` function (and therefore can be queried via the `POST /datalist` endpoint).  The `get_options` kwarg refers to a function that takes at least one argument; the first argument passed to the function will be the `Account` object to use when gathering the datalist options.  If additional args are provided, they will be marked as required arguments to gather the datalist and should be named _exactly_ as another field.  In these cases, the value from the respective filter field will be provided to this function.  This allows filter fields that have datalists to be dependent on the values of other fields within the same filter.

The SDK does not provide any automatic mechanism for filtering data gathered from the `DataSource` class according ot the `SourceFilter` class.  The `SourceFilter` class is simply provided as an argument to the `get_data` function and it is up to the maintainer of a solution to decide how the two classes are to interact with one another.
