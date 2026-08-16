# The curator’s half — what stops the agent | Viglet Shio

> An agent wrote nine pages last night and nobody has seen them yet. The curator half of Shio: the review queue an agent token cannot reach, expiring preview links, inline editing on the rendered page, draft-published diff and restore, reversible deletes, and the six gates that are on by default rather than configurable.

Canonical: https://shio.viglet.org/curator

---

# An agent wrote nine pages last night. Nobody has seen them yet.

That sentence is the product. Shio is built so a coding agent can do the work and a person still decides what the world sees — not as a policy somebody wrote down, but as mechanisms that are on by default and that an eager script cannot switch off on its way past.

A curator's Tuesday The six gates

## Half an hour on a Tuesday morning

Not an architecture diagram. This is the whole interaction most curators will ever have with the fact that an agent built the site.

Overnight

### The agent worked, and published nothing

It read the model, wrote nine pages and proved them against the lint. Every one of them is a draft. The site your readers see has not changed.

09:10

### A queue, not a diff to hunt through

“The agent proposed 9 changes.” One session, what each change touched, and two buttons that mean something: approve, or revert.

09:14

### You open the page before anyone else can

A preview link opens the real rendered page, from a token that expires and is scoped to that one post — not a staging environment somebody has to keep in sync.

09:22

### You fix the headline where you can see it

Inline, on the rendered page itself, through the visual editor — rather than hunting for the field in a form that looks nothing like the result.

09:30

### You publish, or you schedule it

Publishing is its own act. Or set a date and let the sweep fire it — the same path, so anything listening for a publish hears the identical event.

## Five states, and only one of them is public

A published post is an immutable snapshot sitting beside the editable draft rather than an entry in a long history — which is exactly why the diff, the restore and the preview are cheap enough to be always available.

- 01

### DRAFT

The editable row. Every agent write lands here, and so does yours.

- 02

### PREVIEW

An expiring, single-post token that opens the real rendered page.

- 03

### PUBLISHED

An immutable snapshot beside the draft — which is what makes diff and restore cheap.

- 04

### SCHEDULED

A publish or unpublish instant; a sweep fires it down the same path.

- 05

### TRASH

Reversible. Restore and purge are separate acts, and purge is the one nobody does by accident.

## Fix the headline where you can see it

The renderer annotates what it renders, so the visual editor knows which field on which post produced the words under the cursor. You click the headline on the page and you are editing the headline — not hunting for it in a form that looks nothing like the result.

It works on the built-in renderer and on a front end of your own: a published bridge package makes any page editable once it emits the same annotations. And it edits the *draft*, so looking at a page and changing it are the same act with the same safety as every other write. P7

/preview/acme/launch draft

Launching Shio 2026.3

An open-source headless CMS with four ways in: the console, an agent, files in a repository, and the delivery API.

## Each one is a mechanism, and each one has a reason

The reason is the interesting half. A rule with no argument behind it is a rule somebody will turn off the first time it is inconvenient.

### Writing and publishing are different permissions

An agent's write lands in DRAFT, and whether a credential may publish at all is a property of the token rather than of the call.

Because Anything able to write was previously able to publish, which made draft-by-default a convention instead of a gate.

### A delete takes two calls

A delete, a folder delete or any prune that would remove something is refused once with a confirm digest over exactly those deletions; the real run has to present it back.

Because A digest over the deletions means the second call cannot quietly cover more than the first one showed you.

### The plan is the same document as the write

Any batch can be sent as a dry run. What comes back is that batch annotated with what each op would change — not a summary of it.

Because A preview in a different shape from the thing being previewed is a second implementation, and the two drift.

### The agent cannot approve its own work

The review queue is console-authenticated and deliberately not on the agent namespace at all. An agent token cannot reach the approve call.

Because A credential that can both make a change and sign it off is not a review step, it is a log line.

### Deleting is reversible, and so is a folder

A deleted post goes to the trash with restore and purge as separate acts. A deleted folder leaves a trace that can be undone.

Because A mis-click that loses content is the failure a curator cannot recover from, and the one nobody reports until much later.

### Every change has a name and a time on it

The history is written and readable, with an Activity view in the console. A published post is an immutable snapshot beside the editable draft, so the diff is always available.

Because Reviewing a change you cannot attribute is reviewing a rumour.

## Three seats, and you can hold all of them

If you take one thing from this page, take this — it is the whole product, and it is the answer to “so what does the CMS actually do now”.

### The person creates, and decides

Sites, content models, folders, pages, media, publishing, scheduling, the rest of the team — all of it in the console, and none of it needing an agent to have happened first. When there is an agent, this seat also holds the approve button.

### The agent builds — if you want one

Discovers the model in one call, authors content as files, applies a blueprint, renders a preview and proves the result — without a browser, a cookie or a click. Its writes are drafts, and its credential cannot publish them.

### The delivery API delivers

A framework-agnostic delivery API — REST and GraphQL — with TypeScript SDKs, a React SDK and a Next.js starter that is generated rather than copied. It serves whatever the other two seats agreed on.

The first seat is the one that is never empty, and this page is what it is holding. The second can stay empty forever — [an instance with no agent attached](/console) is an ordinary CMS, with the same review queue, the same previews and the same publish act described above.
