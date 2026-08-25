# Shio vs Contentful, Sanity, Strapi and WordPress | Viglet Shio

> An honest comparison on the axis where headless CMSs actually differ: agent-operability. Eighteen checkable questions grouped by the design law each comes from, plus what Contentful, Sanity, Strapi and WordPress are genuinely better at and when to pick them instead.

Canonical: https://shio.viglet.org/compare

---

# Every CMS has an API. Few were designed for the caller.

Comparing content types and delivery APIs produces a tie, because everyone has those. The axis where the products actually differ is agent-operability — and every row below is a question with an answer you can test rather than a feature you can be told about.

The matrix Where Shio loses

## Ten laws, turned into eighteen questions

Grouped by the law each one comes from, so what you are looking at reads as one design position applied repeatedly rather than as a feature list that happens to be long.

| Capability | Shio | Contentful | Sanity | Strapi | WordPress |
| --- | --- | --- | --- | --- | --- |
| P2Discovery — what does the agent's first call cost? |
| --- |
| One call returns the model, the sitemap and the conventions | yes | compose several | compose several | compose several | compose several |
| A machine-readable capability manifest, with unshipped ones reported false | yes | no | no | no | no |
| A digest so a later session can skip re-reading it | yes | no | no | no | no |
| The manifest routes an intent to the one call, instead of listing everything | yes | no | no | no | no |
| P4Authoring — can the agent use its cheapest tools? |
| --- |
| The whole site projected to files, with a three-way merge back | yes | export only | export only | no | no |
| Path addressing — no UUID carried between calls | yes | partial | partial | partial | partial |
| Idempotent desired-state apply (converge, don't script) | yes | build it | build it | build it | build it |
| P6Failure — how expensive is a wrong call? |
| --- |
| Every 4xx carries fix, allowed, didYouMean and example | yes | no | no | no | no |
| Every capability reachable without a browser session | yes | partial | partial | partial | partial |
| P7Safety — what stops a wrong write? |
| --- |
| Dry run: the plan before the batch, as the same document | yes | no | no | no | no |
| A confirm token on a destructive op | yes | no | no | no | no |
| Draft-default and a review queue | yes | yes | yes | yes | yes |
| P9Proof — can the agent check its own work? |
| --- |
| A textual render digest of a page's structure | yes | no | no | no | no |
| A content lint that also proves the route answers | yes | no | no | no | no |
| P3Economy — is the protocol's cost a number? |
| --- |
| Response token budgets with a ceiling the build enforces | yes | no | no | no | no |
| Operations — whose infrastructure, whose source? |
| --- |
| Self-host on your own database | yes | no | no | yes | yes |
| Open source | yes | no | partial | yes | yes |
| Capture an existing site into an authorable one | yes | no | no | no | no |

How to read the other columns. They say whether the product *documents the property as a guarantee*, not whether some path to it exists. An export command is not a file projection with a three-way merge, and an MCP server in front of an API designed for a browser is not a protocol designed for an agent. Where the honest answer is "you can build it", the cell says so.

This reflects 2026.3 — verify against current vendor documentation before deciding. If a row here is wrong, it is a bug and we want the correction.

## Four products Shio does not beat

A table where one column wins every row is a table nobody believes. Here is what each alternative is genuinely better at, and the case where picking it over Shio is the right call.

### Contentful

The enterprise ecosystem — integrations, SLAs, a global CDN you do not operate, and an editor a marketing team already knows how to use.

Pick it instead when your buyer is procurement, the content team is large and non-technical, and nobody on staff wants to run a JVM.

### Sanity

The best structured-content editing experience in the category — real-time collaboration, a genuinely good query language, and a studio you shape to the model.

Pick it instead when editors are the primary operator and the depth of the editing experience is the thing you are buying.

### Strapi

The closest neighbour: open source, self-hosted, Node all the way down, and a plugin ecosystem that fits a JavaScript team's existing habits.

Pick it instead when your team is JS end to end, you want self-hosting, and you do not need an agent protocol — it is a shorter path to the same content API.

### WordPress

A plugin for everything and the largest talent pool on earth. For a content site with commodity requirements, nothing is cheaper to staff.

Pick it instead when the requirements are ordinary, the budget is small, and the people maintaining it in three years are not the people building it now.

### And the case against Shio, stated plainly

If nobody on the project is going to drive it with an agent, most of what this page argues is worth nothing to you — you are buying a self-hosted headless CMS with a smaller ecosystem than the four above and a JVM to run. The protocol is the product. Judge it on whether that is the thing you need.

## The five questions this page usually gets

**Do I have to use an agent?**

No, and nothing is withheld if you never attach one. A person creates the site, defines the content model, writes and publishes the pages, uploads the media and manages the team — in a React console, with a visual editor that edits the rendered page. Agent-first is the order a capability is *built* in (law P1): MCP, then files and the CLI, then REST, then the console. It is a rule about what may not be skipped on the way to shipping something, not a condition on who is allowed to operate it.

**Everyone has an MCP server now. Isn't that the same thing?**

An MCP server is a transport. Put one over an API designed for a browser and the agent gets that API's protocol quality — the same UUID plumbing, the same 400 with no instruction, the same discovery session. The difference this page is about is what the protocol guarantees underneath, which is why every row above is a property you can test rather than a feature you can be told about.

**Our editors will never open a terminal. Is the console a second-class citizen?**

It is the surface the product is judged on by everyone who is not an agent, and it carries the whole ordinary job: sites, folders, post types with fifteen field widgets, a media library, search, a trash that restores, publishing and scheduling, users, groups, roles and tokens. Four things genuinely live on the command line — capturing an existing site, applying a blueprint, the browser audit and the file projection — and each is named on the console page rather than left for you to discover.

**Java and Spring, in 2026?**

One JVM service in a container, with the content engine, the agent gateway, the MCP server and the renderer in the same process. Rewriting it in Node is a standing non-goal: it is high cost, high risk and zero user-visible value. What you interact with is HTTP, a CLI and files.

**What happens to my front end?**

Nothing — it is headless. REST and GraphQL, a zero-dependency TypeScript client, a React SDK and a shared section vocabulary. The built-in renderer exists so a site can exist before a front end does, and so a draft has something to preview.

**Is the agent going to publish something embarrassing?**

Not without a person. Writes land as drafts, publishing is a separate explicit op, a destructive op needs a confirm token, a batch can be planned before it is applied, and every write carries attribution into a review queue. That is law P7, and it is on by default rather than configurable.
