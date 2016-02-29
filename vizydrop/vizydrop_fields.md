---
title: Fields
tags: [api_spec]
---

Fields in Vizydrop denote either user-supplied fields or fields within an information schema.  There are various types of fields that each represent a different type of data.  Fields are also used internally to denote information both required and optional for accounts and filters.

## Field Types

The table below lists the types of fields referred to in the Vizydrop app REST API and in the Vizydrop SDKs.  The first column denotes the string name of the type as expected in the API, the second column the type of underlying data, and any comments and remarks for each field type.

| type 		| datatype		| comments and remarks						|
|-----------|---------------|-------------------------------------------|
| id        | string/uint   | a unique identifier for a record; can be either a string or unsigned integer |
| text 		| string		| UTF-8 encoding, if necessary				|
| number	| numbers		| can be decimal, integer, float, or currency |
| url 		| URI 			| SDKs validate as either HTTP, HTTPS, or FTP protocols |
| date 		| date 			| may also include time; ISO-8601, can also provide relative times (see [Date Spec DSL](datedsl.md)) |
| bool 		| boolean		| validates as true/false or 0/1 			|
| multilist	| variant		| allows multiple selections, designed to be used with filter datalists |
| range		| variant		| allows the user to select a range
| link 		| URI 			| internal type used with accounts and filters to display a help link |
| password	| string		| only used in account schemas, rendered as a password input |

### A Special Note on Dates

Dates, both with and without times, that are parsed as a result of user-input (through the [Date Spec DSL](datedsl.md)) are `timezone-naive` objects.  Dates received from connected applications may be either aware or naive of timezones and should represent those dates as strings in an [ISO-8601 format](http://www.iso.org/iso/catalogue_detail?csnumber=40874).

## Fields in the SDKs

Fields are represented in different ways in the software development kits provided for creating third-party applications.  In the [Python SDK](sdk/python.md), fields are represented as different classes in the `vizydrop.fields` module.