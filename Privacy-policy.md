uBlock Origin does not collect any data of any kind.

- uBlock Origin has no home server.
- uBlock Origin doesn't embed any kind of analytic hooks in its code.

As of version 1.11.0, the quoted passage below is not longer true -- uBlock Origin will no longer use the resource `checksums/ublock0.txt` (the quoted text will be removed once version 1.11.0 is widespread):

> uBlock Origin will download the resource at
> `https://raw.githubusercontent.com/uBlockOrigin/uAssets/master/checksums/ublock0.txt?_=[unix time stamp in ms]`
> 
> - when you visit the _3rd-party filters_ pane in the dashboard;
> - once in a while if you have _Auto-update filter lists_ checked;
> 
> ... to find out whether some assets used by uBlock Origin need to be updated.
> 
> The purpose of the `unix time stamp in ms` portion of the URL is to be sure the browser cache is bypassed.

The only time uBlock Origin connects to a remote server is to update the filter lists and other related assets. If you disable auto-update in the _"3rd-party filters"_ pane in the dashboard, uBlock Origin will not connect to any remote server, unless you click _"Update now"_ and only if there are assets deemed "out of date".

The servers behind `githubusercontent.com` are owned by GitHub, Inc., and thus are unrelated to uBlock Origin, so even if I was interested in analytics (which I am not), I have no access to whatever data is logged by `githubusercontent.com`.

That is all.