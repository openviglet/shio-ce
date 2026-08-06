# Blueprints — appliable units instead of prose recipes | Viglet Shio

> A section of a site the instance can apply: a content model, a folder tree, sample pages, the parameters that make it somebody's, and the promise it keeps about what exists afterwards. A package may not name its own site and may not prune, substitution is one form and nothing else, and everything is validated at load.

Canonical: https://shio.viglet.org/features/blueprints

---

# A recipe is prose. A blueprint applies.

Everything a tutorial tells an agent to do is something it could instead be handed as a unit. A blueprint is a content model, a folder tree, sample pages, the parameters that make it yours — and a promise about what exists when it finishes.

[Read the docs](https://docs.viglet.org/shio/) [The ten laws](/#laws)

## Nothing in the format is a new serialization P10

The post types are the same bytes the CLI already writes, the content files are the same desired-state documents apply already takes, and the front-end sources are ordinary files. That is what keeps a blueprint from becoming a third contract with its own semantics to learn and its own bugs to find.

apply a package

```
shio blueprints                       # the catalogue and its parameters
shio apply --blueprint corporate \
  --param brand=Acme --site acme      # or --dry-run first
```

## A package may not name its own site, and may not prune P7

The site is the caller's, so a site key inside a package is refused at load rather than ignored — an ignored key looks like it worked. And prune's blast radius depends on what an author forgot to mention, which is an unacceptable thing to inherit from a package the user did not write.

## Substitution is one form and nothing else P5

No conditionals and no expressions, so the same parameters always produce the same site. An unknown parameter is a teaching 400 rather than a silent no-op. And a malformed package answers 409, not 400 — nothing the caller sent caused it, and an error that blames the caller for the author's mistake sends them looking in the wrong place.

## The model is provisioned, never upserted P8

An existing post type of the same name is left exactly as it is — including a field a human added — and the response names the fields it lacks instead of overwriting them. A plan writes nothing and needs no write transaction, so looking before you write works on a read-only credential.

## Next

- [Content as files](/features/content-as-files)
- [Rendering and themes](/features/rendering)
