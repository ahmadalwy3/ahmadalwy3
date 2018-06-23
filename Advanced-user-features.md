Advanced user mode can be [enabled from the _Settings_ tab](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#i-am-an-advanced-user) in uBlock Origin's ("uBO") dashboard. **Enable at your own risk.**

## Read the docs
<table><tr><td width="130" align="center">
<img src="http://i.imgur.com/3kJFgHX.jpg" float="right" width="96" height="96">
</td><td>
<p><b>Advanced users are expected to read the documentation. This is very important.</b></p>

<p>If you use advanced features without fully understanding them, uBlock Origin:</p>

<ul>
<li>might</li>
<li><i>probably <b>will</b></i>
</ul>
.. behave in ways unexpected to you.
</td></tr></table>

## Differences

### Advanced settings

You will be given the ability to access the [advanced settings](https://github.com/gorhill/uBlock/wiki/Advanced-settings). Some of these settings are experimental, they may become standard settings or disappear in the future.

***

### Dynamic filtering

[Dynamic filtering](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering) will become available to advanced users.

Novice users could easily mess up uBO's filtering through dynamic filtering, thus it is not available by default.

On the other hand, if you are familiar with [RequestPolicy](https://www.requestpolicy.com/), then you should have no problem dealing with dynamic filtering.

**Important note:** Dynamic filtering engine is completely turned off when you un-check the setting _"I am an advanced user"_. Your dynamic filtering rules are kept intact though, in case you re-enable _advanced user_ mode again.

***

### Ability to filter behind-the-scene network requests

See ["Behind-the-scene network requests"](https://github.com/gorhill/uBlock/wiki/Behind-the-scene-network-requests).