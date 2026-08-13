# Landing page

One campaign page at /get-started, composed of a hero, a feature grid, an FAQ and a call to action from the @viglet/shio-sections vocabulary. The smallest useful blueprint: apply it, edit four sections, ship.

## Install

```
shio marketplace install shio-blueprint-landing
```

Then apply it to a site. Applying is a separate step: installing puts the package where
this instance can see it, and nothing is written to your content until you apply it.

## Parameters

- `brand` **(required)** — The company or product name.
- `headline` — The hero heading — the one sentence the page is about. Default: `Start in an afternoon, not a quarter`.
- `ctaLabel` — Label on the call to action. Default: `Get started`.
- `ctaHref` — Where the call to action points. Default: `/signup`.
- `projectName` — The npm package name of the generated project. Used in the front-end tree this package carries. Default: `my-shio-site`.

## What it provisions

- 8 post type(s)
- 1 content document(s)
- 14 front-end file(s) for you to write

---

Published by Viglet for [Viglet Shio](https://github.com/openviglet/shio).
