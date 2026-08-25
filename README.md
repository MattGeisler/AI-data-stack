# AI-Enabled Data Pipeline, reference architecture

A single-page interactive model of an AI-enabled data pipeline. No build step, no
dependencies. `index.html` is self-contained.

## The spine: six physical data products, bottom to top

`01 Data Source` -> `02 ODS` -> `03 Data Integration` -> `04 Data Lake` -> `05 Aggregate` -> `06 Discovery & Dashboard`

Each is drawn as the thing it is: source tiles, a replicated cylinder, a merge
manifold, the lake cylinder, an aggregate cube, a screen.

## The other axis: modules that plug into the spine

Deterministic modules (quality, semantics and conformance, enforced against the products):

- DQ Module: plugs into Data Source, ODS, Integration, Lake, Aggregate
- Semantic Layer: plugs into Integration, Lake, Aggregate, Discovery & Dashboard
- Linting Model: plugs into ODS, Integration, Lake, Aggregate

Context pipeline (a small pipeline of its own):

- Business Context: business inputs, context modelling, context store, grounding
  service, plugged into Discovery & Dashboard

These are not data products. They attach to the products and do not sit in the
flow. They appear only in the Technical view, collapsed. Click one to open its
components and light up what it plugs into.

## Inside every box: the five concerns

Deterministic Code, Semantic Layer & DQ Tooling, Agentic Layer, Human Decision,
Product Output.

Operating rule: agents propose, deterministic code executes, humans decide.

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
