
 - [Current RAW version of Resources Library ↪](https://github.com/uBlockOrigin/uAssets/blob/master/filters/resources.txt)
 - [General purpose scriptlets](#general-purpose-scriptlets)
 - [Defuser scriptlets](#defuser-scriptlets)
 - [Empty redirect resources](#empty-redirect-resources)
 - [URL-specific sanitized redirect resources](#url-specific-sanitized-redirect-resources-surrogates)
 - [Other](#other)
 - [Glossary](#glossary)



***



## General purpose scriptlets
 - most script relies on `Object` _properties_ ([_methods_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#Methods_of_the_Object_constructor)), altering them may not be the best idea (you should know what you are doing).
 - "optional" for "string/_regular expression_" parameter defaults to "catch all" (`/.?/`) if not specified.
 - "string" parameter means plain character(s)/word(s), quotes will be taken literally, commas [must be escaped](https://github.com/uBlockOrigin/uAssets/commit/2bec415a9bc4f81b29be3bf083ef1a20552f39db#commitcomment-29327114) in regex literals: `/foo\x2cbar\u002cbaz/`
 - "regular expression" parameter means JavaScript [regular expression literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Writing_a_regular_expression_pattern)
 - mime type is `application/javascript` if not present
 - You can use the short alias form when available for scriptlet name
 - You can omit the `.js` from the scriptlet name (eventually in some future this will be the official way to do this)
     - Do **not** skip `.js` when the scriptlet is used with `redirect=`, only when used in `+js(...)`.
 - crossed out resources are deprecated/removed.
 
 

***

### acis.js
### abort-current-inline-script.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1942)
Aborts execution of inline script (_throws_ `ReferenceError`) when attempts to access specified _property_ when content of `<script>` _element_ matches specified text or _regular expression_.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object accessed inside `<script>` tag we want to break
 - optional, string/_regular expression_ matching in `<script>` _element_ content


***

### aopr.js
### abort-on-property-read.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1701)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to read specified _property_. Writes are ignored.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object


***

### aopw.js
### abort-on-property-write.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1668)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to write specified _property_.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object that will be overwritten


***

### aeld.js
### addEventListener-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1879)
Prevents attaching event listeners.

Parameters:
 - optional, string/_regular expression_, name of event listener
 - optional, string/_regular expression_ matching in stringified handler function


***

### aell.js
### addEventListener-logger.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1867)
Logs to the console event listeners created on page.


***

### cookie-remover.js [↪](https://github.com/uBlockOrigin/uAssets/blob/7a841333e440452ec2d9e0dbe5c81459a99b59b4/filters/resources.txt#L2363)
Removes current page cookies specified by name. For current domain, wildcard (dot) subdomain(s), current and `/` path, script accessible (HttpOnly=false), on load and before unload.

Caveats: cookies set for higher level domain will not be removed. For example, if current page domain is `www.example.com`, cookies set for `example.com` will not be removed.

Parameters:
 - optional, string/_regular expression_, matching in the name of the cookie


***

### csp.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1849)
Deprecated by `$csp` network filter option.  
TODO: csp filter is explained on adblockplus.org/en/filters but no direct link  
Applies content security policy by inserting `<meta http-equiv=Content-Security-Policy content="*directive*">` tag to html `<head>` _element_.
Read more at https://www.w3.org/TR/CSP2/#delivery-html-meta-element  
[Content Security Policy Quick Reference Guide](https://content-security-policy.com/)

Parameters:
 - required, valid Content Security Policy directive


***

### disable-newtab-links.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2086)
Prevents creating new tabs/windows by deactivating links with `target` attribute.

Parameters:
 - none


***

### noeval.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1272)
Prevent web pages from using _`eval()`_, and report attempts to console.


***

### noeval-silent.js
### ~silent-noeval.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1279)
Prevent web pages from using _`eval()`_.


***

### noeval-if.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1286)
Prevent web pages from using _`eval()`_ on specific matching payloads.

Parameters:
 - optional, string/_regular expression_, matching in payload string.

***

### nowebrtc.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1306)
Disables WebRTC by preventing web pages from using [`RTCPeerConnection()`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). Report attempts in console.


***

### ra.js
### remove-attr.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2263)
Removes attribute(s) from DOM tree node(s). Will run only once after page load.

Parameters:
 - required, attribute or list of attributes joined by `|`
 - optional, CSS selector, specifies nodes from which attributes will be removed


***

### set-constant.js [↪](https://github.com/uBlockOrigin/uAssets/blob/088f2f61d8b7de5812b2a3c955bf8484091a0867/filters/resources.txt#L2111)
Creates _property_ and initializes it to predefined value from set of available properties. TODO: "constant" is not constant - current implementation does not prevent to assign value of another type.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object
 - required, possible values:
     - positive decimal integer, no sign, with maximum value of 0x7FFF (32767)
     - one value from set of predefined constants:
         - `undefined`
         - `false`
         - `true`
         - `null`<sup>[2018-11-24](https://github.com/uBlockOrigin/uAssets/commit/8fd3f7e3a344e5fc29344f1ba914e82457eb1d13#diff-8809d5783978a0b5b88f93d7dab99de0)</sup>
         - `noopFunc` - function with empty body
         - `trueFunc` - function returning true
         - `falseFunc` - function returning false
         - `''` - empty string<sup>[2019-01-06](https://github.com/uBlockOrigin/uAssets/commit/5051610f0e2374955a03c54be42bbbe9115f05c7#diff-8809d5783978a0b5b88f93d7dab99de0R2132)</sup>


***

### sid.js
### setInterval-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1787)
Defuses calls to _`setInterval()`_ function for specified matching callbacks and intervals by setting callback function to noop.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching interval


***

### sil.js
### setInterval-logger.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1811)
Logs to the console calls to _`setInterval()`_ function.


***

### std.js
### setTimeout-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1754)
Defuses calls to _`setTimeout()`_ function for specified matching callbacks and delays by setting callback function to noop.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching delay


***

### stl.js
### setTimeout-logger.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1776)
Logs to the console calls to _`setTimeout()`_ function.


***

### nano-sib.js
### nano-setInterval-booster.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2222)
Adjusts interval for specified _`setInterval()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching interval
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, interval multiplier


***

### nano-stb.js
### nano-setTimeout-booster.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2176)
Adjusts delay for specified _`setTimeout()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching delay
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, delay multiplier


***

### sharedWorker-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1822)
Deprecated by `$csp` filter option.  
TODO: csp filter is explained on https://adblockplus.org/en/filters but no direct link.  
Defuses sharedWorker by passing empty worker file (Blob URL) for specified worker URLs

Parameters:
 - optional, string/_regular expression_, matching in worker URL


***

### window.open-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1995)
Prevent opening new windows by [`window.open()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) when URL positively or negatively matches to specific string.

Parameters:
 - optional - defaults to "matching", any positive number for "matching", `0` or any string for "not matching",
 - optional, string/_regular expression_, matching/not matching in URL parameter passed to `window.open()`


***

### window.name-defuser [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L874)
Clears `window.name` _property_ which can be misused for tracking purposes.

Parameters:
 - none


***

### overlay-buster.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1102)
Experimental, gets rid of overlay dialogs, works for ~30s after page load. Preferred way to handle overlays is to use standard cosmetic filters and optionally [style injection](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#style).


***

### alert-buster.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1182)
Disables [`alert()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) dialog boxes by redirecting messages to console.


***

## Defuser scriptlets



### ampproject_v0.js
### ~ampproject.org/v0.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/7a841333e440452ec2d9e0dbe5c81459a99b59b4/filters/resources.txt#L2397)
Removes animation (artificial 8s delay) added to desktop pages supporting AMP, when ampproject.org scripts are blocked.

### fingerprint2.js  [↪](https://github.com/uBlockOrigin/uAssets/blob/379a5a69059baa35627fe8205f44d97d129373af/filters/resources.txt#L2348)
Defuses Fingerprintjs2. Sanitize `Fingerprint2` object.

### pornhub-popup-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L647)
Sets specific localStorage items (`InfNumFastPops`, `InfNumFastPopsExpire`)

### forbes-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L697)
Fix '/forbes/welcome/' page redirection. Redirects to URL from `toURL` cookie

### nobab.js
### ~bab-defuser.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L738)
Defuses BlockAdblock. Prevents executing of _`eval()`_ on sets of predefined payloads.

### phenv-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L797)
Defuses "g0yav3-lab" Anti Adblock. TODO Deprecated, sets static properties (`PHENV`)

### sas-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1056)
Deprecated, Convenience, sets static properties (`Ads.display`, `Ads.refresh`)
TODO: Convenience means "patches more than one property", I keep this here, not in "Other", just in case.

### nofab.js
### ~fuckadblock.js-3.2.0~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L186)
Convenience, Sanitize `FuckAdBlock`, `BlockAdBlock`, `SniffAdBlock`, `fuckAdBlock`, `blockAdBlock`, `sniffAdBlock` properties.
Often used as redirect in network filters. TODO: copy to redirect?

### lemonde-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1085)
Sets specific localStorage item (`lmd_me_displayed`)

### popads-dummy.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1465)
Convenience, sets static properties (`PopAds`, `popns`)

### popads.js
### ~popads.net.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1443)
Convenience, abort-on-property-write.js (`PopAds`, `popns`), _throws_ "`magic`"

### rtlfr-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1091)
Deprecated by `:style()` cosmetic filter.
Applies `overflow: auto` style to document body _element_ after window `load` event.

### uabinject-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L640)
Defuses Addefend, convenience, sets static properties (`trckd`, `uabpdl`, `uabInject`, `uabDetect`)

### impspcabe-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1172)
Deprecated, Convenience, sets static properties (`_impspcabe`, `_impspcabe_alpha`, `_impspcabe_beta`, `_impspcabe_path`) TODO: not used, static properties, cannot be set to `about:blank` by sciptlets is this really needed, used on 4 domains

### gpt-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1232)
Deprecated, Convenience, sets static properties (`_resetGPT`, `resetGPT`, `resetAndLoadGPTRecovery`, `_resetAndLoadGPTRecovery`, `setupGPT`, `setupGPTuo`)

### palacesquare.rambler.ru-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1913)
Aborts creation of Promise when executor content matches 'getRandomSelector' (_throws_ `Error`) TODO: Freezes `Promise` properties?

### adfly-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2024)
Defuses anti adblock on adfly shortened links.

### damoh-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2291)
Fix for disappearing videos on chip.de


***

## Empty redirect resources
These are smallest/shortest/fastest to execute files. Can be used in network filters as a parameter to `$redirect` option along with specific matching `$type` option.
They purpose is to mislead page to think that real files have been served.



### Supported types
TODO: filter types, mime types, this needs clarification
TODO: how filter type relates to mime type, needs more [source digging](https://github.com/gorhill/uBlock/blob/master/src/js/scriptlet-filtering.js)
font, image, media, object, script, stylesheet, subdocument, xmlhttprequest


### Available resources
 - Images
	- ~1x1-transparent.gif~ 1x1.gif `image/gif;base64` `$image` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L13)
	- ~2x2-transparent.png~ 2x2.png `image/png;base64` `$image` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L17)
	- ~3x2-transparent.png~ 3x2.png `image/png;base64` `$image` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L22)
	- ~32x32-transparent.png~ 32x32.png `image/png;base64` `$image` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L27)
 - Source code
	- noopcss `text/css` `$stylesheet` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L35)
	- ~noopframe~ noop.html `text/html` `$subdocument` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L44)
	- ~noopjs~ noop.js `application/javascript` `$script` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L38)
	- ~nooptext~ noop.txt `text/plain` `$xmlhttprequest` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L32)
 - Media files
	- ~noopmp3-0.1s~ noop-0.1s.mp3 `audio/mp3;base64` `$media` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L56)
	- ~noopmp4-1s~ noop-1s.mp4 `video/mp4;base64` `$media` [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L74)

TODO: object and font resources are missing? Find discussion about adding them on demand.


***

## URL-specific sanitized redirect resources (surrogates)



### addthis_widget.js
### ~addthis.com/addthis_widget.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L887)
### amazon_ads.js
### ~amazon-adsystem.com/aax2/amzn_ads.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1004)
### monkeybroker.js
### ~d3pkae9owd2lcf.cloudfront.net/mb105.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1610)
### doubleclick_instream_ad_status.js
### ~doubleclick.net/instream/ad_status.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L882)
### google-analytics_ga.js
### ~google-analytics.com/ga.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L252)
### google-analytics_analytics.js
### ~google-analytics.com/analytics.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L353)
### google-analytics_inpage_linkid.js
### ~google-analytics.com/inpage_linkid.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L405)
### google-analytics_cx_api.js
### ~google-analytics.com/cx/api.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L416)
### googletagservices_gpt.js
### ~googletagservices.com/gpt.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L435)
### googletagmanager_gtm.js
### ~googletagmanager.com/gtm.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L575)
### googlesyndication_adsbygoogle.js
### ~googlesyndication.com/adsbygoogle.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L601)
### scorecardresearch_beacon.js
### ~scorecardresearch.com/beacon.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L831)
### outbrain-widget.js
### ~widgets.outbrain.com/outbrain.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L845)
### hd-main.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L140)
### xvideos.com.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1477)

### disqus_forums_embed.js AND disqus_embed.js
### ~disqus.com/forums/*/embed.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L939) AND ~disqus.com/embed.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L959)
Along with [Disqus click-to-load](https://gist.github.com/gorhill/ef1b62d606473c68d524) filter list, allows to have Click-to-ublock experience for Discus comments widgets.

### twitch-videoad.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L2318)
Twitch stream embedded ads bypasser


***

## Other
Deprecated by general purpose scriptlets / outdated (please move to proper section if still used).



### antiAdBlock.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L232)
Sanitize `antiAdBlock.onDetected`, `antiAdBlock.onNotDetected`

### pornhub-sanitizer.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L666)
Removes ad frames on Pornhub (`block_logic`)

### nr-unwrapper.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1191)
Fix memory leaks on spotify, newrelic. https://github.com/uBlockOrigin/uAssets/issues/36

***

### golem.de.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1430)
Deprecated, addEventListener-defuser

### uAssets-17 [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L168)
Deprecated, setTimeout-defuser

### last.fm.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1634)
Deprecated, setTimeout-defuser

### ytad-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L985)
Deprecated, setTimeout-defuser, fix for YouTube "An error occured"

***

### bcplayer-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L909)
Deprecated, sets static properties (`bcPlayer.ads`)

### wpredirect-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L714)
Deprecated, sets static properties (`TWP.Identity.initComplete`)

### kissanime-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L784)
Deprecated, sets static properties (`DoDetect1`, `DoDetect2`, `isBlockAds2`)

### __$dc-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1364)
Deprecated, sets static properties (`Math.mt_random`), _throws_ `TypeError`

### upmanager-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1519)
Deprecated, sets static properties (`upManager`)

### r3z-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1596)
Deprecated, sets static properties (`_r3z.jq`, `_r3z.pub`)

### folha-de-sp.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1254)
Deprecated, sets static properties (`folha_ads`)

### chartbeat.js
### ~static.chartbeat.com/chartbeat.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1653)
Deprecated, sets static properties (`pSUPERFLY.activity`, `pSUPERFLY.virtualPage`)

### entrepreneur.com.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1863)
Deprecated, sets static properties (`analyticsEvent`)

### ligatus_angular-tag.js
### ~ligatus.com/*/angular-tag.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L629)
Deprecated, sets static properties (`adProtect`, `uabpdl`, `uabDetect`)

### openload.co.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L724)
Deprecated, sets static properties (`adblock2`, `OlPopup`, `preserve`, `turnoff`)

### imore-sanitizer.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1158)
Deprecated, sets static properties (`mbn_zones`)

### smartadserver.com.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1564)
Deprecated, sets static properties (`SmartAdObject`, `SmartAdServerAjax`, `smartAd.LoadAds`, `smartAd.Register`)

### lesechos.fr.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1573)
Deprecated, sets static properties (`checkAdBlock`)

### criteo.net.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1580)
Deprecated, sets static properties (`Criteo.criteo`)

### goyavelab-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L684)
Deprecated, sets static properties (`_$14`)

### figaro-defuser.js [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1074)
Deprecated, sets static properties (`adisplaynormal`)



***

## Glossary



 - `throw`:            https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw
 - `eval()`:           https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval
 - `setInterval()`     https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval
 - `setTimeout()`      https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
 - regular expression: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Writing_a_regular_expression_pattern
 - element:            https://developer.mozilla.org/en-US/docs/Web/HTML/Element
 - property:           https://developer.mozilla.org/en-US/docs/Glossary/property/JavaScript
 - method:             https://developer.mozilla.org/en-US/docs/Glossary/Method