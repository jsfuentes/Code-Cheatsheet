# Next Config

Create `next.config.js` in root

```javascript
// next.config.js
const withMdxEnhanced = require("next-mdx-enhanced");

module.exports = withMdxEnhanced({
  layoutPath: "layouts",
  defaultLayout: true,
  fileExtensions: ["mdx"],
  remarkPlugins: [],
  rehypePlugins: [],
  extendFrontMatter: {
    process: (mdxContent, frontMatter) => {},
    phase: "prebuild|loader|both",
  },
})({
  pageExtensions: ["js", "jsx", "md", "mdx", "ts", "tsx"],
});

```

