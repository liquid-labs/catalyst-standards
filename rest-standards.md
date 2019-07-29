# Liquid Dev REST Standards

## Purpose & scope

This document fleshes out the Liquid Dev REST standards.

As any REST intro will tell you, REST is not a specification. Rather, it is a collection of concepts and loose standards. Liquid Dev REST Standards are, in contrast, a specification that fully specifies how REST-ful APIs are to be build.

## Terms

* **list call** is a REST-ful API call which returns list or set of resource items.

## Resource naming

* Resources *must* be referred to in the plural when speaking of the resource type in general and specifically when used in a URI.
* When speaking of a resource class, the term "XXXs resources" or "XXXs" *should* be used.
* Resources with non-regular plural forms *should* utilize a regular form where either is generally acceptable or would be generally understood except in the case of collective nouns, in which case the collective form should be used for both resources and items.
* Individual resource items *should* be referred to as singular instances using either the phrase "a XXX resource item", "a XXX item", or "a XXX".

## GUIDELINE: Referring to resources & items

* When speaking of resources in general, documentation should initially prefer references that make it clear that resource is being spoken of. In other words, use the term "persons resources".
* Subsequent references to the resource within the same document may refer to the resource by name directly, e.g. "persons".
* Similarly, the first references to a resource item should use the phrase "resource item" or "item" initially (e.g., "a person resource item" or "a person item") and later may refer to items directly by item-name where context is clear.
* It should be understood that documentation is not always read sequentially, and authors should not rely on an initial expanded reference such as "persons resources" made many paragraphs or sections ago. When in doubt, use an expanded for form for clarity.
* Resource names employing a collective noun will have the same lexical form as the item name. E.g.: `/sheep/`, "the sheep resource" and " sheep resource item". In this case, the term 'resource' or 'item' should generally be used to distinguish the two cases unless the meaning is abundantly clear in context.

## Requests

### URI paths

* All URI paths *must* match one of the three basic forms:
  * the 'resource list' form `/<resource>/`
  * the 'resource item' form `/<resource>/<item ID>`
  * the 'contextualized resource list' form `/<context resource>/<item ID>/<contextualized resource>`
* All URI paths *must* begin with a resource name.
* Any URI path terminated by a resource name, excepting those called with the `CREATE` method, *must* be understood as a 'list call'.
* All URIs *must* end in a trailing slash. Our reasoning is explained in [On Trailing Slashes](./background/rest-trailing-slashes.md).
* Services *may* redirect otherwise valid requests which lack a trailing slash to valid URI with at trailing slash.
* Services *must not* internally forward requests without a trailing slash.

### List results & parameters

* The base result of any given list call *must* be understood as the universe of resource items to which the currently authenticated user has access. (TODO: link to useful section of auth-auth standards)
* The set of resource items selected by a list call *may* be further limited by filter parameters or request body contents.
* Wherever possible such list filters *should* be included in the URL so that the results are "linkable".
* When it is necessary or practical to encode list filters in the request body, a method *should* be provided to provide user agents with a durable link to the results.
* The following parameters *should* be supported for any list resource supporting filtering:
  * `query`: A query string used to limit the results. (TODO: provide query standards and link)
  * `pageIndex`: The index of the 'page' within the results to return.
  * `itemsPerPage`: An integer indicating the requested number of items per page.
  * `sort`: A string indicating the sort method to apply to the results. Allowable values will be defined by the endpoint. (TODO: include in the query standards)
* GUIDELINE: Particularly complicated filters (or searches) that cannot naturally be represented as `<key>=<value>` constructions may use the request body. However, even in these cases, backend implementations should try and provide a mechanism for directly linking to all results. See [Liquid Dev GUI Standards, "Linking" section](./gui-standards.md#linking)
* URL parameters *should* not be used for other purposes.
* GUIDELINE: In other words, use the request body should be used for all data transfers. This more or less boils down to "use only parameter (where possible) in list `GET` calls and use the request body for everything else".

### Authentication

* Authenticated requests *must* be indicated by including a single `Authorization` header in the request with a value using the `Bearer <token>` format.
* GUIDELINE: Note that this is more properly a matter of request authentication than authorization, despite the slightly unfortunate header header name.
* GUIDELINE: Refer to [Liquid Dev Authentication & Authorization Standards](./authentication-and-authorization-standards.md) for additional guidance on those subjects.

## Responses

### Response envelope

* All successful calls resulting in non-erroneous HTTP codes *must* use a standard response envelope as defined here.
* GUIDELINE: The response envelope has the general form of:
```
{
  "message": "A short string describing what happened.",
  "searchParams": {
    "query": "foo AND name=bar",
    "sort": "nameAsc",
    "pageInfo": {
      "pageIndex": 3,
      "itemsPerPage": 20,
      "totalItemCount": 86,
      "totalPageCount": 5
    }
  }
}
```
* All successful API responses *must* be in in JSON format.
* All responses *must* be wrapped in a common envelope with the following fields:
  * `message`: A `message` field with a short string, in English, describing the result of the call *should* be included with all results.
    * A `message` *must* be included for any response with a non-successful HTTP code.
  * `searchParams`: An object describing the page and filter options used to generate the results *must* be included with all list results. `searchParams` has the following fields:
    * `query`: A `query` field *must* be included. This will reflect back the query provided by the user, if any or be an empty string.
    * `sort`: A `sort` field indicating the method used to sort the results must be included in the response.
      * The `sort` field *must* be valid.
      * Where the request indicated a valid `sort` method, that method *must* be reflected in the response.
      * Where no `sort` is specified with the request, a default sort method *must* be defined by the input and reflected in the response envelope.
      * Invalid request `sort` methods *must* result in an error.
    * `pageInfo`: A `pageInfo` object *must* be included with the results. `pageInfo` has the following fields:
      * `pageIndex`: The page index reflected in the results *must* be included in the response envelope.
      * `itemsPerPage`: The number of items included in the page *must* be included in the response envelope.
      * `totalItemCount`: A `totalItemCount` of items selected by endpoint with regard the user access and request filters, regardless of page, *must* be included with any list call.
      * `totalPageCount`: A `totalPageCount` *must* be included.
        * `totalPageCount` must equal `totalItemCount` divided by `itemsPerPage` and rounded up (integer division).
* GUIDELINE: The current REST standards require underlying objects to be strictly counted. This is not always possible, or desirable for "big data" data sets and future versions will support different modes for reporting page info that support approximate counts and "next page" without fully specifying all pages.

### Erroneous responses

* An error response format, as defined here, *must* be used for all responses resulting in non-success HTTP codes.
* An error response *should* include a text body, in English, describing the error.
  * Where possible, the error response text *should* describe specifics of the error without providing any details which could be useful to an attacker.
  * Where no specific details are provided, error response text *should* describe the meaning of the error code.
  * The HTTP error code (numeric and/or string) *may* be reflected in the error response text.

### Response codes
