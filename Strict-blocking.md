[Back to Wiki home](./)

***
In uBlock Origin ("uBO"), _strict blocking_ is the blocking of a whole page, i.e. the _root_ document is blocked, so that not a single connection is made to the remote server hosting the web page.

By default, strict blocking is enabled in uBO for domain-only filters (this reduces false-positive matches). To force it on any other pattern matching filter, use [`document`](./Static-filter-syntax#document) or [`all`](./Static-filter-syntax#all) static filter option.

This feature is not supported by other blockers, like Adblock Plus, which only blocks secondary resources (see [web pages _themselves_ are **never** filtered](https://adblockplus.org/forum/viewtopic.php?t=18774#p85439)).

So if you were to create a filter such as `||example.com^`, and then navigate to <https://example.com>, Adblock Plus would not prevent you from connecting and loading the web page itself served at `https://example.com`, though all secondary resources pulled by that web page would be subject to filtering.

uBO respected that semantic until version 0.9.3.0. With version 0.9.3.0, uBO will subject web pages themselves to filtering.

This means that using the same test case above, **uBO will block the web page** served by a server found in one of the malware list (unlike Adblock Plus):

![Page was fully blocked](https://cloud.githubusercontent.com/assets/585534/8160013/14466ca0-133a-11e5-8d3c-28169288f35a.png)

Why the change? Because [issue #1013](https://github.com/chrisaljoudi/uBlock/issues/1013) brought forth why it is desirable sometimes to completely block a web site, as opposed to what the ABP-filtering semantic dictates.

In the end, the chosen solution is to now have web page themselves subject to filtering, just like all secondary resources.

In the figure above, the user will be given the choice to go back by closing the window or proceed to the web page by disabling strict blocking by selecting either:

- Temporarily - The site will be temporarily allowed for a limited time (60 seconds, after [1.17.4](https://github.com/gorhill/uBlock/releases/tag/1.17.4) 120 seconds - [configurable](./Advanced-settings#strictblockingbypassduration)).
- Permanently - The site will be permanently allowed.

This will prevent the web page _proper_ for the site from being blocked by uBO in the future: the filtering of the site will be done exactly as per ABP-filtering semantic, and just like with uBO pre-0.9.3.0.

There are many benefits to strict blocking. For example, there is no good reason one should want to connect _at all_ to any of the sites present in any one of the malware domain lists. Strict blocking will prevent this from happening.

**Important note:** Keep in mind that when the above warning occurs, it doesn't necessarily mean the site is harmful, it just means that there is a matching filter in the selected filter lists. You decide whether the site is safe, and whether disabling strict blocking permanently for the site is appropriate.

**Tip:** If you wish, you may entirely disable strict blocking everywhere by adding the rule `no-strict-blocking: * true` to the _My rules_ pane in the dashboard (don't forget to click _Commit_ to make the rule stick).

### Ability to parse the strict-blocked URL

Sometimes, the strict-blocked URL contains a [query string component](https://en.wikipedia.org/wiki/Query_string) which uBO can parse and decompose into detailed query parameters. Oftentimes, once decomposed, the query parameters will show you information which can be useful.

A top example of this is when a redirection URL is strict blocked, you will often find in the query parameters the destination URL which you intended to visit when you clicked a link, which makes it possible to bypass the redirection URL -- typically used for tracking purpose -- and navigate directly to the intended destination URL by just licking on it.

Example:

![a](https://user-images.githubusercontent.com/585534/81292329-6594af00-9039-11ea-99e5-271ae753fe0b.png)

In the example above, a link to _Green Man Gaming_ site was clicked (from [here](https://www.pcgamingwiki.com/wiki/Dead_Rising_2)), but doing so caused the browser to navigate to a strict-blocked redirection link instead of navigating directly to the _Green Man Gaming_ site. By expanding the query strings into components, we can see our actual destination URL -- just click on it and you will finally reach your intended destination whithout having to go through the `dpbolvw.net` server which was strict-blocked by an entry in Peter Lowe's list.