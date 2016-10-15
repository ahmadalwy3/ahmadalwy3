**TL;DR:** if you worry about uBO's added overhead for non-bloated sites, just [disable cosmetic filtering](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-cosmetic-filtering) on a per-site basis, it is the optimal approach: this will keep you protected security- and privacy-wise (as far as your filters/rules allow) while minimizing the added overhead.

***

Yes, uBlock Origin ("uBO") adds overhead to page load. It's impossible for a content blocker to add zero CPU cycles and/or memory overhead.

**However**, for most web pages nowadays, that extra overhead is paid back many times from all the blocked resources which won't consume CPU cycles and memory.

A good metaphor is to see the added overhead as an investment: you want the best return on what you invest, and here the capital is your CPU cycles and computer memory.

The duty of a content blocker is to minimize the capital to invest on behalf of the user so as to lower the point at which it is paid back in full in order to start to profit as soon as possible from your investment -- minimizing the overhead guarantees the best return.

That said, for web pages where uBO finds nothing or very little to block (let's call them "nice sites" from now on), there won't be any return on investment to be had, which means the invested CPU cycles and memory is a net loss -- another reason why content blockers must do their best to minimize added overhead. One way to minimize such "loss" is to disable uBO on such nice sites for which a content blocker seems unnecessary. On the other hand, the "loss" on such sites will obviously be typically already rather low so the added overhead is probably not really an issue.

Disabling uBO for a site to avoid added the overhead is a judgment call to be made by the user, considering many factors:
- There is more than just the CPU cycles and memory return to consider with regard to invested overhead: there is also the peace-of-mind return of knowing your blocker is protecting you. There is no guarantee that a nice site will not stop being nice at any given moment, or that a nice site won't ever be hijacked and start to serve bad stuff.
- If you use [_medium mode_](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-medium-mode), it does not make much sense to disable uBO since typically this mode is used to also protect against [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery).

There is also another way to reduce the overhead without sacrificing the security/privacy benefits as a result of disabling uBO: just [disable cosmetic filtering](https://github.com/gorhill/uBlock/wiki/Per-site-switches#no-cosmetic-filtering) for nice sites -- this will remove good chunk of overhead while keeping you well protected since network filtering is still fully enabled -- whereas, as hinted by its name, cosmetic filtering offers no protection value.

If you are curious about the overhead added by uBO for any given web page, you can use this [page load speed tool](http://www.raymondhill.net/ublock/pageloadspeed.html) (won't work for pages which are not allowed to be embedded into frames), with which you can compare how fast a page load with and without uBO, and with different settings in uBO.

Here is an example of uBO's overhead added to a [atypically large page from a nice site](https://en.wikipedia.org/wiki/List_of_country_calling_codes):

| | Average |
| --- | --- |
|uBO fully enabled | 537.63 ms
|uBO enabled, cosmetic filtering disabled | 488.23 ms
|uBO disabled | 488.41 ms
|No blocker |  474.77 ms

Of course, there is no point benchmarking pages from less nice sites, as these pages will always load much faster when using a blocker -- though you may want to benchmark different blockers with similar settings.

**In conclusion:** if you worry about uBO's added overhead for so-called nice sites for which uBO appears unnecessary, just disabling cosmetic filtering is the optimal approach, this will keep you protected security- and privacy-wise.