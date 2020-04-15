
 - Current RAW version of Resources can be found in [scriptlets.js file ↪](https://github.com/gorhill/uBlock/blob/master/assets/resources/scriptlets.js) and [web_accessible_resources directory ↪](https://github.com/gorhill/uBlock/tree/master/src/web_accessible_resources)
 - [Legacy RAW version of Resources Library ↪](https://github.com/uBlockOrigin/uAssets/blob/master/filters/resources.txt)
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
 - "string" parameter means plain character(s)/word(s), quotes will be taken literally, commas [must be escaped](https://github.com/uBlockOrigin/uAssets/commit/2bec415a9bc4f81b29be3bf083ef1a20552f39db#commitcomment-29327114) in regex literals: `/foo\x2cbar\u002cbaz/`, after [1.21.7b8](https://github.com/gorhill/uBlock/commit/d67340f14db6ce5b446ef0ff4586b5e4d31f1086#diff-b03ba512faa0934947e57d28dc99b43bL242) commas can be escaped by backslash character (`foo\,bar`)
 - "regular expression" parameter means JavaScript [regular expression literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Writing_a_regular_expression_pattern)
 - mime type is `application/javascript` if not present
 - You can use the short alias form when available for scriptlet name
 - You can omit the `.js` from the scriptlet name (eventually in some future this will be the official way to do this)
     - Do **not** skip `.js` when the scriptlet is used with `redirect=`, only when used in `+js(...)`.
 - crossed out resources are deprecated/removed.
 
 

***

### acis.js /
### abort-current-inline-script.js [↪](https://github.com/gorhill/uBlock/blob/1a133d0a1fc44f4bce357ebbea65d645f3eb4e8e/assets/resources/scriptlets.js#L35)
Aborts execution of inline script (_throws_ `ReferenceError`) when attempts to access specified _property_ when content of `<script>` _element_ matches specified text or _regular expression_.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object accessed inside `<script>` tag we want to break
 - optional, string/_regular expression_ matching in `<script>` _element_ content

Examples:
 - `weristdeinfreund.de##+js(acis, Number.isNaN)`
 - `tichyseinblick.de##+js(acis, Math, /\}\s*\(.*?\b(self|this|window)\b.*?\)/)`


***

### aopr.js /
### abort-on-property-read.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L96)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to read specified _property_. Writes are ignored.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object

Examples:
 - `tagesspiegel.de##+js(aopr, Notification)`


***

### aopw.js /
### abort-on-property-write.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L150)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to write specified _property_.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object that will be overwritten

Examples:
 - `yggtorrent.*##+js(aopw, Fingerprint2)`

***

### aeld.js /
### addEventListener-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L182)
Prevents attaching event listeners.

Parameters:
 - optional, string/_regular expression_, name of event listener
 - optional, string/_regular expression_ matching in stringified handler function

Examples:
 - `vev.io##+js(aeld, adb.updated)`
 - `newser.com##+js(aeld, load, Object)`
 - `vivo.sx##+js(aeld, , preventDefault)`
 - `vidto.me##+js(aeld, /^(?:click|mousedown|mousemove|touchstart|touchend|touchmove)$/, system.popunder)`

***

### aell.js /
### addEventListener-logger.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L221)
Logs to the console event listeners created on page.


***

### cookie-remover.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L942)
Removes current page cookies specified by name. For current domain, wildcard (dot) subdomain(s), current and `/` path, script accessible (HttpOnly=false), on load and before unload.

Caveats: cookies set for higher level domain will not be removed. For example, if current page domain is `www.example.com`, cookies set for `example.com` will not be removed.

Parameters:
 - optional, string/_regular expression_, matching in the name of the cookie

Examples:
 - `subdivx.com##+js(cookie-remover, ref_cookie)`


***

### ~csp.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1849)
Removed. Deprecated by `$csp` network filter option.  
Applies content security policy by inserting `<meta http-equiv=Content-Security-Policy content="*directive*">` tag to html `<head>` _element_.
Read more at https://www.w3.org/TR/CSP2/#delivery-html-meta-element  
[Content Security Policy Quick Reference Guide](https://content-security-policy.com/)

Parameters:
 - required, valid Content Security Policy directive


***

### disable-newtab-links.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L869)
Prevents creating new tabs/windows by deactivating links with `target` attribute.

Parameters:
 - none

Examples:
 - `there.to##+js(disable-newtab-links.js)`


***

### json-prune.js [↪](https://github.com/gorhill/uBlock/blob/b97fea09d20d014923b2741a01fa3f3f5555e230/assets/resources/scriptlets.js#L239)

New in [1.23.0](https://github.com/gorhill/uBlock/commit/2fd86a66fcc2665e5672cc5862e24b3782ee7504)

Intercepts calls to `JSON.parse`, and if the result of the parsing is an Object, it will remove specified properties from the result before returning to the caller.

Parameters:
 - optional, string, a list of space-separated properties to remove 
 - optional, string, a list of space-separated properties which must be all present for the pruning to occur

A property in a list of properties can be a chain of properties, example: `adpath.url.first`.

When used without parameters, will log current hostname + json payload to the console.

Examples:
 - `youthhealthmag.com##+js(json-prune, unit_list)`
 - `winfuture.de##+js(json-prune, adtagparameter, enabled)`


***

### noeval.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noeval.js)
Prevent web pages from using _`eval()`_, and report attempts to console.

Examples:
 - `solowarez.org##+js(noeval)`


***

### noeval-silent.js /
### ~silent-noeval.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noeval-silent.js)
Prevent web pages from using _`eval()`_.


***

### noeval-if.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L340)
Prevent web pages from using _`eval()`_ on specific matching payloads.

Parameters:
 - optional, string/_regular expression_, matching in payload string.

Examples:
 - `orgyxxxhub.com##+js(noeval-if, replace)`


***

### norafif.js /
### no-requestAnimationFrame-if.js [↪](https://github.com/gorhill/uBlock/blob/1de0e820b87fdd3717b9f2653baaa7a934075055/assets/resources/scriptlets.js#L522)

New in [1.26.1b12](https://github.com/gorhill/uBlock/commit/1de0e820b87fdd3717b9f2653baaa7a934075055).

**Defuses** calls to _`requestAnimationFrame()`_ function when parameter:
- **is not prefixed** with `!` and **matches** the stringified _callback_ argument to _`requestAnimationFrame()`_; OR
- **is prefixed** with `!` and  **does not match** the stringified _callback_ argument to _`requestAnimationFrame()`_.

Parameters:
 - optional, string/_regular expression_, matching in the stringified _callback_ argument passed to
requestAnimationFrame.

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`requestAnimationFrame()`_ to the console.

Examples:
 - `bloomberg.com##+js(norafif, paywall-inline-tout)`

***

### nosiif.js /
### no-setInterval-if.js [↪](https://github.com/gorhill/uBlock/blob/9367a6015b8cbb6b49347b00a105aab8f24df861/assets/resources/scriptlets.js#L585)

New in [1.22.3b](https://github.com/gorhill/uBlock/commit/9367a6015b8cbb6b49347b00a105aab8f24df861)

**Defuses** calls to _`setInterval()`_ function when parameters:
- **are not prefixed** with `!` and **match** the _`setInterval()`_ argument; OR
- **are prefixed** with `!` and **do not match** the _`setInterval()`_ argument.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching _interval_

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`setInterval()`_ to the console.

Examples:
 - `jpidols.tv##+js(nosiif)`
 - `finanzen.*##+js(nosiif, nrWrapper)`
 - `yachtrevue.at##+js(nosiif, text/css, 10)`


***

### nostif.js /
### no-setTimeout-if.js [↪](https://github.com/gorhill/uBlock/blob/9367a6015b8cbb6b49347b00a105aab8f24df861/assets/resources/scriptlets.js#L656)

New in [1.22.3b](https://github.com/gorhill/uBlock/commit/9367a6015b8cbb6b49347b00a105aab8f24df861)

**Defuses** calls to _`setTimeout()`_ function when parameters:
- **are not prefixed** with `!` and **match** the _`setTimeout()`_ argument; OR
- **are prefixed** with `!` and **do not match** the _`setTimeout()`_ argument.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching _delay_

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`setTimeout()`_ to the console.

<sub>Test page: https://gorhill.github.io/uBlock/tests/scriptlet-injection-filters-1.html</sub>

Examples:
 - `computerbild.de##+js(nostif, ())return)`
 - `lablue.*##+js(nostif, push, 500)`


***

### nowebrtc.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L721)
Disables WebRTC by preventing web pages from using [_`RTCPeerConnection()`_](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). Report attempts in console.

Examples:
 - `x1337x.*##+js(nowebrtc)`


***

### ra.js /
### remove-attr.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L362)
Removes attribute(s) from DOM tree node(s). Will run only once after page load.

Parameters:
 - required, attribute or list of attributes joined by `|`
 - optional, _CSS selector_, specifies nodes from which attributes will be removed

Examples:
 - `userscloud.com##+js(ra, onclick, .btn-icon-stacked)`
 - `magesy.*,majesy.*##+js(ra, oncontextmenu)`
 - `zerodot1.gitlab.io##+js(ra, oncontextmenu|onselectstart|ondragstart)`


***

### rc.js /
### remove-class.js [↪](https://github.com/gorhill/uBlock/blob/c2f0cae2cca2de785f326ae1c28dc1d61599bd7b/assets/resources/scriptlets.js#L461)

New in [1.25.3b5](https://github.com/gorhill/uBlock/commit/49d9929191461cc8534ebf5707d94a5970945bde).

Removes classes from DOM tree node(s). Will run only once after page load. Syntax based on [`remove-attr.js`](#remove-attrjs-)

Parameters:
 - required, class name or list of class names joined by `|`
 - optional, _CSS selector_, specifies nodes from which classes will be removed


***

### ~raf-if.js~ /
### ~requestAnimationFrame-if.js~ [↪](https://github.com/gorhill/uBlock/blob/c2f0cae2cca2de785f326ae1c28dc1d61599bd7b/assets/resources/scriptlets.js#L492)

Deprecated by [`no-requestAnimationFrame-if.js`](#no-requestanimationframe-ifjs-)

New in [1.22.0](https://github.com/gorhill/uBlock/commit/6831967f5f9d64412a9c063f3b64104d9dce7b07), `requestAnimationFrame-if.js` alias available in [1.22.1b2](https://github.com/gorhill/uBlock/commit/35854e4baf8b3b3aeb3f0f63ae9e7d3e46a4ba64)

**Defuses** calls to _`requestAnimationFrame()`_ function when parameter:
- **is not prefixed** with `!` and **does not match** the stringified _callback_ argument to _`requestAnimationFrame()`_; OR
- **is prefixed** with `!` and **matches** the stringified _callback_ argument to _`requestAnimationFrame()`_.

Parameters:
 - optional, string/_regular expression_, matching in the stringified _callback_ argument passed to
requestAnimationFrame.

Use with `!` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`requestAnimationFrame()`_ to the console.

Examples:
 - `bloomberg.com##+js(raf-if, !paywall-inline-tout)`


***

### set.js /
### set-constant.js [↪](https://github.com/gorhill/uBlock/blob/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce/assets/resources/scriptlets.js#L478)
Creates _property_ and initializes it to predefined value from set of available properties.

Scriptlet will succeed only when:
 - original _property_ is `undefined` (scriptlet is called early enough) or `null`<sup>[1.24.3b9](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **OR**
 - new _property_ written by `set.js` is `undefined` or `null`<sup>[1.24.3b9](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **OR**
 - type of original _property_ is equal to type of new _property_

Additionally, original _property_ (if exist) must not have getter.

Value set by scriptlet can be overwritten by page script when:
 - current _property_ was not set to `undefined` or `null`<sup>[1.24.3b9](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **AND**
 - new _property_ is not `undefined` or `null`<sup>[1.24.3b9](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **AND**
 - type of original _property_ is different than type of new _property_ 

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

Examples:
 - `kompetent.de##+js(set, Object.keys, trueFunc)`
 - `t-online.de##+js(set, abp, false)`
 - `identi.li##+js(set, t_spoiler, 0)`


***

### ~sid.js~ /
### ~setInterval-defuser.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L474)

Deprecated by [`no-setInterval-if.js`](#no-setinterval-ifjs-)

Defuses calls to _`setInterval()`_ function for specified matching callbacks and intervals by setting callback function to noop.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching interval


***

### ~sil.js~ /
### ~setInterval-logger.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L500)

Deprecated by [`no-setInterval-if.js`](#no-setinterval-ifjs-)

Removed in [1.22.0](https://github.com/gorhill/uBlock/commit/c5536577b29cd0bcd401f7ecd143a921acdb4eb6).

Logs to the console calls to _`setInterval()`_ function.


***

### ~std.js~ /
### ~setTimeout-defuser.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L515)

Deprecated by [`no-setTimeout-if.js`](#no-settimeout-ifjs-)

Defuses calls to _`setTimeout()`_ function for specified matching callbacks and delays by setting callback function to noop.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching _delay_


***

### ~stl.js~ /
### ~setTimeout-logger.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L541)

Deprecated by [`no-setTimeout-if.js`](#no-settimeout-ifjs-)

Removed in [1.22.0](https://github.com/gorhill/uBlock/commit/c5536577b29cd0bcd401f7ecd143a921acdb4eb6).

Logs to the console calls to _`setTimeout()`_ function.


***

### nano-sib.js /
### nano-setInterval-booster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L239)
Adjusts interval for specified _`setInterval()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching interval
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, interval multiplier

Examples:
 - `identi.li##+js(nano-sib, , ,0.02)`
 - `platinmods.*##+js(nano-sib)`
 - `1ink.cc##+js(nano-sib, mSec, 1050)`


***

### nano-stb.js /
### nano-setTimeout-booster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L289)
Adjusts delay for specified _`setTimeout()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching delay
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, delay multiplier

Examples:
 - `bdupload.*##+js(nano-stb)`
 - `imgrock.*##+js(nano-stb, /.?/, 4000)`


***

### ~sharedWorker-defuser.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1822)
Removed. Deprecated by `$csp` filter option.  
Defuses sharedWorker by passing empty worker file (Blob URL) for specified worker URLs

Parameters:
 - optional, string/_regular expression_, matching in worker URL


***

### webrtc-if.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L556)
Allows opening RTC connections to matching [RTCIceServer](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceServer) only.

Parameters:
 - required, string/_regular expression_, matching in `RTCIceServer` `urls`, `username` or `credential`.

***

### window.open-defuser.js [↪](https://github.com/gorhill/uBlock/blob/b27848a060eee961e2403192097448467b3bc7b5/src/web_accessible_resources/window.open-defuser.js)
Prevent opening new windows by [_`window.open()`_](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) when URL positively or negatively matches to specific string.

Improved in [1.25.3b1](https://github.com/gorhill/uBlock/commit/b27848a060eee961e2403192097448467b3bc7b5):

If second argument is present and a valid integer value, the defuser will return a valid window object even though no popup window is opened. The returned window object will cease to be valid after the specified number of seconds. If not present, no window will be opened and the scriptlet will return `null`.

Parameters:
 - optional, string/_regular expression_, prefixed by `!` for negation, matching in URL parameter passed to _`window.open()`_,
 - optional, positive decimal integer, number of seconds after returned `window` object will be invalidated.

Parameters syntax deprecated after 1.25.3b1:
 - optional - defaults to "matching", nothing or `1` for "matching", `0` for "not matching",
 - optional, string/_regular expression_, matching/not matching in URL parameter passed to _`window.open()`_

Examples:
 - `file-up.org##+js(window.open-defuser)`


***

### window.name-defuser [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L624)
Clears `window.name` _property_ which can be misused for tracking purposes.

Parameters:
 - none


***

### overlay-buster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L633)
Experimental, gets rid of overlay dialogs, works for ~30s after page load. Preferred way to handle overlays is to use standard cosmetic filters and optionally [style injection](./Static-filter-syntax#style).


***

### alert-buster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L691)
Disables [_`alert()`_](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) dialog boxes by redirecting messages to console.


***

## Defuser scriptlets



### ampproject_v0.js /
### ~ampproject.org/v0.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/ampproject_v0.js)
Removes animation (artificial 8s delay) added to desktop pages supporting AMP, when ampproject.org scripts are blocked.

### fingerprint2.js  [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L929)
Defuses Fingerprintjs2. Sanitize `Fingerprint2` object.

### nobab.js /
### ~bab-defuser.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/nobab.js)
Defuses BlockAdblock. Prevents executing of _`eval()`_ on sets of predefined payloads.

### nofab.js /
### ~fuckadblock.js-3.2.0~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/nofab.js)
Convenience, Sanitize `FuckAdBlock`, `BlockAdBlock`, `SniffAdBlock`, `fuckAdBlock`, `blockAdBlock`, `sniffAdBlock` properties.
Often used as redirect in network filters. TODO: copy to redirect?

### popads-dummy.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/popads-dummy.js)
Convenience, sets static properties (`PopAds`, `popns`)

### popads.js /
### ~popads.net.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/popads.js)
Convenience, abort-on-property-write.js (`PopAds`, `popns`), _throws_ "`magic`"

### gpt-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L700)
Deprecated, Convenience, sets static properties (`_resetGPT`, `resetGPT`, `resetAndLoadGPTRecovery`, `_resetAndLoadGPTRecovery`, `setupGPT`, `setupGPTuo`)

### adfly-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L805)
Defuses anti adblock on adfly shortened links.

### damoh-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L886)
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
	- ~1x1-transparent.gif~ 1x1.gif `image/gif;base64` `$image` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/1x1.gif)
	- ~2x2-transparent.png~ 2x2.png `image/png;base64` `$image` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/2x2.png)
	- ~3x2-transparent.png~ 3x2.png `image/png;base64` `$image` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/3x2.png)
	- ~32x32-transparent.png~ 32x32.png `image/png;base64` `$image` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/32x32.png)
 - Source code
	- ~noopframe~ noop.html `text/html` `$subdocument` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.html)
	- ~noopjs~ noop.js `application/javascript` `$script` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.js)
	- ~nooptext~ noop.txt `text/plain` `$xmlhttprequest` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.txt)
 - Media files
	- ~noopmp3-0.1s~ noop-0.1s.mp3 `audio/mp3;base64` `$media` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop-0.1s.mp3)
	- ~noopmp4-1s~ noop-1s.mp4 `video/mp4;base64` `$media` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop-1s.mp4)

Example rule:

`||ad.server.com/$script,redirect=noop.js,domain=www.google.com`

TODO: object and font resources are missing? Find discussion about adding them on demand.


***

## URL-specific sanitized redirect resources (surrogates)



### addthis_widget.js /
### ~addthis.com/addthis_widget.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/addthis_widget.js)

### amazon_ads.js /
### ~amazon-adsystem.com/aax2/amzn_ads.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/amazon_ads.js)

### monkeybroker.js /
### ~d3pkae9owd2lcf.cloudfront.net/mb105.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/monkeybroker.js)

### doubleclick_instream_ad_status.js /
### ~doubleclick.net/instream/ad_status.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/doubleclick_instream_ad_status.js)

### google-analytics_ga.js /
### ~google-analytics.com/ga.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_ga.js)

### google-analytics_analytics.js /
### ~google-analytics.com/analytics.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_analytics.js)

### google-analytics_inpage_linkid.js /
### ~google-analytics.com/inpage_linkid.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_inpage_linkid.js)

### google-analytics_cx_api.js /
### ~google-analytics.com/cx/api.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_cx_api.js)

### googletagservices_gpt.js /
### ~googletagservices.com/gpt.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googletagservices_gpt.js)

### googletagmanager_gtm.js /
### ~googletagmanager.com/gtm.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googletagmanager_gtm.js)

### googlesyndication_adsbygoogle.js /
### ~googlesyndication.com/adsbygoogle.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googlesyndication_adsbygoogle.js)

### scorecardresearch_beacon.js /
### ~scorecardresearch.com/beacon.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/scorecardresearch_beacon.js)

### outbrain-widget.js /
### ~widgets.outbrain.com/outbrain.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/outbrain-widget.js)

### hd-main.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/hd-main.js)

### disqus_forums_embed.js AND disqus_embed.js /
### ~disqus.com/forums/*/embed.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/disqus_forums_embed.js) AND ~disqus.com/embed.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/disqus_embed.js)
Along with [Disqus click-to-load](https://gist.github.com/gorhill/ef1b62d606473c68d524) filter list, allows to have Click-to-unblock experience for Discus comments widgets.

### twitch-videoad.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L913)
Twitch stream embedded ads bypasser


***

## Other
Deprecated by general purpose scriptlets / outdated (please move to proper section if still used).

***

### golem.de.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L756)
Deprecated, addEventListener-defuser

***

### upmanager-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L777)
Deprecated, sets static properties (`upManager`)

### chartbeat.js /
### ~static.chartbeat.com/chartbeat.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/chartbeat.js)
Deprecated, sets static properties (`pSUPERFLY.activity`, `pSUPERFLY.virtualPage`)

### ligatus_angular-tag.js /
### ~ligatus.com/*/angular-tag.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/ligatus_angular-tag.js)
Deprecated, sets static properties (`adProtect`, `uabpdl`, `uabDetect`)


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
 - CSS selector:       https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
