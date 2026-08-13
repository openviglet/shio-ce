# Documentation

A documentation tree: a DocPage post-type, /docs with guides and reference sections, and four pages wired together — an index, two guides and one reference page.

## Install

```
shio marketplace install shio-blueprint-docs
```

Then apply it to a site. Applying is a separate step: installing puts the package where
this instance can see it, and nothing is written to your content until you apply it.

## Parameters

- `productName` **(required)** — What the documentation is about. It has no sensible default.
- `projectName` — The npm package name of the generated project. Used in the front-end tree this package carries. Default: `my-shio-site`.

## What it provisions

- 1 post type(s)
- 1 content document(s)
- 14 front-end file(s) for you to write

---

Published by Viglet for [Viglet Shio](https://github.com/openviglet/shio).
