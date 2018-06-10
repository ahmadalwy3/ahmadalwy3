Privileged Pages are the webpages that browser-developers consider as an entitled webpage/s where extensions are tasked to not work/have their functionality ceased entirely.

For Chromium<sup>1</sup>:
```
chrome.google.com/webstore/*
```

- On the aformentioned domain, ALL Chromium/Chrome extensions will cease their functionality.

For Firefox<sup>2</sup>:
```
accounts-static.cdn.mozilla.net
accounts.firefox.com
addons.cdn.mozilla.net
addons.mozilla.org
api.accounts.firefox.com
content.cdn.mozilla.net
content.cdn.mozilla.net
discovery.addons.mozilla.org
input.mozilla.org
install.mozilla.org
oauth.accounts.firefox.com
profile.accounts.firefox.com
support.mozilla.org
sync.services.mozilla.com
testpilot.firefox.com
```

- Just like Chrome, Firefox's WebExtensions will also cease to work on these aformentioned domains.

- To allow WebExtensions in Firefox to run on these pages (at your own risk) open `about:config` and modify the following <sup>3</sup> :

    - Set `extensions.webextensions.restrictedDomains` to be an empty string.<sup>4</sup>
    - Set `privacy.resistFingerprinting.block_mozAddonManager` to `true`.<sup>5</sup> (must be manually created by right clicking and selecting _New > Boolean_<sup>3</sup>)

***

[1] [stackoverflow.com](https://stackoverflow.com/questions/11613371/chrome-extension-content-script-on-https-chrome-google-com-webstore/11614440#11614440), [chrome_extensions_client.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/chrome/common/extensions/chrome_extensions_client.cc#235), [extension_urls.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/extensions/common/extension_urls.cc#33)

[2] https://hg.mozilla.org/mozilla-central/rev/39e131181d44

[3] https://www.ghacks.net/2017/10/27/how-to-enable-firefox-webextensions-on-mozilla-websites/

[4]  https://bugzilla.mozilla.org/show_bug.cgi?id=1445663#ch-3

[5] https://bugzilla.mozilla.org/show_bug.cgi?id=1310082#c24

