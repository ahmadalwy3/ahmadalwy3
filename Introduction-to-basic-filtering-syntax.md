## Cosmetic filtering

Example DOM tree:

    <div id="unique-identifier" class="first-class second-class" data-storage="123-456">
    <div class="first-class">

- `##` - this is always present in cosmetic filters - this means this is cosmetic filter
- `##div` - selecting by element type
- `###unique-identifier` - selecting by `id`, `##` + `#` - this should be very efficient, because there should be only one unique identifier for page
- `##.first-class` - selecting by `class`, `##` + `.` - will match other elements with same class, so:
- `##.first-class.second-class` - use both classes to select only first line from example DOM.

Using dot for classes automatically split value of the class attribute on space characters.

Selecting by attribute:

- `##[data-storage="123-456"]` - will match exactly
- `##[data-storage^="123-"]` - will match from the beginning 
- `##[data-storage$="-456"]` - will match from the end
- `##[data-storage*="3-4"]` - will match in the middle
- `##[id="unique-identifier"]` equivalent of `###unique-identifier`
- `##[class="first-class"]` equivalent of `##.first-class`, but will match only second line from example DOM - class attribute is compared literally, no splitting on space characters.