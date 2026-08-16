# Viglet Shio — a complete CMS your agent can drive too

> An open-source, self-hosted headless CMS with four ways in: a full React console needing no agent at all, an MCP and CLI surface for coding agents, content projected to files for a repository workflow, and REST plus GraphQL delivery with TypeScript SDKs. Same content, same drafts, same publish button.

Canonical: https://shio.viglet.org/

---

# A complete CMS. Your agent can drive it too.

Write the pages yourself in the console, hand the work to Claude Code, keep the content as files in your repository, or read it all through REST and GraphQL. Four ways in, one content engine — and the same drafts, previews and publish button behind every one of them.

The agent path is what makes Shio unusual, not what makes it usable. Never attach one and nothing is withheld: it is an ordinary headless CMS, and it hosts no model, no prompts and no provider keys.

Find your way in [Use it without an agent](/console) [Docs](https://docs.viglet.org/shio/)

A full console — no agent required Drafts by default — nothing publishes itself Self-hosted, your database, open source

Create the site

● Content › Sites › New

a site, its root folder and its home page — nothing else required

Shape the model, or keep the one that shipped

● Content › Post types

fields, each drawn by one of fifteen widgets — no schema file to write

Write the launch page

● Content › acme › New › Page

a form built from the type — the same fields, drawn from the same model

Save it

● the sticky save bar

status DRAFT — the live site is unchanged, exactly as for an agent write

Look at it, and fix the headline where you can see it

● Preview · Universal Editor

the real rendered page, and the field edited on the page itself

Publish it, or schedule it

● Publish

an immutable snapshot beside the draft — or a date, and a sweep that fires it

Content › Sites

```
acme                    just now
  ├─ (root folder)
  └─ Home               DRAFT
 
or: Import a .zip export of a site you already have
```

Six screens. One page, published — and no agent involved.

## Pick the way you already work. It is the same CMS underneath.

These are not tiers, and not a migration path you commit to once. They are four surfaces over one content engine — the same posts, the same drafts, the same publish act — and a site can be worked on through all four in the same week.

### By hand, in the console

editors, marketers, anyone who has used a CMS before

Create the site, shape the content model, write the pages, upload the media, publish or schedule it, and add the rest of the team. No agent, no terminal, no YAML — a CMS behaving the way a CMS is expected to behave.

What it takes: a browser and a login

- React console
- Universal Editor
- Preview links

### With a coding agent

anyone who already works with Claude Code or another MCP client

Discovery in one call, content authored as files, blueprints applied as units, a render digest instead of a screenshot. The agent writes drafts and cannot publish them — which is what makes handing it write access reasonable.

What it takes: one command to attach it

- MCP
- shio CLI
- /api/v2/agent

### As files, in your repository

teams who would rather review content in a pull request

Pull the whole site to disk as front-mattered Markdown, edit it with the editor you already use, push it back through a three-way merge — and put shio apply --check in CI so drift fails a build instead of surprising somebody.

What it takes: the CLI and a repo

- shio pull / push
- shio apply --check
- Git

### Through the delivery API

front-end and platform engineers

Headless in the ordinary sense: REST and GraphQL, a TypeScript client with zero runtime dependencies, a React SDK, a generated Next.js starter, and a bridge that makes your own front end inline-editable.

What it takes: a token

- REST
- GraphQL
- @viglet/shio-client

The design laws below say every capability lands on the agent surface first. That is a rule about the order things are *built* in, so nothing ends up reachable only by a mouse — it has never been a rule about who is allowed to operate the CMS.

## Six shapes a real deployment takes. Only three involve an agent.

The first one is the case a headline about coding agents accidentally argues you out of, so it goes first: a team that wants a CMS, and gets one.

### A team that just wants a CMS

a marketing or comms team, no agent anywhere in sight

Someone creates the site, defines the types, and the team writes pages in a form and publishes them. Everything an editor touches is the console. The agent surface sits there unused, costing nothing — and the day somebody wants it, no content has to move.

- console

### A front end you wrote, content someone else owns

an engineering team with a Next.js app and non-technical editors

The delivery API feeds your application and the console is where the copy lives. Add the editor bridge and your own pages become inline-editable, so a reviewer fixes a headline on the real page rather than hunting for a field in a form.

- API
- console

### An agent does the first build; people keep it

a small team with a large site to stand up

The agent applies a blueprint, writes forty pages and proves them against the lint — all as drafts. Then it stops being interesting: the people who maintain the site work in the console, and the agent comes back only for the next bulk job.

- agent
- console

### Content reviewed like code

a docs or product team already living in pull requests

The site projects to Markdown in your repository, changes arrive as a diff a reviewer can read, and CI runs the drift check and the content lint before a merge. Publishing stays a separate, deliberate act on the instance.

- files
- console

### An old site that has to become an editable one

an agency, or whoever inherited the site nobody can change

Capture the existing site under robots.txt, review what the crawl proposes, convert it into drafts, and prove by arithmetic that nothing was lost. What you get at the end is content in a model — not a screenshot with a CMS behind it.

- agent
- console

### Many sites, one instance

a platform team serving several brands or clients

Tenant isolation reaches every surface, including the agent's. Scoped API tokens, roles and groups, webhooks on publish, and an activity log that says who changed what — whether the who was a person or a credential you issued.

- console
- API
- agent

## The person creates and decides. The agent builds, if there is one. The API delivers.

Three seats over one content engine, each with the surface it is actually good at — and any of them can be empty.

### The person creates, and decides

Sites, content models, folders, pages, media, publishing, scheduling, the rest of the team — all of it in the console, and none of it needing an agent to have happened first. When there is an agent, this seat also holds the approve button.

- React console
- Universal Editor
- Preview links

### The agent builds — if you want one

Discovers the model in one call, authors content as files, applies a blueprint, renders a preview and proves the result — without a browser, a cookie or a click. Its writes are drafts, and its credential cannot publish them.

- MCP
- shio CLI
- /api/v2/agent

### The delivery API delivers

A framework-agnostic delivery API — REST and GraphQL — with TypeScript SDKs, a React SDK and a Next.js starter that is generated rather than copied. It serves whatever the other two seats agreed on.

- REST
- GraphQL
- @viglet/shio-client

One person can hold all three. Most instances start that way: somebody creates the site, writes the pages and points a front end at them, and no agent is ever issued a token. The seats describe what a surface is *for* — not a staffing requirement.

## Ten laws. A feature that breaks one is wrong even if requested.

They are not marketing copy. They are checked into the repository as the rule every contributor and every agent works under, and each one below has a section on this page that shows it rather than claims it.

They govern how the product is *built* — what a feature must reach before it can ship. None of them is a condition on how you use it: a team that never attaches an agent gets every capability the ten laws forced into existence.

- P1 Agent-first design order Every capability lands MCP → files/CLI → REST → console. A console-only feature is incomplete — and the order is about what may not be skipped on the way to shipping, never about who is allowed to operate the CMS.
- P2 One call replaces a session Discovery is a product feature — a manifest and a context pack — not a documentation problem.
- P3 Tokens are a measured budget Response budgets plus a CI benchmark. A token regression fails the build like any other test.
- P4 Files beat APIs for authoring Content is projected to disk, because Edit, Write and Grep are an agent's cheapest tools.
- P5 Determinism over cleverness Stable ordering, path addressing, idempotent writes, byte-identical serialization.
- P6 Errors are instructions Every 4xx carries fix, allowed, didYouMean and example — so the retry is the next call, not the next session.
- P7 Never surprise the curator Draft-default, dry-run, explicit publish, confirm tokens, attribution, a review queue.
- P8 Skipping steps needs appliable units Blueprints — a package that applies — instead of a recipe written in prose.
- P9 Close the perception loop Cheap textual proof — a lint, the routes, a render digest — instead of asking someone to look.
- P10 Compose, don't fork MCP is a shape over the delivery API and the console services, never a third contract.

[agents.md](https://github.com/openviglet/shio/blob/HEAD/agents.md) · [the concept spec (SH74)](https://github.com/openviglet/shio/blob/HEAD/docs/specs/SH74-agent-native-cms.md)

## Six capabilities, reachable from every door

Each of these got its CLI verb and its MCP tool before it got a console screen — which is the design order, not a restriction. What a capability is reachable from is a separate question, and the answer is: all four ways in.

[The agent gateway MCP over the same services the console uses, a manifest that answers first, and a context pack that ends the discovery session. See it](/features/agent-gateway) [Content as files The whole site projected to disk with a three-way merge behind it, so authoring is Edit and Write rather than a REST call per field. See it](/features/content-as-files) [Blueprints Appliable units instead of prose recipes — post types, folders, content and carried files, converged in one transaction. See it](/features/blueprints) [Render and prove Pages, layouts, regions and a section vocabulary — with a digest, a lint and an audit that make a page checkable without a screenshot. See it](/features/rendering) [Replication Point it at a site that already exists and get one a curator can edit — capture, convert, prove. See it](/replicate) [Delivery REST and GraphQL, a zero-dependency TypeScript client, a React SDK and a generated Next.js starter. See it](/features/delivery)

## Discovery is a feature, and it has a price

Most CMSs make an agent crawl a REST surface to learn what exists. Shio answers that in one call — and the cost of every answer is a ceiling the build refuses to exceed.

the whole discovery session

```
# One call. The model, the sitemap,
# the conventions and the write vocabulary
# — plus a digest, to skip it next time.

GET /api/v2/agent/context?include=all,manifest,ops

# Or, from a client that only speaks MCP:
shio://context
```

The response carries a digest. Session N+1 sends it back and is told nothing changed, which turns "re-read the context" from a decision an agent has to make into a free default. P2

### The same job, over an API designed for a browser

Each task is benchmarked twice — once on the agent surface, once on the id-keyed REST path an agent would otherwise have to drive. The build asserts the agent path stays *at least* this much cheaper.

| - | On the agent surface | Cheaper than REST by |
| --- | --- | --- |
| Task | Calls | Tokens | Calls | Tokens |
| --- | --- | --- | --- | --- |
| Build a marketing site | 6 | 3,800 | 3× | 2× |
| Add a type and ten posts | 3 | 2,100 | 3.6× | 3× |
| Translate a site | 3 | 800 | 2.6× | 4.5× |
| Fix a broken link | 3 | 400 | 2× | 10× |

Those last two are floors the suite enforces, not the best number anyone has seen — a falling ratio means the baseline improved or the protocol regressed, and both are worth knowing.

### The ceiling on what a call may cost

Not a best case — a limit. A response that grows past one of these fails the build the same way a broken test does.

Capability check 390

manifest?include=features,limits — what a session opens with

response.manifest.check

Full manifest 2,650

every capability, every limit, a curated endpoint index

response.manifest

Every MCP tool schema 2,500

tools/list, re-sent on every turn before any work happens

mcp.tools.list.total

Build a site, end to end 3,800

the whole task, measured to the verify — not to a page a person opened

benchmark.build-marketing-site.tokens

P3 Every number on this page is generated at build time from shio-app/src/test/resources/token-budgets.properties — the one file the test suite asserts against. A renamed key fails this build rather than quietly dropping a bar, because a figure on a marketing page that has drifted from the build is worse than no figure.

## An agent's cheapest tools are Edit, Write and Grep

So the site is projected to disk. Pull it, edit it with the tools the agent already has, push it back — with a three-way merge underneath, because the instance moved while you were working.

shio pull --content

```
shio/
├─ post-types/
│  ├─ Page.json                 the model, as code
│  └─ Article.json
├─ content/
│  └─ acme/
│     ├─ index.md               post:acme/          the home page
│     ├─ launch.md              post:acme/launch
│     └─ blog/
│        └─ hello-world.md      post:acme/blog/hello-world
├─ assets/
│  └─ acme/img/hero.png
└─ .shio/
   └─ content-base.json         the fingerprint the 3-way merge reads
```

shio/content/acme/launch.md

```
---
postType: Page
title: Launching Shio 2026.3
status: DRAFT
folder: folder:acme/
---

An open-source headless CMS with four ways in: the console,
an agent, files in a repository, and the delivery API.
```

### One address grammar, everywhere P5

The same four forms in the CLI, over REST and over MCP. Writes take only the first two, because an id is not a place anyone can name.

**post:<site>/<friendly-url>**

a post — and post:acme/ is the home page

**folder:<site>/<name-chain>**

a folder, by the names a person reads

**site:<name>**

the site itself

**id:<uuid>**

when you already have the id — reads only

P5 Stable ordering, path addressing, idempotent writes and byte-identical serialization — so pulling twice produces the same bytes, and a diff means somebody changed something.

## Eleven tools, six resources, and no second contract

MCP is a shape over the delivery API and the console services — never a parallel semantic. Whatever the agent can do here it can also do from the CLI and over REST, in that order, by law.

### POST /mcp

shio_context

model, sitemap and conventions in one call

shio_find

search the tree by address, type or term

shio_read

one post, one folder, one schema

shio_write

a batch of ops — upsert, move, delete

shio_apply

converge to a document, or to a blueprint

shio_publish

the separate, explicit act

shio_assets

binaries in and out of the media library

shio_changes

what moved since a cursor

shio_verify

the lint, and optionally the route proof

shio_digest

one page's structure, as text

shio_remember

what session N leaves for session N+1

shio_marketplace

packages this instance could install

#### Resources

- shio://manifest
- shio://context
- shio://ops
- shio://blueprints
- shio://schema/{postType}
- shio://blueprint/{name}

P10 Hand-rolled rather than pulled from a vendor SDK, and the reason is written down with a date on it — the premise is re-checked on a schedule and a test fails the build when it expires. [modelcontextprotocol.io](https://modelcontextprotocol.io)

### $ shio <verb>

The same capabilities where an agent already has a shell.

**shio init**

scaffold a front end, or apply a blueprint

**shio pull / push**

the model and the content, as files

**shio apply**

a desired-state document; --check is the CI drift guard

**shio verify**

the content lint; --delivery adds the route proof

**shio digest**

a page's structure, cheap enough to read every turn

**shio audit**

the browser as an instrument — overflow, contrast, dead requests

**shio snapshot**

a PNG, for whoever has to look

**shio clone**

capture an existing site, writing no content

**shio report**

the handoff — what changed, with a preview link each

**shio remember**

the instance memory, so the next session is cheaper

P1 A capability the console has and the agent does not is an unshipped feature. Where something genuinely lives elsewhere, the manifest says so by name instead of reporting false and letting a client guess.

## A 400 that costs one retry, not one session

An agent that gets Bad Request and nothing else does the expensive thing: it goes back and re-reads documentation, or it guesses. Both cost more than the call did. So every 4xx on the agent surface carries the fix in the body.

**title / detail**

what went wrong, in words the caller can log

**didYouMean**

the near miss, when the mistake was a typo

**allowed**

the closed set, so the next call is a choice not a guess

**fix**

the instruction — what to do instead, in one sentence

**example**

a call that would have worked, ready to send

P6 The same rule applies to the CLI: a refusal that teaches nothing is treated as a defect and gets filed like one.

400 — and what to do about it

```
{
  "status": 400,
  "title": "Unknown post type 'Artcile'",
  "detail": "No post type by that name exists on site 'acme'.",
  "didYouMean": ["Article"],
  "allowed": ["Page", "Article", "Author", "File"],
  "fix": "Use one of 'allowed', or create the type first with post-type.upsert.",
  "example": {
    "op": "post.upsert",
    "address": "post:acme/blog/hello-world",
    "postType": "Article"
  }
}
```

## The agent cannot see the page. So the page describes itself.

Asking someone whether it looks right is the round trip that makes an agent slow. Four instruments replace it — three of them text, and the fourth deliberately for a person.

shio verify

### The content lint

Broken references, undeclared fields, a field a template reads that no type declares. Exits 1 on an error; --delivery adds a proof that the route actually answers.

shio digest

### The page, as text

One page's structure — regions, sections, what each resolved to — cheap enough to read after every edit instead of asking somebody to look.

shio audit

### The browser as an instrument

Renders at each width and prints findings, not a picture: horizontal overflow reported where it is introduced, contrast, collapsed boxes, failed requests, console errors.

shio snapshot

### A picture, for a person

The one output that is deliberately for a person. A per-pixel diff against a baseline, and a draft is stamped as a draft because the image cannot say so itself.

the proof, as text

```
$ shio verify --delivery

  ok    post:acme/            200  layout Home  4 regions resolved
  ok    post:acme/launch      200  layout Page  hero, prose, cta
  warn  post:acme/launch      hero image has no alt text
  ok    post:acme/blog/hello  200  layout Article

  4 checked, 0 errors, 1 warning   exit 0
```

P9 A warning exits 0 on purpose. A gate that fires on something a designer signed off is the exit code everybody wraps in || true, and then the errors stop being read too. --strict is there for a project that decided otherwise.

The warnings do not vanish either — shio report restates them as open questions in the handoff a curator reads.

## An agent with write access to your site. What stops it?

Six mechanisms, not a policy document. Every one of them is on by default, and none of them is a setting an eager script can turn off on its way past.

### Draft by default

A write lands as a draft. Publishing is a separate, explicit act with its own op — there is no flag that quietly does both.

### Dry run first

Every batch can be planned instead of applied. The plan is the same document, annotated with what each op would change.

### Confirm tokens

A destructive op is refused once with a token, and accepted only when the token comes back — so no single call deletes anything.

### Attribution on every write

The record says which agent wrote it and when. A curator reviewing a change never has to guess where it came from.

### A queue, not a firehose

Changes arrive in a review queue with a preview link each, plus the verify warnings restated as open questions.

### Nothing is gone

Deletes land in the trash with untrash and purge as separate acts, and the file projection keeps a fingerprint for the three-way merge.

P7 And the boundary that is not a setting at all: Shio hosts no model, runs no prompts and holds no provider keys. There is no inference inside the content engine to misfire.

[A curator’s Tuesday, and the reason behind each gate](/curator)

## A recipe is prose. A blueprint applies.

Everything an agent is told to do in a tutorial is something it could instead be handed as a unit: post types, folders, content and the files a front end needs, converged in one transaction.

- 01

### List what applies

```
shio blueprints
```

the catalogue, with the parameters each package takes

- 02

### Apply one

```
shio apply --blueprint corporate --param brand=Acme --site acme
```

post types, folders, content and carried files, in one transaction

- 03

### Or scaffold from it

```
shio init --blueprint corporate --site acme
```

the front end and the content half in the same command

P8 An apply is idempotent and can be planned first, so running it twice is not a mistake and running it once is not a leap of faith.

## Point it at a site you already have

Not a mirror — a site a curator can edit. The capture reads the pages, the conversion derives the content model from them, and the proof says whether the replica serves what the source did.

### Capture

```
shio clone https://example.com
```

walks one origin under robots.txt and writes an inventory — pages, assets, locales, forms, navigation, third-party scripts — and no content at all.

### Convert

```
shio convert --site example
```

derives post types from the pages themselves, proposes them for review, and turns the capture into content a curator can edit.

### Prove

```
shio verify --delivery && shio audit /
```

the replica answers its own routes, and the audit says whether the page a reader gets is the page you meant.

### The bounds, because they are the point

One origin, and every off-host link recorded rather than followed. robots.txt is obeyed, and a capture taken with --ignore-robots records that in the inventory — so it can never later be mistaken for one taken with permission. A ceiling marks the capture PARTIAL: there are no silent caps, because a bounded capture read as a complete one is the failure the whole thing is built to prevent. And the capture writes *no content at all*, so the conversion you are asked to review does not already exist.

[The four verbs, the two modes, and what the crawl refuses](/replicate)

## Headless where it counts: the front end is yours

REST and GraphQL, a zero-dependency TypeScript client, a React SDK, a shared section vocabulary and a Next.js starter that is generated rather than copied out of a tutorial.

the delivery client

```
import { createShioClient } from "@viglet/shio-client";

const shio = createShioClient({
  url: "https://cms.example.com",
  token: process.env.SHIO_CDA_TOKEN,
});

// Zero runtime dependencies — Node, browser, edge, server components.
const page = await shio.post("acme", "launch");
```

npm create @viglet/shio-app

Scaffolds a Next.js App Router site already wired to a site's content — and with --blueprint, its content half in the same command.

- [@viglet/shio-client Framework-agnostic TypeScript client for the delivery API. Zero runtime dependencies — Node, browser, edge, server components.](https://www.npmjs.com/package/@viglet/shio-client)
- [@viglet/shio-react-sdk Hooks and render components over the same core.](https://www.npmjs.com/package/@viglet/shio-react-sdk)
- [@viglet/shio-sections The page-section vocabulary — one shared language for the agent, the console and the front end.](https://www.npmjs.com/package/@viglet/shio-sections)
- [@viglet/create-shio-app Generates a Next.js App Router site already wired to a site's content.](https://www.npmjs.com/package/@viglet/create-shio-app)
- [@viglet/shio-editor-cors The Universal Editor bridge — inline editing on any front end that emits the data attributes.](https://www.npmjs.com/package/@viglet/shio-editor-cors)
- [@viglet/shio The CLI. Also the MCP stdio bridge: claude mcp add shio -- shio mcp.](https://www.npmjs.com/package/@viglet/shio)

## Every CMS has an API. Few were designed for the caller.

The axis is agent-operability, not feature count. On everything else — an ecosystem, hosted scale, an editor everyone already knows — the alternatives are strong, and pretending otherwise would make this table worthless.

| Capability | Shio | Headless SaaS CMS | Git-backed / DIY |
| --- | --- | --- | --- |
| One call replaces discovery | yes | no | not applicable |
| MCP server, first-class | yes | partial | build it |
| Content addressable as files | yes | no | yes |
| 4xx bodies carry the fix | yes | no | not applicable |
| Dry run before every write | yes | partial | git diff |
| Draft-default + review queue | yes | yes | pull request |
| Token cost measured in CI | yes | no | no |
| Textual render proof | yes | no | build it |
| Capture an existing site | yes | no | build it |
| Self-host, your database | yes | no | yes |

The honest summary is one row: everywhere else an agent is a client of an API designed for a browser, and the protocol quality it gets is whatever fell out.

[The full matrix, named products, and where Shio loses](/compare)

## Your infrastructure, your content, your call

Nothing here phones home, and there is no hosted tier you are being funnelled towards. Clone it, read it, run it.

### Spring Boot 4, Java 21

One JVM service. The content engine, the agent gateway, the MCP server and the renderer are the same process — nothing to orchestrate on day one.

### Your database

The schema is Liquibase's. H2 out of the box for a trial; PostgreSQL and MariaDB are proved on every release by containerized integration tests.

### Multi-tenant, if you need it

Tenant isolation reaches every surface, including the agent's. The agent path is not a privilege escalation — the same scopes apply on all of them.

docker-compose.yaml

```
services:
  shio:
    image: ghcr.io/openviglet/shio-ce:2026.3
    ports:
      - 2710:2710
    volumes:
      - ./volumes/shio/store:/app/store
    environment:
      SPRING_DATASOURCE_URL: jdbc:mariadb://shio-mariadb:3306/shio
      SPRING_DATASOURCE_USERNAME: shio
      SPRING_DATASOURCE_PASSWORD: shio
```

Then hand it to the agent:

The bridge speaks stdio, so it works from any MCP client — and the agent's first call is the manifest, which tells it everything this particular instance can do.

## Read it before you run it

The design is written down — including the parts that are unfinished, and the ones that were deliberately not built.

[Documentation Install, model, author, deliver — the end-user documentation set.](https://docs.viglet.org/shio/) [The CLI on npm@viglet/shio — init, pull, push, verify, clone, and the MCP bridge.](https://www.npmjs.com/package/@viglet/shio) [The concept spec SH74 — the agent-native CMS: the protocol design, the tool surface and a worked example.](https://github.com/openviglet/shio/blob/HEAD/docs/specs/SH74-agent-native-cms.md) [Roadmap and changelog The open backlog and the shipped ledger, both in the repository.](https://github.com/openviglet/shio/blob/HEAD/docs/ROADMAP.md)
