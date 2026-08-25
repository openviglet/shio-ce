# Delivery: REST, GraphQL and the TypeScript SDKs | Viglet Shio

> Headless where it counts: a framework-agnostic delivery client with zero runtime dependencies, a React SDK over the same core, the shared section vocabulary, a generated Next.js starter and a bridge that makes any front end inline-editable.

Canonical: https://shio.viglet.org/features/delivery

---

# Headless where it counts: the front end is yours

The content engine is a JVM service and nothing you build has to know that. What reaches your application is HTTP, a typed client with no runtime dependencies, and components you can take or leave.

[Read the docs](https://docs.viglet.org/shio/) [The ten laws](/#laws)

## A client that runs wherever your code does

Zero runtime dependencies, which is a constraint rather than a boast: it is what lets the same package work in Node, in a browser, on an edge runtime, in a server component and in a plain script, and what keeps a CMS client from dragging a dependency tree into your bundle.

@viglet/shio-client

```
import { createShioClient } from "@viglet/shio-client";

const shio = createShioClient({
  url: "https://cms.example.com",
  token: process.env.SHIO_CDA_TOKEN,
});

const page = await shio.post("acme", "launch");
```

## The starter is generated, not copied P8

A Next.js App Router site wired to a real site's content, produced by a generator rather than pasted out of a tutorial. With a blueprint it brings the content half in the same command, so what you get on the first run is a site with pages in it.

one command

```
npm create @viglet/shio-app
# or, with the content:
shio init --blueprint corporate --site acme
```

## Inline editing on a front end you wrote

The renderer annotates what it renders, and a published bridge package does the same job for markup you produce yourself. Once a page emits the annotations, a curator clicks the headline on the real page and edits the field that produced it, on the draft, with the same safety as every other write.

## A token scope per job P7

Read for published content, preview for drafts, write for the editing path, and a separate agent scope that reads like preview and writes only on the agent surface. They are four scopes rather than a hierarchy on purpose: the agent's credential is deliberately not a superset of the one that can patch published content.

## Next

- [Rendering and themes](/features/rendering)
- [The curator’s half](/curator)
