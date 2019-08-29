[Back to _Dynamic-filtering_](./Dynamic-filtering)

***

Dynamic filtering pane ([available only to advanced users](./Advanced-user-features)) can be toggled by clicking on `requests blocked` or `domains connected`:

![figure 1](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-01.png)

> ***
> **Important:** _Static filtering_ refers to the filters which comes from the filter lists, i.e. _EasyList_, _EasyPrivacy_, hpHosts, etc. _Dynamic filtering_ are those filtering rules which have an air of firewall rules. 
> ***

**First column**: what is to be dynamically filtered:

![figure 2](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-02.png)

As you can see, you can create dynamic filtering rules for resource types, or hostnames according to their origin.

The color of an entry indicates whether all requests were blocked (reddish), all requests were allowed (greenish), or some were blocked some were allowed (yellowish).

In bold, domain names. Domain names are hostnames, but hostnames are not necessarily domain names from uBlock's point of view: domain names are extracted as per [Mozilla Public Suffix list](https://publicsuffix.org/).

**Second column**: **_global_** dynamic filtering rules, i.e. whatever rule appears in this column applies everywhere, on _all_ sites:

![figure 3](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-03.png)

**Third column**: **_local_** dynamic filtering rules, i.e. whatever rule appears in this column applies to the _current_ site only:

![figure 4](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-04.png)

The cells in the third column gives an overview of how many requests were blocked/allowed:

- `-` or `+` = between 1-9 network requests were blocked or allowed, respectively
- `--` or `++` = between 10-99 network requests were blocked or allowed, respectively
- `---` or `+++` = 100 or more network requests were blocked or allowed, respectively
- blank cell = no network requests occurred for the specific hostname

So there are **global** dynamic filtering rules, and **local** dynamic filtering rules.

By default, there are no dynamic filtering rules at install time, so nothing is blocked by default by the dynamic filtering engine. You will have to create your own rules, according to your own prerogatives.

Sensible security- and privacy-wise: blocking all 3rd-party frames by default everywhere: 

![figure 5](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-05.png)

> ***
> **Important:** _Dynamic filtering_ overrides _static filtering_.
> 
> This means a _block_ dynamic rule will override any existing _allow_ static filters. This means you can block with 100% certainty using dynamic filtering rules. Similarly, an _allow_ dynamic filtering rule will override any existing _block_ static filters, i.e. you can allow with 100% certainty with dynamic filtering (useful to un-break sites broken by some static filters).
> 
> This may help understand how static and dynamic filtering interact: [Overview of uBlock's network filtering engine](./Overview-of-uBlock's-network-filtering-engine).
> ***

All embedded 3rd-party frames were blocked on the page. Good. However it appears there was an embedded YouTube video in the article:

![figure 6](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-06.png)

If you want to block all 3rd-party frames by default, except for embedded YouTube videos on that particular site, two solutions.

##### First solution

Create a local  _noop_ rule for 3rd-party frames:

![figure 7](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-07.png)

It works, the embedded YouTube video can now be played.

Note that a cell with a _noop_ rule is dark gray, while a cell with no rule at all is light gray (the default color). Hence gray means that no dynamic filtering will be applied to a cell. If a cell inherit a _block_ or _allow_ rule from a higher precedence cell, a _noop_ rule can be used to override the inherited _block_ or _allow_ rule. Conceptually, the purpose of _noop_ rules is to punch holes in your dynamic filtering ruleset so that network requests can pass through unimpeded.

However the above rule would result in all 3rd-party frames on the site to be unblocked. Not so good.

##### Second solution

Create a local _noop_ rule for `youtube.com`:

![figure 8](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-08.png)

This will prevent dynamic filtering rules to apply to anything from `youtube.com`, but only on that site.

> ***
> **Important:** Remember that _noop_ rules bypass **only** broader dynamic filtering rules, static filtering is left completely intact, which means you won't see ads in the embedded YouTube videos.
> ***

What if you want to block 3rd-party frames everywhere by default, but want whatever embedded YouTube video to not be blocked by default on any site?

It is just a matter of creating a global _noop_ rule for `youtube.com`:

![figure 9](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-09.png)

Which means: do not apply any dynamically filtering rule to `youtube.com` by default (i.e. everywhere).

> ***
> **Important:**  _Local_ dynamic filtering rules override _global_ ones.
> 
> In other words: **More specific dynamic filtering rules override less specific ones.** For example, dynamic filtering rules for `youtube.com` (specific) override dynamic filtering rules for `3rd-party frames` (generic).
> ***

All dynamic rules are temporary by default: Click the padlock if you want to persist the ruleset for a specific web site.

![figure 12](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-12.png)

- The padlock will be visible **if and only if** there is at least one temporary rule in the pane
- This is really the optimal way to use dynamic filtering, as using this feature is often a matter of trial and error
- This prevents ruleset pollution: your ruleset will be only those rules which you will have explicitly persisted
- If you <kbd>Ctrl</kbd>-click to set/unset a rule, it will be immediately persisted (<kbd>command ⌘</kbd>-click on Mac)

***

We covered the _block_ and _noop_ dynamic filtering rules. What about the _allow_ rule?

The dynamic filtering _allow_ rule is most useful to un-break sites broken by some static filters.

[Someone found out](https://twitter.com/r3volution11/status/549584186320117760) Boldchat site was broken when using uBlock:

![figure 10](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-10.png)

The content of the dynamic filtering pane makes it clear that there is a static filter somewhere blocking network requests to `boldchat.com`. Turned out there was static filter `boldchat.com` in _"Peter Lowe's Ad Server"_ list.

Using a local  _allow_ dynamic filtering rule fixes the breakage:

![figure 11](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-11.png)

It is easier for a user to point-and-click for a quick fix than to actually craft an exception static filter like `@@||boldchat.com$~third-party` and force a reload of all static filters (big memory churning).

<sup>[Another example](https://www.youtube.com/watch?v=8bzB6tESynM) of un-breaking a site.</sup>

> ***
> **Important:** Typically, use only narrow _allow_ dynamic filtering rules to un-break sites. As these _allow_ rules override any static filtering, this means if you use a too broad _allow_ dynamic filtering rule you could start to allow in ads/trackers/annoyances.
> ***

More: [Take control of your privacy in your own hands](https://github.com/chrisaljoudi/uBlock/issues/433#issuecomment-68488686) (will move this here eventually, I need a break)
