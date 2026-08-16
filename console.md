# Shio without an agent — the CMS in the browser | Viglet Shio

> The traditional path, in full: create a site, build the content model with fifteen field widgets, write pages in a form, upload media, preview and edit on the rendered page, publish or schedule, and manage users, roles and tokens — all in the console. Plus the four things that genuinely live on the command line, and what changes if you attach an agent later.

Canonical: https://shio.viglet.org/console

---

# It is a CMS first. The agent is optional.

Create the site, shape the content model, write the pages, upload the media, publish or schedule it, and add the rest of the team — in a browser, with no terminal, no YAML and no agent anywhere in the picture. Nothing on this page needs a capability the console does not have.

Six screens, one page live What the console does not do

## From an empty instance to a published page, in six screens

The landing page shows a coding agent doing this same job in six calls. It is the same content model, the same drafts and the same publish act — which is the whole point of showing both.

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

Note where the draft appears. A person's write lands in `DRAFT` exactly as an agent's does, and publishing is a separate, deliberate act in both cases. The safety on this product is not a leash for the agent — it is how the content lifecycle works.

## The ordinary job, in full

Six groups, and every line is a screen in the console rather than a plan. If your team has used a CMS before, none of this will need explaining.

### Content

- Sites, created from scratch or imported from a .zip export
- Folders, and a tree you move and copy things around in
- Posts of any type, with search across the instance
- A trash that restores — deleting and purging are separate acts

### The content model

- Post types built in the browser: add a field, pick a widget, order them
- Fifteen widgets — text, rich text, date, select, file, relator, tabs, code
- Relations between posts, and a content browser to pick them
- The types the instance ships with, if you would rather not start empty

### Publishing

- Draft, preview, publish, schedule, unpublish
- Preview links that open the real rendered page from an expiring token
- Inline editing on that page through the Universal Editor
- A review queue and an activity log — who changed what, and when

### Media and files

- A media library for the binaries a page references
- Static files served beside the site
- The file widget, so a field is a picker rather than a URL to paste

### People and access

- Users, groups and roles
- External authentication providers, and email configuration
- API tokens, scoped per job — read, preview, write, agent
- Tenants, when one instance serves several brands or clients

### Delivery and integration

- A GraphQL explorer against your own content
- Webhooks per site, so a publish can tell your build about it
- The package marketplace, with the dry run shown before anything installs

## Four things that genuinely live on the command line

Each one needs a shell or a browser the instance deliberately does not run. None of them is required to operate the CMS, and naming them is what makes the list above worth reading.

- 1

### Capturing a site that already exists

shio clone walks an origin under robots.txt and writes an inventory. It needs a crawler, and the instance does not run one.

- 2

### Applying a blueprint to a site

The console browses and installs packages, with the dry run shown first. Applying one to a site is shio apply --blueprint, or shio_apply over MCP.

- 3

### Screenshots and the browser audit

shio audit and shio snapshot drive a real browser. That stays in the CLI, where the shell already is — the instance running Chromium per request is a different operational thing entirely.

- 4

### The file projection and the CI drift check

Pulling the site to disk and failing a build on drift is what the CLI is for. Nothing about it is required to run the CMS.

The CLI is `npx @viglet/shio` and it talks to the same instance over the same API. It is an extra door, not a dependency: an instance nobody ever runs it against behaves identically.

## What changes the day you attach an agent

Less than you would expect, which is the argument for starting without one. No migration, no second store, no content to move.

### Nothing moves

The agent reads the same posts, the same types and the same folders the console writes. There is no second store, no export step and no parallel model — law P10 forbids a third contract, and this is what that buys.

### Its writes look like drafts, because they are

An agent write lands in DRAFT with attribution on it. Whether a credential may publish at all is a property of the token, so the console's publish button stays the only way anything reaches a reader.

### You get a queue, not a surprise

Changes arrive in the review queue with a preview link each and the verify warnings restated as open questions. The queue is console-authenticated, and an agent token cannot reach the approve call.

### And you can turn it off

Do not issue an AGENT token, and nothing on that surface can write. The capability is additive in the literal sense: the CMS you were running is the CMS you keep.

[What stops an agent write](/curator) [Attach one in a command](/claude-code)

## Run it, and see whether the console is enough for you

One container and a database. The installation guide is the same one everybody uses, and there is no hosted tier you are being funnelled towards.

[Install it](https://docs.viglet.org/shio/) [The self-host section](/#self-host)
