1. uBlock will load the default selection of filter lists:
    - This causes short-term memory churning (loading/parsing/sorting/storing); short-term memory will be garbage-collected eventually
    - All this short-term memory churning causes uBlock's baseline memory footprint to grow further
1. **A few minutes later**, uBlock will look whether one or more filter lists needs to be updated
1. If one or more filter lists need to be updated, uBlock will launch a background task which will fetch an updated version of whatever filter list is obsolete
1. Once all filter lists are brought up to date, uBlock will flush from memory all filters and reload them with the latest version
    - This will cause another round of short-term memory churning; short-term memory will be garbage-collected eventually
    - Again, all this short-term memory churning causes uBlock's baseline memory footprint to grow further
    - You can disable auto-update if you want, but it is optimal to let uBlock take care of this, i.e. manually forcing an update is sub-optimal
1. **A few minutes later**, assuming no change in selection of filter lists, or change in the content of selected filter lists, uBlock will make a selfie
    - A selfie allows uBlock to skip the parsing/sorting of data next time it loads
    - Generating the selfie also causes short-term memory churning; short-term memory will be garbage-collected eventually
    - Again, this short-term memory churning causes uBlock's baseline memory footprint to grow further
    - Any change in the selection of filter lists, or change in the content of selected filter lists will invalidate uBlock's selfie
1. Even after the growth in memory baseline, uBlock's _own memory_ footprint is still quite a bit smaller than that of Adblock Plus (ABP) -- once the garbage collector does its job
1. uBlock's much smaller _contributed memory_ footprint to web pages is much smaller than that of ABP
    - The contributed footprint to web pages is part of the memory footprint of the web pages themselves 
    - As opposed to an extension's own memory footprint, visible using Chromium's _"Task Manager"_, the contributed memory footprint to web pages cannot be easily seen by users
    - Though this measure is not readily visible, it's where you get the biggest bang for the buck with uBlock relative to ABP -- because uBlock **does not** inject thousands of CSS rules into pages and embedded frames (unlike ABP)

Once you have reached the point where there is a valid uBlock selfie, uBlock will run the most efficiently.

The next time you launch uBlock and there is a valid selfie, the load time will be a fraction of the load time when no selfie is available <sup>[1]</sup>, and uBlock's baseline memory footprint will be smaller than when uBlock launches without a selfie available.

So my point is that uBlock will perform at best efficiency if you give it time to optimize itself after installation: In subsequent launches, uBlock will perform more efficiently than what you may have observed immediately after you installed it.

<sub>[1] See <https://www.youtube.com/watch?v=BpypOeK10N8></sub>
***

Also, if you want to look at memory figures, in addition to the above notes regarding garbage collection, keep in mind:

- The [Chromium bug](https://code.google.com/p/chromium/issues/detail?id=441500) which causes systematically a memory leak when opening an extension popup UI.
- Currently opened extension option page(s) contribute to increase the extension's memory use
- Sometimes a browser's garbage collector ("GC") is lazier than others, i.e. it may takes longer to kick in.
    - In my benchmarks, it has happened I had to force a GC cycle using dev tools.

***

- Notes: the above is especially true for Chromium-based browser. However with the [early preview of the Firefox version](https://github.com/gorhill/uBlock/issues/27#issuecomment-67308172), the memory churning referred to above seems to result in much smaller memory peak usage.
- Related: ["Notes on memory benchmarks, selfies"](./Notes-on-memory-benchmarks,-selfies)
- Beware: ["Popup UI of extensions causes systematic memory leaks"](https://code.google.com/p/chromium/issues/detail?id=441500)
