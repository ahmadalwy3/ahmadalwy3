[Back to _Blocking mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode)

***

_Ubiquitous sites_ are those 3rd parties which resources are embedded in countless web pages. Your privacy exposure is sharply increased by such _ubiquitous sites_.

An obvious example is Facebook: the Facebook widgets to _like_ something are embedded in countless web pages, and as such these widgets serve as excellent tracking devices for Facebook to build a profile of your browsing history.

![b](https://user-images.githubusercontent.com/585534/37596582-07533d5a-2b53-11e8-8690-0883e831349d.png)

This is also true for other entity such as Twitter, Google, Disqus, etc.

> ***
> Recommended reading: [_Internet Companies: Confusing Consumers for Profit_](https://www.eff.org/deeplinks/2015/10/internet-companies-confusing-consumers-profit) (EFF)
> ***

uBlock Origin's [_dynamic filtering_](https://github.com/gorhill/uBlock/wiki/Dynamic-filtering) can help you foil the ability of ubiquitous servers from building a profile of your browsing habits.

Will use Facebook as an example. Facebook will still have the ability to track your browsing habits when using uBlock Origin with its default settings [see benchmark's raw data for [_Easy Mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode): notice in the [list of 3rd parties](https://github.com/gorhill/uBlock/wiki/Blocking-mode#easy-mode) how `facebook.net` is ubiquitous].

First, we block Facebook-related hostnames globally, such that network requests to Facebook servers are blocked _by default, everywhere_:

![Block `facebook.net` everywhere](https://user-images.githubusercontent.com/585534/37596805-b94d377c-2b53-11e8-8bd9-a846f7c399d1.png)

All suggested global `block` rules for Facebook:<sup>[1]</sup>

    * facebook.net * block
    * facebook.com * block
    * fbcdn.net * block

These rules will cause Facebook to be blocked everywhere by default, _even_ when visiting Facebook's own site. This is what foils the ability of Facebook to gather data about your browsing habits.

Blocking Facebook when visiting Facebook is not ideal though, and there is no real benefit for doing so. Thus we will create an exception to the above global rules, but just for when we visit Facebook's own site:

![Do not block `facebook.com` while visiting Facebook](https://cloud.githubusercontent.com/assets/585534/10513464/b3e0f09c-7315-11e5-8e0b-90d3cc8614f7.png)

All suggested global `noop` rules for Facebook.<sup>[1]</sup>

    facebook.com facebook.com * noop
    facebook.com facebook.net * noop
    facebook.com fbcdn.net * noop

The same sort of dynamic filtering rules can be used for whatever sites for which you still would want Facebook widgets to work:

    example.com facebook.com * noop
    example.com facebook.net * noop
    example.com fbcdn.net * noop

This is just an example, the same can be applied to any of the ubiquitous servers out there. The dynamic filtering pane in uBlock Origin's popup UI will keep you informed about all the 3rd-party servers a web page connects (or tries to), and from there one can simply point-and-click to create global/local block/noop rules to foil the ability of 3rd parties to record your browsing history.

`block` rules to ubiquitous web sites will easily reduce _significantly_ your privacy exposure.

Using the above example of blocking Facebook everywhere with the [benchmark result for _Easy mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode#easy-mode) (uBlock Origin's default mode), the count of 3rd parties would have been decreased from 512 to 
437, an easy way to significantly reduce your privacy exposure with just a few clicks.

***

<sub>[1] At time of writing. Ubiquitous servers may eventually change their hostnames or add new ones. As a good habit, regularly investigate which 3rd parties are embedded in the web pages you visit.</sub>