# Liquid Dev Documentation Standards

## Purpose & Scope

These standards address standards and best practices for documentation within the Liquid Dev framework.

## Terms

Within the scope of Liquid Labs products and technologies, the following should
be understood as follows:

* **a guideline** provides guidance on how to understand and/or implement a standard.
* **inline documentation** is documentation embedded within source or configuration files
* **requirement level** indicates whether a given *standard statement* is required, recommended, or optional.
* **standalone documentation** is any documentation in a file which is purely documentation. In other words, not embedded within source or configuration files.
* **a standard** defines an objective, measurable objective which be either required, recommended, or optional per the *requirement level*.

## Standalone documentation types and formats

* MarkDown for text. TODO: expand.
* For UI.
* For types:
  * network diagram
  * software spec
  * general spec (like this)

## Standards

* Standards must be itemized with a single "standard statement" per line.
* Standards must be written "one rule per statement".
* GUIDELINE: In practice this means that most standard statements should consist of a single sentence. Standard statements include multiple sentences when it is cleaner or more clear to do so. Subsequent sentences may further specify or expand on prior statements.
* The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).
* GUIDELINE: In Liquid Dev compliant documents, the terms 'required', 'recommended', and 'optional' may be used in guidelines, summaries, or other supporting documentation, but should be avoided in standard statements where the 'must', 'should', and 'may' keywords should be preferred. "Shall" should be avoided altogether redundant.
* Each standard statement must include a single use of either 'may', 'should', or 'must', or the negation, to indicate the requirement level.
* GUIDELINE: Note that 'must not' indicates a negative requirement and 'should not' indicates a negative recommendation. The term 'may not', which would be equivalent to 'not optional',
* Standard statements should use examples sparingly.
* Guideline statements should be embedded within the standards document and used in proximity to the standard statements they modify.
* 'Sub-standards' must be indicated as a clear sub-list nested under a single standard statement.
* GUIDELINE: A 'sub-standard' should always be written with the hyphen and understood as similar to a 'sub-task'. Do not confuse the concept with "substandard".
* A standard is considered met when all sub-standard statements are fulfilled, regardless of the sub-standard binding (? TODO: what's the term for the optional/recommended/required relationship ?)
