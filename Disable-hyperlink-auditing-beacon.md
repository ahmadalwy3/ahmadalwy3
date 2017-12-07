### Background information

See [_"Hyperlink-Auditing aka `<a ping>` and Beacon aka `navigator.sendBeacon()`"_](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/).

### Chromium-based browsers

For those browsers, the network requests fired as a result of calling `navigator.sendBeacon()` are send as [behind-the-scene](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests) network requests.

#### Caveats for browsers based on Chromium version 48 or less

Network requests created as a result of web pages using `navigator.sendBeacon()` **will not be blocked** when the setting _"Disable hyperlink auditing/beacon"_ is checked. This is a limitation of the chrome API prior to v49, as network request fired as a result of calling `navigator.sendBeacon()` are reported as the generic type `other` by the browser.

The [webRequest API](https://developer.chrome.com/extensions/webRequest) was extended in Chromium 49 to support new request types, and thus the settings works fine for any browser based on Chromium 49 or higher, as there is now a specific network request type, `ping`, which uBO normalizes to `beacon` -- and hence can now filter correctly.