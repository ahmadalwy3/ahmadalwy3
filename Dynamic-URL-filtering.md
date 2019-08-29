[under construction]

Dynamic URL filtering became available in uBlock Origin version 0.9.8.0.

The primary purpose of dynamic URL filtering ("URL filtering") is as a diagnosis/mitigation tool to fix web page breakage caused by dynamic filtering or static filtering. Secondary purpose of URL filtering is to offer higher granularity than what dynamic filtering can support.

URL filtering has precedence over dynamic filtering and static filtering. See ["Overview of uBlock's network filtering engine"](./Overview-of-uBlock's-network-filtering-engine) to see where URL filtering fits and to better understand its purpose.

URL filtering is accessible from the logger, i.e. you will create and manage dynamic URL rules through the logger UI, by clicking on the 4th cell in the row specific to the resource for which a rule needs to be created:

![a](https://cloud.githubusercontent.com/assets/585534/7814025/5bf1df88-038d-11e5-9956-ecd3f56efeb0.png)

URL filtering uses _rules_, which resemble dynamic filtering rules, except that the destination hostname is replaced by a URL:

    [source hostname] [destination URL] type action

`source hostname` is the _context_ from which a request is fired, and just like with dynamic filtering rules, the hostname of the URL in the address bar is used to determine the context. The global context (`*`) can be used to create a URL filtering rule which applies everywhere.

`destination URL` is URL to match: the URL of a resource must **start exactly** with the `destination URL` of a rule for a match to occur.

`type` is the type of a resource.  The special type `*` can be used to create a URL filtering rule which applies to any type of resource.

`action` tells the URL filtering engine what to do when there is a match. Same as with dynamic filtering rules: `allow`, `noop` or `block`.

It is very important to understand that URL filtering rules override dynamic filtering rules and static filters. So you could create an `allow` URL filtering rule which override a `block` plain dynamic filtering rule.

#### Examples of URL filtering usefulness.

Un-break a web site: a real case was reported in [issue #240](https://github.com/gorhill/uBlock/issues/240). The web site required the resource `http://s7.addthis.com/js/300/addthis_widget.js` for the comment section to render properly. However, `addthis.com` is blocked by uBlock's _Privacy_ filter list with the `important` filter option, meaning the filter cannot be overridden by an exception filter. [URL filtering to the rescue](https://github.com/gorhill/uBlock/issues/240#issuecomment-105019619), since URL filtering overrides both dynamic filtering rules and static filters.

Finer-grained dynamic filtering: [need a better concrete example] block all 3rd resources by default using dynamic filtering rule `* * 3p block`, but allow one very specific 3rd-party resource `example.org https://foo.com/widget.js script allow`, something which would not be possible before URL filtering was available, the only solution was to allow everything from `foo.com`
