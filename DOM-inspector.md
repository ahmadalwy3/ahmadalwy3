uBlock Origin comes with its own custom DOM inspector, to assist in the creation of cosmetic filters, as a complementary tool to the element picker (click the `</>` to access it):

![a](https://user-images.githubusercontent.com/585534/33130150-5d6201da-cf60-11e7-9637-831792c96e7e.png)

A custom DOM inspector -- rather than creating hooks into the browser's own DOM inspector -- has benefits:

- Portability: does no depend on specific browser API.
- Optimal: the UI is optimized to specifically deal with cosmetic filters.

Whereas the element picker is useful to interactively create cosmetic filters through point-and-click, the DOM inspector is useful to create cosmetic filters through the internal structure of the document in your browser. For instance this allows:

- To create very specific cosmetic filters by selecting an element directly in the DOM hierarchy.
- To create exception cosmetic filters.

[TODO: complete]