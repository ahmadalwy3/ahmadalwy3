Just a place for me to keep track of contributed memory to web pages over time.  I consider the contributed memory to web pages to be more important than the own memory footprint. Unfortunately it is not possible for a user to see how much memory overhead an extension contributes to a web page, without running a benchmark like the one here. Keep in mind the results here are only for **one simple web page.**

Using [Acid Test 3](http://acid3.acidtests.org/), a rather simple web page, with embedded `iframes`. Web page was opened in a new tab for each extension (important), after a browser restart.

Each extension tested alone, with no other extension enabled.  Browser left on idle for more than 1 minute to ensure web page memory was garbage collected.

The following steps were added for benchmarks dated December 2014 and later:

1. Click _"Stats for nerds"_ in _"Task Manager"_: _"About memory"_ opens
1. Wait a few seconds
1. Close the _"About memory"_ tab
1. Wait a few seconds
1. Repeat all above steps until the memory footprint of the Acid Test tab stops decreasing

I found this was now necessary as it appears Chromium's garbage collector has become rather lazy. The above steps forces it into action.

### 24 December 2014

- Chromium 39.0.2171.65 64-bit (Linux)
- uBlock 0.8.2.2 (default lists: _EasyList_, _Peter Lowe’s Ad server_, _EasyPrivacy_, malware domain lists, _Fanboy’s Social Blocking List‎_)
- Adblock Plus 1.8.8 (_EasyList_, _EasyPrivacy_, _Malware Protection List_, _"Acceptable ads"_ disabled)

Summary of results:
- Reference memory usage for the web page: 23 MB
- uBlock adds over 10 MB
- Adblock Plus adds over 33 MB
- Adblock Plus with same filter lists as uBlock adds over 46 MB

No extension (reference):<br>
![no extension](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20141224-none.png)

uBlock:<br>
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20141224-ublock.png)

Adblock Plus:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20141224-abp.png)

Adblock Plus with same filter lists as uBlock:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20141224-abp-more.png)

### 19 September 2014

- Chromium 37.0.2062.94 64-bit (Linux)
- uBlock 0.6.2.1 (default filter lists)
- Adblock Plus 1.8.5 (_EasyList_, _EasyPrivacy_, _Malware Protection List_, _"Acceptable ads"_ disabled)

Summary of results:
- Reference memory usage for the web page: 22 MB
- uBlock Plus adds over 9 MB
- Adblock Plus adds over 32 MB

No extension (reference):<br>
![no extension](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20140919-none.png)

uBlock:<br>
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20140919-ublock.png)

Adblock Plus:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-in-page-20140919-abp.png)

Observations:

Last time I ran this benchmark [was on Chromium 34 64-bit](./%C2%B5Block-vs.-ABP:-efficiency-compared#added-memory-footprint-to-web-pages), and it does appear that Chromium 37 is causing web pages to consume more memory -- reference result went from ~17 MB to ~22 MB.
