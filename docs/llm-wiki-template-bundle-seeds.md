# llm-wiki template knowledge bundle: seed pages

Each section below is a candidate wiki page for a bundle whose purpose is to teach users about the llm-wiki-memory-template. Bullets under each heading are questions the page should answer. An LLM authoring the bundle should treat this document as the page structure, then ground the actual content in the template's shipping documentation.

Suggested page count: 13. Suggested naming: kebab-case, matching the section titles below.

---

## Page 1: `What-is-the-llm-wiki-Template`

**Type**: index / overview. **Up**: `Home`.

Purpose: give a new user a working understanding in one read.

- What is the llm-wiki-memory-template?
- What is an llm-wiki?
- What problem does the template solve?
- What does the template give me when I install it?
- How is this different from a normal wiki?
- How is this different from Obsidian, Notion, Roam, Confluence?
- How is this different from NotebookLM or vanilla RAG?
- Is this for research groups, individuals, or both?
- What does "LLM-authored wiki" mean, concretely?
- What does "durable memory" mean here?

---

## Page 2: `Template-Philosophy`

**Type**: synthesis. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: the ideas behind the template's design, for readers who want to know why it works the way it does.

- Why should the LLM write the wiki instead of me?
- What is the compounding-artifact argument for wikis over raw RAG?
- What are the three operations (ingest, query, lint) and why those three?
- What does the template capture beyond facts?
- What is the difference between knowledge, expertise, and experience in a wiki?
- Why does the template favor lightweight structural typing over heavy content-graph engineering?
- Why not use SPARQL as the primary retrieval mechanism?
- What is the "context envelope" and why does it matter for scientific work?
- What is a retrieval-hop versus a reasoning-hop?
- What is the Matrix helicopter analogy for, and where does it break down?
- What is rapid competence acquisition in the template's framing?
- What intellectual traditions does the template draw on (extended cognition, tacit knowledge, deliberate practice)?

---

## Page 3: `Installation-and-Setup`

**Type**: procedure. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: get a new user from zero to working project.

- What are the prerequisites (git, Python, an LLM agent)?
- Which Python version is needed, and which packages (rdflib, pyshacl, PyYAML)?
- Which LLM agents are supported (Claude Code, Cursor, OpenCode, others)?
- How do I create a new project from the template?
- What does `scripts/instantiate.sh` do?
- What files land in a fresh project after instantiation?
- Why is the wiki a separate git repository?
- How do I clone or bootstrap the wiki subdirectory?
- What does the `SessionStart` hook do (auto-clone the wiki)?
- What is `init-wiki.sh` and when do I run it?
- How do I set up the GitHub wiki remote?
- How do I check the template version I am on?
- How do I pull template updates into an existing project?

---

## Page 4: `Everyday-Operations`

**Type**: procedure. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: what a user does day to day.

- How do I ingest a paper, article, or web page into the wiki?
- How do I file the results of an experiment?
- How do I ask a question against my wiki?
- How do I run a lint pass on the wiki?
- What are the slash commands and what do they do?
- What does `/wiki-source` do, and when do I invoke it?
- What does `/wiki-experiment` do, and when do I invoke it?
- What does `/wiki-lint` do, and when do I invoke it?
- How do I add or edit a page by hand?
- How do I get the LLM to update a page after new information arrives?
- What is the Verification Gate and when does it fire?
- What is the wiki-write-protocol and when does it fire?

---

## Page 5: `Wiki-Structure-and-Conventions`

**Type**: reference. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: describe the wiki's structure so a user can find their way around and follow conventions.

- What files exist in a new wiki after `init-wiki.sh`?
- What is `Home_[project].md` for?
- What is `index_[project].md` for?
- What is `log_[project].md` for and how do I append to it?
- What is `SCHEMA_[project].md` and what does it define?
- What is `Edge-Types.md` and how do I use it?
- What frontmatter fields are standard (type, up, area, source, related, extends, supports, criticizes)?
- What node types are recognized (Concept, Synthesis, Entity, Index, SourceSummary, etc.)?
- How do I link between pages (wikilinks vs `[Text](Target)` cross-references)?
- Does the difference between a wikilink and a body cross-reference matter for the graph?
- What is a hub page and how does one become a hub?
- What is an orphan page and how do I fix one?

---

## Page 6: `Best-Practices`

**Type**: synthesis. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: help users get real value out of the template rather than a decorative wiki.

- What content belongs in the wiki?
- What content should stay out of the wiki?
- How often should I commit? Should I let the LLM commit for me?
- Should I push the wiki, or keep it local until published?
- How do I organize pages when the wiki gets larger?
- When should I use `extends:` versus `related:`?
- Is aggressive typed-edge discipline worth the effort for my project?
- How do I document a failed experiment honestly?
- How do I record decisions so my future self can find them?
- How do I keep the wiki healthy over months of use?
- Should I let the LLM auto-write pages, or approve every one?
- How do I review LLM-authored content critically?
- How do I capture expertise and experience, not just facts?
- Do I need to run `/wiki-lint` regularly, and when?

---

## Page 7: `Knowledge-Graph`

**Type**: reference. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: explain the KG pipeline for users who want to understand or query it.

- Why does the template build a knowledge graph from the wiki?
- Do I need to know SPARQL to use the template?
- How do I rebuild the graph after wiki edits?
- What does `scripts/kg/build-graph.sh` do?
- What does `wiki-to-jsonld.py` extract from the wiki?
- What outputs land in `scripts/kg/build/` and what is each for?
- What is RDF Turtle, and why does the template use it?
- What is materialized (inverses, area inheritance, hub flags) and why?
- What SPARQL queries ship with the template?
- When would I write my own SPARQL query?
- What is SHACL validation and what does a failure mean?
- Why is the pipeline in Python (rdflib + pyshacl) rather than Java (Jena)?
- When would I switch to a Fuseki endpoint?

---

## Page 8: `Team-Workflow`

**Type**: procedure. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: help groups collaborate on a shared wiki.

- Can multiple people edit the same wiki concurrently?
- How do we handle merge conflicts on the wiki?
- What is the wiki-write-protocol (`wiki_push`), and why not just `git push`?
- What is the discipline-gates document and how does it protect us?
- Can students see the faculty's wiki?
- How do we share wikis across labs or institutions?
- Can I clone another group's wiki as a reference?
- What happens if two LLM agents write to the wiki at the same time?
- How do we assign attribution when the LLM authors most of the content?
- How does licensing work if we share the wiki publicly?

---

## Page 9: `Knowledge-Bundles-Overview`

**Type**: synthesis. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: introduce bundles as a first-class use of the template.

- What is a knowledge bundle in the llm-wiki context?
- How is a bundle different from a wiki?
- How do I create a bundle from my wiki?
- How do I consume a bundle authored by someone else?
- What existing topical bundles are available (knowledge engineering, LLMs, others)?
- How do students consume a bundle via their own LLM?
- Can I extend a bundle with my own notes?
- Will the template support OKF (Google Open Knowledge Format) import/export? What for?

---

## Page 10: `Troubleshooting`

**Type**: reference. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: help users recover from common failure modes.

- The wiki is not loading at session start. What do I check?
- The graph build failed. What is the first thing to look at?
- The LLM keeps writing pages without asking. How do I slow it down?
- I have a merge conflict on the wiki. What is the safe recovery?
- The wiki has grown too large to browse. How do I archive old content?
- The LLM is citing pages that no longer exist. What happened, and how do I fix it?
- SHACL validation is failing. What is a shape violation and how do I read the report?
- I accidentally committed private content to the wiki. How do I unwind?
- The `SessionStart` hook did not clone the wiki. What do I do?
- `arq` or `rdflib` is not installed. Which error indicates which?

---

## Page 11: `Extending-the-Template`

**Type**: procedure. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: help users adapt the template to their specific needs.

- Can I add my own slash commands? Where do they go?
- Can I add my own skills (model-side procedures)?
- Can I add custom edge types beyond the standard vocabulary?
- Can I add custom node types?
- Can I use a different LLM agent than the ones supported out of the box?
- Can I add my own SPARQL queries to the library?
- Can I export the wiki to a different format?
- Can I add project-specific rules to `CLAUDE.md` without breaking template updates?
- How do I add a `SessionStart` hook of my own?
- Can I run the wiki without git?

---

## Page 12: `When-to-Use-When-Not`

**Type**: synthesis. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: help a prospective user decide whether this is the right tool.

- When is this the right tool?
- When is this the wrong tool?
- Is this overkill for a small personal project?
- Do I need a lot of source material for the template to pay off?
- Does this help for a single-book or single-paper project?
- Is this useful outside research (business, personal knowledge, hobby)?
- What is the minimum team size that makes shared use worthwhile?
- Does the template help students, or is it primarily for faculty and researchers?

---

## Page 13: `Concepts-Glossary`

**Type**: reference. **Up**: `What-is-the-llm-wiki-Template`.

Purpose: quick-reference definitions for concepts a user will encounter in the template's own documentation and community discussion.

- What is a Markov chain in the context of retrieval?
- What is random walk with restart (RWR)?
- What is personalized PageRank?
- What is entity resolution, and why does the template avoid heavy versions of it?
- What is a structural graph versus a content graph?
- What is the difference between vanilla RAG and graph-informed retrieval?
- What is the extended-mind tradition and why does the template draw on it?
- What is the DIKW pyramid?
- What is tacit knowledge?
- What is procedural knowledge versus declarative knowledge?
- What is deliberate practice?
- What is RDF Turtle? RDF-star? JSON-LD?
- What is SHACL?

---

## Authoring notes for the LLM building this bundle

- Ground every answer in the actual template documentation (github.com/crcresearch/llm-wiki-memory-template). Do not invent template features.
- Where a question cannot be answered from the template docs, either skip it or mark "not documented in the template as of {date}, see [pointer to where to look]."
- Add typed frontmatter (`type`, `up`, `related`, `source`) to every page. Use `up: "[[Home]]"` at minimum.
- Cross-link liberally between the 13 pages via wikilinks in prose and `related:` in frontmatter.
- Cite specific files, scripts, and skills by path where relevant (`.claude/skills/wiki-source.md`, `scripts/kg/build-graph.sh`, `SCHEMA_[project].md`, etc.).
- Append a log entry per page created to `log_[project].md` noting what was authored and which sources were consulted.
- Follow the Verification Gate at `wiki/agents/verification-gate.md` before committing.
- Commit incrementally so a human reviewer can catch drift early.
