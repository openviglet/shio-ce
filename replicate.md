# Replicate an existing site into an editable one | Viglet Shio

> Point shio clone at a site that already exists and get one a curator can edit: capture under robots.txt writing no content, a proposal that groups blocks by signature rather than by page, a conversion into drafts, and arithmetic at the end that says whether anything was lost. Fidelity keeps the source appearance; authorable gives editable fields.

Canonical: https://shio.viglet.org/replicate

---

# Point it at a site you already have

Four verbs turn a site that exists into one a curator can edit. Not a mirror and not a screenshot — a content model derived from the pages themselves, with a review step you cannot skip and arithmetic at the end that says whether anything was lost.

The four verbs What it will not do

## Capture, propose, convert, prove

Five commands, and each one makes a promise the next depends on. They are separate on purpose: a single button that crawled a stranger's site and wrote content into yours would be the surprise the whole design forbids.

### Capture

```
$ shio clone https://example.com --max-pages 50
```

Walks one origin under robots.txt and writes an inventory: the pages with titles and paths, the assets they reference, the locales and how each shows up in a URL, the forms and their fields, the navigation as the source spells it, and the third-party scripts.

It writes no content at all. The thing you are about to be asked to review does not already exist.

### Propose

```
$ shio propose --site example
```

Reads the capture and reports candidates: for each, the pages it recurs on, the section type it looks like and why, the fields it would carry, and what accepting it would set aside. Accepting writes one line into a plan file.

It applies nothing — no post, no post type, no layout. Review and mutation in one command is the surprise law P7 forbids.

### Convert

```
$ shio convert --site example --dry-run
```

Turns the accepted plan into the desired-state document that `shio apply` already takes, and sends it down that same path. One post per candidate, not per page — the hero that recurs on twelve pages is one section reused.

Every post lands in DRAFT, and `publish` is absent rather than false — so re-running can never unpublish a page a curator has since published.

### Prove

```
$ shio diff --against capture --site example
```

Walks the capture's pages, asks the instance for each one, and reads the served bytes with the same scanner that wrote the declared counts. Internal links, external links, assets, forms and prose — arithmetic, not a second opinion.

A fact the replica gained is never a failure; a lost one exits 1. Every artefact carries the identity of what declared it, so nothing is guessed or re-fetched.

### Accept

```
$ shio judge --site example
```

Runs the instruments, answers once, and names where two of them disagreed — which is where every real finding of this work came from. Then it holds that answer to a written bar: a finding at or below it prints as a task for later, one above it fails, and a kind the bar does not name fails too.

A round can end ACCEPTED, which is not the same as ending empty. What the bar leaves out is the point: looking like the source is not a test an authorable replica has to pass — it is presented by Shio's theme on purpose, so it answers for its content, its structure and its routes. `--fidelity` is how you ask for the pixel comparison instead.

## Their look, or a site somebody can maintain

Every captured block has exactly two honest futures, and the proposal asks you which one per block rather than deciding for you. This is the choice the whole pipeline exists to put in front of a reviewer.

### Fidelity

**keeps**

The source's appearance, exactly — the block's markup is written verbatim into a layout.

**offers**

No fields. A curator editing “the hero headline” is editing an HTML file.

Pick it when the page has to keep looking like it looks, and nobody is going to edit it.

### Annotated fidelity

**keeps**

The source's own markup, byte for byte — strip the annotations back out and they are identical.

**offers**

Editable fields on that markup. `convert --annotate` stamps them onto the nodes the proposal already derived, so a curator edits a heading in place.

Pick it when the page has to keep looking exactly like it looks, and somebody still has to edit it.

### Authorable

**keeps**

The content, as structured fields a curator edits in the console or on the page itself.

**offers**

The site's own theme, in the source's own colours, type and corner radius. The structure is replaced, deliberately — not ruined, and not judged against the source's own pixels.

Pick it when somebody is going to maintain this site, and the model matters more than the pixels.

### A page is usually both, and that is the point

The choice is per block, so most pages end up mixed — the hero accepted, the source's header and footer kept. The kept markup is not a leftover: each run of it is a section in the page's own list, in the place it stood, so a curator can move it, replace it with a real section, or delete it — from the same control they compose the rest of the page with. That is how a replica becomes authorable one block at a time instead of all at once, and the page keeps the source's stylesheet for as long as any of its markup is still there.

### Why there are two, and not one mode that does both

Because the one that tried was measured. An authorable replica of a real site rendered 1,066,436 bytes, 99% of it the captured stylesheet — roughly 2,894 rules meeting nineteen class attributes, with not one source class surviving. Carrying the source's classes through recovers about seven of the twenty-two that style a single heading; the rest sit on wrapper elements a generated layout does not have, so it buys typography and no layout. Translating them into a stable contract is not a repair, it is a design system per replicated site. So the *promise* changed instead of the implementation being patched: two good answers rather than one mode half-doing both.

## A candidate is a signature, not a block

Which is what makes reviewing a site affordable instead of a chore: the same hero on sixty pages is one decision, not sixty.

the proposal

```
$ shio propose --site example

  fidelity keeps the source's appearance and offers no fields;
  authorable gives these fields, presented by the site's own theme.

  hero-a91c   Hero          on 12 pages
              fields: heading, subheading, image, ctaLabel, ctaHref
              discards: 3x<iframe>  1x onclick
              replaces: 22 class name(s) of the source's styling

  grid-4f02   CardGrid      on 6 pages
              fields: title, items[].title, items[].href
              replaces: 41 class name(s) of the source's styling

  2 candidate(s) - accept with --accept hero-a91c grid-4f02
```

### It costs the same at four pages and sixty

Measured, and printed on every run: four pages of four blocks costs about 294 tokens and sixty pages costs about 295. What grows is a path per page, not a candidate per page — the per-block implementation an author naturally writes would have produced 240 candidates for the same site. P3

### Two kinds of loss, because they are two conversations

discards: is what the section genuinely cannot hold — an <iframe>, an onclick, an id an anchor targets. That is damage, and a reviewer should weigh it. replaces: is the count of source classes being set aside, which is the mode's contract rather than damage. Conflating them made every line read as an argument for fidelity on every block.

### The stylesheet is read as tokens, not just concatenated

A source's CSS *contains* its palette, its type scale and its spacing rhythm, so a conversion that only appends the file throws all of it away — and the replica then looks right and cannot be changed. Eight groups are lifted into the theme's design tokens, and the report is honest about which ones are real: a declared custom property is genuinely editable, while a literal repeated twenty-three times is the palette by observation and changes nothing until somebody rewires the CSS. [How tokens work →](/features/rendering)

### The loss is computed, never listed

It is the complement of what the fields consumed — the only definition that cannot *under*-report, and under-reporting is the one failure this artefact must not have.

## What it refuses to do, and why that is the point

A crawler you cannot bound is a crawler nobody should run against somebody else's site. Each of these is recorded in the artefact rather than in whoever ran the command.

### One origin, and no further

Every off-host link is recorded and never followed. A seed that redirects off-host is refused, naming the host it actually served — because example.com → www.example.com followed silently files every path under an origin nobody named.

### robots.txt decides, and the answer is recorded

An exact agent group beats * outright, the longest rule wins and Allow wins a tie. --ignore-robots is written into the inventory, so a capture taken without permission can never later look like one taken with it.

### A ceiling marks the capture PARTIAL

No silent caps. A bounded capture read as a complete one is the failure the whole file exists to prevent, so --max-pages says so in the artefact rather than in your memory of the command you ran.

### Assets are same-origin, and the rest are named

Mirroring a CDN's bytes into somebody's media library is a licensing decision this tool is not entitled to make — but somebody has to be able to, so the hosts left behind are listed rather than dropped.

### Deterministic, so two runs can be diffed

Sequential over a sorted frontier, and no timestamp in the file — --max-pages 50 cuts the same fifty pages every run. The inventory exists to be compared with the next crawl, and a set that moves on its own makes every diff noise.

### It is somebody's content

The tool records what it was allowed to do and refuses to guess about the rest. Capturing a site you do not own is a decision about their content, and it stays your decision.

## Three things this is not

It is not a mirror.

A mirror is bytes. What comes out here is a content model — post types with typed fields, sections a curator edits, a theme and the scripts — which is why the review step exists at all.

It is not a pixel comparison.

shio diff is arithmetic over declared and produced facts. If you want pixels, shio snapshot is that and says so — and it hands the picture to a person, because that is the one judgement a digest cannot make.

It is not a migration button.

There is a review you cannot skip and a plan file that applies nothing until you run the next verb. What it displaces is a migration project; what it is not is a migration that happens to you.
