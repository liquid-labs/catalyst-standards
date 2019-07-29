# On trailing slashes

## Purpose & scope

One of the many perennial questions regarding REST-ful APIs is how to handle trailing slashes. E.g., should be have `/persons` or `/persons/`? ([Here's one such discussion.](https://restfulapi.net/resource-naming/))

## Always include a trailing slash

The primary reason why we recommend always including a trailing slash is because it is necessary for relative URI and general semantics. Consider `/company/123/employees/` vs `/company/123/employees`.

REST endpoints should be hierarchical and contextual. `/company/123/employees/` and `/company/123/employees` would both be understood as "the employees of company 123". If we've made a request and the response contains relative links, how will they be understood?

* In a context, `..` should get you back to the parent. In this case, `..` should answer "Employees of which company?"
  * Applying the `..` relative link to `/company/123/employees/` resolves correctly to `/company/123/`
  * Applying the link to `/company/123/employees` resolves to `/company/`, which is not what we want.
* If we think of "simple browsing through lists", `..` should get you back to the list.
  * Applying the `..` relative link to `/company/123/` resolves correctly to `/company/`.
  * Applying the link to `/company/123` resolves incorrectly to `/`.
* This always works going forward. Applying `./employees/` to a company resource should resolve to the employees.
  * `/company/123/` would indeed resolve to `/company/123/employees/`.
  * But `/company/123` would resolve to `/company/employees`.

This point, along with the relative resolution algorithm, is discussed in greater detail [here](https://cdivilly.wordpress.com/2014/03/11/why-trailing-slashes-on-uris-are-important/). To make the non-slash versions work with relative links, you would get odd results. E.g., "The employer of `/company/123/employees` is `./`." and "The employees of `/company/123` are found at `./123/employees`".

## Alternatives

In considering the question, there are three basic options.

_Option 1:_ Always include a trailing slash; as discussed above.

_Option 2:_ Include a trailing slash for "group" resources, but no trailing slash for "individual" resources. This seems to be the most popular option. Perhaps because, as [Martin York points out](https://softwareengineering.stackexchange.com/a/187006/113880), this is what was done in the original paper on REST. This view is also held by the very good and (seemingly) popular [REST Resource Naming Guide](https://restfulapi.net/resource-naming/).

_Option 3:_ Never include a trailing slash. This is argued by [some](https://blog.restcase.com/7-rules-for-rest-api-uri-design/) on the basis that:

1. The slash doesn't add any syntax.
2. Some assert it can be confusing to users. (Though we have not been able to find reasoning on this).
3. The slash should be used to indicate hierarchy. The implication (seemingly) being that there is no further hierarchy beyond the final "path element".

To be fair, the main argument referenced above is not so much that the "API" should not include a trailing slash, but that "links to users" should not provide a trailing slash. For us, however, this is an unnecessary distinction. Most links are provided to users behind some label or button, so who cares? And even when the link is printed, it will be "clickable" the vast majority of the time. So again, who cares? Finally, the service is free to redirect either way so when a user might type in a URL (or be given a non-slash ended URL), this can (almost always) be easily dealt with.

On the point of "slashes should indicate hierarchy", we feel the reasoning is incorrect. Just because there is no further hierarchy in the current request doesn't mean that no further hierarchy is available. Even when no further hierarchy is provided by the current API, future versions may do so. In general, it's hard to think of a case where an object could not become a parent in some hierarchy.
