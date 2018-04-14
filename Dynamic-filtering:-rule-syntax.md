[Back to "Dynamic-filtering"](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering)

***

### Rule syntax

A dynamic filtering rule is made of four components: a source, a destination, a request type, and then a keyword which tells what to do with a request which happens to match the three former components:

    source destination type action

Valid rules:

| rule type | source | destination | request type | action |
|---|---|---|---|---|
| **Type-based** | `*`<br>_hostname_ | `*`<br>&nbsp; | `*`<br>`image`<br>`inline-script`<br>`1p-script`<br>`3p`<br>`3p-script`<br>`3p-frame` | `block`<br>`noop`<br>`allow` |
| **Hostname-based** | `*`<br>_hostname_ | <br>_hostname_ | <br>`*` | `block`<br>`noop`<br>`allow` |

Source hostname always corresponds to the hostname extracted from the URL of the web page in the browser.

The destination hostname corresponds to the hostname extracted from the URL of a remote resource which the web page is fetching (or trying to).

A rule always automatically propagates to all subdomains of the source hostname and all subdomains of the destination hostname -- unless the rule is overridden by a narrower rule in one of the subodmains.

Given that rules always propagate to subdomains, there is no need to prefix the hostname part with a wildcard `*.`, doing so is invalid and will cause the the rule to be discarded.

The type is the type of the fetched resource.

A request can be blocked (`block`), allowed (`allow`), or ignored (`noop`). A `noop` rule will cause matching network requests to be ignored by the dynamic filtering engine, but those ignored network requests will still be subjected to static filtering (filter lists).

***

### Type-based rules

Type-based rules are used to filter specific types of request on a web page. There currently exists seven types of request which can be dynamically filtered:

- `*`: any type of request
- `image`: images
- `3p`: any request which 3rd-party to the web page
- `inline-script`: inline script tags, i.e. scripts embedded in the main document
- `1p-script`: 1st-party scripts, i.e. scripts which are pulled from the same domain name of the current web page
- `3p-script`: 3rd-party scripts, i.e. scripts which are pulled from a different domain name than that of the current web page
- `3p-frame`: 3rd-party frames, i.e. frames elements which are pulled from a different domain name than that of current web page

These rules can apply everywhere, or be specific to a web site. For instance blocking 3rd-party frames is a very good habit security-wise: `* * 3p-frame block`. This rule translates into "globally block 3rd-party frames".

Another example: `wired.com * image block`, which means "block images from all origins when visiting a web page on wired.com".

Note that with type-based rules, the destination hostname is **always** `*`, meaning "from anywhere".

***

### Hostname-based rules

Hostname-based rules are used to filter network resources according to their origin, i.e. according to which remote server a resource is pulled. Hostname-based rules have a higher specificity than type-based rules, and thus hostname-based rules always override type-based rules whenever a network request end up matching both a type- and a hostname-based rule.

With hostname-based rule, the request type is always `*`, meaning the rule will apply to any type of request.

For example, `* disqus.com * block` means "globally block all net requests to `disqus.com`".

Just like type-based rules, a hostname-based rule can apply only when visiting a specific web site, for example: `wired.com disqus.com * noop`, which means "do not apply dynamic filtering to network requests to `disqus.com` when visiting a web page on `wired.com`. Since this last rule is more specific than the previous one, it will override the global blocking of `disqus.com` everywhere.

***

### Actions

A matching rule can do one of three things:

- `block`: matching network request will be blocked.
    - `block` dynamic filter rules override any existing [static exception filters](https://adblockplus.org/en/filters#whitelist).
    - Thus you can use them to block with 100% certainty (unless you set another overriding dynamic filter rule).
- `allow`: matching network request will be allowed.
    - `allow` dynamic filters rules override any existing static and dynamic block filters.
    - Thus they are most useful to create finer-grained exceptions, and to un-break web sites broken by some static filters somewhere.
- `noop`: exclude network requests from being subjected to dynamic filtering.
    - It cancels dynamic filtering, but it does not cancel static filtering.