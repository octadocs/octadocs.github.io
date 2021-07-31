---
title: Introduce Blueprints
status: accepted
date: 2021-07-21
author: Anatoly Scherbakov
number: 5
---

## Context

Theoretically, Octadocs can support quite complicated use cases and automate the generation of documentation in MkDocs for many particular cases, such as these:

- Generate a list of ADR documents (such as this one) with status and sorting by creation date;
- Generate a `reveal.js` presentation from a directory of Markdown files, one file per slide;
- Perform a structured search and display its results;
- Or just display a list of pages as cards.

Currently, in order to do any of these things, we'd have to:

- Create one or more HTML templates for the pages in question;
- Create a custom `context.yaml` file and assign it to the pages in question;
- (Oftentimes) execute one or more inference queries when `on_files` event fires.

How to do that?

## Decision

It could also be useful to expose custom Jinja2 macros to Markdown pages content via `mkdocs-macros` but, say, for ADR that's not a requirement. I believe some sites can even not need `mkdocs-macros` at all. That means we are not going to use pluglets as pluggable Octadocs components.

What is left is to use MkDocs plugins as such.

For example:

1. Run `pip install mkdocs-decisions`;
2. Add `decisions` to `plugins` sections at `mkdocs.yml`;
3. If there is a `decisions` directory in the site,
   - and it has an `index.md` document, the ADR index template will be assigned to that file,
   - and any other `.md` file under that directory will be assigned the ADR template.

## Consequences

All of this will enable us to easily install a plugin and make Octadocs useful even if we do not give a heck about RDF or SPARQL and are not yet prepared to learn anything of the kind.
