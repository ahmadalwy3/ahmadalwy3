The concept of procedural cosmetic filtering was introduced with uBlock Origin ("uBO") [version 1.8.0](https://github.com/gorhill/uBlock/releases/tag/1.8.0).

Normal, standard cosmetic filters are _declarative_, i.e. they are used as selector in a CSS rule, and completely handled by browsers through `style` tag elements.

_Procedural_ means javascript code is used to find DOM elements which must be hidden. A procedural cosmetic filter makes use of cosmetic filter _operator_, which will tell uBO how to find/filter DOM elements in order to find which DOM elements to target.

## Cosmetic filter operators

### `subject:has(arg)`

- Description: Select element _subject_ if and only if evaluating _arg_ in the context of _subject_ returns one or more elements.
- _subject_: **must** be a plain CSS selector.
- _arg_: **must** be a plain CSS selector.
- Examples:
    - `strikeout.me##body > div:has(img[alt="AdBlock Alert"])`
    - `yandex.ru##.serp-item:has(:scope > .organic > .organic__subtitle > .label_color_yellow)`

The `:has(arg)` operator is actually a planned pseudo-class in CSS4, but as of writing no browser supports it. Instead of waiting for browser vendors to provide support, uBO provides support for `:has(arg)` as a procedural operator. By restricting `subject` and `arg` to be valid CSS selectors, this means uBO will be able to support the `:has(...)` operator declaratively once a browser supports it.

### `subject:has-text(needle)`

- Description: Select element _subject_ if and only if the text _needle_ is found inside the element _subject_.
- Chainable: Yes.
- _subject_: Can be a plain CSS selector, or a procedural cosmetic filter (i.e. chainable).
- _needle_: The literal text which must be found, or a literal regular expression.
- Examples:
    - `example.com##body > div:last-of-type span:has-text(/^Promoted by/)`

