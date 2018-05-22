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


***

[1] [stackoverflow.com](https://stackoverflow.com/questions/11613371/chrome-extension-content-script-on-https-chrome-google-com-webstore/11614440#11614440), [chrome_extensions_client.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/chrome/common/extensions/chrome_extensions_client.cc#235), [extension_urls.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/extensions/common/extension_urls.cc#33)

[2] https://hg.mozilla.org/mozilla-central/rev/39e131181d44