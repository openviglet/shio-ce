# Drive Shio from Claude Code — the plugin, the MCP bridge | Viglet Shio

> Hand a Shio CMS instance to Claude Code in one command: the plugin (MCP server, skills, slash commands, AGENTS.md fragment) or a bare stdio bridge, the three calls a session opens with, and the AGENT token scope — which writes on the agent surface only and is deliberately not a superset of a write key.

Canonical: https://shio.viglet.org/claude-code

---

# Hand the CMS to Claude Code in one command

Shio is built to be operated by a coding agent, so the distance between running an instance and having the agent do something is the number that matters. It is one install and three calls — and the first call is the instance telling the agent what it can do.

Install it The credential it runs on

## Two ways in, and the second needs no plugin

The plugin is the shortcut: it arrives with the MCP server wired up and the workflows already written. Everything it does is reachable without it.

### AThe plugin

claude — the marketplace route

```
claude plugin marketplace add openviglet/shio
claude plugin install shio

# then point it at your instance
export SHIO_URL=http://localhost:2710      # the default
export SHIO_USER=admin
export SHIO_PASSWORD=...
```

The plugin's MCP server runs the CLI's own stdio bridge through npx, so there is nothing else to install.

### BThe bare bridge

any MCP client

```
# No plugin, any MCP client — the CLI is
# the stdio bridge.
claude mcp add shio -- npx -y @viglet/shio mcp

# POST /mcp — JSON-RPC 2.0, revision 2025-06-18.
# GET /mcp is a deliberate 405: this server
# sends nothing unprompted.
```

Same server, no marketplace. You get the eleven tools and six resources and none of the skills or commands — which is the right trade if you are wiring Shio into something that is not Claude Code.

## A session that starts already knowing Shio

Instead of spending its first ten calls discovering the instance. The skills load when the work calls for them rather than on every turn — a schema you pay for each turn is a schema you pay for whether you use it or not.

### Skills

**shio-site**

Building and changing pages — addressing, apply, draft-then-publish, moves

**shio-content-model**

Post types and widgets as code — pull/push, the DSL, the traps

**shio-verify**

Checking work before handing it over — the lint's severities, digests, incidents

### Commands

**/shio-start [site]**

Reads the instance — model, sitemap, blueprints, lint state — and stops

**/shio-blueprint <name> <site>**

Plans a blueprint, asks, applies, reports the verification

**/shio-check [site]**

Verifies and reports errors, warnings and not-checked separately

### Project instructions

**AGENTS.fragment.md**

Paste into your project's AGENTS.md so the conventions survive a session without the plugin

## What a session actually opens with

Three calls, in this order, whether the agent came through the plugin or through a bare bridge. The first two are discovery and the third is the work.

- 1

Can this instance do what I need?

```
GET /agent/manifest?include=features,limits
```

Capabilities and limits. Unshipped ones read false, never absent; where a capability lives elsewhere, `elsewhere` names the command.

- 2

What is here, and how do I write to it?

```
GET /agent/context?include=all,manifest,ops
```

The content model, the sitemap, the conventions and every op with the keys it takes — plus a digest, so session N+1 can skip this.

- 3

Change something

```
POST /agent/batch  { dryRun: true, ops: [...] }
```

The plan first: what each op would change. Then the same document without dryRun — and it lands as a draft.

P2 The same three exist as MCP tools — shio_context, shio_write — and as resources a client can read directly: shio://manifest, shio://context, shio://ops.

## A scope of its own, and deliberately not a superset

An agent needs to write, and the two credentials that already existed were both wrong: one can patch live content outside the agent protocol's guards, and the other is every capability the account holder has, with no expiry.

| Scope | Reads | Writes |
| --- | --- | --- |
| READ | published content | nothing |
| PREVIEW | published + drafts | nothing |
| WRITE | published + drafts | the delivery API, including published content |
| AGENT | published + drafts | the agent surface only — /api/v2/agent/** and /mcp |

### The invariant this exists to hold

The agent path is never a privilege escalation — and since AGENT exists, it is not a privilege *superset* either. It reads like a preview token, because an agent works on drafts; it writes on /api/v2/agent/** and /mcp and nowhere else, so it cannot reach the delivery write path that patches published content directly. Tenant isolation and the content ACL apply identically on every surface. P7

## Four rules, all of them expensive to learn the other way

- Content is addressed by path, never by a UUID carried between calls.
- shio_apply before shio_write: a statement re-runs safely, a script does not.
- dryRun first, always. Read the plan — a delete line is a stop-and-ask.
- Writes land in DRAFT. Publishing is a separate, explicit step.

They are in the plugin so a session does not have to discover them, and in AGENTS.fragment.md so they survive a session that does not have the plugin.

### Two things Shio will not do

It hosts no model and runs no prompts. There is no provider API key in the CMS, no bundled inference and no "generate this page for me" button. Shio is the substrate your agent drives; the agent is yours, and so is the model behind it.

It does not make MCP the only door. Every capability lands on MCP, the CLI and REST — in that order, by law. A reader who does not use Claude Code loses the skills and the slash commands, and nothing else. P1

[claude-plugin/](https://github.com/openviglet/shio) in the repository is the source for everything on this page.
