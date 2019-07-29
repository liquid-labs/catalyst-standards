# Liquid Dev Development Standards

## Purpose & scope

These standards address standards around the development process.

## Terms

* **work** when used in the context of "work on/in/within a package/code/app/etc." refers to the process of modifying any file within a package and the process of validating and publishing those changes.
* **local work** is work initiated and visible exclusively or primarily to a private workstation or device. Such work may be shared through the standard means, but is not considered "generally available".

## Workflow

### Workflow scope

* These standards address work performed within one or more Liquid Dev packages.
* We consider any external changes as appearing exclusively within the context of dependency management as expressed within the `package.json` and/or `go.mod` files.

### Local work

These standards are implemented by the Liquid Dev CLI project. (TODO: link after name update)

* Local work may involve multiple packages and the standards in this section apply equally to each package in isolation and the entire set of packages involved in a given unit of work.
* Local changes should be visible in a minimal amount of time.
  * It must be possible to accomplish update of all local assets, up to and including updates of any local service and/or interactive components (such as a locally hosted website), through a single user action.
    * Options for rebuilding, redeploying, and managing assets on a project-by-project basis should be provided, though these need not be robust against all user errors.
  * Automated "rebuild on change" should be used in cases where such a rebuild can be accomplished quickly.
  * In cases where a rebuild cannot be accomplished quickly,
