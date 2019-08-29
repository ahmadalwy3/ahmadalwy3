<sup>[中文](https://github.com/fang5566/uBlock/wiki/%C2%B5Block-%E5%92%8C-ABP-%E5%9C%A8%E8%BF%90%E8%A1%8C%E6%95%88%E7%8E%87%E6%96%B9%E9%9D%A2%E7%9A%84%E5%AF%B9%E6%AF%94)</sup>

***

Here is a quick illustrated comparison of efficiency using various angles. Each extension were tested alone, as the only extension present. Benchmarking was performed with Chromium on Linux Mint 64-bit.

- [Own memory footprint](#own-memory-footprint)
- [Added CPU overhead to each net request](#added-cpu-overhead-to-each-net-request)
- [Added memory footprint to web pages](#added-memory-footprint-to-web-pages)
- [Added CPU overhead to web pages](#added-cpu-overhead-to-web-pages)

### Own memory footprint

These screenshots show the memory footprint of ABP and uBlock _after_ they have gone through this rather [demanding benchmark](./Reference-benchmark). Once the benchmark was completed, I forced the browser to garbage collect the memory in each extension by clicking the trash icon (in dev console) a couple of times -- this is an _important step_, or else the shown memory footprint is not too reliable.

##### Adblock Plus
![ABP](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/abp-own-mem.png)

##### uBlock
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/ublock-own-mem.png)

Both extensions had _EasyList_, _EasyPrivacy_, _Peter Lowe's Ad Server_ list, and malware protection (there are more filters in µBlock for this last one).

### Added CPU overhead to each net request

<sup>Last updated on: 30 January 2015.</sup>

ABP and uBlock need to evaluate the URL of each net request against their dictionary of filters, and eventually tell the waiting browser whether the request should be cancelled or not. Since the browser is waiting for an answer, this is a time critical part and determining whether the request should be allowed or not must be done as fast as possible.

Below are the average time it takes for each extension to handle a net request in their respective `chrome.webRequest.onBeforeRequest` handler, using the same [benchmark](./Reference-benchmark).

##### Adblock Plus 1.8.10

    ABP> onBeforeRequest: 0.425 ms (9141 samples)
    ABP> onBeforeRequest: 0.423 ms (9230 samples)
    ABP> onBeforeRequest: 0.423 ms (9233 samples)
    ABP> onBeforeRequest: 0.423 ms (9310 samples)
    ABP> onBeforeRequest: 0.423 ms (9390 samples)
    ABP> onBeforeRequest: 0.423 ms (9477 samples)
    ABP> onBeforeRequest: 0.423 ms (9524 samples)
    ABP> onBeforeRequest: 0.422 ms (9687 samples)
    ABP> onBeforeRequest: 0.421 ms (9704 samples)
    ABP> onBeforeRequest: 0.421 ms (9861 samples)

##### uBlock 0.8.7.0

    uBlock> onBeforeRequest: 0.131 ms (8664 samples)
    uBlock> onBeforeRequest: 0.131 ms (8763 samples)
    uBlock> onBeforeRequest: 0.131 ms (8839 samples)
    uBlock> onBeforeRequest: 0.130 ms (8914 samples)
    uBlock> onBeforeRequest: 0.131 ms (8988 samples)
    uBlock> onBeforeRequest: 0.131 ms (9033 samples)
    uBlock> onBeforeRequest: 0.130 ms (9192 samples)
    uBlock> onBeforeRequest: 0.130 ms (9206 samples)
    uBlock> onBeforeRequest: 0.129 ms (9324 samples)
    uBlock> onBeforeRequest: 0.129 ms (9329 samples)

##### Methodology

Note that the results above are the tail end of running the [reference benchmark](./Reference-benchmark), except `wait` set to 15, and `repeat` set to 1. Both ABP and uBlock set to use _EasyList_, _EasyPrivacy_, _"Peter Lowe’s Ad server list"_, _"Malware domains"_. ABP-specific: _"Acceptable ads"_ disabled. µBlock-specific: default settings.

The results depend heavily on the processor: I benchmarked on an i5-3xxxK CPU @ 3.4 GHz x 4.

### Added memory footprint to web pages

Extensions have their own memory footprint, but they also cause increased memory footprint in web pages. Below you can see the added memory footprint in a very simple web page, [Hacker News](https://news.ycombinator.com/). First screenshot is when no extension at all is used, so consider it as the reference memory footprint for this web page, other screenshots show the increased memory footprint caused by each extension. The browser was left on idle after loading the page in order to allow the garbage collector to kick in.

**No extension:**<br>
![No extension](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/hn-alone.png)

**Adblock Plus:**<br>
![ABP](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/hn-abp.png)

**uBlock:**<br>
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/hn-ublock.png)

Now keep in mind this is the added footprint for a very simple web page which has no embedded frames. You can multiply the added footprint on the main page by the number of frames embedded on a page, so page with frames can end up consuming a _lot_ more memory than they would have otherwise. For instance, a very simple web page with a couple of `iframe` in it, [The Acid3 Test](http://acid3.acidtests.org/):

![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/acid3test-mem.png)<br>
<sup>Added memory footprint: Left = no extension. Middle = Adblock Plus. Right = µBlock.</sup>

A good stress test which further demonstrate this is the [infamous vim test](https://github.com/gorhill/httpswitchboard/wiki/Adblock-Plus-memory-consumption).

##### uBlock vs. Adblock: memory usage differential during reference benchmark

![uBlock vs. Adblock: memory usage differential during reference benchmark](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/media/ublock-vs-abp-cpu-2.png)

Above picture gives an overview of how much more memory Adblock Plus consumes over uBlock. It represents the **extra memory** ABP consumes relative to µBlock -- so essentially uBlock is the horizontal axis. If memory consumption of ABP and uBlock were exactly the same, there would be no graph. The [reference benchmark](/gorhill/uBlock/wiki/Reference-benchmark) was used, which consists of visiting 60 front pages of high traffic web sites.

The vertical axis represents MB. The horizontal axis is time in seconds, and the data was tediously extracted from [this video](https://www.youtube.com/watch?v=DKM78oV_ftg) (consider the video to be the raw data -- [here is the spreadsheet](https://github.com/gorhill/uBlock/blob/master/doc/benchmarks/ublock-vs-abp-timeline.ods) so people can double check in doubt).

The blue area represents how much more ABP itself consumes more memory than µBlock. The orange area represents how much more ABP causes the web pages themselves to consume more memory. ABP systematically causes web pages to consume more memory, and often quite a lot, north of 100 MB for some sites. This kind of added short term memory overhead is not cheap, as it also means the CPU is working harder.

### Added CPU overhead to web pages

This is the benchmarks comparing CPU usage in the background page when loading [si.com](http://www.si.com) ten times (so you can shift one decimal to the left for per page figures). Each page load was triggered after the previous page load completed.

**Top:** Adblock Plus 1.8.3. **Bottom:** uBlock 0.5.1.0.

![CPU benchmark](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/bgpage-cpu-si.comx10.png)

I did measure CPU usage for content scripts (above benchmarks are for background pages), but given the web page used for the benchmark is quite a bloated one, the useful figures were drowned in a sea of noise. But the fact that ABP inserts 14,000+ CSS rules caused the CPU to used be much more than uBlock (2-3 to 1 ratio) when comparing content script CPU usage (again, above is background page CPU usage).

Also, the amount of work µBlock does in its content scripts is proportional to the complexity of a web page. So given uBlock did much better CPU-wise than ABP in its content script for such a bloated web site means it was a worst-case scenario for µBlock, and yet it did its job of hiding elements between 2 and 3 times faster.

### Related wiki pages

- [Counterarguments: Who cares about efficiency, I have 8 GB](./Counterarguments#who-care-about-efficiency-i-have-8-gb)
- [Net request filtering efficiency: HTTP Switchboard vs. Adblock Plus](https://github.com/gorhill/httpswitchboard/wiki/Net-request-filtering-efficiency:-HTTP-Switchboard-vs.-Adblock-Plus)
- [Adblock Plus memory consumption](https://github.com/gorhill/httpswitchboard/wiki/Adblock-Plus-memory-consumption)
