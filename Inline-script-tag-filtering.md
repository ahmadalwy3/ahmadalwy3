Back to [Static filter syntax](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax).

***

- [Caveats](#caveats)
- [Overview](#overview)
- [Compatibility with Adblock Plus](#compatibility-with-adblock-plus)
- [Concrete examples of usefulness](#concrete-examples-of-usefulness)
- [Why is the new inline script tag filter a cosmetic one?](#why-is-the-new-inline-script-tag-filter-a-cosmetic-one)
- [Does Adblock Plus support this filter syntax?](#does-adblock-plus-support-this-filter-syntax)

***

#### Caveats

Script tag filters do not work in all browsers, due to browser API limitations:

- Not supported in Chromium-based browser.
    - Starring the [related Chromium issue](https://code.google.com/p/chromium/issues/detail?id=168175) may help motivate Chromium devs to implement support.
    - Falling back on wholesale blocking of all inline script tags may work.<sup>[1]</sup>
- Not supported in Firefox's WebExtensions version of uBO.

<sub>[1] Through the use of the `inline-script` static filter option (`||example.com^$inline-script`), or through the use of a dynamic filtering block rule for _inline scripts_.</sub>

***

#### Overview

There are many ways to block script tags from executing in uBlock Origin:

- Block external script resources: these are taken care by network filtering.
- Block all inline script tags embedded in a page at once.<sup>[1]</sup>

Inline script tags are those blocks of javascript code which are embedded in the main page: they can not be blocked from downloading unless the whole page itself is blocked, which is not very useful. Here is a example of a web page's HTML code with two inline script tags:

```html
<html>
<head>
<meta name="referrer" content="origin">
<link rel="stylesheet" href="main.css" />
<script type="text/javascript">
    function usefulCode() {
        ...
    }
    ...
</script>
<title>lorem ipsum</title>
</head>
<body>
<h1>lorem ipsum</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
<script type="text/javascript">
    function nuisanceCode() {
        ...
    }
    ...
</script>
</body>
```

In this example, blocking inline script tags wholesale would not be a good solution because both script tags would be blocked and we would lose the `usefulCode` function as well.

uBlock Origin 1.2.0 introduces a new way to block **specific** inline script tag in a web page through the script tag cosmetic filter:

    example.com##script:contains(...)

Where the value inside the parenthesis in `contains(...)` can be a plain string or a literal javascript regular expression (`/.../`). A script tag cosmetic filter will prevent the execution of whatever javascript inside a **specific** script tag when there is a match, i.e. when the plain text or the regular expression is found inside the script tag.

So we can use script tag filtering for our above example to specifically disable one of the script tag (assuming the page's URL is `https://foo.example/bar.html`):

    foo.example##script:contains(nuisanceCode)

This filter means: for any web pages from the `foo.example` web site, disable all inline script tags which contains the string `nuisanceCode`.

In the cat and mouse game between web sites and blockers, the new script tag filter is a welcomed new tool on the user side, to foil attempt by site to work around blockers.

The big advantage of this new filter is that it can fix _at the source_ many of the anti-blocker workarounds used by some web sites.

For example, the web site at `http://focus.de/` will resort to deface itself with ridiculous ads when the site detects that the user is using a blocker, and using _EasyList_ + _EasyList Germany_ does not work, as the images pulled by the page are randomly named, defeating pattern-based network filters and cosmetic filters as well.

Wholesale blocking of inline script tags does prevent the self-defacing, but possibly at the cost of disabling other possible useful functionalities on the page. However, a script tag filter to block the specific inline script tag which contains the self-defacement javascript code allows a more targeted approach: prevent the undesirable inline javascript code from executing while keeping the desirable inline javascript code intact. At time of writing, this script tag filter worked for the site:

    www.focus.de##script:contains(uabInject)

***

#### Compatibility with Adblock Plus

It appears inline script tag cosmetic filters can be used in filter lists which are also meant to be used for Adblock Plus ("ABP") -- ABP will ignore the `[...]##script:contains([...])` filters. This makes it possible for maintainers of filter lists to make use of this new filter syntax for the benefit of uBlock Origin users while not causing problem for users of ABP.

The compatibility was verified for the Firefox version of ABP however, I did not check for the Chromium version of ABP. This will need confirmation for whether using the new filter on a Chromium version of ABP has no negative consequences.

**Update:** Compatibility was verified with the Chromium version of ABP, and unfortunately this new filter syntax breaks ABP, as it fails to discard invalid CSS selectors.

***

#### Concrete examples of usefulness

A concrete example of a site which resorts to self-defacement when it detects that a blocker is in use -- the front page of [rp-online.de](http://www.rp-online.de/):

Without inline script tag filtering:<br>
![without inline script tag filtering](https://cloud.githubusercontent.com/assets/585534/10417577/ec9bbe80-700e-11e5-8fc1-3f21358b45ee.png)

With an appropriate inline script tag filter:<br>
![with inline script tag filtering](https://cloud.githubusercontent.com/assets/585534/10417578/eeb27aba-700e-11e5-9c2e-0845cd27b404.png)

The _uBlock filters_ list, which is selected by default, already contains a couple of inline script tag filters to take care of some of these annoyances.

***

#### Why is the new inline script tag filter a cosmetic one?

Because blocking inline script tags are conceptually closer to cosmetic filtering than network filtering: inline script tags are embedded in a web page, so if the web page is downloaded, the inline script tags are downloaded -- there is no way around this.

Whatever can't be blocked using a network request filter can be taken care by a cosmetic filter, which is the hiding of DOM elements in a web page. Hence inline script tag filtering is implemented using the cosmetic filter syntax -- the only difference is that when blocked, inline script tags are not removed from view (they are already invisible) but instead the execution of the javascript code inside the script tag is blocked.

***

#### Does Adblock Plus support this filter syntax?

No. And apparently, they won't -- [Wladimir Palant ("trev") on Adblock Plus issue tracker](https://issues.adblockplus.org/ticket/748#comment:9):

> Not quite the same thing - he is "blocking" individual scripts (something that inevitably causes a massive performance overhead). Not that it is significantly more useful as a result, anti-adblock messages can easily be combined with required website functionality in the same `<script>` tag. They won't do that for a small extension like uBlock but they will definitely do it if we implement something like that.

My comment about this post:

> inevitably causes a massive performance overhead

Notice the lack any data/figures for such an authoritative statement. Also by all appearances, he did not look at the code: the event listener which enforces inline script tag filtering is installed **if and only if** there are actual inline script tag filters to enforce on any given page.

Also, when script tag filters are present, it's entirely reasonable to imagine that whatever extra overhead inline script tag filtering _may_ cause, such overhead might likely be offset completely or more by the entire cascade of events **not** happening in the browser as a result of the blocking.

Inline script tag filters are something to use as last resort when all else fail. Without inline script tag filters, when all else fail, the remedy is to disable the blocker -- which is the absolute worst option, which has a much worst effect on performance than the code used to enforce inline script tag filters. Currently this is what users of Adblock Plus have to do: disable the extension on _Bild_.

> ***
> Keep in mind that currently a common way for Adblock Plus to deal with anti-blockers is to create exception filters, i.e. to no longer block specific 3rd-party network requests which would have otherwise been blocked ([example](https://adblockplus.org/forum/viewtopic.php?p=140159#p140159), [example](https://forums.lanik.us/viewtopic.php?f=91&t=26996#p81898) => [opening the door to `pagead2.googlesyndication.com`!](https://hg.adblockplus.org/listefr/rev/413aa948bd6d)), so essentially to allow more unwanted 3rd parties into your browser. This can often be avoided with inline script tag filters (respectively, [example](https://github.com/gorhill/uBlock/commit/52b1b2c2947698eaa86284bcf28d8848adb1d2d3), [example](https://github.com/gorhill/uBlock/commit/19576b37e9c41604bac043e8b834be81497786d5)).
> ***

Quote:

> They won't do that for a small extension like uBlock but they will definitely do it if we implement something like that.

The cat and mouse game between blockers and sites will never stop -- and inline script tag filtering does not pretend to put an end to this: it's one more tool on the end user side. It makes no sense to claim that such filtering ability is pointless because it will be worked around, when sites such as _Bild Online_ are _already_ successfully working around Adblock Plus.

In short, this comment from Wladimir Palant shows more of the same mindset as [happened in the past](https://bugzilla.mozilla.org/show_bug.cgi?id=988266#c39).

In [another issue](https://issues.adblockplus.org/ticket/3207), another developer comments:

> As outlined on the linked uBlock wiki page, such a filter can only be supported on Firefox for the time being. However, with Gecko-based extensions being phased out I doubt that it's worth adding this functionality at the moment.

The `beforescriptexecute` event is not specific to "Gecko-based extensions", it is part of the latest [W3C Recommendation](http://www.w3.org/TR/html5/scripting-1.html#scripting-1).