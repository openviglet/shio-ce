# The agent gateway: manifest, context pack, batch | Viglet Shio

> The namespace shaped for a coding agent rather than a browser: a manifest that reports unshipped capabilities as false and says where a capability lives when it lives elsewhere, a context pack that replaces the discovery session, a write vocabulary you can read before writing, and 4xx bodies that carry the fix.

Canonical: https://shio.viglet.org/features/agent-gateway

---

# A namespace shaped for a caller that cannot click anything

Everything here is a shape over the delivery API and the console services, never a parallel semantic. What makes it a gateway rather than a second API is that it answers the questions a browser never has to ask: what can you do, what is here, and what did I just get wrong.

[Read the docs](https://docs.viglet.org/shio/) [The ten laws](/#laws)

## The manifest answers first, and answers honestly P2

A capability that has not shipped is reported false rather than omitted, because an absent flag sends a caller probing, which is the exact cost the manifest exists to remove. And where a capability genuinely lives somewhere else, an elsewhere map names the command instead: reporting false for a screenshot reads as not possible, when the truth is possible, from the CLI.

the cheapest read on the surface

```
GET /api/v2/agent/manifest?include=features,limits

# At most 390 tokens, a ceiling the build enforces. The
# full document's is 2820, and the difference is
# the reason this projection exists.
```

## One call for the model, the sitemap and the conventions P2

The context pack is the discovery session collapsed into a response, and it carries a digest. Session N+1 sends the digest back and is told nothing changed, which turns re-reading the context from a decision an agent has to make into a free default. Ask for the write vocabulary in the same call and every op arrives with the keys it takes.

the whole of discovery

```
GET /api/v2/agent/context?include=all,manifest,ops
```

## A batch can be planned before it is applied P7

The plan is the same document as the write, annotated with what each op would change, not a summary in a different shape, because two shapes drift. A destructive op is refused once with a confirm digest over exactly those deletions, so the second call cannot quietly cover more than the first one showed you.

look, then write

```
POST /api/v2/agent/batch
{
  "dryRun": true,
  "ops": [
    { "op": "post.upsert",
      "address": "post:acme/launch",
      "postType": "Page",
      "fields": { "title": "Launching Shio" } }
  ]
}
```

## A wrong call costs one retry, not one session P6

Every 4xx carries the fix in the body: what was wrong, the near miss if the mistake was a typo, the closed set of what is allowed, an instruction, and a call that would have worked. An agent that gets Bad Request and nothing else does the expensive thing: it re-reads documentation, or it guesses.

## Next

- [Drive it from Claude Code](/claude-code)
- [Content as files](/features/content-as-files)
