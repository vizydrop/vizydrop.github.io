---
title: Python 3 SDK
tags: [getting_started, sdk, python]
---

Vizydrop's applications gallery - codenamed Hermione - is written using the same SDK library provided here.  The Python SDK is the preferred platform for developing your third-party applications as a result of this.

### Requirements

- Python 3 (Python 2 is _not_ supported)
- [Tornado](http://tornado-web.org)

### Installing the SDK

The Vizydrop Python SDK is available on [GitHub](https://github.com/vizydrop/vizydrop-python-sdk) and can be easily installed via PyPi:  `pip install vizydrop-sdk` or `easy_install vizydrop-sdk`.  This will download all required dependencies, such as Tornado, automatically for you.

### Using the SDK

The Vizydrop Python SDK is very easy to use and you can have your custom application running in a matter of a few minutes.  The package provides a series of base classes that you can easily extend to provide your custom datasource.

### Examples

The Vizydrop Python SDK comes with some example applications that can provide a great boilerplate for starting your own integrations.  These examples include integrations that both [read information from flat files](https://github.com/vizydrop/vizydrop-python-sdk/tree/master/examples/flatfile) as well as [pull information from external API's](https://github.com/vizydrop/vizydrop-python-sdk/tree/master/examples/external_api).  An [advanced example of performing concurrent API calls on a paginated API](https://github.com/vizydrop/vizydrop-python-sdk/tree/master/examples/concurrent_external_api) is also included.  Check out the [examples in the Vizydrop Python SDK repository](https://github.com/vizydrop/vizydrop-python-sdk/tree/master/examples).


## Running your app

Running your Vizydrop third-party application is easy once all required subclasses have been written.  To start our third-party application, simply run `python -m vizydrop.tpa <module> <port>` where _module_ is the name of the Python module that contains your subclass of the `Application` class.  Suppose our `Trello` application class exists in a file called `trelloapp.py`, we can run our application by simply running `python -m vizydrop.tpa trelloapp`.  The _port_ argument is optional and allows you to specify on which port the asynchronous HTTP server should listen on (the default is port 8080).  Once your application is running, you may register it on the Vizydrop site as a custom data source!

## Example apps

All public app connectors included in Vizydrop that utilize the official Python SDK are available open-source under the BSD License and can be viewed on [GitHub](https://github.com/vizydrop/vizydrop-python-sdk/tree/master/examples).  Interested in contributing?  We're more than happy to accept pull requests for both the SDK and for our existing applications.