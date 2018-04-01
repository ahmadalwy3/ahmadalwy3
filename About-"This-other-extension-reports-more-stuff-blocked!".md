TL;DR: Do **not** rely on the number shown over an extension badge to judge blocking power, i.e. to assess how well your privacy is protected, you could fool yourself big time.

***

For both Adblock Plus and uBlock (and many other such extensions), the badge on the icon reports the number of net requests blocked by the extension.

Sometimes, for the same page, one extension can report more stuff blocked than the other, while the reality could be the opposite.

The less a blocker blocks, the higher the number of network requests. The higher the number of network requests, the more likely some of them will need to be blocked. So sometimes you end up with more network requests blocked as shown by the badge, while internally more network requests were actually allowed for the web page.

Ultimately, for me it's the [benchmarks I run](/gorhill/uBlock/wiki/%C2%B5Block-vs.-others:-Blocking-ads,-trackers,-malwares) to report blocking power which tells the real story. The badge is really not a good way to assess blocking power of an extension, you could well end up concluding the opposite of what is really happening.

If you don't want to run a benchmark, I have this [little online tool](http://raymondhill.net/httpsb/har-parser.html) with which you can find out the requests which were **not** prevented from leaving your browser. To use it, open the dev console for the page for which you want a report, and go to the _Network_ tab. **Edit:** since then I have created [uBO-Scope](https://github.com/gorhill/uBO-Scope), an extension which purpose is to inform you about what was not blocked.

Clear the browser cache by right-clicking somewhere in the _Network_ tab console. Force a reload of the web page, then right-click in the _Network_ tab console, and select _"Copy all as HAR"_. Then paste the result in the text area of [this online tool](http://raymondhill.net/httpsb/har-parser.html), and click _Parse_. You will be shown the hostnames which were hit by the browser for the particular page you loaded.

For example, for the front page of <http://www.cnet.com/>, **uBlock shows 10 request blocked**, while **ABP shows 16 request blocked** (both with a lot of filter lists). However here is what really happened internally:

Remote servers reached:

Adblock Plus
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com
- 1ab45d4854fe036a37ff-6643978b1699ef52a80b7f45a7bcfe3d.r85.cf2.rackcdn.com
- www.googletagservices.com
- zor.livefyre.com
- platform.twitter.com
- s.yimg.com
- dw.cbsimg.net
- geo.query.yahoo.com

uBlock:
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com

So uBlock caused the browser to hit many less remote servers, meaning it blocked more, and yet its badge displayed a lower number of requests blocked.

So the point is, do not rely on the badge to judge blocking power, i.e. to assess how well your privacy is protected, you would fool yourself big time.

On the other hand, blocking too much may "break" some aspects of a web site, so in the end, as long as you understand what is really happening under the hood, you can make informed choices.