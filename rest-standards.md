# Liquid Dev REST Standards

## Purpose & scope

This document fleshes out the Liquid Dev REST standards.

As any REST intro will tell you, REST is not a specification. Rather, it is a collection of concepts and loose standards. Liquid Dev REST Standards are, in contrast, a specification that fully specifies how REST-ful APIs are to be build.

## Terms

* **list call** is a REST-ful API call which works with a list or set of resource items.

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
* GUIDELINE: Particularly complicated filters (or searches) that cannot naturally be represented as `<key>=<value>` constructions may use the request body. However, even in these cases, backend implementations should try and provide a mechanism for directly linking to all results. See [Liquid Dev GUI Standards, "Linking" section](./gui-standards.md#linking)
* URL parameters *should* not be used for other purposes.
* GUIDELINE: In other words, use the request body should be used for all data transfers. This more or less boils down to "use only parameter (where possible) in list `GET` calls and use the request body for everything else".

### Authentication

* Authenticated requests *must* be indicated by including a single `Authorization` header in the request with a value using the `Bearer <token>` format.
* GUIDELINE: Note that this is more properly a matter of request authentication than authorization, despite the slightly unfortunate header header name.
* GUIDELINE: Refer to [Liquid Dev Authentication & Authorization Standards](./authentication-and-authorization-standards.md) for additional guidance on those subjects.
