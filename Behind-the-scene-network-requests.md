[Back to _Dynamic filtering: default-deny_](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-default-deny)

***

The filtering of behind-the-scene network request is available to [advanced users](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests).

### What are behind-the-scene network requests

_Behind-the-scene_ network requests are network requests which uBlock cannot associate with a specific tab in your browser: these requests come from _somewhere_, but uBlock is missing information to report exactly from where.

All network requests without a specific origin are classified as _behind-the-scene_. Typically, all blockers will ignore and automatically whitelist behind-the-scene network requests.

For the Chromium browser, examples of _behind-the-scene_ network requests:

- made by the browser to update extensions
- made by the browser because of specific functionality, like the setting _"Use a prediction service to help complete searches and URLs typed in the address bar"_
- made by web pages using [`navigator.sendBeacon()`](https://developer.mozilla.org/en-US/docs/Web/API/navigator.sendBeacon), [hyperlink auditing](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/), et al.
- made by installed extensions for not-so-good or good reasons (uBlock makes _behind-the-scene_ requests to fetch the filter lists when they need to be updated)

### How to inspect the behind-the-scene popup panel

- uBO from Chrome store: `chrome-extension://cjpalhdlnbpafiamejdnhcphjbkeiagm/popup.html?tabId=-1&fullsize=1`.
- uBO from Opera store: `chrome-extension://kccohkcpppjjkkjppopfnflnebibpida/popup.html?tabId=-1&fullsize=1`.
- uBO from AMO (Firefox): `chrome://ublock0/content/popup.html?tabId=-1&fullsize=1`.

For Chromium-based browsers, if you install uBO manually, you will have to replace the id part (i.e. `cjpalhdlnbpafiamejdnhcphjbkeiagm`) by the id used in your installation.

### How to inspect behind-the-scene network requests

Starting with uBlock version 0.8.6.0, you can inspect _behind-the-scene_ network requests using the network request logger. Simply select the _"Behind the scene"_ entry in the drop down list.

![c](https://cloud.githubusercontent.com/assets/585534/5888630/0691e7ee-a3d5-11e4-8510-ed0955f39deb.png)<br><sup>Various extensions installed to show that that these too make behind-the-scene requests</sup>

Typically, you will leave the network request logger opened for a long duration in order to catch any and all _behind-the-scene_ network requests.

The ability to inspect behind-the-scene network requests is available to all users. You do not need to enable _"advanced user"_ mode to see them in the network request logger.

### How to filter behind-the-scene network requests

**Important:** The blocking of behind-the-scene network requests can cripple important functionality of your browser or installed extensions. **If you decide to block some behind-the-scene network requests, you are entirely responsible for the consequences.**

The ability to filter _behind-the-scene_ network requests is only available when _"Advanced user"_ is enabled in the uBlock options.

The _behind-the-scene_ virtual tab is whitelisted by default.  No filtering will occur even after you enable _"Advanced user"_ mode.

To access the filtering settings for _behind-the-scene_ network requests, simply open the popup UI in the network request logger while the _"Behind the scene"_ entry is selected:

![Behind-the-scene popup](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/behind-the-scene-popup.gif)<br><sup>The popup UI will be filled with the settings/data of whatever tab is being currently inspected in the request logger.</sup>

The image above shows what happens when you navigate through Github: Github makes use of `navigator.sendBeacon()` to send data to Google Analytics, which results in the firing of _behind-the-scene_ requests in the Chromium browser.

**Important:** Filter behind-the-scene requests at your own risk. I will close without further comment any reported issue which is a direct consequence of blocking behind-the-scene network requests.

Remember that if you block indiscriminately, you could cripple the ability of your browser to update parts of itself or update extensions as well as the ability of extensions to work properly.  This is why this is an advanced user feature.
 
To turn off the filtering of _behind-the-scene_ requests, whitelist the _"Behind the scene"_ scope or turn off _"Advanced user"_ mode.

To whitelist the _behind-the-scene_ scope, add `behind-the-scene` as a whitelist directive in the _Whitelist_ tab of the uBlock dashboard.

If there are only very specific behind-the-scene network requests you would like to filter, a good approach to minimize potential problems is to use dynamic filtering: set a local rule for the `all` cell to _allow_ (green) (i.e. `behind-the-scene * * allow`). This will ensure nothing is blocked in the _behind-the-scene scope_, just as if uBlock is disabled for that scope. Then create _block_ rules for the specific hostnames for which you want to block all network requests, or `noop` if you want to subject those hostnames to static filtering only.