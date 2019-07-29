# Liquid Dev Graphical Interface Standards

## Purpose & scope

These standards apply to all graphical user interfaces, both mobile and web within the Liquid Dev context.

## General

* General style should follow [Material Design](https://material.io/) standards in general.
  * This is enforced in the first instance by the implementation toolset.
  * Specific requirements as relates to UI should be incuded in the implementation spec. Developers are not expected to apply any particular Material Design recommendation or standard other than those included in the implementation spec.
* Where not specifically specified, [Material UI](https://material-ui.com/) components should be utilized for all elements.
  * Work may be rejected for failing to use reasonably obvious components. E.g., if the spec says "place a button", then the Material UI `Button` or `IconButton` component is expected to be used.
* Implementation specs may refer to examples and include language such as "It should look like this" and link to a visual example.

## Viewport Sizes & General Layout

* All user content must be accessible and properly rendered on viewports:
  * of a minimum of 320 px wide (iPhone 5/SE in portrait),
  * and a maximum of 1920 px wide. Wider viewports should follow the same rules as the 1920 rules with no further special casing.
* The [Material UI breakpoints](https://material-ui.com/layout/breakpoints/) should be used whenever sufficient.
  * Special case breakpoints may be introduced when necessary.
* Layout is generally accomplished on a grid (using the [`Grid` component](https://material-ui.com/layout/grid/) and the underlying [flexbox model](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox).
  * Specific rules for grid layout should be included in any specification as necessary.
* Where a spec describes a relation between visual artifacts, these should hold true for all screen sizes and breakpoints, unless different behavior is specified for particular breakpoints or sizes. E.g.:
  * "The text should be right-aligned to the row and the button left-aligned, both vertically centered" would hold true for all breakpoints.
  * "Each card should stack under the xs breakpoint, display 2 to a row up to the md breakpoint, and display 3 to a row at the lg breakpoint and beyond."

## Styling

* Styling should be done with JS+CSS and inline style.
* "Styling components" should be used where appropriate. These may be used to abstract common styling rules affecting multiple components or to break apart or break out complex styling.
* Adding lobal styling rules or modifying the `Theme` must be avoided unless specified in the spec or explicitly approved.

## Linking

* All user views *should* be "linkable", meaning that single URL link, with no request body, can be saved to return the user or other appropriately authorized users to the same view.
* GUIDELINE: Where possible, the "link" should be the link displayed in the a user's web browser and identical with the URL used to access the view. When this is not possible, a "share" control should provide access to such a link.
* GUIDELINE: The linked view should be understood as inherently dynamic and, of course, may not contain the same results upon subsequent visits.
