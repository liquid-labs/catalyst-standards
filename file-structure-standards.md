# Liquid Dev File Structure Standards

## Terms

Within this standard, the following terms should be understood as follows:

* **technology**: A high level language, protocol, or technical service. The following are considered "technologies" under this definition:
  * A programming language such as "Javascript", "C", and "Ruby".
  * Each (mostly) compatible class/implementations of DBs such as "SQL", "MongoDB", and "Cassandra".
  * "Frameworks" are not generally considered technologies themselves, but are rather viewed as "within" a technology.
  * It is certainly possible for technologies to encapsulate other technologies. In this case, the "highest" or "outermost" technology should be used for organizational purposes.

## General conventions

* Folder and file names should match be alphanumeric and use '-' for internal spacing.
* File names should include an extension set off by '.'.
* Names should be all lower case unless indicated by technology or other applicable conventions.
* Directories should not be collapsed, but rather follow the standards laid out herein in order to provide context. E.g., use `src/js/components/widget/SomeComponent.jsx` even if `SomeComponent.jsx` is the only file in `src`.

## Project root

* The following files must be in the Catalyst project root directory:
  * `README.md`
  * `LICENSE.txt`
  * `.catalyst`
  * `package.json`
* All other non-transitory not exclude by `.gitignore` should be located in a subdirectory.
* One of the following standard subdirectories should be used whenever appropriate:
  * `src`: any source code and configuration files.
  * `data`: any schema and static/initialization data files.
  * `public`: for webapp projects, these are files which are directly served.
  * `docs`: all documentation about the project excepting documentation inline with code and the `README.md` file.

## `src` & `data`

* `src` and `data` should directly contain only folders named after the "general technology" which would consume the files.
* The following are the Catalyst standard technologies which may be found within `src`:
  * `bash`
  * `go`
  * `js`
* The following are the Catalyst standard technologies which may be found within `data`:
  * `sql`
* Additional child folders should be used where none of the above are appropriate.
* SQL and other DB-related code dealing with procedures which specifically enforce constraints and/or process data in response to standard SQL triggers should be stored in `data` next to the table definitions. Such procedures are considered part of the data model primarily and SQL "code" secondarily.
* SQL and other DB-related code that implements procedures called on an ad-hoc basis in response to non-trigger events (such as user actions or schedule events) should be stored in `src`.

### `js` + React

Where a Catalyst package is React library or application, the following standards should be applied to `js`.

* `components` for all React component files.
* `components` is further divided into:
  * `views`: for top level components that define the "user view".
  * Files within `view` should end with `View` where useful to distinguish from a widget. Where the "simple" name of a component implies its "view" nature, then the `View` suffix may be omitted, such as with `Dashboard.jsx` because a "dashboard" is naturally the thing which one would view.
  * `widgets`: visible/content generating components used to build higher level widgets and views.
  * `layouts`: non-visible/non-content components used to build higher level layouts, widgets, and views.
  * `utils`: non-visible/non-content components which effect flow and/or modify other components.
  * Files within widget, layout, and util files should generally not use any 'type' suffix as is done with the view files.
