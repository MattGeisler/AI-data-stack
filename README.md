# AI-Enabled Data Pipeline, reference architecture

A single-page interactive model of an AI-enabled data pipeline. No build step, no
dependencies. `index.html` is self-contained.

## The spine: six physical data products, bottom to top

`01 Data Source` -> `02 ODS` -> `03 Data Integration` -> `04 Data Lake` -> `05 Aggregate` -> `06 Discovery & Dashboard`

Each is drawn as the thing it is: source tiles, a replicated cylinder, a merge
manifold, the lake cylinder, an aggregate cube, a screen.

## The other three layers

Context, agent and logical are layers in their own right, not details of a
physical product. Each is a column of named concerns:

- Context: Business knowledge, Skills, Tools, Events

Business knowledge is the odd one: it is not assembled from other parts of the
stack. It is the material only people can write. Monthly business reviews,
board reporting, the analyses already done and what they concluded, and the
commentary stakeholders leave against a metric and a period. The data informs
it (a trend can contradict an earlier finding) and an agent can draft the
recurring parts, but a person writes what it means. All of it is versioned with
an author and a date, superseded documents are marked and never deleted, and a
finding is filed against the metric it concerns.
- Agent: Task, Domain expert, Process owner
- Logical: Transformation SQL, DQ Module, Linting Model, Semantic Layer

The summary shows the names alone. Clicking one opens its page: which of the
six physical layers it covers, what it is made of by type, what it provides.
A physical layer opens the same way, into its own four-type breakdown.

On a phone the four columns cannot sit side by side, so each one names itself
and they stack in order. The four cards at the top become tabs below 1000px:
tapping one shows that domain alone. Above 1000px the cards are the column
headers and tapping one dims the rest instead.

## Inside every box: the four components

Every dataset in the stack is made of four things, read left to right in the
same order everywhere on the page:

`Context` > `Agent` > `Logical` > `Physical`

- Context: what it means to this business, and what the agent is told
- Agent: the models that propose work against it
- Logical: the declared rules, SQL, semantics, conformance and quality
- Physical: the tables, files and systems that hold the bytes

Each `comps` array in `NODES` and `MODULES` is index-aligned to `TYPES`, so the
two have to be reordered together.

The physical column has six cells, one per data product. Each of the other
three is a single column holding the concerns of that type. A concern is one
thing across many layers, not one entry per layer, so each card carries a scale
showing which of the six it covers, reading 01 on the left through 06 on the
right:

- Context: Business Context, 06 only
- Agent: Agent Runtime, 01 to 06
- Logical: DQ Module 01 to 05, Semantic Layer 03 to 06, Linting Model 02 to 05,
  Transformation SQL 02 to 05

Coverage comes from each concern's `plugs` list. The summary shows the cards
alone; clicking one opens its page. A layer's own four-type breakdown sits
behind "About this layer" on its physical cell.

Human decisions are not a fifth type. They arrive as PRs and requirements
against the four, and the operating rule states the pattern: agents propose,
deterministic code executes, humans decide. The per-layer decision items are
kept in a `decisions` field in the data, unrendered, so they can come back.

## The component bar

Above the stack sit four cards, one per component type. They replaced the
consumers tier, which showed dashboards, alerts, embedded product and ad-hoc
questions. That content was already layer 06's "What it provides", word for
word, so nothing was lost.

Clicking a card enters focus mode: `body[data-focus="physical"]` and so on.
Every layer opens showing only that component, so one of the four can be read
straight down the stack. The module rail hides, since focus is about the
vertical read. Click the active card again, press Escape, or use "Show all
four" to leave. Focus works in both views.

## The two views

In the Executive view, clicking any layer opens a panel with four parts: what
this layer is (prose), what it provides (the functionality of the data product),
produced with (the deterministic modules that make it, and what each contributes
at that layer), and built from (deterministic code, agentic layer, human
decision). The Executive view is the spine alone: six shapes, one line and one
output each, with no cross-cutting clutter.

The Technical toggle (top right, or press `T`) opens every product into its
attributed components and brings in the module rail.

## Component pages

Every leaf component in a "Built from" column, and in an opened module, can have
its own page. Clicking one routes to `#/<parent>/<slug>`, for example
`#/lake/lineage-capture`. The page is rendered from the `DETAIL` array in
`index.html`, so it stays one file with no build step, and the URL is
linkable and works with the back button.

Each page has three parts: what it is, how it works (numbered steps), and what
breaks without it.

Written so far: the ten components of `04 Data Lake`. The other 104 render as
plain text until an entry is added for them. To add one, append to `DETAIL` with
`parent`, `slug`, `lane`, `label` matching the text in that comps array, `lead`,
`what`, `how` and `breaks`.

## Publishing

GitHub Pages, source `main` at root. `.nojekyll` is committed so Pages serves the
file as-is.

Matt Geisler
