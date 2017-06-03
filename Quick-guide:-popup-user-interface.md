[Back to Wiki home](https://github.com/gorhill/uBlock/wiki)

***

- [The title bar](#the-title-bar)
- [The large power button](#the-large-power-button)
- [The number of requests blocked](#the-number-of-requests-blocked)
- [The tools](#the-tools)
- [The number of domains connected](#the-number-of-domains-connected)
- [The per-site switches](#the-per-site-switches)

***

This is uBlock's popup UI when you click on uBlock's icon in the toolbar:

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26748913/b0de57b8-47d0-11e7-8d8a-f862bf5aa84f.png)

***

#### The title bar

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26748961/439dd57e-47d1-11e7-8579-1e5c008ee938.png)

Click the title bar of the popup to go to uBlock's dashboard.

***

#### The large power button

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26748994/858a70aa-47d1-11e7-9e2c-409b83de99b9.png)

Click the large power button to turn off uBlock **for the current site** (a.k.a. _whitelist_ the current site). This will be remembered the next time you visit the site.

Alternatively, you can also <kbd>Ctrl</kbd>-click to turn off uBlock only for the current page (<kbd>command ⌘</kbd>-click on Mac).

For more advanced whitelisting control, see ["How to whitelist a web site"](https://github.com/gorhill/uBlock/wiki/How-to-whitelist-a-web-site).

***

#### The tools

![a](https://cloud.githubusercontent.com/assets/585534/26748901/97dc024c-47d0-11e7-89d0-63fd5a092b02.png)

#### Zap an element on the current page

Click the _flash_ icon to enter [element zapper mode](https://github.com/gorhill/uBlock/wiki/Element-zapper), which allows you to interactively remove one or more elements on the current page. Removing an element is always temporary, i.e. the removed elements will be back when the page is reloaded.

#### Create a filter for the current site

Click the _eye-dropper_ icon to enter [element picker mode](https://github.com/gorhill/uBlock/wiki/Element-picker), which allows you to create a filter by interactively picking an element on a page, thus permanently removing it from the page.

#### Open the logger

Click the _list_ icon to open the [logger](https://github.com/gorhill/uBlock/wiki/The-logger) in a separate tab. This allows you to inspect real-time network traffic within the browser.

Tip: press the <kbd>Shift</kbd> key while clicking the icon to toggle between opening the logger in a separate window or separate tab. uBO will remember that setting when you open the logger without the <kbd>Shift</kbd> key.

***

#### The number of requests blocked

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26749010/ba071586-47d1-11e7-8bc6-74bce249d497.png)

This shows the number of network requests uBlock blocked on the current page. Also, less useful (but people like this kind of thing), the number of network requests uBlock blocked since you installed it. The percentage figure tells you how many requests were blocked out of all the requests made.

***

#### The number of domains connected

![Popup UI](https://cloud.githubusercontent.com/assets/585534/26749020/da09c446-47d1-11e7-9d49-e46634058915.png)

The number of **distinct** domains with which a network connection was established, out of all connections (established + blocked). The domains are derived using the official [Public Suffix List](https://publicsuffix.org/).

In general, it must be assumed that each distinct domain is managed by a distinct administrative authority. In practice, it is not uncommon to have a multiple distinct domains which are under the same administrative authority (example 1: `google.com`, `ajax.googleapis.com` and `gstatic.com`, example 2: `wikipedia.org` and `wikimedia.org`).

That said, this statistic may be seen this way: the more distinct domains your browser connects to, the greater the privacy exposure.

In a best-case scenario, the number of distinct domains to which a web page connects should be **only one**:  that of the remote server from which the web page was fetched.

**The higher the number, the higher you are exposing yourself privacy-wise.**

There is a good correlation between the _domains connected_ count and: unneeded page bloat, high privacy exposure, increased likelihood of being the target of data mining.

Example: the web page on <http://www.ibtimes.com/> (which can be read fine in all cases, by the way):

 uBlock's mode | turned off | default settings | [default-deny](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering)
--- | --- | --- | ---
domains connected | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1e.png) | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1d.png) | ![](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1f.png)
privacy exposure | very high | medium | very low
bloat | ridiculously high | medium | very low

And I had click-to-play enabled in all cases, so it could have been worse (except for default-deny)...

***

#### The per-site switches

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1g.png)

The per-site switches allow you to control some settings on a per-site basis. See [detailed documentation about per-site switches](https://github.com/gorhill/uBlock/wiki/Per-site-switches).