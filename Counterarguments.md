Just a page to collect my counterarguments when I spot something which I believe deserve countering.

#### Who cares about efficiency, I have 8 GB

I heard this argument so often from apologists of bloated software that I decided to give the counterargument its [own page](./Who-cares-about-efficiency,-I-have-8-GB-and%7Cor-a-quad-core-CPU).

#### Just use a hosts file

uBlock supports the parsing/enforcing of hosts files, and ships with a couple of them. One of them, _"Peter Lowe’s Ad server list"_ is enabled out of the box.

Using a hosts file at OS level rather than uBlock level is definitely the better solution for lists of malware domain, since these malware-linked domains would be blocked system-wide at OS level, and all applications would benefit from it.

However, for lists of domain linked to ad servers, trackers, analytics, etc., this is not a good solution: **You can't easily un-break web pages with a [hosts file](http://en.wikipedia.org/wiki/Hosts_(file)) at OS level.**

With hosts file under control of uBlock, it is possible to un-break web sites: a user can just disable uBlock for the web site which breaks, or an exception filter can be created to counter the blocking of a specific hostname appearing in a hosts file.

Many of the exception filters in [_"uBlock filters"_](https://github.com/gorhill/uBlock/blob/master/assets/ublock/filters.txt) are actually exception filters to counter entries in the hosts files shipped with uBlock.

I want the project to be committed to fully support the hosts files which ship with uBlock, i.e. report any issues arising from using these, and appropriate exception filters will be created.

I personally use all of these hosts files, and so far not much breakage.

#### uBlock is a fork of Adblock Plus code

No. Code is wholly original, it was written from scratch. There are a very few places I borrowed code from elsewhere, and this is clearly identified. For example, for the element picker, I [embedded](https://github.com/gorhill/uBlock/blob/master/js/element-picker.js#L27) [CSS.escape](http://mths.be/cssescape) from Mathias Bynens (because Chromium doesn't support yet [CSS.escape](https://developer.mozilla.org/en-US/docs/Web/API/CSS.escape)).

#### Adblock Edge is as light as uBlock

No it's not. Adblock Edge is like Adblock Plus, except that notably it doesn't have the _"Acceptable ads"_ exception filters out of the box. See for yourself: [here](https://bitbucket.org/adstomper/adblockedge/diff/lib/filterClasses.js?diff1=f89367e6ddc7&diff2=a642b932365d9521042cf8fec56089caca496a7d&at=default) is a diff of a code change for Adblock Edge, and [here](https://github.com/adblockplus/adblockplus/commit/384cb64c6d3c2aa698b5f15c9d8aaefd22c889aa#diff-3) is the same exact diff for Adblock Plus. The timestamps shows that Adblock Edge pulled code changes from the Adblock Plus project.
