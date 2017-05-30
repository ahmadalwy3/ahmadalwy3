[Back to _"Static filter syntax"_](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax)

***

The concept of procedural cosmetic filtering was introduced with uBlock Origin ("uBO") [version 1.8.0](https://github.com/gorhill/uBlock/releases/tag/1.8.0).

The initial implementation was revised to allow chained/recursive use of the procedural operators with version [1.11.0](https://github.com/gorhill/uBlock/releases/tag/1.11.0)+. There is no limit on the number of operators chained, or the number of recursion level, aside common sense. As a reminder, use procedural cosmetic filters only for when plain CSS selectors won't solve a case.

Normal, standard cosmetic filters are _declarative_, i.e. they are used as selector in a CSS rule, and completely handled by browsers through `style` tag elements.

_Procedural_ means javascript code is used to find DOM elements which must be hidden. A procedural cosmetic filter makes use of cosmetic filter _operator_, which will tell uBO how to find/filter DOM elements in order to find which DOM elements to target.

**Important:** Procedural filters must always be specific, i.e. prefixed with the hostname of the site(s) on which they are meant to apply. If a procedural cosmetic filter is generic, i.e. meant to apply everywhere, it will be discarded by uBO. Examples: Good, because specific: `example.com##body > div:has-text(Sponsored)`. Bad, because generic: `##body > div:has-text(Sponsored)`. The element picker always prefix automatically the hostname to ensure created cosmetic filters are specific.

Efficient procedural cosmetic filters (or any cosmetic filters really) are the ones which result in the smallest set of nodes to visit. The element picker input field will display the number of elements matching the current filter. The element picker will only consider the entered text up to the first line break, while leaving the rest as is. You can use this feature to break up your filter to find out the size of the resultset of the first part(s) of your filter: the smallest resultset the most efficient is your cosmetic filter.

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

The purpose of `:if(...)` resembles the purpose of the `:has(...)` operator, however the difference is that the argument for the `:has(...)` operator **can not** be anything else than a plain CSS selector. This limitation to the `:has(...)` operator is to ensure that they can be implemented declaratively once a browser supports `:has(...)` as a valid CSS4 selector.

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

### `subject:xpath(arg)`

- Description: Create a new set of elements by evaluating a XPath using _subject_ as the context node (optional) and _arg_ as the expression.
- Chainable: Yes.
- _subject_: Optional. Can be a plain CSS selector, or a procedural cosmetic filter.
- _arg_: A valid XPath expression.
- Examples:
    - `facebook.com##:xpath(//div[@id="stream_pagelet"]//div[starts-with(@id,"hyperfeed_story_id_")][.//h6//span/text()="People You May Know"])`

The `:xpath(...)` operator is different than other operators. Whereas all other operators are used to filter down a resultset of elements, the `:xpath(...)` operator can be used both to create a new resultset or filter down an existing one. For this reason, _subject_ is optional. For example, an `:xpath(...)` operator could be use to create a new resultset consisting of all ancestors elements of a subject element, something not otherwise possible with either plain CSS selectors or other procedural operators.
