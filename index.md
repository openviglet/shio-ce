# Viglet Shio — the CMS whose operator is Claude Code

> An open-source, self-hosted headless CMS designed for a coding agent: MCP-native, one call replaces a discovery session, content lives as files, every 4xx carries the fix, and every write lands as a draft a curator approves.

Canonical: https://shio.viglet.org/

---

# The CMS whose operator is Claude Code.

Your agent builds the site. You approve it. Shio is a headless CMS designed backwards from that sentence — one call replaces a discovery session, content lives as files an agent can `Grep`, and every write lands as a draft with your name on the approve button.

Judged in agent cycles and tokens, not in clicks. Shio hosts no model and no prompts — it is the substrate your agent drives.

[Get started](https://docs.viglet.org/shio/) The ten laws

Drafts by default — nothing publishes itself Self-hosted, your database No model, no prompts, no keys in the CMS

> What is this instance, and what can I do to it?

● shio_context P2

model + sitemap + conventions + write vocabulary — 1 call, 1 digest to skip it next time

> Give me the site on disk

● shio pull --content P4

shio/content/** · 42 posts, 9 folders, front-mattered Markdown

> Write the launch page

● Edit shio/content/acme/launch.md P4

one file, one post — no API call to author with

> Push it back

● shio push --content P7

1 created · status DRAFT · nothing is live yet

> Prove it before a curator looks

● shio verify --delivery P9

ok — 0 errors, 1 warning: hero image has no alt text

> Hand it over

● shio report --since last P7

a Markdown summary with a preview link per change, and the warning as an open question

the handoff, as Markdown

```
## 1 change awaiting review - **Launching Shio 2026.3** - created  preview: /preview/acme/launch ### Open questions- The hero image has no alt text. Intentional?
```

One session. One page. Six calls, and you still decide.

## The agent builds. The curator approves. The API delivers.

Not one operator with a chat box bolted on — three, each with the surface it is actually good at.

### The agent builds

Discovers the model in one call, authors content as files, applies a blueprint, renders a preview and proves the result — without a browser, a cookie or a click.

- MCP
- shio CLI
- /api/v2/agent

### The curator approves

Approves, corrects and tweaks. Everything the agent wrote arrives as a draft with attribution on it, in a queue, with a preview link that opens the real page.

- React console
- Universal Editor
- Preview links

### The CDA delivers

A framework-agnostic delivery API — REST and GraphQL — with TypeScript SDKs, a React SDK and a Next.js starter that is generated rather than copied.

- REST
- GraphQL
- @viglet/shio-client

## Ten laws. A feature that breaks one is wrong even if requested.

They are not marketing copy. They are checked into the repository as the rule every contributor and every agent works under, and each one below has a section on this page that shows it rather than claims it.

- P1 Agent-first design order Every capability lands MCP → files/CLI → REST → console. A console-only feature is incomplete.
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

## Six surfaces, one operator

Each of these exists because a coding agent needed it, and each one has a CLI verb and an MCP tool before it has a console screen.

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

Shio is a CMS whose primary operator is a coding agent.
The curator approves. The delivery API delivers.
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
