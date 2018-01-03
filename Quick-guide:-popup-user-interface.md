[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

- [The title bar](#the-title-bar)
- [The large power button](#the-large-power-button)
- [The number of requests blocked](#the-number-of-requests-blocked)
- [The tools](#the-tools)
- [The number of domains connected](#the-number-of-domains-connected)
- [The overview panel](#the-overview-panel)
- [The per-site switches](#the-per-site-switches)

***

This is uBlock's popup UI when you click on uBlock's icon in the toolbar:

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26748913/b0de57b8-47d0-11e7-8d8a-f862bf5aa84f.png)

***

### The large power button

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26748994/858a70aa-47d1-11e7-9e2c-409b83de99b9.png)

Click the large power button to turn off uBlock **for the current site** (a.k.a. _whitelist_ the current site). This will be remembered the next time you visit the site.

Alternatively, you can also <kbd>Ctrl</kbd>-click to turn off uBlock only for the current page (<kbd>command ⌘</kbd>-click on Mac).

For more advanced whitelisting control, see ["How to whitelist a web site"](https://github.com/gorhill/uBlock/wiki/How-to-whitelist-a-web-site).

***

### The tools

![a](https://cloud.githubusercontent.com/assets/585534/26748901/97dc024c-47d0-11e7-89d0-63fd5a092b02.png)

#### Zap an element on the current page

Click the _flash_ icon to enter [element zapper mode](https://github.com/gorhill/uBlock/wiki/Element-zapper), which allows you to interactively remove one or more elements on the current page. Removing an element is always temporary, i.e. the removed elements will be back when the page is reloaded.

#### Create a filter for the current site

Click the _eye-dropper_ icon to enter [element picker mode](https://github.com/gorhill/uBlock/wiki/Element-picker), which allows you to create a filter by interactively picking an element on a page, thus permanently removing it from the page.

#### Open the logger

Click the _list_ icon to open the [logger](https://github.com/gorhill/uBlock/wiki/The-logger) in a separate tab. This allows you to inspect real-time network traffic within the browser.

Tip: press the <kbd>Shift</kbd> key while clicking the icon to toggle between opening the logger in a separate window or separate tab. uBO will remember that setting when you open the logger without the <kbd>Shift</kbd> key.

#### Open the dashboard

Click the _cogs_ icon to open uBlock's dashboard.

***

### The number of requests blocked

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26749010/ba071586-47d1-11e7-8bc6-74bce249d497.png)

This shows the number of network requests uBlock blocked on the current page. Also, less useful (but people like this kind of thing), the number of network requests uBlock blocked since you installed it. The percentage figure tells you how many requests were blocked out of all the requests made.

***

### The number of domains connected

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26749020/da09c446-47d1-11e7-9d49-e46634058915.png)

The number of **distinct** domains with which a network connection was established, out of all connections (established + blocked). The domains are derived using the official [Public Suffix List](https://publicsuffix.org/).

In general, it must be assumed that each distinct domain is managed by a distinct administrative authority. In practice, it is not uncommon to have a multiple distinct domains which are under the same administrative authority (example 1: `google.com`, `ajax.googleapis.com` and `gstatic.com`, example 2: `wikipedia.org` and `wikimedia.org`).

That said, this statistic may be seen this way: the more distinct domains your browser connects to, the greater the privacy exposure.

In a best-case scenario, the number of distinct domains to which a web page connects should be **only one**:  that of the remote server from which the web page was fetched.

**The higher the number, the higher you are exposing yourself privacy-wise.**

There is a good correlation between the _domains connected_ count and: unneeded page bloat, high privacy exposure, increased likelihood of being the target of data mining.

Example: the web page on <http://www.ibtimes.com/> (which can be read fine in all cases, by the way):

 uBlock's mode | turned off | default settings | [default-deny](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode)
--- | --- | --- | ---
domains connected | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1e.png) | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1d.png) | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1f.png)
privacy exposure | very high | medium | very low
bloat | ridiculously high | medium | very low

And I had click-to-play enabled in all cases, so it could have been worse (except for default-deny)...

***

### The overview panel

When you click on either the _"requests blocked"_ or _"domains connected"_ label, uBO's popup UI will expand to show you more details about requests blocked and domains connected:

![a](https://user-images.githubusercontent.com/585534/34523870-48cb57b2-f067-11e7-9069-5b83f9a8f9e3.png)

The pluses and minuses denote network requests which were either allowed (not blocked) or blocked, respectively for the specific domain/hostname on which they appear. The number of pluses and minuses are proportional to the number of requests allowed or blocked:
- `+`, `-`: under 10 network requests were allowed, blocked.
- `++`, `--`: under 100 network requests were allowed, blocked.
- `+++`, `---`: 100 or more network requests were allowed, blocked.

To hide that panel, just click again on either the _"requests blocked"_ or _"domains connected"_ label.

Unless you are in "advanced user", this panel is read-only and available only for informational purpose.

In ["advanced user"](https://github.com/gorhill/uBlock/wiki/Advanced-user-features) mode, the panel is fully interactive and can be used for advanced filtering control.

***

### The per-site switches

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1g.png)

The per-site switches allow you to control some settings on a per-site basis. See [detailed documentation about per-site switches](https://github.com/gorhill/uBlock/wiki/Per-site-switches).