# Content as files — the projection and the three-way merge | Viglet Shio

> The whole site projected to one Markdown file per post, with a three-way merge back. The path is the URL, only the draft projects, losslessness beats prettiness, and the field set is a table with a test — so a key the format drops is declared with a reason rather than discovered later.

Canonical: https://shio.viglet.org/features/content-as-files

---

# Authoring with the tools the agent already has

Edit, Write and Grep cost an agent almost nothing, and a REST call per field costs it a turn. So the site projects to disk: one Markdown file per post, pulled, edited with ordinary tools and pushed back through a merge that knows the instance moved while you were working.

[Read the docs](https://docs.viglet.org/shio/) [The ten laws](/#laws)

## One file per post, and the path is the URL P4

YAML frontmatter for the metadata and the fields, and the post's first rich-text field as the document body — with the file recording which field that was, so reading it back never needs the model. A URL is unique per site so the tree cannot collide, and the folder travels in frontmatter because the two namespaces are deliberately separate. A file whose path and url disagree is an error, not a guess: a half-done rename is a move on one side and a create on the other.

shio/content/acme/launch.md

```
---
postType: Page
title: Launching Shio 2026.3
status: DRAFT
folder: folder:acme/
bodyField: content
---

An open-source headless CMS with four ways in.
```

## The field set is a table with a test P5

Ten keys travel, and everything a post carries that the projection drops is declared with a reason in a test. That table exists because a round-trip guard can test the values of fields the format has and cannot see a field it lacks — so the thing that would otherwise be discovered by somebody losing content is an assertion instead.

## The merge happens in the projection's own domain P5

The base, the server side and the file side are all compared as the file tree holds them. Skipping that step was measured and it produced a permanent phantom change: a CRLF body read as a local edit on every pull, forever, and a drift check that failed on content nobody had touched. Fingerprinting the projected document alone is only half the fix — it converts the phantom into the opposite phantom.

## Only the draft projects, and publish is an instruction P5

A publish key in a file travels forwards as an intent; the merge deliberately never writes state backwards into it. And losslessness beats prettiness — a value that would not survive the round trip stays as JSON in fields rather than being prettified into the body it cannot come back from.

## Next

- [The agent gateway](/features/agent-gateway)
- [Blueprints](/features/blueprints)
