uBlock Origin comes with a logger, which gives the ability to inspect what uBlock is doing with network requests and DOM elements, whether something is blocked or allowed, and which filter, if any, matched a network request or DOM element. This logger is _unified_, meaning it will display _everything_ uBlock does as it occurs.

The logger is the tool of choice to see, understand, diagnose and fix the functioning of uBlock.

To access the logger, click on the _list_ icon of uBlock Origin's popup UI:

![Figure 1](https://user-images.githubusercontent.com/886325/62736450-a8cfdc00-ba2d-11e9-8f24-9d6004371f8c.png)

The request logger will open in a new tab (which was moved to its own window below):

![Figure 2](https://user-images.githubusercontent.com/886325/62732907-c00acb80-ba25-11e9-8206-76d7f071657e.png)

The color of a row hints at how the resource was filtered:
- No color: The request for the resource was allowed to go through because it matched no filter/rule.
- Red: The request for the resource was canceled (`--`) because of a block filter/rule.
- Green: The request for the resource was allowed to go through (`++`) because it matched a filter/rule whose purpose is to bypass a matching block filter/rule.
- Yellow:
    - A DOM element which was blocked by a cosmetic filter; OR
    - A blocked request for a resource was redirected (`<<`) to a local, "neutered" replacement resource.
    - A defuser scriptlet was injected into the page (`+js(...)`)

When a resource is blocked/allowed/hidden/redirected, the second column in the row will provide further information. For blocked/allowed/hidden resources, the column will contains the responsible filter. For redirection, the column will contains the local resource used as replacement to the blocked network request.

Take note that the network request logger in uBlock is a forward-looking logger: this means only future requests can be logged.

In the spirit of efficiency, uBlock will log entries **IF AND ONLY IF** the logger is opened. Otherwise, if the logger is not opened, no CPU/memory resources are consumed by uBlock for logging purpose.

#### Tip
Hold the <kbd>Shift</kbd> key while clicking the "Open the logger" icon to toggle between opening the logger in a separate window or in a separate tab. uBO will remember that setting when you open the logger next time, without having to hold the <kbd>Shift</kbd> key.

***

- [Page selector](#page-selector)
- [Reload](#reload)
- [DOM inspector](#dom-inspector)
- [Accessing popup UI of a specific page](#accessing-popup-ui-of-a-specific-page)
- [Expand](#expand)
- [Void log entries](#void-log-entries)
- [Clear](#clear)
- [Pause the logger](#pause-the-logger)
- [Filtering the logger output](#filtering-the-logger-output)
- [Finding from which list(s) a static filter originates](#finding-from-which-lists-a-static-filter-originates)
- [Creating filters](#creating-filters)
    - [Dynamic URL filtering rules](#dynamic-url-filtering-rules)
    - [Static network filters](#static-network-filters)

***

### Components

***

#### Page selector

![Figure 3](https://user-images.githubusercontent.com/886325/62740200-6ca17900-ba37-11e9-9a76-d64ef10b761d.png)

The drop-down selector is to display log entries which are related to a specific page. This will hide from view all log entries which are not related to the selected page. By selecting _All_ again, all log entries will be displayed again.

Note in the figure above the entry named _"Tabless"_: selecting this entry allows to show network requests not associated with any tab. _Tabless_ request are denoted in the log by font shadow effect and `0` in "Context" column (fifth).

***

#### Reload

![Figure 4](https://user-images.githubusercontent.com/886325/62740268-affbe780-ba37-11e9-9144-cdc4c52370aa.png)

The big reload button aside the page selector is to force a reload of the content of the selected page. This button is enabled only for when a specific page is selected.

***

#### Dom inspector

![Figure 4.5](https://user-images.githubusercontent.com/886325/62740302-c4d87b00-ba37-11e9-8d11-2fe9e1fc4d5d.png)

Complementary tool to the element picker.

Please read more on dedicated page: ["DOM inspector"](./DOM-inspector)

***

#### Accessing popup UI of a specific page

![Figure 10](https://user-images.githubusercontent.com/886325/62734523-863bc400-ba29-11e9-82ce-0bf4211ea7d3.png)

By clicking this button you can access the popup UI of a specific tab.

***

#### Expand

![Figure 5](https://user-images.githubusercontent.com/886325/62740377-f7827380-ba37-11e9-8be0-fef923ada0d3.png)

By default log entries in the logger are collapsed so as to take no more than one line. Some log entries however might be truncated as a result. This button is to force all those entries with truncated extraneous information to be fully visible.

***

#### Void log entries

![Figure 6](https://user-images.githubusercontent.com/886325/62740422-13861500-ba38-11e9-911b-6d377afe71f8.png)

With "All" selected in "Page selector" if you close a tab for which there are entries in the logger, these entries will be marked as _void_, i.e. they will be faded out, to indicate the tab for these entries does not exist anymore.

The `X` button in the toolbar allows you to remove those void entries from the logger.

***

#### Clear

![Figure 7](https://user-images.githubusercontent.com/886325/62740450-2c8ec600-ba38-11e9-9f6b-e6b113cd8ebe.png)

This is to clear the logger, to remove all entries from the selected/filtered context (Ars Technica tab in this example).

***

#### Pause the logger

![Figure 7](https://user-images.githubusercontent.com/886325/62740475-46c8a400-ba38-11e9-9930-25af7d205abe.png)

TODO

***

#### Filtering the logger output

![Figure 8](https://user-images.githubusercontent.com/886325/62740615-97d89800-ba38-11e9-9b4c-869fac0d0129.png)

You can visually filter entries in the logger using filter expressions. Log entries which do not match _all_ filter expressions will be hidden from view. Syntax for a filter expression:

- Enter `foo` to only show entries which have a string `foo`.
- Enter `|foo` to only show entries which have a field starting with `foo`.
    - Tip: use `|--` to show only entries which were blocked (`--` may work for the most part, but there could be false positives).
- Enter `foo|` to only show entries which have a field ending with `foo`.
- Enter `|foo|` to only show entries which have exactly a field with `foo`.
- Prefix any expression with `!` to reverse the meaning of the expression.
    - `!foo` means display only entries which do not have the string `foo` in it.
    - `!|--` means display only entries which were **not** blocked.
- When more than one filter expression appear, a logical _and_ between the expressions is implied.
- You can _or_ multiple expressions together:
    - `css || image` means display entries which match either `css` or `image`.
    - `xhr || other |http:` means display entries which match either `xhr` or `other` and have a field which starts with `http:`.
    - `!css || image` means display entries which do not match either `css` or `images` (equivalent to `!css !image` really).
    - Warning: With _or_'ed expressions, the _not_ (`!`) operator can only apply to the resulting _or_'ed expression.
- A special keyword can be used to filter behind-the-scene requests: `bts`, or `|bts` for a stricter filtering.

Examples:

- `!|-- facebook`: show only non-blocked entries with the string `facebook` in it.
- `|xhr google`: show only entries of type `XMLHttpRequest` with the word `google` in it.
- `!|image !|css`: show only entries which are not of type `image`, neither `css`.

***

#### Maximum number of entries

![Figure 9]()

This is the maximum number of entries allowed in the logger. When the maximum is reached, the oldest entries at the bottom will be removed to make place to newest entries at the top.

This is useful to be sure the logger does not unduly consume a huge amount of memory if left open for long period of time. Usually, the most recent entries are the ones of interest. When this value is not set, there is a built-in limit of 5,000 entries.

***

#### Finding from which list(s) a static filter originates

You can find out from which filter list(s) a static filter originates, by simply clicking on it:

![c](https://cloud.githubusercontent.com/assets/585534/8145767/e2d4eafe-11e3-11e5-9af3-6692531403fa.png)

![a](https://cloud.githubusercontent.com/assets/585534/8145768/e431716a-11e3-11e5-859c-794d37c7c41e.png)

When the filter list is rendered as a link, clicking on it will bring you to the support site for that list.

***

#### Creating filters

![Figure 11](https://cloud.githubusercontent.com/assets/585534/8037213/8bac33f8-0dca-11e5-8610-010d0f9ed030.png)

Clicking on the 4th cell of a log entry will give you access to the filtering tools dialog (modal), from where you can easily create dynamic URL filtering rules or just standard static filters, and launch the element picker.

***

##### Dynamic URL filtering rules

![Figure 12](https://cloud.githubusercontent.com/assets/585534/8037337/31bf8a2e-0dcb-11e5-8a23-aef78f943727.png)

Point-and-click to create dynamic URL filtering rules. These rules are temporary by default, you need to click the padlock if you want them to be permanent. Useful to find out which network requests need to be blocked or allowed on a page in order, to fix a broken page, or to further block more useless resources from a page.

See [_"Overview of uBlock's network filtering engine: details"_](./Overview-of-uBlock's-network-filtering-engine:-details) for more details about where dynamic URL filtering fits in the overall filtering engine.

***

##### Static network filters

![Figure 13](https://cloud.githubusercontent.com/assets/585534/8037377/6ed2d4d4-0dcb-11e5-826c-e5109f72b86b.png)

This dialog will assist you in creating static filters compatible with [ABP filter syntax](https://adblockplus.org/filter-cheatsheet). Note that creating static filters incur a significant overhead relative to dynamic URL filtering rules. Typically, you will first use dynamic URL filtering rules to quickly diagnose which network requests need to be allowed/blocked.

See [_"Overview of uBlock's network filtering engine: details"_](./Overview-of-uBlock's-network-filtering-engine:-details) for more details about where static filtering fits in the overall filtering engine.
