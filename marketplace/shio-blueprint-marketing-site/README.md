# Marketing site

A three-page marketing site built from the @viglet/shio-sections vocabulary: home, pricing and about, each composed of known sections (hero, feature grid, logo wall, testimonials, FAQ, call to action). The React components that render these sections ship in @viglet/shio-sections, so the front end is a dependency rather than a rewrite.

## Install

```
shio marketplace install shio-blueprint-marketing-site
```

Then apply it to a site. Applying is a separate step: installing puts the package where
this instance can see it, and nothing is written to your content until you apply it.

## Parameters

- `brand` **(required)** — The company or product name. Appears in every heading, so there is no useful default.
- `tagline` — One line under the hero heading. Default: `Software that gets out of the way`.
- `ctaLabel` — Label on the primary call to action. Default: `Talk to us`.
- `ctaHref` — Where the primary call to action points. Default: `/contact`.
- `projectName` — The npm package name of the generated project. Used in the front-end tree this package carries. Default: `my-shio-site`.

## What it provisions

- 8 post type(s)
- 2 content document(s)
- 14 front-end file(s) for you to write

---

Published by Viglet for [Viglet Shio](https://github.com/openviglet/shio).
