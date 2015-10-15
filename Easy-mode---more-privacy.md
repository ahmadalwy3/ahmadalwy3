[Back to _Blocking mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode)

***

_Ubiquitous sites_ are those 3rd parties which resources are embedded in countless web pages. Your privacy exposure is sharply increased by such _ubiquitous sites_.

An obvious example is Facebook: the Facebook widgets to _like_ something are embedded in countless web pages, and as such these widgets serve as excellent tracking devices for Facebook to build a profile of your browsing history. This is also true for other entity such as Twitter, Google, Disqus, etc.

> ***
> Recommended reading: [_Internet Companies: Confusing Consumers for Profit_](https://www.eff.org/deeplinks/2015/10/internet-companies-confusing-consumers-profit) (EFF)
> ***

uBlock Origin's [_dynamic filtering_](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering) can help you foil the ability of ubiquitous servers from building a profile of your browsing habits. Will use Facebook as an example.

First, we block Facebook-related hostnames globally, such that network requests to Facebook servers are blocked _by default_:

![Block `facebook.net` everywhere](https://cloud.githubusercontent.com/assets/585534/10513149/aa42ac9e-7313-11e5-8b71-42383b58fcd4.png)

All suggested global `block` rules for Facebook:

    * facebook.net * block
    * facebook.com * block
    * fbcdn.net * block

These rules will cause Facebook to be blocked everywhere by default, _even_ when visiting Facebook's own site. This is what foils the ability of Facebook to see gather your data about your browsing habits.

Blocking Facebook when visiting Facebook is not ideal though, and there is no real benefit for doing so. Thus we will create an exception to the above global rules, but just for when we visit Facebook's own site:

![Do not block `facebook.com` while visiting Facebook](https://cloud.githubusercontent.com/assets/585534/10513464/b3e0f09c-7315-11e5-8e0b-90d3cc8614f7.png)

All suggested global `noop` rules for Facebook.

    facebook.com facebook.com * noop
    facebook.com facebook.net * noop
    facebook.com fbcdn.net * noop

This is just an example, the same can be applied to any of the ubiquitous servers out there. The dynamic filtering pane in uBlock Origin's popup UI will keep you informed about all the 3rd-party servers a web page connects (or tries to), and from there one can simply point-and-click to create global/local block/allow rules to foil the ability of 3rd parties to record your browsing history.

`block` rules to ubiquitous web sites will easily reduce _significantly_ your privacy exposure.