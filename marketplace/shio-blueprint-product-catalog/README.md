# Product catalogue

A Product post-type with SKU, price and a repeatable spec list, plus /products with an accessories subsection and three sample products.

## Install

```
shio marketplace install shio-blueprint-product-catalog
```

Then apply it to a site. Applying is a separate step: installing puts the package where
this instance can see it, and nothing is written to your content until you apply it.

## Parameters

- `storeName`: The store's name, used in the sample copy. Default: `Store`.
- `currency`: Currency code the sample products are priced in. Default: `USD`.
- `projectName`: The npm package name of the generated project. Used in the front-end tree this package carries. Default: `my-shio-site`.

## What it provisions

- 1 post type(s)
- 1 content document(s)
- 14 front-end file(s) for you to write

---

Published by Viglet for [Viglet Shio](https://github.com/openviglet/shio).
