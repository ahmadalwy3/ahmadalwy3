**Note:** Results have been updated with latest Firefox 41 and Chromium 45. The page is the same as the old one (Firefox 35/Chromium 39, [archived here](https://github.com/gorhill/uBlock/wiki/Firefox-version:-benchmarking-memory-footprint-(2015-03-07))), except all figures have been updated using latest browser versions.

***

[![Vim test](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/vim-test-abp-vs-ublock.png)](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/vim-test-abp-vs-ublock.png)<br><sup>Infamous VIM test: ABP 370 MB vs. uBlock 373 MB. Firefox 41 64-bit. On Chromium-based browsers, ABP still suffers memory footprint issues from injecting a huge stylesheet in each page and in each embedded frames on a page.</sup>

#### Setup

1. Ensure the blocker is the only active extension (to avoid results to be polluted by other extensions)
1. Ensure click-to-play (or whatever equivalent) is enabled before launching the benchmark
1. Select the following filter lists in the benchmarked blockers:
    - EasyList
    - Peter Lowe's Ad server list
    - EasyPrivacy
    - Fanboy's Social Blocking List
    - Malware domain lists
    - ABP-specifics: _"Acceptable ads"_ disabled
    - uBlock-specifics: uBlock's filters enabled (+140 filters), extra malware domains (+1,487 filters)

#### Steps

1. Have the benchmarked blocker enabled and properly setup
1. Have only the "new tab" opened
1. Quit Firefox
1. Launch Firefox
1. Paste <http://news.yahoo.com/> in address bar, wait for page to finish loading
1. Open new tab, paste <http://news.google.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.huffingtonpost.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.cnn.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.nytimes.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.foxnews.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.nbcnews.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.dailymail.co.uk/>, wait for page to finish loading
1. Open new tab, paste <http://www.washingtonpost.com/>, wait for page to finish loading
1. Open new tab, paste <http://www.theguardian.com/>, wait for page to finish loading
1. Open new tab, paste <https://news.ycombinator.com/>, wait for page to finish loading
1. Leave the browser idle for two minutes
1. Open new tab, paste `about:memory`, wait for page to finish loading
1. Firefox: Click _"Minimize memory usage"_ button in _"Free memory"_ section
1. Firefox: Click _Measure_ button in _"Show memory reports"_ section
1. Firefox: Write down _"Explicit Allocations"_ value (see notes below) / Chromium: Write down _Σ_ value

So I did the **exact** above steps for no blocker, ABP, uBlock.

#### Results

- **Firefox 52** (benchmark results updated on April 3rd, 2017)
    - Two measurements needed with FF 52.0: Main Process + Web Content
    - No blocker: 175 MB + 1,397 MB = **1,572 MB** (reference memory usage)
    - **Adblock Plus** 2.8.2: 241 MB + 626 MB = **867 MB** (reference _minus_ 705 MB)
    - **uBlock Origin** 1.11.4: 176 MB + 488 MB = **664 MB** (reference _minus_ 908 MB, ABP _minus_ 203 MB)
- **Chromium** (benchmark results updated on April 3rd, 2017)
    - No blocker: **1,615 MB** (reference memory usage)
    - **Adblock Plus** 1.13.2: **1,253 MB** (reference _minus_ 362 MB)
    - **uBlock Origin** 1.11.4: **832 MB** (reference _minus_ 783 MB, ABP _minus_ 421 MB)

**Important:** You can't compare directly the figures between the browsers -- they are taken using different methodology from one browser to the other. The benchmarks are more to compare the figures for various blockers within the same browser.

#### Notes

Tested on Firefox 41.0 64-bit and Chromium 45.0.2454.85 64-bit on Linux Mint. No other extensions were present.

For Firefox, I chose the _"Explicit Allocations"_  figure because as per Firefox, it is "the single best number to focus on" with regard to memory usage.

Without going into details, hardware is i5 quadcore + 8 GB

If other users feel like repeating the tests, it would be nice just to confirm I got everything right.
