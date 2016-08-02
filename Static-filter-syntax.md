uBlock Origin ("uBO") supports Adblock Plus ("ABP") filter syntax, so you can refer to [existing filter syntax documentation from Adblock Plus web site](https://adblockplus.org/en/filter-cheatsheet).

However uBO does not support some very specific cases, and also adds its own extensions to ABP filter syntax (which at time of writing are not recognized by ABP).

## Not supported		

`document` for _exception_ filters (those prefixed with `@@`):

Not supported. The purpose of the `document` option when used with an exception filter is to disable uBO completely. The purpose of the `document` option in static exception filters is mostly for the sake of "acceptable ads" support, which uBO does not support.

The reason it is not supported is to be sure that users explicitly disable uBO themselves if they wish (through [whitelisting](https://github.com/gorhill/uBlock/wiki/How-to-whitelist-a-web-site)), not having some external filter list decide for them.

## Extended syntax

uBO extends Adblock Plus filter syntax.

### Network filters

#### HOSTS files

uBO can also parse HOSTS file-like resources. However, this creates an ambiguity with ABP filter syntax, which is pattern-based. For exemple, consider the following filter entry:

    example.com

ABP filter syntax dictates that this is interpreted as "block network requests which URL contains `example.com` at any position". However if the entry comes from a HOSTS file, the interpretation must be "block network requests to the site `example.com`".

So in uBO, any entry which can be read as a valid hostname, will be assumed to be a HOSTS file entry. If ever you want such filter to be parsed as an ABP filter, just add a wildcard at the end:

    example.com/*

#### "All URLs"

The wildcard character `*` can be used to apply a filter to **all** URLs. This is not recommended though, unless you further narrow the filter using filter options. Examples:

- `*$third-party`: block all 3rd-party network requests.
- `*$script,domain=example.com`: block all network requests to fetch script resources from `example.com`.

Usually, it is far more convenient to use [dynamic filtering rules](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering) in lieu of such generic static filters.

#### `document`

For _block_ filters only. This will cause web pages which match the filter to be subjected to [strict blocking](https://github.com/gorhill/uBlock/wiki/Strict-blocking).

#### `first-party`

This is equivalent to `~third-party`. Provided strictly for convenience (0.9.9.0).

#### `important`

The filter option `important` means to ignore all _exception_ filters (those prefixed with `@@`).

It applies only to network _block_ filters. The `important` option will allow you to block with 100% certainty specific network requests.

Example: `||google-analytics.com^$important,third-party` will block all network requests to `google-analytics.com`, disregarding any existing network _exception_ filters. Another example: `||twitter.com^$important,third-party`. Etc.

#### `inline-script`

To specifically disable inline script tags in a main page: `||example.com^$inline-script`.

#### `popunder`

To block "popunders" windows/tabs. To be used in the same manner as the `popup` filter option, except that it will block popunders.

#### `redirect`

To cause a blocked network request to be redirected to a local "neutered" version of the resource. (more documentation will eventually be made.)

### Cosmetic filters

#### Entity-based cosmetic filters

Filters which are to be applied to a specific _entity_. For example:

    google.*###tads.c

An _entity_ is defined as follow: a formal domain name with the Public Suffix part replaced by a wildcard.

Examples: `google.*`  will apply to all similar Google domain names: `google.com`, `google.com.br`, `google.ca`, `google.co.uk`, etc. Another example: `facebook.*` will apply to all similar Facebook domain names: `facebook.com`, `facebook.net`.

Since the base domain name is used to derive the name of the "entity", `google.evil.biz` would **not** match `google.*`.

#### `script:contains(...)`

uBO supports a special cosmetic filter which purpose is to prevent the execution of specific inline script tags in a main HTML document. See [_"Inline script tag filtering"_](https://github.com/gorhill/uBlock/wiki/Inline-script-tag-filtering) for further documentation.

#### `script:inject(...)`

This allows the injection of specific javascript code into pages. The `...` part is a token identifying a javascript resource from the [resource library](https://github.com/gorhill/uBlock/blob/master/assets/ublock/resources.txt). Keep in mind the resource library is completely under control of the uBO project, hence only javascript code vouched by uBO can be inserted into web pages, through the use of a valid resource token.

Generic `script:inject` filters are ignored: those filters **must** be specific, i.e. they must apply to specific hostnames, e.g. `example.com##script:inject(yavli-defuser.js)`.

#### `:has()`

This is a planned CSS4 operator, but no browser supports it yet. I decided to go ahead and implement it so that it can already be used. See [The Relational Pseudo-class: `:has()`](https://drafts.csswg.org/selectors/#relational) in the Selector Level 4/Editor's Draft.

uBO's implementation is simplified so as to ensure performance. The `:has` operator **must** be used with at least one hostname (it must be _specific_), and must be of the form (example):

    yandex.ru##.serp-item:has(.label_color_yellow)

In this example, `yandex.ru` is the hostname. The part preceding `:has(...)` -- `.serp-item` above -- is the DOM node which will be targeted (i.e. hidden by uBO), and must be a valid CSS expression. The part inside the `:has` parentheses -- `.label_color_yellow` above -- must be a valid CSS expression, and is the condition that must be fulfilled -- i.e. in the above example, nodes which have a class `serp-item` will be hidden if and only if they have a descendant with class `label_color_yellow`.

#### `:xpath()`

This new cosmetic filter operator is to support and leverage the power of [XPaths](https://en.wikipedia.org/wiki/XPath). The `:xpath()` operator must always be used in a _specific_ cosmetic filter, i.e. they must apply to at least one hostname or entity. An example of its use (to solve a real reported case) for [this web page](http://forum.pcastuces.com/envahi_par_des_popup-f25s77301.htm):

    forum.pcastuces.com##:xpath(/html/body/table//tr[@class="formsubtitle2"][.//text()="Publicité"])
    forum.pcastuces.com##:xpath(/html/body/table//tr[@class="formsubtitle2"][.//text()="Publicité"]/following-sibling::tr[1])

Notice how these xpath-based cosmetic filters allows to uniquely solve the issue here, by filtering based on the _text content_ of the child nodes in the DOM. This is not possible with standard ABP-compatible filtering syntax. (Use the per-site switch to toggle cosmetic filtering on/off to more easily see the effect of these filters on the page).

#### `:style()`

Related issue: [Support cosmetic filters with explicit style properties](https://github.com/gorhill/uBlock/issues/781).

By default, the implicit purpose of cosmetic filters is to hide unwanted DOM elements. However sometimes it may be useful to re-style a specific DOM element on a page rather than hide it. Here is an [recent example](https://github.com/uBlockOrigin/uAssets/issues/71#issuecomment-229503444) of such cases. This is the purpose of the new `:style`-based selector. The syntax is as follow:

    example.com##h1:style(background-color: blue !important)

So mainly it's exactly the same syntax of plain cosmetic filters, except that the `:style(...)` suffix is appended at the end. The content in the parentheses must be one or more [CSS property declarations](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax) (separated by the standard `;`).

As with the other new cosmetic filtering selectors, the `:style` can be used only for _specific_ cosmetic filters, i.e. there must be a hostname of entity specified for the filter.

Adguard [already support such feature](https://adguard.com/en/filterrules.html#cssInjection), although using a different syntax. However uBO is able to transparently convert and make use of the Adguard's "CSS injection rules" if ever you use an Adguard filter list in uBO (well, this essentially means you can use Adguard's syntax in uBO if you prefer).

For example, [Adguard English filter](https://adguard.com/en/filters.html#english) contains ~50 styling filters, [Adguard Russian filter list](https://adguard.com/en/filters.html#russian) contains ~250 styling filters, etc. Note that often styling filters are used to foil anti-blocker mechanism on web pages. Given this, you may want to benefit from [Adguard's filter lists](https://adguard.com/en/filters.html):

![a](https://cloud.githubusercontent.com/assets/585534/16540886/2905a580-4042-11e6-9c68-7e18a645dea1.png)
