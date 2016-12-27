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
- _subject_: Can be a plain CSS selector, or a procedural cosmetic filter.
- _needle_: The literal text which must be found, or a literal regular expression.
- Examples:
    - `example.com##body > div:last-of-type span:has-text(/^Promoted by/)`

### `subject:if(arg)`

- Description: Select element _subject_ if and only if the result of evaluating _arg_ is one or more elements.
- Chainable: Yes.
- _subject_: Can be a plain CSS selector, or a procedural cosmetic filter.
- _arg_: A valid plain CSS selector or procedural cosmetic filter, which is evaluated in the context of the _subject_ element.
- Examples:
    - `mobile.twitter.com##main [role="region"] > [role="grid"] > [role="rowgroup"] [role="row"]:if(div:last-of-type span:has-text(/^Promoted by/))`

The purpose of `:if(...)` resembles the purpose of the `:has(...)` operator, however the difference is that the argument for the `:has(...)` operator **can not** be anything else than a plain CSS selector. This limitation to the `:has(...)` operator is to ensure that they will be able to be implemented declaratively once a browser supports `:has(...)` as a valid CSS4 selector.

### `subject:if-not(arg)`

Essentially the same as the `:if(...)` operator, except that the element _subject_ is selected if and only if the result of evaluating _arg_ is exactly zero elements.

### `subject:matches-css(arg)`

- Description: Select element _subject_ if and only if the result of evaluating _arg_ is one or more elements.
- Chainable: Yes.
- _subject_: Can be a plain CSS selector, or a procedural cosmetic filter.
- _arg_: A declaration in the form `name: value`, where `name` is a valid CSS style property, and `value` is the expected value for that style property. `value` can be a literal text or literal regular expression.
- Examples:
    - `extratorrent.*##body > div[class]:matches-css(position: absolute)`
    - `facet.wp.pl##div[class^="_"]:matches-css(background-image: /^url\("data:image/png;base64,/)`

### `subject:matches-css-before(arg)`

Same as `:matches-css(...)`, except that the style will be looked-up for the `:before` pseudo-class of the _subject_ element.

### `subject:matches-css-after(arg)`

Same as `:matches-css(...)` except that the style will be looked-up for `:after` pseudo-class of the _subject_ element.
