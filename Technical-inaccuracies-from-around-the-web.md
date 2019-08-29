There is so much of these... I will collect then here in the hope this will be used as reference for common misunderstanding.

###### [uBlock counts that many?](http://linustechtips.com/main/topic/461485-ublock-counts-that-many/)

> it would be blocking ads and cookies, so the longer you watch, the more ads and cookies there are

The real answer: the count in the uBlock Origin icon is the number of **blocked network requests** since the page was last fully loaded. These blocked network requests can be that of "ads" or anything else which is worth blocking as per selected filter lists. For details about the blocked network requests, use the [logger](./The-logger). uBlock Origin does not block cookies directly, it blocks network requests. If a blocked network request has a `Set-Cookie` header, the cookie payload will be blocked indirectly as a consequence of blocking the network request.
