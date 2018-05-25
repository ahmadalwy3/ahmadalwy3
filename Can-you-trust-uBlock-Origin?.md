After I added the `privacy` permission in order to make uBlock Origin  reliable when it comes to blocking network requests, a lot of people questioned uBlock Origin's trustworthiness.

First, uBlock Origin is completely developed in full public view. All the sources and all the changes to the sources are fully accessible on GitHub.

Second, uBlock Origin does not have a dedicated server, it can't "phone home" with your browsing data, there is only GitHub, and GitHub is completely unrelated to uBlock Origin.

Third, I have no intent to _ever_ monetize uBlock Origin, it's started as a personal project, and it still is a personal project. So uBlock Origin has absolutely no interest in data mining you.

I think it's time I give examples of how requiring _less_ permissions is **not** a sure sign a higher trustworthiness.

#### Web Protector - Reliable Phishing Protection

Chrome store: [Web Protector - Reliable Phishing Protection](https://chrome.google.com/webstore/detail/web-protector-reliable-ph/kfecnpmgnlnbmipaogfhoacoioifjgko).

This extension requires the same permission as uBlock, _minus_ the `privacy` one. Some might be inclined that it can thus be more trusted than uBlock, which requires the `privacy` permission.

However, Web Protector has a home server, and it does "phone home" as opposed to uBlock (which has no home in the first place).

For **every** web page you visit, you can see Web Protector sending behind-the-scene network requests to `webovernet.com`:

![c](https://cloud.githubusercontent.com/assets/585534/8253895/fe92dd8c-1661-11e5-9134-5c2b9159a57c.png)

***

This is just to demonstrate that the permissions _alone_ do not tell the whole story. What must be assessed are:

- Is the code developed in **full** view?
- Under which license does the code fall?
- Is there a home server?
- What network requests are made by an extension behind the scene?
    - uBlock Origin's logger allows you to see all behind-the-scene network requests, including its own (to GitHub, for updating filter lists).
- How is an extension monetizing itself?
    - Learning about this factor will help you best understand whether the extension's developer's interests are aligned or at odd with yours.
