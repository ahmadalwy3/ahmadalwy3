Motivation for creating this page, this comment made in the spirit of _Fake News_ (i.e. with no supporting objective evidences, merely a _"just trust me"_ statement):

> Ublock is inferior in capabilities [to ABP] as a result of being lighter on the browser [[source](http://forums.mozillazine.org/viewtopic.php?p=14743232#p14743232)]

There is nothing wrong with preferring ABP to uBO. There is however something wrong when someone engages in misinformation regarding uBO because of their preference for ABP.

This is my reference answer to such claims.

uBlock Origin is lighter on the browser because of many choices which were made regarding how the filtering engine is designed internally. A coarse enumeration of these choices are:
- lean in-memory filter representation
- plain string comparisons instead of regular expressions wherever possible
    - a majority of network filters can be reduced to plain string comparison, and this is what uBO does internally for these filters, whereas ABP convert _all_ network filters into regular expressions.
    - Example, `&ad_zones=` (filter found in EasyList).
        - ABP's code conceptually is: `/&ad_zones=/.test(url)` -- the whole URL must be scanned
        - uBO's code conceptually is: `url.startsWith('&ad_zones=', i)` -- no scanning of the URL
- does not unconditionally inject 18,000+ (that is with EasyList only) generic CSS rules in all pages/frames<br><sup>meaning no undue [memory usage issues](https://bugzilla.mozilla.org/show_bug.cgi?id=1320872)</sup>

Do these design choices really cause uBO to be _"inferior in capabilities"_ compared to ABP? See the capabilities comparison grid below for an answer (at time of writing):

Features |  ABP  |  uBO
-------- | :---: | :---:
**network filtering**
[multi-stage filtering engine](https://github.com/gorhill/uBlock/wiki/Overview-of-uBlock's-network-filtering-engine)<br><sup>ability for users to easily override filters in 3rd-party filter lists on a per-site basis</sup> |     | yes
`@@...$document` | yes | [no](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#not-supported)
can read hosts files |     | yes
`inline-script`<br><sup>to prevent execution of inline javascript</sup> | [no](https://issues.adblockplus.org/ticket/748) | [yes](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#inline-script)
`important`<br><sup>to be able to override exception filters</sup> |     | [yes](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#important)
`popunder` | [no](https://issues.adblockplus.org/ticket/2095) | yes
`redirect`<br><sup>to redirect to local resources, key to privacy and to counter anti-blockers</sup> |     | yes
`csp=`<br><sup>see [rationale](https://github.com/gorhill/uBlock/issues/1930#issuecomment-301055346)</sup> |     | yes<br><sup>v1.12.5</sup>
[strict blocking](https://github.com/gorhill/uBlock/wiki/Strict-blocking) |     | yes
rule-based filtering<br><sup>firewall-like or URL-based rules with corresponding point-and-click UI</sup> |     | yes
behind-the-scene<br><sup>uBO's logger reports behind-the-scene request, filtering is opt-in</sup> |     | [yes](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests)
**cosmetic filtering**
entity-based filters |     | [yes](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#entity-based-cosmetic-filters)
`-abp-properties` | yes | [no](https://github.com/gorhill/uBlock/issues/139)
`:has` | [not yet](https://issues.adblockplus.org/ticket/2360) | yes
`:has-text`<br>`:if` `:if-not`<br>`:matches-css` `:matches-css-before` `:matches-css-after`<br>`:xpath` |     | yes
`:style` | [no](https://issues.adblockplus.org/ticket/756) | yes
`script:contains` |     | Firefox only
`script:inject`<br><sup>key to counter anti-blockers</sup> |     | yes
**privacy**
pro-user default settings<br><sup>uBO is not monetized, it's under no pressure to [compromise](https://adblockplus.org/forum/viewtopic.php?f=17&t=50215) on pro-user interests</sup> |     | yes
disable pre-fetching |     | [yes](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-pre-fetching)
disable hyperlink auditing |     | [yes](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-hyperlink-auditing)
disable local IP addresses leakage through WebRTC |     | [yes](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#prevent-webrtc-from-leaking-local-ip-address)
**other features**
pre-compilation of filter lists for fast loading of filters |     | [yes](https://github.com/gorhill/uBlock/wiki/Launch-and-filter-lists-load-performance)
"acceptable ads" | yes | [no](https://github.com/gorhill/uBlock/blob/master/MANIFESTO.md)
disable everywhere | yes |
count filter hits | yes | [no](https://github.com/gorhill/uBlock/issues/1353)
ability to globally ignore generic cosmetic filters<br><sup>useful for low-performance mobile devices</sup> |     | yes
cloud storage |     | yes
point-and-click firewall-like filtering<br><sup>allows for [relax](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode) or [strict](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-hard-mode) default-deny approach</up> |     | yes
logger | per-page | unified
point-and-click per-site no-popups |     | [yes](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-popups)
point-and-click per site no-cosmetic-filtering |     | [yes](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-cosmetic-filtering)
point-and-click per site no-large-media-elements |     | [yes](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-large-media-elements)
point-and-click per site no-remote-fonts |     | [yes](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-remote-fonts)
integrated element picker | Chromium-based browsers only | [yes](https://github.com/gorhill/uBlock/wiki/Element-picker)
easy backup/restore of all settings | Firefox only | yes
