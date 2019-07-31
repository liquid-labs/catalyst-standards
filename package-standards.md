# Liquid Dev Package Standards

## Purpose & scope

These standards address the organization of software code and related work products into packages. General file layout structure and naming conventions can be found within the [Liquid Dev File Structure Standards](./file-structure-standards.md).

## Terms

* **package** the fundamental unit of distribution for code (as libraries, frameworks, applications, etc.).

## Package organization

* All packages are published primarily as node packages using the NPM protocol.
* Each package must contain at least one `package.json` file in the package root.
* Additional `package.json` files may be included as part of example code or as part of an embedded example project.
* GUIDELINE: Do consider breaking example projects out into an independent project/package as well, as this is often cleaner.
* Each package should contain at most one `go.mod` file.
* Packages should be organized as "micro" packages (as opposed to monolithic packages) which enable a well defined set of related ontologies and behaviors which cannot be easily or usefully decomposed into clear component ontologies or behaviors.
* Packages should not generally be split by technology.
* GUIDELINE: In particular, where ontologies are represented in multiple technologies (such as SQL, go, and JS) each technology-specific model should be defined within the same model package.
* GUIDELINE: Where a package deals with transmission across technology boundaries, both technologies "endpoints" should be contained in the same package. E.g., a REST-ful framework that generates common REST responses from go-implemented endpoints and JS consumer libraries that know how to unpack the response.
* `go.mod` must be placed in the package root. TOOD: It seems that 'replace' directives only work when this is the case. However, this produces warnings from the GCP dev-server tool. It's not clear what's going on.

## Versioning

* Published packages *must* utilize a valid [semver](https://semver.org/) version.
* Published package versions *should* be understood in light of these standards.
* Packages *should* set the pre-release ID to either 'alpha', 'beta', or 'rc'.
  * 'alpha' indicates an unreliable runtime and/or unstable interface.
  * 'beta' indicates an unreliable runtime and relatively stable, but still uncertain interface.
  * 'rc' indicates a generally reliable runtime and guaranteed interface.
* GUIDELINE: 'alpha' should be used for prototype and experimental builds. The "alpha -> beta -> rc" progression is critical because semver does NOT understand these terms themselves, but rather sorts pre-release versions alphabetically.
* Packages *must* set the pre-release ID to ensure proper sorting of published versions.

## Publishing standards

* All published packages *should*:
  * conform to the [Liquid Dev Testing Standards](./testing-standards.md)
  * pass all tests
  * ensure that all dependencies refer to published packages and, in particular, that local packages (such as those linked through `yalc` or go-module replacements) are not referenced in the published dependencies; this applies specifically to:
    * `package.json`
    * `go.mod`
  * ensure that where the `package.json` and `go.mod` files refer to the same package, they refer to the same version of that package.
  * have a clean `npm audit` report at the time of publishing.
  * include a `README.md` file.
* The `package.json` `description`, the first content line of the `README.md` (after the header), and the GitHub project description *should* match.
