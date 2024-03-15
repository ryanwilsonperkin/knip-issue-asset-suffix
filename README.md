# Reproduction of issue for knip with ?url suffix in assets

https://github.com/webpro/knip/issues/202

When an application uses `?` style suffixes on asset imports to hint to the
bundler how they should be treated (as documented for example by Vite:
https://vitejs.dev/guide/assets) Knip correctly finds the underlying import by
stripping away the suffix, but then clashes when marking whether or not that
asset is used.

In this example we provide the compiler `svg: () => ''` to indicate that SVG
assets should be included in dead code analysis, and then provide 2 svg imports
in the `main.js`, one with a `?url` suffix and one without. The one with the
suffix is incorrectly marked as an unused file.

Reproduce this result by running the following in this repo:
```
yarn knip
```
