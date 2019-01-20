### uBlock's required (Chromium) permissions

uBlock's required permissions are the same as those of [Privacy Badger](https://www.eff.org/privacybadger), except that Privacy Badger requires one extra permission, `cookies`. These are uBlock's required permissions:

    "permissions": [
        "contextMenus",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "http://*/*",
        "https://*/*"
    ],

[`"privacy"`](https://developer.chrome.com/extensions/privacy) is the only permission added in [version 0.9.8.2](https://github.com/gorhill/uBlock/releases/tag/0.9.8.2). All the others were there since when uBlock was first published (except for `"contextMenus"` which was added at some point, to support blocking element from within the context menu).

The `privacy` permission is needed for uBlock to be able to disable the setting "Prefetch resources to load pages more quickly". This will ensure no connection is opened at all for blocked requests: It's for your own protection privacy-wise.

This is Privacy Badger required permissions:

    "permissions": [
        "contextMenus",
        "cookies",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "http://*/*",
        "https://*/*"
    ],

### "Access your data on all web sites"

Since [first version](https://github.com/gorhill/uBlock/blob/b5fdac90539b19a0db8f36ea537bd150edb4d9c8/manifest.json).

- To be able to inspect all net requests so that they can be cancelled if needed.
    - Only on http- and https-based URL addresses.

See code:

- [chrome.webRequest](https://github.com/gorhill/uBlock/search?q=%22chrome.webRequest%22&type=Code)

### "Access your tabs and browsing activity"

Since [first version](https://github.com/gorhill/uBlock/blob/b5fdac90539b19a0db8f36ea537bd150edb4d9c8/manifest.json).

This is necessary to be able to:

- Create new tabs (when you click on a filter list, to see its content)
- To detect when a tab is added or removed:
- To update badge
- To flush from memory internal data structures
- To find out which tab is currently active (to fill popup menu with associated stats/settings)
- To be able to inject the element picker script
- To implement the popup-blocker

See code:

- [chrome.tabs](https://github.com/gorhill/uBlock/search?q=%22chrome.tabs%22&type=Code)
- [chrome.webNavigation](https://github.com/gorhill/uBlock/search?q=%22chrome.webNavigation%22&type=Code)

### "Change your privacy-related settings"

Since [version 0.9.8.2](https://github.com/gorhill/uBlock/commit/e65c2939757f09db646d277b82da8690aaf3adbc) ([release notes](https://github.com/gorhill/uBlock/releases/tag/0.9.8.2)).

This is necessary to be able to:

- Disable _"Prefetch resources to load pages more quickly"_
    - This will ensure no TCP connection is opened **at all** for blocked requests: **It's for your own protection privacy-wise.**<sup>[1]</sup>
    - For pages with lots for blocked requests, this will actually remove overhead from page load (if you did not have the setting already disabled).
    - When uBlock blocks a network request, the expectation is that it blocks **completely** the connection, hence the new permission is necessary for uBlock to do **truthfully** what it says it does.
- Disable [hyperlink auditing/beacon](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/) (0.9.8.5)

uBlock's primary purpose is to block **network connections**, not just data transfer. Not blocking the connection while just blocking the data transfer would mean uBlock is lying to users. So this permission will stay, and sorry for those who do not understand that it actually allows uBlock to do its intended job more thoroughly<sup>[2]</sup>. A blocker which does not thoroughly prevent connections is not a real blocker.

**Privacy Badger also requires exactly the same permissions.** I want uBlock to also serve privacy-minded users first.

If _prefetching_ had been disabled by default, this new permission would not be needed, but _prefetching_ is unfortunately enabled by default, and under _Privacy_ heading, which is itself hidden by default under _"advanced settings"_, and even at this point, you would still have to dig to find out the [negative side effects of prefetching](https://wikipedia.org/wiki/Link_prefetching#Issues_and_criticisms) (related: [dark patterns](http://darkpatterns.org/)).

![c](https://cloud.githubusercontent.com/assets/585534/7914528/924b9314-0845-11e5-8012-f67e4b1814cd.png)

Also, the benefits of _prefetching_ are probably marginal, and in the context of a blocker, the benefits could be negative, since a lot of useless connections would be made, just to be discarded after the browser find out the requests won't be made anyway. So do not fall for the _"lost of major performance boost"_ claim I read elsewhere, this is just a silly and baseless claim.

**Edit:** actually, prefetching is worst than I first thought, I had tested that it was just a connection issue, but [as per Google](https://support.google.com/chrome/answer/1385029):

> If you turn this setting on in Chrome, websites (and any of their embedded resources) that are prerendered or prefetched may set and read their own cookies as if you had visited them before -- even if you don’t visit the prerendered or prefetched pages after all.

See code:

- [chrome.privacy.network](https://github.com/gorhill/uBlock/commit/e65c2939757f09db646d277b82da8690aaf3adbc)

<sub>[1] Merely opening a TCP connection leaks your IP address to the remote server -- this is incompatible with an extension which primary purpose is to **completely** prevent connections to remove server, not just merely prevent the transfer of data. For instance, [see what can be found](https://www.browserleaks.com/whois) with a just that connection being established (IP, OS Fingerprinting, IP Address Location).</sub>

<sub>[2] In version 0.9.8.3, there will be [a setting to allow re-enabling prefetching](https://github.com/gorhill/uBlock/issues/274), default will still be  to disable it though.
</sub>