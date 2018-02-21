Parsing raw filter lists is a CPU and memory intensive task. Adblock Plus-compatible filter syntax is complex, and thus parsing those filters requires a lot of CPU cycles. To add to the parsing complexity, uBlock also supports the parsing of hosts files. Though uBlock could parse filter lists at a satisfying speed, this doesn't mean trying to improve performance in that area should not be attempted.

So this is what has been done in 0.8.9.0. The idea is rather simple: create and cache a compiled version of a filter list, so that next time it needs to be loaded in memory, all the costly parts of the parsing operation have been done already:

![Figure 1](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/setup-performance-internals.png)

The compiled version of a filter list contains very deterministic content, such that no complicated parsing is required. This improves launch time performance (smaller is better):

![Figure 2](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/setup-performance-0.8.9.0.png)

And this also improve the performance when filter lists have to be reloaded:

![Figure 3](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/filters-load-performance-0.8.9.0.png)

A compiled filter lists is made of a sequence of _atomic_ filters, i.e. filters which can't be decomposed into smaller functional filters. ABP-compatible filter syntax allows the creation of composite filters, i.e. filter declarations which really represents many filters. For example, a raw filter found in _EasyList_:

    /advertisers.$image,script,subdocument

From uBlock's point of view, this is really three separate filters:

    /advertisers.$image
    /advertisers.$script
    /advertisers.$subdocument

It can quickly get more complicated (just added the domain filter option for demonstration purpose):

    /advertisers.$image,script,subdocument,domain=example.com|whatever.org

Translate internally into:

    /advertisers.$image,domain=example.com
    /advertisers.$script,domain=example.com
    /advertisers.$subdocument,domain=example.com
    /advertisers.$image,domain=whatever.org
    /advertisers.$script,domain=whatever.org
    /advertisers.$subdocument,domain=whatever.org

These are atomic filters, they can't be decomposed into smaller filters.

Compiling filter lists involves more then just _atomizing_, it also involves pre-computing as much as possible so as to be as close as possible to the in-memory filter representations, in order to reduce the amount of work to do when a compiled filter list is translated into in-memory data.

So roughly this is it.

There are nice virtuous side effects with using compiled filter lists. One of them is the very accurate counting of distinct filters, and the ability to _completely_ detect duplicates. Prior to 0.8.9.0, uBlock tried best to detect duplicate, but it wasn't perfect, as it was using the raw representation of a filter to decide whether the filter was already processed.

So this meant that the following duplicated filters would not have been seen as duplicates by uBlock, even though they essentially accomplish the same thing:

    /advertisers.$image,script
    /advertisers.$script,image

In 0.8.9.0, since all filters are normalized into atomic filter representation, uBlock is now able to detect 100% of filters which are functional duplicates.

And since uBlock's now report the number of atomic filters, expect the count to go up somewhat compared to previous versions. For instance, currently using default filter lists, 0.8.9.0 reports over 58,000 network filters, while previous versions reported around 55,000 network filters.