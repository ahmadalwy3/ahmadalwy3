uBlock Origin can parse and enforce hosts files. For instance, out-of-the-box, uBlock supports [Peter Lowe’s Ad server](http://pgl.yoyo.org/) list which contains the hostnames of over 2,400 ad servers.

But there is an interesting hosts file available which is not enabled by default out-of-the-box: [hpHosts ad/tracking servers](http://hosts-file.net/) list. This list contains over 20,000 hostnames linked to ad servers, trackers, and other such nuisances.

![hpHosts](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/wiki-hphosts.png)

I have been using this list for days now, and I really do not see many issues, i.e. numerous unexpected web site "breakage".

I cannot select this list by default for new installs, since I have no idea yet of its likelihood of "breaking" web pages. But you may want to give it a try, adding an extra 20,000 ad servers to the filtering engine surely is of help. See results of [this benchmark](Reference-benchmark) below to compare using **hpHosts ad/tracking servers** vs out-of-the-box default lists (remember, figures are what was **not** blocked, thus the lower the numbers the better).

**With** hpHosts ad/tracking servers:

> - Domains: **219** / 220
> - Hosts: 347 / 564
> - Scripts: 558 / 832
> - Outbound cookies: 36 / 158
> - Net requests: 2,329 / 4,864

**Without** hpHosts ad/tracking servers (out-of-the-box settings):

> - Domains: **243** / 244
> - Hosts: 393 / 612
> - Scripts: 596 / 871
> - Outbound cookies: 48 / 175
> - Net requests: 2,513 / 5,099

For reference, Adblock Plus with _EasyList_, _EasyPrivacy_ and Malware protection enabled ("Acceptable ads" disabled):

> - Domains: **250** / 251
> - Hosts: 401 / 619
> - Scripts: 613 / 894
> - Outbound cookies: 45 / 183
> - Net requests: 2,505 / 5,106

Eventually, if more users try the **hpHosts ad/tracking servers** list, and report any and all issues with it, we can create the appropriate exception filters to prevent web page breakages, and then it might become feasible to enable it out of the box.

For instance, the recent [hacking of Reuters through the Taboola content delivery network](https://medium.com/@FredericJacobs/the-reuters-compromise-by-the-syrian-electronic-army-6bf570e1a85b) would have left you unaffected if you were using this list, as **hpHosts ad/tracking servers** does contain the hostname `cdn.taboola.com`, which is from where the compromised javascript file was downloaded.

So if you wish to help in making it possible to enable this list out of the box, try it, and report any breakage (after verifying the same breakage doesn't occur when the list is disabled) in [issue #17](https://github.com/gorhill/uBlock/issues/17).