# Coding guidelines

## Element display
If an element has to be hidden at some point we prefer not to render it at all instead of using a css class to hide it (especially using tailwind).
 - Faster to render ;
 - Testing is easier (hiddden class from tailwind is not recognized as a hiding param by react-testing-library's `not.toBeVisible`).
