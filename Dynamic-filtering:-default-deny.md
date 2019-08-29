[Back to _Dynamic filtering_](./Dynamic-filtering)

***

Default-deny is an awesome blocking mode for whoever agrees that in general most 3rd-party resources from web pages:

- are not really _all_ required
- increase privacy exposure

Strictly speaking, default-deny means to block everything and let the user choose what should not be blocked. This strictest mode of default-deny is impractical though, as this means that most web pages would be broken, and more than likely most users would not make use if it.

With uBlock it is possible to use more relax (and thus practical) versions of default-deny: _default-deny 3rd-party_ resources (stricter), or _default-deny 3rd-party scripts/frames_ (more relax).

_default-deny 3rd-party_ will result in more remote resources being blocked, as anything which is 3rd-party to the current site will be blocked by default. This means a higher likelihood that web pages won't render or behave properly:

![Block anything which is 3rd-party](https://cloud.githubusercontent.com/assets/585534/8889495/c0694db0-32aa-11e5-9c1d-919e89d80c4b.png)<br><sup>Default-deny anything 3rd-party: more likely to break, this will need fixing by the user.</sup>

A more friendly approach is to use default-deny only for 3rd-party scripts/frames. In such case the likelihood of page breakage is much lower than when blocking anything which is 3rd-party, and yet most of the benefits are still felt:

![Block only 3rd-party scripts/frames](https://cloud.githubusercontent.com/assets/585534/8889496/c573989c-32aa-11e5-9a40-297ef60a58d0.png)<br><sup>Default-deny 3rd-party scripts/frames: less breakage, yet most 3rd-party resources are blocked as seen in the picture.</sup>

The 3rd-party status of a network request is determined as follow: if the domain of a network request does not match the domain of the web page from which it originates, the network request is deemed 3rd-party. The domain information is extracted as per the official [Public Suffix List](https://publicsuffix.org/).

The benefits of using default-deny are plenty:

- Faster page load
- Reduction of bandwidth consumption
- Reduction of privacy exposure
- Increase browser security
- Easier on your browser's memory and CPU footprint

The advantages do not come for free. Often, default-deny will require a bit of work the first time you visit a web site. Using [The Guardian](http://www.theguardian.com/) as our current example:

![Default-deny](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-dd-03.png)

As seen in the picture above, a few 3rd-party domains related to `theguardian.com` had to be un-blocked for the page to display and behave properly. Notice that `noop` rules (dark gray) were used to un-block the domains.

A `noop` rule is different than an `allow` rule (green): an `allow` rule will cause all block filters from static filtering to be bypassed, while a `noop` rule will just disengage dynamic filtering and keep static filtering engaged.

~~Keep in mind that all rules are permanent as soon as they are set (or unset).~~ As of v0.8.8.0, you need to click the padlock to save your rules: all rules are now temporary by default. This allows users to fiddle with rules without worries about polluting their good ruleset. When you want to keep rules for a specific site, click the padlock. The padlock appears if and only if there is at least one temporary rules in the pane.

You can disengage default-deny for the current site with one click: set the "3rd-party" local setting to `noop` if you prefer to work this way:

![Default-deny](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-dd-02.png)<br>
<sup>Default-deny cancelled locally. Notice that the blocking of 3rd-party frames is still in effect: cells with higher precedence won't have their rules overriden by cells with lower precedence.</sup>

This results in default-deny being disengaged for the current site ([The Guardian](http://www.theguardian.com/) in our example), **while** keeping engaged static filtering (_EasyList_, _EasyPrivacy_, etc.). In this particular example, as can be seen in the picture, 3rd-party frames will still be blocked (usually a [good thing privacy- and security-wise](./Dynamic-filtering:-Benefits-of-blocking-3rd-party-iframe-tags)).

***

This is an important aspect of  uBlock's dynamic filtering compared to [uMatrix](https://github.com/gorhill/uMatrix), [RequestPolicy](https://addons.mozilla.org/en-us/firefox/addon/requestpolicy/), [Policeman](https://addons.mozilla.org/en-us/firefox/addon/policeman/): in uBlock, rules are ternary, not binary.

***
> working on it.. topic to cover:
> 
> no need to use malware domain lists since all 3rd-parties are blocked by default = leaner uBlock
>
> ubiquitous servers blocked by default, i.e. no need to pre-emptively block facebook, google, twitter, linkdin, etc. to prevent tracking by these
>
> provide many real-life examples of how easy it is to un-break websites
