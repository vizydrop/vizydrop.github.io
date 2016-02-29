---
title: DateSpec DSL
tags: [api_spec, date_dsl]
keywords: popovers, tooltips, user interface text, glossaries, definitions
---

In order to make filtering by dates and date ranges easier on the end-user, Vizydrop uses a custom domain specific language to represent dates and date ranges.  The syntax allows a user to specify either a static date or a dynamic date range using simple mathematic operators and plain English statements.

## Arbitrary Dates

Dates can be easily and quickly specified without any knowledge of the DSL by simply inserting a date in either _MM/DD/YYYY_ or _MM-DD-YYYY_ format.

The Date Spec DSL also includes various keyword elements that can be used to quickly insert dynamic values.  In your date specification you may specify _today_, _tomorrow_, and _yesterday_ to get the appropriate date value.  These date values will always parse iun relation to the current day, allowing you to specify a date or date range of, or relative to, these dates.

## Periods

Periods in the date spec DSL is where the majority of the magic happens.  The DSL understands various time periods, as outlined in the chart below.  These time periods can be referenced either aligned to their appropriate boundaries (calendar months, full weeks, quarters, etc.) or arbitrarily aligned to a particular day (the past month, past week, etc.).

| period         | aligned value                  | arbitrary value                |
|----------------|--------------------------------|--------------------------------|
| day            | a day                          | a day                          |
| week           | calendar week (Sun - Sat)	  | 7 days                         |
| month          | calendar month (1st day start) | 30 days                        |
| quarter        | calendar quarter (Q1, Q2, etc.)| 90 days	  				       |
| year			 | calendar year (Jan 1 - Dec 31) | 365 days                       |

## Basic Math

In order to make the DSL more dynamic, you can perform simple addition and subtraction operations to your dates.  These operations can occur between dates and periods.  Consider the following examples:

| DSL statement                   | value                                          |
|---------------------------------|------------------------------------------------|
| today + 1 day                   | tomorrow                                       |
| yesterday - 6 days              | one week (7 days) ago                          |
| today - 2 months				  | two months (60 days) ago                       |
| 12/1/2008 + 6 months			  | 6/1/2009                                       |
| 12/31/2009 + 1 year			  | 12/31/2010                                     |

**Note:** It is possible to chain together multiple math operations.  For example, `today - yesterday + tomorrow - 1 day` would yield today.

## Using Periods, LAST and PAST keywords

Periods can be referenced, as mentioned earlier, either aligned to an appropriate date boundary or arbitrarily aligned.  When using an aligned period, the period fits to the calendar representation of that period.  For example, an aligned month starts on the 1st day and ends on the last, whereas an arbitrary month would represent 30 days starting or ending on a particular day.

**Note:** Both the LAST and PAST keywords will return only the _start date_ of the period unless coupled with an advanced statement.  See the _IN_ statement below.

### LAST Periods

The _last_ keyword creates a period aligned to the previous period represented.  Consider the following examples:

| DSL statement        | value                                                 |
|----------------------|-------------------------------------------------------|
| `last week`          | the previous full calendar week starting from Sunday  |
| `last month`         | the previous full month, starting from the 1st		   |
| `last quarter`	   | the previous full quarter                             |

### PAST Periods

The _past_ keyword creates a period whose end date is aligned to today.  Consider the following examples:

| DSL statement        | value                                                 |
|----------------------|-------------------------------------------------------|
| `past week`          | the past 7 days                                       |
| `past month`         | the past 30 days                            		   |
| `past quarter`	   | the past quarter (90 days)                            |

## IN/DURING statements

To easily specify a LAST or PAST period as a date range rather than as the start date of the period, you can use the _IN_ statement.  Prefixing a LAST or PAST keyword with _IN_ or _DURING_ will make the parser return a date range rather than a single date.

| DSL statement           | value                                          |
|-------------------------|------------------------------------------------|
| `in the past week`      | between one week ago and today                 |
| `during the past week`  | synonymous with `in the past week`             |
| `in the last week`	  | between Sunday and Saturday last week          |
| `during last month`	  | between the 1st of last month and the last day |
| `in the past quarter`   | between 90 days ago and today                  |
| `during the past year`  | occurring within one year of today             |
| `in last year`          | in the previous calendar year                  |

**Note:** _IN_ and _DURING_ are two synonymous keywords in the DSL.  The literal _THE_ is optional and can be omitted if desired.  Both will achieve the same result and it is a matter of personal preference.

## SINCE statements

The _SINCE_ keyword allows you to quickly specify a date range using a specified start date and always using today as the end date of the period.  A _SINCE_ can be followed with some representation of a date.  The result will be a date range between that date and today.

| DSL statement           | value                                                |
|-------------------------|------------------------------------------------------|
| `since last week`       | between last week Sunday and today                   |
| `since last month`	  | between the 1st day of the last full month and today |
| `since 1/1/15`		  | between Jan 1, 2015 and today                        |

## BETWEEN statements

The _between_ keyword allows you to specify a date range or minimum and maximum values to filter on with more power and precision than an _IN_ or _DURING_ statement.  The full format for this statement is `BETWEEN date AND date` where both dates are some representation of a date (this can be an arbitrary date, keyword, math operation, or period).

Consider the following examples:

| DSL statement                                  | value                                                        |
|------------------------------------------------|--------------------------------------------------------------|
| `between 1/1/98 and 12/31/98`                  | between Jan 1 and Dec 31, 1998                               |
| `between 1-1-13 and today`					 | between Jan 1, 2013 and today                                |
| `between today - 1 month and today`			 | within the past 1 month, synonymous with `in the past month` |
| `between today - 3 months and today - 1 month` | between 3 months ago and 1 month ago                         |
| `between last year and today - 6 months`       | between Jan 1 last year and 6 months ago                     |

# Receiving Parsed Dates

The Vizydrop DateSpec DSL parses an input date with each use of a filter that utilizes a date-type field.  These dates are provided to application connectors as either a string-representation of a single date or a dictionary object representing a date range.  User-input dates and date ranges are timezone-naive.

When the user enters a single date in a field, this date will be parsed and further represented as a string in [ISO-8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) format.  Dates without times are represented as `YYYY-MM-DD` where dates with times are represented as `YYYY-MM-DDTHH:MM:SS`.

When a user enters a DSL that results in a date range, these dates will be passed to connected applications as dictionaries with two keys, `_min` and `_max`, holding the minimum and maximum dates in the range.  Their values will be represented as a string in [ISO-8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) format.  If a user enters a date range with no defined maximum, such as would be the case when using the `SINCE` keyword, the `_max` key will not be present and the dictionary will have only `_min` as its single key-value pair.