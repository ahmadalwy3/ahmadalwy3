I've seen an increase in misrepresentation and disinformation lately regarding uBlock -- and not surprisingly always from anonymous sources.

I will set the official record here.

There seems to be underhanded attempts to discredit uBlock lately in various venues. Here is a typical comment:

> uBlock who is recently found to not actually "block" ads, but rather hide them after its been displayed. Adblock actually blocks them before they can even display them.

The statement above is plain fear-using-disinformation. That kind of disinformation happens to be convenient to the incumbent blockers, **or** to those who have an interest in people using those incumbent blockers. 

Also another myth: I've seen in [many](https://np.reddit.com/r/AskReddit/comments/35s2je/whats_a_product_that_everybody_uses_but_nobody/cr7h8l6) [places](https://twitter.com/1v1MeInBed/status/611658444244951040) [lately](https://np.reddit.com/r/explainlikeimfive/comments/363569/eli5_how_come_adblockublock_doesnt_let_the_ad/crafo5p?context=3) [the](https://www.reddit.com/r/softwaregore/comments/3g8gg3/youtube_has_found_a_new_way_to_prevent_you_from/ctvybvc) following assertion:

> ublock blocks ads just like adblock plus, but triggers the ads API to think it got viewed

Completely false. uBlock Origin does not "trigger" any "ads API" (whatever that is). It prevents network requests from being made according to filter lists (or [dynamic filtering rules](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering)) so that your browser does not connect to remote servers, period.

***

Whoever claims that uBlock does not block network requests as expected should open [an issue with uBlock](https://github.com/gorhill/uBlock/issues) along with **all** the details supporting the claim. If the issue is not addressed satisfactorily, the claimant should report its finding + proof to the [PRISM Break project](https://github.com/nylira/prism-break/issues) in order to ensure [uBlock](https://prism-break.org/en/projects/ublock-origin/) is removed from that project.

***

There are two kinds of [ABP-compatible filters](https://adblockplus.org/en/filters): network filters and cosmetic filters. _Cosmetic filters_ are referred to as _element hiding_ filters by Adblock Plus ("ABP").

#### Network filters

**Short answer:** resources blocked: network requests are cancelled before they leave the browser.

The purpose of network filter is to prevent a network request to be made to a remote server, so as to prevent downloading a remote resource. uBlock will prevent the network request from even being made. This saves bandwidth, decrease privacy exposure -- as the remote server won't be able to log anything if you do not contact it.

#### Hosts file

**Short answer:** resources blocked: network requests are cancelled before they leave the browser.

uBlock also support the parsing and enforcing of hosts files -- something which ABP does not. All entries in a hosts file are parsed as network filters, i.e. no resource will be fetch from a remote server which appear in a hosts file, no connection will even be attempted.

![uBlock blocks reliably](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/ublock-blocks.gif)<br><sup>Blocked network requests are nipped in the bud.</sup>

#### Cosmetic filters

**Short answer:** resources hidden -- in various ways depending on the class of cosmetic filters.

These filters serve to remove DOM elements from a web page. They have no value privacy-wise, it is essentially to make web page look better by removing unwanted content, which usually cannot be blocked using network filters. Just like ABP, uBlock will hide DOM elements on a web page which match cosmetic filters. uBlock uses a [different method](https://github.com/gorhill/uBlock/wiki/Cosmetic-filtering-in-%C2%B5Block:-version-0.4.0.0-update) than other big-name blockers to hide the DOM elements though.

Different classes of cosmetic filters are applied differently:

- Specific cosmetic filters: injected before page's root DOM is loaded
    - No flickering
- Generic cosmetic filters: injected after page's root DOM is loaded
    - These are cacheable
    - Since these cosmetic filters are applied after page load, DOM elements **may** be hidden after they are rendered
        - Notice the emphasized "may": generally, you won't see this: the slower the computer, the higher the likelihood
        - Solution for when the behavior occurs and is an issue for a user: to create the appropriate specific cosmetic filter.
- Cached generic cosmetic filters: injected before page's root DOM is loaded
    - No flickering

Also, a very simple test page to find out if cosmetic filtering can be bypassed in your blocker: <http://raymondhill.net/ublock/adbox.html>.

#### More details regarding network filtering

When a network request is filtered, **both** uBlock and ABP will collapse the DOM counterpart -- if any -- of a blocked network request. They both work the same way in such scenario, in the absence of a cosmetic filter matching the DOM counterpart of a blocked network request.

In **both** uBlock and ABP, this occurs **after** the DOM is loaded, so in both cases, users **may** be able to visually notice the placeholder collapsing after the page loads.

Yet, uBlock is at an advantage in such case: since it does not inject thousands of CSS rules in a page (and frames within that page), this means it makes itself available sooner to handle the task of collapsing the DOM counterpart of blocked network requests. This can be clearly appreciated in the following [test page](http://raymondhill.net/ublock/tiles1.html):

- Chromium + uBlock: minimal flickering (sometimes none)
- Chromium + ABP: noticeable flickering
- Firefox + uBlock: no flickering
- Firefox + ABP: no flickering

Another advantage of uBlock here is that these collapsed-DOM-counterpart-of-blocked-network-requests are cached as temporary specific cosmetic filters internally.