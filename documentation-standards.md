# Liquid Dev Documentation Standards

## Purpose & scope

These standards address standards and best practices for documentation within the Liquid Dev framework.

## Terms

Within the scope of Liquid Labs products and technologies, the following should
be understood as follows:

* **a guideline** provides guidance on how to understand and/or implement a standard.
* **guideline section** is a section within a standards document which contains only guidelines and no standards. These may be provided as introductory, overview, and summary sections, as well as for other purposes.
* **guideline statement** is a single sentence or short paragraph embedded within and in proximity to the standards to which in refers.
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

* Standards *must* be itemized with a single "standard statement" per line.
* Standards *must* be written "one rule per statement".
* GUIDELINE: In practice this means that most standard statements should consist of a single sentence. Standard statements include multiple sentences when it is cleaner or more clear to do so. Subsequent sentences may further specify or expand on prior statements.
* The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document *must* be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).
* GUIDELINE: In Liquid Dev compliant documents, the terms 'required', 'recommended', and 'optional' may be used in guidelines, summaries, or other supporting documentation, but should be avoided in standard statements where the 'must', 'should', and 'may' keywords should be preferred. "Shall" should be avoided altogether redundant.
* Each standard statement *must* include a single use of either 'may', 'should', or 'must', or the negation, to indicate the requirement level.
* GUIDELINE: Note that 'must not' indicates a negative requirement and 'should not' indicates a negative recommendation. The term 'may not', which would be equivalent to 'not optional',
* Standard statements *should* use examples sparingly.
* Guideline section titles *must* be begin with 'GUIDELINE:' to indicate that the section is composed of guidance rather than standards.
* Guideline statements *must* be prepended with 'GUIDELINE:' to indicate that the following statement is guidance and not a standard.
* Guideline statements *should* be embedded within the standards document and used in proximity to the standard statements they modify.
* 'Sub-standards' *must* be indicated as a clear sub-list nested under a single standard statement.
* GUIDELINE: A 'sub-standard' should always be written with the hyphen and understood as similar to a 'sub-task'. Do not confuse the concept with "substandard".
* Sub-standard statements *must* be of compatible requirement levels with regard to the super-statement.
* GUIDELINE: E.g.: a required primary standard may have required, recommended, and optional sub-standards; a recommended standard may have recommended and optional, but not required sub-standards; an optional standard may only have optional sub-standards.
* A standard *must not* be considered fulfilled until all sub-standard statements are fulfilled.
* A standard statement *may* utilize enumerated points.
* GUIDELINE: A standard statement using enumerated points must not include requirement level keywords within the enumerated points, which are understood as equivalent to a comma separated list of the primary statement. This is the primary method of distinguishing a standard with sub-standards and a standard with enumerated points, which may both render in a similar fashion.
