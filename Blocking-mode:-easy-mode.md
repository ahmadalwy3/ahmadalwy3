[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

This is uBlock Origin's default mode.

Roughly similar to using Adblock Plus with many filter lists.

Ads are blocked through _EasyList_ and _Peter Lowe’s Ad server list_, and privacy exposure is reduced through the use of _EasyPrivacy_. Some malware filter lists are selected by default. Also, uBlock Origin's own filter lists are selected as complement to the selected 3rd-party filter lists.

This mode is suitable for those who are concerned about reducing their privacy exposure, but yet still prefer an install-and-forget approach.

##### Characteristics

- Low likelihood of web pages being broken.
- Web pages should load somewhat faster compared to the [_very easy mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-very-easy-mode).

##### How to enable this mode

_Settings_ pane:
- _I am an advanced user_: unchecked.

_3rd-party filters_ pane:
- All of uBlock origin's custom filter lists: checked
- _EasyList_: checked
- _Peter Lowe’s Ad server list_: checked
- _EasyPrivacy_: checked
- _Malware Domain List‎_: checked
- _Malware domains_: checked
- All other filter lists: unchecked

##### Tips

You can augment the blocking power in easy mode by merely enabling more filter lists. If you add more filter lists, keep in mind:

- the more filter lists one uses, the higher the probability of web page breakage.
- not all filter lists are of good quality:
    - some may cause too much web page breakage.
    - some may result in some network requests to unexpectedly become unblocked ([example](https://github.com/gorhill/uBlock/issues/357)).
