# Rendering, themes and design tokens | Viglet Shio

> Pages resolve through layouts and regions to a shared section vocabulary, and a theme carries its design tokens in the W3C DTCG shape that Style Dictionary, Figma and Tokens Studio already export, so the commonest change to a site is a reviewable field edit rather than a stylesheet rewrite.

Canonical: https://shio.viglet.org/features/rendering

---

# A site can exist before a front end does

The built-in renderer is not a competitor to your Next.js app: it is what makes a draft previewable, an agent's work checkable and a replica servable on the day it is captured. A page resolves through a layout and its regions to sections from a vocabulary the agent, the console and the front end all share.

[Read the docs](https://docs.viglet.org/shio/) [The ten laws](/#laws)

## One vocabulary, three consumers P8

A page is an ordered list of known sections rather than an ad-hoc content model per site. That is what lets an agent compose a page it has never seen the design of, a console render an editor for it without configuration, and a front end import the matching components from a published package.

## A theme's tokens are declared data, in a vocabulary that was adopted rather than invented P5

A theme carries its tokens in the W3C Design Tokens Community Group shape, the same thing Style Dictionary, Figma and Tokens Studio already export, so a designer's file pastes in and no dialect is invented for an agent to learn. They compile to custom properties on :root and are prepended to the theme's own CSS, so every existing layout gets tokens without being edited; shipping them behind a separate template handle would have shipped the feature switched off. The same values are also a dotted map for the places var() cannot reach.

Theme.TOKENS, and what it compiles to

```
{ "color": { "accent": { "$value": "#0b5" } } }

/* prepended to the theme CSS */
:root { --color-accent: #0b5; }

{{! and for where var() cannot reach }}
{{theme.tokens.color.accent}}
```

## Why that matters: the commonest change stops being a stylesheet rewrite P7

The accent colour, the type scale, the density: these are what actually change about a site, and as raw CSS each one is a diff a curator cannot review and an agent cannot make safely. As declared fields they are a reviewable edit with a name. Raw CSS stays as the escape hatch rather than the only door, and a theme with no tokens emits nothing at all rather than an empty block, because the render digest is over exactly those bytes.

## A capture reads tokens too, and says which ones are real P9

Replication runs the argument backwards: a source's stylesheet contains its palette, its type scale and its spacing rhythm, so a conversion that concatenates the file into CSS throws all of it away and the replica looks right but cannot be changed. Eight groups are read (colour, font family, font size, font weight, spacing, radius, border width and shadow), and the report distinguishes two kinds honestly. A declared custom property is the strong case: the source's own CSS already says var(), so changing the token changes the replica. A recurring literal is weaker: writing #0b5 twenty-three times is the accent colour, and naming it is how a curator learns the palette exists, but nothing references the name until somebody rewires the CSS.

## What it deliberately will not do P7

Rewrite those twenty-three literals into var() calls across a stranger's stylesheet. This scans CSS; it does not parse it into a model it could safely rewrite. A search-and-replace over somebody else's bytes, one of them inside a content: string or a data URI, breaks the replica in a way no digest catches. A token whose name would not round-trip back to the property the source actually wrote is reported rather than written, because nothing gets guessed into a file nobody reviewed.

## Next

- [Replicate an existing site](/replicate)
- [Delivery](/features/delivery)
