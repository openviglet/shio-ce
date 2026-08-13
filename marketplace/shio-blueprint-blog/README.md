# Blog

An Article post-type, a /blog folder and three published sample posts. The starting point for anything with a feed: the model is the part that is tedious to get right, and the samples show the field usage a later session should match.

## Install

```
shio marketplace install shio-blueprint-blog
```

Then apply it to a site. Applying is a separate step: installing puts the package where
this instance can see it, and nothing is written to your content until you apply it.

## Parameters

- `blogTitle` — The blog's name, used in the sample copy. Default: `Blog`.
- `authorName` — Byline on the sample posts. Default: `Editorial`.
- `projectName` — The npm package name of the generated project. Used in the front-end tree this package carries. Default: `my-shio-site`.

## What it provisions

- 1 post type(s)
- 1 content document(s)
- 14 front-end file(s) for you to write

---

Published by Viglet for [Viglet Shio](https://github.com/openviglet/shio).
