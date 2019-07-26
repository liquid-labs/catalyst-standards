# Liquid Dev Package Standards

## Scope

These standards address the organization of software code and related work products into "packages".

## Terms

* **package** the fundamental unit of distribution for code (as libraries, frameworks, applications, etc.).

## Package organization

* All packages are published primarily as node packages using the NPM protocol.
* Each package must contain at least one `package.json` file in the package root.
* Additional `package.json` files may be included as part of example code or as part of an embedded example project.
* GUIDELINE: Do consider breaking example projects out into an independent project/package as well, as this is often cleaner.
* Each package should contain at most one `go.mod` file.
* Packages should be organized as "micro" packages (as opposed to monolithic packages).
* GUIDELINE: If a package contains a subset of code which is independent, or through refactoring of base dependencies within the package, be made independent and that subset is utilized without reference to the remainder of the code in the package, then that subset should be considered for separation into an independent package.


## Publishing standards

* All published packages should:
  * conform to the [Liquid Dev Testing Standards](./testing-standards.md)
  * pass all tests
  * ensure that all dependencies refer to published packages and, in particular, that local packages (such as those linked through `yalc` or go-module replacements) are not referenced in the published dependencies; this applies specifically to:
    * `package.json`
    * `go.mod`
  * ensure that where the `package.json` and `go.mod` files refer to the same package, they refer to the same version of that package.
