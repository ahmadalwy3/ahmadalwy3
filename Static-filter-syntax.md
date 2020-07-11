uBlock Origin ("uBO") supports Adblock Plus ("ABP") filter syntax, so you can refer to [existing filter syntax documentation from Adblock Plus web site](https://adblockplus.org/en/filters) and ABP's filter [cheatsheet](https://adblockplus.org/filter-cheatsheet). For quick overview you can also check [Introduction to basic filtering syntax](./Introduction-to-basic-filtering-syntax) in this wiki.

However uBO does not support some very specific cases, and also adds its own extensions to ABP filter syntax (which at time of writing are not recognized by ABP). Few most surprising cases are documented [here](./Syntax-quirks).

Starting with 1.26.0 (commit [one](https://github.com/gorhill/uBlock/commit/703c525b01aa3fb9dab94d6a9918a0a69c6d18da), [two](https://github.com/gorhill/uBlock/commit/ca80d2826bfd92a3081f20da8ba60138509a183b)), very long filters can be split into multiple lines: append space and backslash character to first line and indent continuation line by four spaces.

- [Not supported](#not-supported)
- [Pre-parsing directives](#pre-parsing-directives)
- [Extended syntax](#extended-syntax)
    - [Static network filtering](#static-network-filtering)
    - [Static extended filtering](#static-extended-filtering)
        - [Entity](#entity)
        - [Cosmetic filters](#cosmetic-filters)
            - [Procedural cosmetic filters ↪](./Procedural-cosmetic-filters)
            - [Action operators](#action-operators)
        - [HTML filters](#html-filters)
        - [Scriptlet injection](#scriptlet-injection)
			- [Resources library ↪](./Resources-Library)

***

## Not supported

#### `document` for [_entire page exception_](https://adblockplus.org/filters#whitelist)

Not supported. The purpose of the `document` option when used with an exception filter is to disable uBO completely. The purpose of the `document` option in static exception filters is mostly for the sake of "acceptable ads" support, which uBO does not support.

The reason it is not supported is to be sure that users explicitly disable uBO themselves if they wish (through [whitelisting](./How-to-whitelist-a-web-site)), not having some external filter list decide for them.

Note: it [still works](https://github.com/gorhill/uBlock/issues/1754) to negate [strict blocking](./Strict-blocking) when explicitly enabled by blocking filter `document` option.

***

#### `genericblock`

Not supported.

This option is meant to be used with an exception filter to disable _generic_ network filters on target pages. _Generic_ in this case means network filters without a `domain=` filter option. Filters such as `||example.com^` are still considered generic.

This option is not supported because using such filter option would cause large amount of filters to be silently disabled for a site where it's used.

For instance, when used for a specific site, the `genericblock` option would cause all the filters in hosts files to be disabled, including those from the malware lists. EasyPrivacy and other anti-tracking lists also contain countless so-called "generic" filters, and as a consequence these would also end up being disabled.

***

#### ~`elemhide`~

**Supported** starting with uBO [1.23.0](https://github.com/gorhill/uBlock/commit/23c4c80136ba4974a6444488ef8162ba75b0cb84), also aliased as `ehide`.

Before 1.23.0 it was translated internally to `generichide`. `elemhide` was only available as ["No cosmetic filtering"](./Per-site-switches#no-cosmetic-filtering) switch.

Keep in mind `generichide` is a cosmetic filtering-related option, and as such using it has no negative consequence with regard to privacy since cosmetic filtering has no privacy value.

***

## Pre-parsing directives

uBO 1.16.0 and above supports pre-parsing directives. Pre-parsing directives are prefixed with `!#`, so this means older versions of uBO or other blockers will see the pre-parsing directives as comment and discard them.

The pre-parsing directives are executed before a list content is parsed, and influence the final content of a filter list.

***

#### `!#include [file name]`

The `!#include` directive allows to import another filter list in place where the directive appears. The purpose is to allow filter list maintainers to create filters which are specific to uBO, while keeping their list compatible with other blockers. Other blockers will ignore the `!#include` directive, because it will be seen as a comment and thus discarded. uBO will attempt to load the resource found at `[file name]` (the sub-list) and load its content into the current list.

The sub-list **must** be in the same directory as the main one, i.e. it is not allowed to load a sub-list which is located outside where the current one resides.

Correct usage:
- `!#include ublock-filters.txt`
- `!#include ublock/filters.txt`

Incorrect usage:
- `!#include https://github.com/uBlockOrigin/uAssets/blob/master/filters/filters.txt`
- `!#include ../filters.txt`

***

#### `!#if [condition]`

The `!#if` directive allows filter list maintainers to create areas in a filter list which will be parsed **only** if certain conditions are met (or not met). For example this can be used to create filters which are specific to a particular browser.

Example, to compile a block of filters only if uBO is being run as a Firefox extension:

    !#if env_firefox
    ...
    !#endif

Another example, compile a block of filters only if uBO is _not_ being run as a Firefox extension:

    !#if !env_firefox
    ...
    !#endif

Support for pre-processor directives are the result of discussion with AdGuard developers, see <https://github.com/AdguardTeam/AdguardBrowserExtension/issues/917>.

For the time being, only a single token is supported in a `!#if` directive (can be negated using `!`), and uBO supports only the following tokens, anything else will be ignored:

    ext_ublock
    env_chromium
    env_edge
    env_firefox
    env_mobile
    env_safari
    false (1.21.9b7)
    cap_html_filtering
    cap_user_stylesheet

Starting from [1.22.0](https://github.com/gorhill/uBlock/commit/1d805fb9da1aad918d02cc74796d5aa5e974b184) you can use `!#if false` directive to disable a large block of your filters without having to remove them. 

    !#if false
    ...
    !#endif

Before this version, you could use negated `ext_ublock`, since this token is always true in uBO.

***

## Extended syntax

uBO extends Adblock Plus filter syntax.

## Static network filtering

#### HOSTS files

uBO can also parse HOSTS file-like resources. All hostname entries from a HOSTS file resource from uBO's point of view will be syntactically equivalent to a filter of the form `||hostname^`.

However, this creates an ambiguity with ABP filter syntax, which is pattern-based. For example, consider the following filter entry:

    example.com

ABP filter syntax dictates that this is interpreted as "block network requests which URL contains `example.com` at any position".

However in uBO the interpretation will be "block network requests to the site `example.com` and all of its subdomains" -- i.e. equivalent to `||example.com^`. Note that this includes blocking main document itself, see ["Strict blocking"](./Strict-blocking) and [`document` option](#document).

So in uBO, any pattern which can be wholly read as a valid hostname, will be assumed to be equivalent to a filter of the form `||example.com^`. If ever you want such filter to be syntactically parsed according to ABP's interpretation, just add a wildcard at the end:

    example.com/*

***

#### `*` aka "all URLs"

The wildcard character `*` can be used to apply a filter to **all** URLs. This is not recommended though, unless you further narrow the filter using filter options. Examples:

- `*$third-party`: block all 3rd-party network requests.
- `*$script,domain=example.com`: block all network requests to fetch script resources at `example.com`.

Usually, it is far more convenient to use [dynamic filtering rules](./Dynamic-filtering) in lieu of such generic static filters.

***

#### `1p`

Equivalent to [`first-party`](#first-party) uBO option, which in turn is negated `third-party` [option](https://adblockplus.org/filters#options) (`~third-party`). For convenience.

***

#### `3p`

Equivalent to `third-party` [option](https://adblockplus.org/filters#options). For convenience.

***

#### `all`

New in [1.20.0](https://github.com/gorhill/uBlock/commit/1888033070003cd5e6a3687a4029448bf41fccea).

The `all` option is equivalent to specifying all
network-based types + `popup`, `document`,
`inline-font`, `inline-script`.

Example:

    ||bet365.com^$all

Above will block all network requests, block all popups,
prevent inline fonts/scripts from `bet365.com`. EasyList-
compatible syntax does not allow to accomplish that
semantic when using only `||bet365.com^`.

See also [#2385](https://github.com/gorhill/uBlock/issues/2385)

***

#### `badfilter`

To disable an existing filter. Sometimes, disabling an existing blocking filter is better than creating an exception filter. Just for example sake, let's say that a mind-absent filter list maintainer added the following filter in his list:

    *$image

Now all images from everywhere are blocked on your side. An exception filter (`@@*$image`) is not a good solution because it would also cause images which should be legitimately blocked from no longer being blocked. In such case, the `badfilter` option is best:

    *$image,badfilter

This will cause the `*$image` filter to be discarded. Just appending `badfilter` option to any instance of static network filter will prevent the loading of that filter.

After [1.19.0](https://github.com/gorhill/uBlock/commit/3f3a1543ea7fa51d700157a7f6bf0da08dd7a32b) any filter which fulfill ALL the following conditions:

- Is of the form `|https://` or `|http://` or `*`; and
- Does have a `domain=` option; and
- Does not have a negated domain in its `domain=` option; and
- Does not have `csp` option; and
- Does not have a `redirect=` option

Will be processed in a special manner:

- The `domain=` option will be decomposed so as to create as many
  distinct filter as there is distinct value in the `domain=` option
- It now become possible to `badfilter` only one of the
  distinct filter without having to `badfilter` all of them.
- The logger will always report these special filters with only a
  single hostname in the `domain=` option.

***

#### `css`

Equivalent to `stylesheet` [option](https://adblockplus.org/filters#options). For convenience.

***

#### `cname`

New in [1.26.0](https://github.com/gorhill/uBlock/commit/c3bc2c741d61db3e99b313835c2ae34a4a008359).

Option for exception filters only.

By default, network requests which are result of resolving a [canonical name](https://en.wikipedia.org/wiki/CNAME_record) are subject to filtering. This filtering can be bypassed by creating exception filters using the `cname` option. 

Example:

    @@*$cname

The filter above tells the network filtering engine to except network requests which fulfill all the following conditions:

- network request is blocked
- network request is that of an unaliased hostname

Filter list authors are discouraged from using exception filters of `cname` type, unless there no other practical solution such that maintenance burden become the greater issue. Of course, such exception filters should be as narrow as possible, i.e. apply to specific domain, etc.

***

#### `csp`

This option will inject [`Content-Security-Policy`](https://developer.mozilla.org/en-US/docs/Glossary/CSP) header to the HTTP network response of the requested web page. It can be applied to main document and documents in frames.

This is special filter - it will not block matching resource, but only apply HTTP header to pages matching it. Because of this it cannot be mixed with other options speciyfing resource type, like for example `image`, `script` or [`frame`](#frame) (`subdocument`). It can still be used with [`1p`](#1p) (`first-party`), [`3p`](#3p) (`third-party`) or [`domain`](#domain) options.

Because of how `csp` filters are implemented, they allow for some interesting applications. For example you can block scripts only in some specific path in page:

    ||example.com/subpage/*$csp=script-src 'none'

And even block them everywhere except main page (note end anchor):

    ||example.com/*$csp=script-src 'none'
    @@||example.com^|$csp=script-src 'none'

Exception filter for specific `csp` blocking filter must have exactly the same content of `csp` option as blocking filter. However, exception filter with empty `csp` option will disable all `csp` injections for matching page:

    @@||example.com^$csp

CSP option syntax may look unusual compared to other filters. It works mostly in "whitelist" mode - data can be downloaded only from addresses explicitly specified in this option. Refer to ["Content Security Policy (CSP)
Quick Reference Guide"](https://content-security-policy.com/) or [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) for further syntax help.

See also [`denyallow`](#denyallow).

***

#### `denyallow`

New in [1.26.0](https://github.com/gorhill/uBlock/commit/c3bc2c741d61db3e99b313835c2ae34a4a008359).

The purpose of `denyallow` is bring default-deny/allow-exceptionally ability into static network filtering arsenal. 

Example:

    *$3p,script,denyallow=x.com|y.com,domain=a.com|b.com

The above filter tells the network filtering engine that when the context is `a.com` or `b.com`, block all
3rd-party scripts except those from `x.com` and `y.com`.

Essentially, the new `denyallow` option makes it easier to implement default-deny/allow-exceptionally in static filter lists, whereas before this had to be done with unwieldy regular expressions[1], or through the mix of broadly blocking filters along with exception filters[2].

[_"Entity"_](#entity) wildcard matching is not supported.

[1] hg.adblockplus.org/ruadlist/rev/f362910bc9a0

[2] Typically filters which pattern are of the form `|http*://`

***

#### `document`

This is a _type_ option (like `image` or `script`) which specifies _main frame_ (a.k.a. the root document) of a web page. This option is automatically enabled in filters specifying only host part of the URL, see ["HOSTS files" section](#hosts-files). This will cause web pages which match the filter to be subjected to ["Strict blocking"](./Strict-blocking).

See also: [`all`](#all)

***

#### `domain`

Restrict the filter to be applied only on specified domain(s).

Multiple domains can be specified by joining them using `|` symbol.

Preceding domain name by `~` will prevent filter to be applied on this domain.

Starting with [1.28.0](https://github.com/gorhill/uBlock/commit/3c67d2b89f8ac6d680e74af3e11b916889f7feed) support for [_"entity"_](#entity) matching has been added. You can now use `filter$domain=google.*` to apply filter to pages on all top level domains of specified domain.

Example:

    ||doubleclick.net^$script,domain=auto-motor-und-sport.de
    ||adnxs.com^$domain=bz-berlin.de|metal-hammer.de|musikexpress.de|rollingstone.de|stylebook.de
    /adsign.$domain=~adsign.no

***

#### `elemhide`

Alias: `ehide`.

Before uBO [1.23.0](https://github.com/gorhill/uBlock/commit/23c4c80136ba4974a6444488ef8162ba75b0cb84) option was translated internally to `generichide`.

Option for exception filters only. Turns off all cosmetic filtering on matching pages.

***

#### `empty`

New in [1.22.0](https://github.com/gorhill/uBlock/commit/3e5c9e00ab3603ae0c02e08b007b084404bbb71d).

The filter option `empty` is converted to `redirect=empty` by uBO internally; however unlike when the [`redirect`](#redirect) option is used expressly, the `empty` option does not require a resource type.

When `empty` is used, only network requests which are meant to return a text response will be redirected to an empty response body by uBO - so `empty` will not work for resources such as images, media, or other binary resources.

See also: [`mp4`](#mp4), [`redirect`](#redirect)

***

#### `first-party`

Equivalent to `~third-party` [option](https://adblockplus.org/filters#options). Provided strictly for convenience (0.9.9.0).

***

#### `frame`

Equivalent to `subdocument` [option](https://adblockplus.org/filters#options). For convenience.

***

#### `generichide`

Alias: `ghide`.

Option for exception filters only. Turns off _generic_ cosmetic filtering on matching pages.

Generic cosmetic filters, are hiding filters which apply to all pages - `##.ad-class`.

***

#### `important`

The filter option `important` means to ignore all _exception_ filters (those prefixed with `@@`).

It applies only to network _block_ filters. The `important` option will allow you to block with 100% certainty specific network requests.

Example: `||google-analytics.com^$important,third-party` will block all network requests to `google-analytics.com`, disregarding any existing network _exception_ filters. Another example: `||twitter.com^$important,third-party`. Etc.

***

#### `inline-script`

To specifically disable inline script tags in a main page via CSP: `||example.com^$inline-script`.

***

#### `inline-font`

To specifically disable inline font tags in a main page via CSP: `||example.com^$inline-font`.

***

#### `mp4`

New in [1.22.0](https://github.com/gorhill/uBlock/commit/68ae847ba385c09c5efa511d18a18a4753af47be).

The `mp4` filter option will be converted to `redirect=noopmp4-1s` internally, and `media` type will be assumed.

See also: [`empty`](#empty), [`redirect`](#redirect)

***

#### `popunder`

To block "popunders" windows/tabs, where original page is redirected to advertisement and desired content is loaded in newly created one. To be used in the same manner as the `popup` filter option, except that it will block popunders.

***

#### `redirect`

To cause a blocked network request to be redirected to a local "neutered" version of the resource. The "neutered" resource must be referenced using a resource token. The resources are defined in [Resources Library](./Resources-Library#defuser-scriptlets). Special, reserved token `none` can be used to disable specific redirect filters.

The filter syntax for `redirect=` filter option is a subset of ABP-compatible filtering syntax, and is as follow:

    ||example.com^$script,redirect=noopjs,domain=github.com
    ||example.com/path/to/image$image,redirect=2x2-transparent.png,domain=github.com
    ||example.com/$script,redirect=noopjs,first-party

Specifically, notice that the filter **must** start with `||` or `*`, otherwise no redirection directive will be created, although a blocking filter will be created. Essentially, a redirection filter must always have a destination hostname specified, or `*` if the filter is to apply to all destinations<sup>__*__</sup>.

A source hostname should always be specified, so the `domain=` option is strongly recommended. It is allowed to use `first-party` instead of `domain=[...]`, in which case the source hostname will be that of the destination hostname.

<sub>__*__ redirections applied to all destinations (starting with `*`) cannot be narrowed by `first-party` or `~third-party` option [#3590](https://github.com/gorhill/uBlock/issues/3590)</sub>


***

#### `redirect-rule`

New in [1.22.0](https://github.com/gorhill/uBlock/commit/aa73f292eced0d34a2a2989b1b27ace1214a2809).

Allows to create standalone [`redirect`](#redirect) rule without being forced to create blocking filter.

For example, consider the following filter:

    ||example.com/ads.js$script,redirect=noop.js

The above filter will result in a block filter `||example.com/ads.js$script` **and** a matching redirect directive. Now consider this following filter:

    ||example.com/ads.js$script,redirect-rule=noop.js

The above filter will not cause a block filter to be created, only a redirect directive will be created. Standalone redirect directives are useful when the blocking of a resource is optional but we still want the resource to be redirected should it ever be blocked by whatever mean - whether through a separate block filter, a dynamic filtering rule, etc.

***

#### `specifichide`

Alias: `shide`.

New in uBO [1.23.0](https://github.com/gorhill/uBlock/commit/23c4c80136ba4974a6444488ef8162ba75b0cb84)

Option for exception filters only. Turns off _specific_ cosmetic filtering on matching pages.

Specific cosmetic filters, are filters which apply only to pages in domains specified in filter - `example.com##.ad-class`.

***

#### `xhr`

Equivalent to `xmlhttprequest` [option](https://adblockplus.org/filters#options). For convenience.

***

## Static extended filtering

Static extended filters are all of the form:

    [hostname(s)]##[expression]
    [hostname(s)]#@#[expression]

The most common type of static extended filters are cosmetic filters, also known as "element hiding filters" in Adblock Plus.

***

#### Entity

All static extended filters can be declared to apply to a specific _entity_. For example:

    google.*###tads.c

An _entity_ is defined as follow: a formal domain name with the [Public Suffix](https://publicsuffix.org) part replaced by a wildcard.

Examples: `google.*`  will apply to all similar Google domain names: `google.com`, `google.com.br`, `google.ca`, `google.co.uk`, etc. Another example: `facebook.*` will apply to all similar Facebook domain names: `facebook.com`, `facebook.net`.

Since the base domain name is used to derive the name of the "entity", `google.evil.biz` would **not** match `google.*`.

***

#### Specific-generic

New in [1.25.0](https://github.com/gorhill/uBlock/commit/3fab7bfdb4f892f3d33159fd53ccf1d5342a090a).

A specific cosmetic filter of the following form...

    *##.selector

... will be unconditionally injected into all web pages, whereas a cosmetic filter of the form...

    ##.selector

... would be injected only when uBO's DOM surveyor finds at least one matching element in a web page.

The new specific-generic form will also be disabled when a web page is subject to a `generichide` exception filter, since the filter is essentially a generic one -- the only difference from the usual generic form is that the filter is injected unconditionally instead of through the DOM surveyor.

Specific-generic cosmetic filters will NOT be discarded when checking the "Ignore generic cosmetic filters" option in the "Filter lists" pane -- since the purpose of this option is primarily to disable the DOM surveyor.

Related issue: [#803](https://github.com/uBlockOrigin/uBlock-issues/issues/803).

***

### Cosmetic filters

#### Procedural cosmetic filters

`:has(...)`, `:has-text(...)`, `:if(...)`, `:if-not(...)`, `:matches-css(...)`, `:matches-css-before(...)`, `:matches-css-after(...)`, `:min-text-length(n)`, `:not(...)`, `:nth-ancestor(n)`, `:upward(arg)`, `:watch-attr(...)`, `:xpath(...)`.

See [detailed documentation](./Procedural-cosmetic-filters).

***

#### Action operators

By default, the implicit purpose of cosmetic filters is to hide unwanted DOM elements. However sometimes it may be useful to re-style a specific element or remove it completely from DOM tree.

***

#### `subject:remove()`

- Description: _action operator_, instruct to remove elements from the DOM tree.
- Chainable: No, _action operator_ can only be used at the end of the root chain.
- _subject_: Can be a plain CSS selector, or a procedural cosmetic filter.
- Examples:
    - `gorhill.github.io###pcf #a18 .fail:remove()`

New in uBO [1.26.0](https://github.com/gorhill/uBlock/commit/72bb70056843024b1a31fe1ab9c90bd4e8260ba2). Fixes [#2252](https://github.com/gorhill/uBlock/issues/2252)

Since `:remove()` is an "action" operator, it must only be used as a trailing operator (just like the [`:style()` operator](#subjectstylearg)).

AdGuard's cosmetic filter syntax `{ remove: true; }` will be converted to uBO's `:remove()` operator internally.

***

#### `subject:style(arg)`

- Description: _action operator_, applies specified style to selected elements in DOM tree.
- Chainable: No, _action operator_ can only be used at the end of the root chain.
- _subject_: only native, plain CSS selectors are supported, see [#382](https://github.com/uBlockOrigin/uBlock-issues/issues/382).
- _arg_: one or more [CSS property declarations](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax), separated by the standard `;`. Property values with `url(...)` are forbidden.
- Examples:
    - `example.com##h1:style(background-color: blue !important)`
    - `motobanda.pl###mvideo:style(z-index: 1!important)`

Related issue [Support cosmetic filters with explicit style properties](https://github.com/gorhill/uBlock/issues/781) and [example](https://github.com/uBlockOrigin/uAssets/issues/71#issuecomment-229503444) where it's useful.

It's exactly the same syntax of plain cosmetic filters (i.e. must be a valid CSS selector), except that the `:style(...)` suffix is appended at the end. The content in the parentheses must be one or more [CSS property declarations](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax) (separated by the standard `;`). It is not allowed to use property values with `url(...)`, such `style`-based cosmetic filters will be discarded.

As with the other new cosmetic filtering selectors, the `:style` can be used only for _specific_ cosmetic filters, i.e. there must be a hostname or entity specified for the filter.

uBO is able to transparently convert and make use of the AdGuard [CSS injection rules](https://kb.adguard.com/en/general/how-to-create-your-own-ad-filters#cosmetic-css-rules-syntax). This essentially means you can use AdGuard's syntax in uBO if you prefer.

Note that often styling filters are used to foil anti-blocker mechanism on web pages. Given this, you may want to benefit from [AdGuard's filter lists](https://kb.adguard.com/en/general/adguard-ad-filters), which can be enabled from the [3rd-party filters pane](./Dashboard:-3rd-party-filters).

***

### HTML filters

Supported by [uBO 1.15.0](https://github.com/gorhill/uBlock/releases/tag/1.15.0)+ in Firefox 57+.

**READ VERY CAREFULLY:** HTML filtering acts on the **response data** (before browser parsing). Do not use the browser inspector from developer tools to create HTML filters. You **must** use `view-source:[URL of page]` instead to look at the **response data** and find out relevant information to create relevant HTML filters. Only UTF-8 encoding is supported natively by browsers. For other (most used) encodings, custom encoders are implemented in JavaScript. Because of this, HTML filtering will work only on pages with character encoding compatible with: UTF-8, ISO-8859-1, Windows-1250, Windows-1251 and Windows-1252 ([detailed mapping](https://github.com/gorhill/uBlock/blob/2a91a685ce3d2dae5d3c285cff1bc74a1982be74/src/js/text-encode.js#L32))

The purpose of HTML filters is to remove elements from a document _before_ it is parsed by the browser.

The syntax is similar to that of cosmetic filters, except that you must prefix your selector (CSS or procedural) with the character `^`:

    example.com##^.badstuff
    example.com##^script:has-text(7c9e3a5d51cdacfc)

These HTML filters will cause the elements matching the selectors to be **removed from the streamed response data**, such that the browser will never know of their existence once it parses the modified response data. This makes it a powerful tool in uBO's arsenal.

With the introduction of HTML filtering, the `script:contains(...)` is now deprecated and internally converted into an equivalent `##^script:has-text(...)` HTML filter. The result is essentially the same: to prevent the execution of specific inline script tags in a main HTML document. See [_"Inline script tag filtering"_](./Inline-script-tag-filtering) for further documentation.

Support for chaining procedural operators with native CSS selector syntax (i.e. `a:has(b) + c`) was added in [1.20.1b3](https://github.com/gorhill/uBlock/commit/41685f4cce084f3f89e9cdd8fc1cde5b57862958). Only procedural operators which make sense in the context of HTML filtering are supported.

***

### Scriptlet injection

    +js(...)

<sub>`script:inject(...)` up to [1.15.12](https://github.com/gorhill/uBlock/commit/ec56165d0d36ab91fba7d5cf44a4552d19fefdd5).</sub>

This allows the injection of specific javascript code into pages. The `...` part is a token identifying a javascript resource from the [resource library](./Resources-Library). Keep in mind the resource library is completely under control of the uBO project, hence only javascript code vouched by uBO can be inserted into web pages, through the use of a valid resource token.

Some scriptlets support additional parameters, which can be specified after scriptlet name, separated by comma. Commas in parameters must be escaped. Before [1.22.0](https://github.com/gorhill/uBlock/commit/d67340f14db6ce5b446ef0ff4586b5e4d31f1086#diff-b03ba512faa0934947e57d28dc99b43bL242) this was possible only in regex literals (`/foo\x2Cbar\u002Cbaz/`), now backslash character is sufficient (`foo\,bar`).

Generic `+js` filters are ignored: those filters **must** be specific, i.e. they must apply to specific hostnames, e.g. `example.com##+js(nobab)` will inject [`bab-defuser`](./Resources-Library#bab-defuserjs-) into pages on `example.com` domain.

Starting with [1.22.0](https://github.com/gorhill/uBlock/commit/bf3c92574e5f2386fe2abb4de779e782b0b5a1d2) new exception syntax has been added, allowing to wholly disable scriptlet injection for a given site without having to create exceptions for all matching scriptlet injection filters.

The following exception filter will cause scriptlet injection to be wholly disable for `example.com`:

    example.com#@#+js()

Or to disable scriptlet injection everywhere:

    #@#+js()

The following form is meaningless and will be ignored:

    example.com##+js()
