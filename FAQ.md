Collection of questions which have been asked, along with the answer I provided, or I would have provided.

#### Is there a Chinese translation of this Wiki?

Yes, it is here: [中文](https://github.com/fang5566/uBlock/wiki/FAQ)

#### Can uBlock Origin filter Youtube ads?

If the filter lists you enable include filters to block YouTube ads, then yes it will.  EasyList, which is enabled by default, includes filters to block YouTube ads.

#### Is [other blocker] still needed with uBlock?

It all depends of the filter lists you use, and whether you use dynamic filtering in uBlock. I run benchmarks regarding blocking efficiency; these may help you decide whether you should keep another blocker to complement uBlock, or whether you should drop it and configure uBlock to block more: [uBlock and others: Blocking ads, trackers, malwares](https://github.com/gorhill/uBlock/wiki/uBlock-and-others:-Blocking-ads,-trackers,-malwares). The [resulting diffs](https://github.com/gorhill/uBlock/wiki/uBlock-and-others:-Blocking-ads,-trackers,-malwares#data-diffs) are particularly useful in making a decision.

#### Is the Firefox version considered stable?

Yes.

#### How often are filter lists updated within uBlock?

Currently, after four to five days a filter list is deemed "obsolete".

#### How to show Google Search ads without disabling uBlock?

Just toggle off the [cosmetic filtering switch](https://github.com/gorhill/uBlock/wiki/Quick-guide:-popup-user-interface#no-cosmetic-filtering) while on the search page. This will disable cosmetic filtering for the Google Search site.

#### Web pages appear only as text

You probably have a bad filter entry in your _"My filters"_ pane in the dashboard. You will have to find it and remove it. For examples, filter entries which look like:

    http:

Will cause that exact problem.

#### Why is uBlock injecting a CSS selector with "www.faceporn.net" in it...?

About that `[href^="http://www.faceporn.net/free?"]` CSS selector injected in some web pages, see: [Github (non)issue #161, _"Style injection?"_](https://github.com/chrisaljoudi/uBlock/issues/161).

TL;DR: it's a element hiding filter from _EasyList_.

#### The badge count is very high, doesn't this slow down uBlock?

- Open a new document in a plain text editor
- Type "1"
- Notice the text editor's responsiveness
- Replace "1" with "1,000,000"
- Notice the text editor's responsiveness

Sounds absurd?  It is.  So is the claim that a high badge count slows down uBlock.  It's just a _counter_ for the number of blocked network requests.

#### I am concerned about stability, should I wait for v1.0?

uBlock is considered stable.  The version number is just a convenience to differentiate one release from another one.  It doesn't have any more meaning than this.

#### YouTube filtering options à la ABP (or, Facebook filtering options à la ABP)

These filter lists do not come with a Creative Commons license, thus uBlock is not shipping with these lists. But you can add them manually as custom filter lists. You can find URLs to various external lists on this page: [Filter lists from around the web](https://github.com/gorhill/uBlock/wiki/Filter-lists-from-around-the-web).

#### Are you paid to develop uBlock?

No.

I like to code, and the reward is to see the resulting work useful to others, sometimes [in unexpected ways](https://www.youtube.com/watch?v=90NsjKvz9Ns).

#### Why did you develop the Chromium version before the Firefox version?

In as few words as possible, with as little private matters disclosed:

- Fall 2013
- I am Firefox/NoScript user
- Other user is Chromium/ABP
- Worried about Chromium user not being protected against `iframe` loading freely (as opposed to Firefox/NoScript)
- Looked into Chrome API to just quickly [hack together](https://news.ycombinator.com/item?id=6871331) a homespun `iframe` blocker
