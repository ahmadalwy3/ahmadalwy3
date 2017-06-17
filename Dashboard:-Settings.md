- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

![Figure 1](https://user-images.githubusercontent.com/585534/27254308-dfe1dce0-5353-11e7-9dd3-913601747be6.png)

### Below more details for the non-self-explanatory items

***

#### Make use of context menu where appropriate

If checked, this gives permission for uBlock to add items in the context menu which are meant to improve convenience. Currently, only one item is added to the context menu, _"Block element"_, which purpose is to launch the element picker in order to filter out a specific element on a page.

***

#### Color-blind friendly

Currently mostly useful for users who checked _"I am an advanced user"_ (see below).

***

#### I am an advanced user

If you check this, this will enable [uBlock's dynamic filtering](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering), and the dynamic filtering pane will become available from uBlock's popup UI.

Unchecking this disables the dynamic filtering. And the dynamic filtering pane in the popup UI will no longer be available.

_Advanced user_ mode also gives access to the advanced settings (normally hidden), and enables the ability to filter [behind-the-scene network requests](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests).

You should avoid playing with advanced features and settings unless [you understand fully what you are doing](https://github.com/gorhill/uBlock/wiki/Advanced-user-features).

***

#### Disable pre-fetching

Checking this will disable prefetching in your browser. When prefetching is enable, the browser _can_ still establish connections to remote servers even if the resource from these remote servers are meant to be blocked by uBlock.

This prevent the browser from bypassing uBlock's filtering engine before establishing connections to remote servers.

Mozilla's [_"Link prefetching FAQ"_](https://developer.mozilla.org/docs/Web/HTTP/Link_prefetching_FAQ):

> **Privacy implications** Along with the referral and URL-following implications already mentioned above, prefetching will generally cause the cookies of the prefetched site to be accessed.

Google's [_"Make webpages load faster"_](https://support.google.com/chrome/answer/1385029):

> If you turn this setting on in Chrome, websites (and any of their embedded resources) that are prerendered or prefetched may set and read their own cookies as if you had visited them before -- even if you don’t visit the prerendered or prefetched pages after all.

***

#### Disable hyperlink auditing

Checking this will prevent hyperlink auditing<sup>[1]</sup>. _Hyperlink auditing_ is best summarized as "phone home" features (or more accurately "phone anywhere"). The details are well explained [here](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/).

***

#### Prevent WebRTC from leaking local IP address

![c](https://cloud.githubusercontent.com/assets/585534/8344622/0ce20cc4-1ab2-11e5-8f46-a0a387c91d63.png)

Background info: [STUN IP Address requests for WebRTC](https://github.com/diafygi/webrtc-ips)

Test case: <https://github.com/gorhill/uBlock/wiki/Prevent-WebRTC-from-leaking-local-IP-address>.

Keep in mind that this feature is to prevent **leakage** of your non-internet-facing IP adresses. The purpose of this feature is not to hide your current internet-facing IP address -- so be cautious to not misinterpret the results of the tests above. For example, if you use a VPN, your internet-facing IP address is that of the VPN, so your ISP-provided IP address should not be visible to outside world with this setting checked. However, if you are not behind any VPN or proxy, your ISP-provided IP address will be visible regardless of this setting.

**Caveats:**
- Chromium-based browsers: the feature works only on version 42 and above.
- Firefox: the only way to prevent local IP address leakage is to disable completely WebRTC.
    - WebRTC is required for Firefox Hello to work properly.

***

#### Backup/restore section

The bottom-most section is for you to easily backup/restore/reset all settings in uBlock.

It is suggested you backup all your settings regularly.