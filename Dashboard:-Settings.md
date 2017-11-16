- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

![Figure 1](https://user-images.githubusercontent.com/585534/27254308-dfe1dce0-5353-11e7-9dd3-913601747be6.png)

## General

***

### Make use of context menu where appropriate

If checked, this gives permission for uBlock to add items in the context menu which are meant to improve convenience. Currently, only one item is added to the context menu, _"Block element"_, which purpose is to launch the element picker in order to filter out a specific element on a page.

***

### Color-blind friendly

Currently mostly useful for users who checked _"I am an advanced user"_ (see below).

***

### I am an advanced user

If you check this, this will enable [uBlock's dynamic filtering](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering), and the dynamic filtering pane will become available from uBlock's popup UI.

Unchecking this disables the dynamic filtering. And the dynamic filtering pane in the popup UI will no longer be available.

_Advanced user_ mode also gives access to the advanced settings (normally hidden), and enables the ability to filter [behind-the-scene network requests](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests).

You should avoid playing with advanced features and settings unless [you understand fully what you are doing](https://github.com/gorhill/uBlock/wiki/Advanced-user-features).

***

## Privacy

### Disable pre-fetching

Checking this will disable prefetching in your browser. When prefetching is enable, the browser _can_ still establish connections to remote servers even if the resource from these remote servers are meant to be blocked by uBlock.

This prevent the browser from bypassing uBlock's filtering engine before establishing connections to remote servers.

Mozilla's [_"Link prefetching FAQ"_](https://developer.mozilla.org/docs/Web/HTTP/Link_prefetching_FAQ):

> **Privacy implications** Along with the referral and URL-following implications already mentioned above, prefetching will generally cause the cookies of the prefetched site to be accessed.

Google's [_"Make webpages load faster"_](https://support.google.com/chrome/answer/1385029):

> If you turn this setting on in Chrome, websites (and any of their embedded resources) that are prerendered or prefetched may set and read their own cookies as if you had visited them before -- even if you don’t visit the prerendered or prefetched pages after all.

**IMPORTANT NOTE:** On Chromium 51 and above (including browsers based on Chromium 51 and above), this setting does not block DNS lookups and preconnections. For details, see:
- <https://github.com/gorhill/uBlock/issues/3219>
- <https://bugs.chromium.org/p/chromium/issues/detail?id=785125>

***

### Disable hyperlink auditing

Checking this will prevent hyperlink auditing<sup>[1]</sup>. _Hyperlink auditing_ is best summarized as "phone home" features (or more accurately "phone anywhere"). The details are well explained [here](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/).

***

### Prevent WebRTC from leaking local IP address

![c](https://cloud.githubusercontent.com/assets/585534/8344622/0ce20cc4-1ab2-11e5-8f46-a0a387c91d63.png)

Background info: [STUN IP Address requests for WebRTC](https://github.com/diafygi/webrtc-ips)

Test case: <https://github.com/gorhill/uBlock/wiki/Prevent-WebRTC-from-leaking-local-IP-address>.

Keep in mind that this feature is to prevent **leakage** of your non-internet-facing IP adresses. The purpose of this feature is not to hide your current internet-facing IP address -- so be cautious to not misinterpret the results of the tests above. For example, if you use a VPN, your internet-facing IP address is that of the VPN, so your ISP-provided IP address should not be visible to outside world with this setting checked. However, if you are not behind any VPN or proxy, your ISP-provided IP address will be visible regardless of this setting.

**Caveats:**
- Chromium-based browsers: the feature works only on version 42 and above.
- Firefox: the only way to prevent local IP address leakage is to disable completely WebRTC.
    - WebRTC is required for Firefox Hello to work properly.

***

### Block CSP reports

You can block network requests made as a result of your browser reporting Content Security Policy violations ("CSP reports") to a remote server (which can be 3rd-party to the site where the violation occurred).

**Important:** disabling CSP reporting is not something which will break web pages, the purpose of CSP reporting is _strictly_ a development tool for web sites.

Consider this excerpt from [Reporting API / Privacy Considerations](http://wicg.github.io/reporting/#privacy) (my emphasis):

> 8.6. Disabling Reporting
> 
> [...]
> 
> That said, it can’t be the case that this general benefit be allowed to take priority over the ability of a user to individually opt-out of such a system. Sending reports costs bandwidth, and potentially could reveal some small amount of additional information above and beyond what a website can obtain in-band ([NETWORK-ERROR-LOGGING], for instance). **User agents MUST allow users to disable reporting with some reasonable amount of granularity in order to maintain the priority of constituencies espoused in [HTML-DESIGN-PRINCIPLES].**

There is currently no way to easily toggle CSP reporting in either Chromium or Firefox. This per-site switch is to address this shortcoming.

Note that as opposed to all other network requests, behind-the-scene network requests which are actual CSP reports will also be filtered out according to this setting. So if you globally disable CSP reporting in uBO, this will also apply to behind-the-scene network requests.

Note that the blocking of CSP reports is implemented as a per-site switch internally in uBO, so this means that an advanced user could create rules in the _My rules_ pane in the dashboard to allow a more granular control of the blocking of CSP reports. For example:

    no-csp-reports: example.com false

The above rule means CSP reports would not be blocked on `example.com` when CSP reports are blocked globally. The reverse will also work:

    no-csp-reports: example.com true

The above rule means CSP reports would be blocked on `example.com` when CSP reports are not blocked globally.

***

## Backup/restore section

The bottom-most section is for you to easily backup/restore/reset all settings in uBlock.

It is suggested you backup all your settings regularly.