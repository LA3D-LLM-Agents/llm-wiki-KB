# llm-wiki template bundle: gold-standard answers (test harness)

Ground-truth answers to every question in
[`llm-wiki-template-bundle-seeds.md`](llm-wiki-template-bundle-seeds.md),
for use as a test harness against the `llm-wiki-KB` knowledge bundle
(queried via `scripts/agent-comms/ask.sh llm-wiki-KB "<question>"`, or any
LLM reading the bundle directly).

## How to use this harness

1. Pose the question to the bundle (via `ask`, or an LLM session in the
   wiki).
2. Grade the response against the entry's **Must include** facts, not
   against exact wording. Responses vary in phrasing; the facts are what
   matter.
3. A response **fails** if it omits load-bearing facts, contradicts a
   **Caveat**, or presents an aspirational/planned feature as shipped.

Suggested scoring per question: `key_facts_present / key_facts_total`,
with an automatic fail if any **Caveat** is violated (this is where the
honest-reporting discipline is tested). An LLM-judge can grade against
the **Must include** list; a human can eyeball the same.

## Source of truth

These answers are grounded in the **primary sources**, not merely copied
from the bundle pages, so the harness can also catch a bundle page that
is itself wrong:

- The template repo `crcresearch/llm-wiki-memory-template` (README,
  `CLAUDE.md.template`, `llm-wiki.md`, `.claude/`, `wiki/`, `scripts/`).
- The template's own wiki (Wiki-LLM-Pattern, Three-Operations,
  Knowledge-Bundles-Framing, OKF-Alignment-Ideas, Implementation-Status,
  Multi-Agent-Write-Protocol, Agent-Overlays, etc.).
- The WGRA flyer (`la3d.github.io/WGRA`).
- The vision wiki (`chrissweet/llm-wiki-vision`): Vision,
  Knowledge-Expertise-Experience, Knowledge-Bundles,
  Lightweight-Structural-Graphs, Retrieval-Context-Envelope-Site.

**Status conventions used below** (as of 2026-07-14):
- *Shipped*: present in template `main` / this bundle.
- *Reference impl, not wired*: exists and CI-tested but not in the default path.
- *Planned / analysis stage*: designed or discussed, not implemented.
- *Vision-wiki framing*: reasoning-trail concept, not a shipped mechanic.

`Source:` names the bundle page whose content the answer should track.

---

## Page 1: What-is-the-llm-wiki-Template

**Q: What is the llm-wiki-memory-template?**
- **Answer.** A GitHub template repository (`crcresearch/llm-wiki-memory-template`) that scaffolds a project with a small, LLM-maintained, cross-linked Markdown wiki as durable memory. It packages the llm-wiki pattern (tobi/Karpathy lineage) and adds a discipline layer: agent overlays, a verification gate, a typed-edge ontology, attribution-aware logging, and a knowledge-graph pipeline.
- **Must include:** GitHub template repo; you instantiate a project from it; LLM-maintained Markdown wiki as durable memory; extends the llm-wiki pattern with a discipline layer.
- **Source:** What-is-the-llm-wiki-Template.

**Q: What is an llm-wiki?**
- **Answer.** A directory of interlinked Markdown files with YAML frontmatter that an LLM writes and maintains while a human reads and directs. It sits between the raw sources and the human, holding the compiled, cross-referenced understanding of a project. It is just a git repo of Markdown.
- **Must include:** interlinked Markdown + frontmatter; LLM writes/maintains, human reads/directs; sits between raw sources and the human; git repo.
- **Source:** What-is-the-llm-wiki-Template.

**Q: What problem does the template solve?**
- **Answer.** RAG-style workflows rediscover knowledge from scratch on every query; nothing accumulates. The template makes a persistent, compounding artifact where an insight, once filed, is referenced rather than re-derived. It automates the bookkeeping (cross-references, summaries, contradiction-flagging) that causes humans to abandon wikis.
- **Must include:** RAG re-derives / nothing accumulates; compounding persistent artifact; automates the maintenance/bookkeeping that kills human wikis.
- **Source:** What-is-the-llm-wiki-Template, Template-Philosophy.

**Q: What does the template give me when I install it?**
- **Answer.** A wiki sub-repo at `wiki/<repo>.wiki/` seeded with Home, index, log, SCHEMA, Edge-Types; a generated `CLAUDE.md` with the memory-boundary and wiki-maintenance rules; an agent overlay (Claude Code ships slash commands, skills, a SessionStart hook, an optional PostToolUse hook); agent-agnostic discipline files under `wiki/agents/`; and a knowledge-graph pipeline under `scripts/kg/`.
- **Must include:** wiki sub-repo with seeded special files; generated CLAUDE.md; agent overlay (commands/skills/hooks); discipline files; KG pipeline.
- **Source:** What-is-the-llm-wiki-Template, Installation-and-Setup.

**Q: How is this different from a normal wiki?**
- **Answer.** A normal wiki is human-maintained and gets abandoned because maintenance outgrows value; in an llm-wiki the LLM does the maintenance, so keeping it current costs almost nothing.
- **Must include:** normal wiki is human-maintained and decays; LLM does the maintenance here; near-zero maintenance cost.
- **Source:** What-is-the-llm-wiki-Template.

**Q: How is this different from Obsidian, Notion, Roam, Confluence?**
- **Answer.** Those are human-authoring surfaces; the llm-wiki inverts the roles so the LLM authors and the human reads/directs. It is complementary to Obsidian in particular (LLM edits on one side, Obsidian browses the graph on the other): Obsidian is the IDE, the LLM the programmer, the wiki the codebase.
- **Must include:** those are human-authoring tools; llm-wiki is agent-first (LLM authors, human directs); complementary to Obsidian, not a replacement.
- **Source:** What-is-the-llm-wiki-Template.

**Q: How is this different from NotebookLM or vanilla RAG?**
- **Answer.** RAG/NotebookLM index raw sources and synthesize fresh on every query; the synthesis then disappears. The llm-wiki adds a layer where an insight settles and is referenced by name, so knowledge accumulates instead of being re-derived. It is not a rejection of RAG, which remains right for single-hop lookups.
- **Must include:** RAG re-derives per query and discards; wiki lets insight settle / accumulate; complementary, not a replacement for RAG.
- **Source:** What-is-the-llm-wiki-Template, When-to-Use-When-Not.

**Q: Is this for research groups, individuals, or both?**
- **Answer.** Both. The WGRA positioning frames it around research groups (durable institutional memory, the "long-serving lab technician"), but it applies equally to an individual on a weeks-long deep-dive, reading a book, or a solo project.
- **Must include:** both; research-group institutional-memory framing; also individuals/solo use.
- **Source:** What-is-the-llm-wiki-Template, When-to-Use-When-Not.

**Q: What does "LLM-authored wiki" mean, concretely?**
- **Answer.** The human almost never writes pages by hand. You drop a source or run an experiment and tell the LLM to file it; it reads, discusses takeaways, writes a summary page, updates the index, revises related pages, fixes cross-references both ways, and appends a log entry, touching 5-15 pages in one pass. You review and guide emphasis.
- **Must include:** human rarely writes pages; LLM reads/summarizes/cross-references/files; touches ~5-15 pages per ingest; human curates/directs/reviews.
- **Source:** What-is-the-llm-wiki-Template, Everyday-Operations.

**Q: What does "durable memory" mean here?**
- **Answer.** Knowledge that survives across sessions, users, and machines rather than living in one conversation's context. The agent reads the wiki to recall project context and writes to it to remember; because it is git-backed, the memory is versioned, auditable, and portable. Distinct from the per-user Claude-memory layer (which holds user identity/preferences).
- **Must include:** survives across sessions/users/machines; read-to-recall / write-to-remember; git-versioned; distinct from per-user Claude-memory (project vs user boundary).
- **Source:** What-is-the-llm-wiki-Template, Template-Philosophy.

---

## Page 2: Template-Philosophy

**Q: Why should the LLM write the wiki instead of me?**
- **Answer.** Because the value-destroying part of a knowledge base is the bookkeeping, not the thinking, and LLMs do not get bored of bookkeeping or forget a cross-reference, and can touch 15 files in one pass. The human curates sources, directs, asks questions, and decides meaning; the LLM does the rest.
- **Must include:** bookkeeping is the burden that kills human wikis; LLM does maintenance tirelessly/consistently; human curates and directs.
- **Source:** Template-Philosophy.

**Q: What is the compounding-artifact argument for wikis over raw RAG?**
- **Answer.** RAG over raw sources re-synthesizes the same things every session with no place for an insight to settle. The wiki is that place: a filed finding is referenced by name, and cross-references compound so each new link makes a finding easier to surface. It is human-readable and version-controlled, not a black box.
- **Must include:** RAG has no place for insight to settle; wiki is that place; cross-references compound; human-readable/versioned.
- **Source:** Template-Philosophy.

**Q: What are the three operations (ingest, query, lint) and why those three?**
- **Answer.** Ingest = write new knowledge (create/update pages, fix cross-refs both ways, update index, append log, commit); Query = read (index → pages → synthesize, optionally file the answer back); Lint = maintain (orphans, dead links, stale claims, missing frontmatter, and apply fixes). Three is the empirical minimum: two would conflate adding knowledge with maintaining it, four+ overlap.
- **Must include:** ingest=write, query=read, lint=maintain; each named correctly; three is the minimum / two conflates ingest and lint.
- **Source:** Template-Philosophy, Everyday-Operations.

**Q: What does the template capture beyond facts?**
- **Answer.** Three layers (vision-wiki framing): knowledge (facts), expertise (the author's judgment: tradeoffs, preferences, load-bearing criticisms), and experience (concrete cases, what was tried, what failed, dead ends). A wiki with all three is closer to a graduate advisor than a textbook.
- **Must include:** knowledge / expertise / experience; expertise = judgment, experience = grounded cases/failures; advisor-not-textbook.
- **Source:** Template-Philosophy. **Caveat:** the three-layer framing is vision-wiki framing, not a formal template feature.

**Q: What is the difference between knowledge, expertise, and experience in a wiki?**
- **Answer.** Knowledge is declarative facts; expertise is procedural judgment (which tradeoffs matter); experience is tacit, case-based grounding (what was tried and failed). Separable but not hierarchical: experience can exist without expertise, and vice versa. Each maps loosely onto established literature (DIKW's K, procedural knowledge/professional judgment, tacit knowledge/case-based reasoning).
- **Must include:** knowledge=facts/declarative; expertise=judgment/procedural; experience=cases/tacit; separable, not hierarchical.
- **Source:** Template-Philosophy, Concepts-Glossary.

**Q: Why does the template favor lightweight structural typing over heavy content-graph engineering?**
- **Answer.** Heavy content graphs are only as reliable as their entity resolution, which is unsolved for real corpora (under-merging and over-merging both break crisp queries, worst on the rare entities researchers ask about). Structural edges and lightweight extracted content are cheap, have no resolution step to fail, and degrade gracefully. Aggressive typing still pays off in bibliographic/review wikis.
- **Must include:** heavy graphs depend on fragile entity resolution; structural + lightweight is cheap and degrades gracefully; aggressive typing pays off for review/bibliographic wikis.
- **Source:** Template-Philosophy, Knowledge-Graph. **Caveat:** the cost-benefit argument is vision-wiki framing.

**Q: Why not use SPARQL as the primary retrieval mechanism?**
- **Answer.** SPARQL over typed edges answers well when structure is objective and complete, but returns empty/misleading results when structure is provisional or sparse (the common experimental case). It is excellent for topology questions and wiki maintenance, but the recommended pattern is to use the graph to find where to look, then read the pages for what they say.
- **Must include:** SPARQL good for topology / complete structure; brittle on sparse/provisional structure; use graph to find where, read files for what.
- **Source:** Template-Philosophy, Knowledge-Graph.

**Q: What is the "context envelope" and why does it matter for scientific work?**
- **Answer.** The local neighborhood of concepts, layout, and cross-document evidence around a question; retrieval is really about assembling it, and the model cannot answer without it even when the correct chunk is in the top-K. It matters for science because evidence-based reasoning is multi-source by construction.
- **Must include:** neighborhood of evidence around the question; model fails without it even with the right chunk present; science is multi-source/multi-hop.
- **Source:** Template-Philosophy. **Caveat:** vision-wiki framing, not a shipped template mechanic.

**Q: What is a retrieval-hop versus a reasoning-hop?**
- **Answer.** A reasoning-hop is a step in decomposing the question; a retrieval-hop is a step in assembling the evidence on the index side. Question decomposition addresses reasoning-hops but does not assemble retrieval-hops, which is why dense similarity fails on deep multi-hop questions.
- **Must include:** reasoning-hop = question decomposition; retrieval-hop = evidence assembly on index side; the two are different / decomposition doesn't fix retrieval.
- **Source:** Template-Philosophy, Concepts-Glossary. **Caveat:** vision-wiki framing.

**Q: What is the Matrix helicopter analogy for, and where does it break down?**
- **Answer.** It names the ambition of rapid competence acquisition (Trinity instantly gains a pilot's compiled knowledge/expertise/experience). It breaks down at the mechanism: direct brain-writing of skills is science fiction (skill is gradual and embodied). The template substitutes the receiver's LLM-assisted workflow for their neurology, and unlike the film, bundle contents are inspectable, extendable, and cite-able.
- **Must include:** names ambition = rapid competence acquisition; breaks down on mechanism (no brain download); substrate is the LLM/workflow, not neurology; bundle is auditable.
- **Source:** Template-Philosophy, Knowledge-Bundles-Overview. **Caveat:** vision-wiki framing.

**Q: What is rapid competence acquisition in the template's framing?**
- **Answer.** The practical goal the Matrix analogy points at: a bundle consumer, reading through their own LLM, gains working competence fast because the bundle ships judgment and experience alongside facts and the LLM walks it beside the consumer's own notes.
- **Must include:** gain working competence fast; bundle ships expertise+experience not just facts; via the consumer's LLM.
- **Source:** Template-Philosophy. **Caveat:** vision-wiki framing.

**Q: What intellectual traditions does the template draw on?**
- **Answer.** Extended cognition (Bush's Memex 1945, Licklider 1960, Engelbart 1962, Clark & Chalmers 1998), tacit knowledge and reflective practice (Polanyi 1966, Schön 1983, Nonaka & Takeuchi 1995), and deliberate practice / expert performance (Ericsson & Charness 1994). Bush's Memex is the closest ancestor; the maintenance he couldn't solve is what the LLM handles.
- **Must include:** extended cognition (Bush/Memex, Clark & Chalmers); tacit knowledge (Polanyi); deliberate practice (Ericsson); Memex as closest ancestor.
- **Source:** Template-Philosophy, Concepts-Glossary. **Caveat:** drawn from the vision wiki / llm-wiki.md.

---

## Page 3: Installation-and-Setup

**Q: What are the prerequisites (git, Python, an LLM agent)?**
- **Answer.** git (the wiki and its tooling assume git throughout); an LLM coding agent (Claude Code validated; Cursor and a no-overlay minimal mode also ship); and Python 3 only if you use the optional knowledge-graph pipeline. The core wiki needs no Python.
- **Must include:** git required; an LLM agent (Claude Code); Python only for the optional KG pipeline.
- **Source:** Installation-and-Setup.

**Q: Which Python version is needed, and which packages (rdflib, pyshacl, PyYAML)?**
- **Answer.** Python 3 (no specific minor version pinned) plus PyYAML, rdflib, and pyshacl, and Bash 4+, only for the KG pipeline. If you never build the graph, none is required.
- **Must include:** Python 3 (unpinned); PyYAML + rdflib + pyshacl; only for the KG pipeline.
- **Source:** Installation-and-Setup, Knowledge-Graph. **Caveat:** do not assert a specific Python minor version; the docs say "Python 3".

**Q: Which LLM agents are supported (Claude Code, Cursor, OpenCode, others)?**
- **Answer.** Claude Code is behaviorally validated end-to-end. Cursor ships an overlay but is structurally validated only. `--agent=none` installs no overlay (minimal mode) for OpenCode/Pi/others, which read CLAUDE.md and follow the procedures manually; whether a given agent actually does is empirically open.
- **Must include:** Claude Code validated; Cursor structural-only; --agent=none / minimal mode for others.
- **Source:** Installation-and-Setup, Extending-the-Template. **Caveat:** do not claim Cursor or OpenCode are behaviorally validated.

**Q: How do I create a new project from the template?**
- **Answer.** Run the template's `scripts/instantiate.sh "Project Name" --agent=claude-code` (Path B, local wiki), then commit and push. Path A adds `--github-wiki` and requires creating the wiki's first "Home" page in the GitHub UI first. You can add features with `--features=<name>`.
- **Must include:** run instantiate.sh with project name + --agent; Path B local vs Path A --github-wiki (Home page first); commit/push after.
- **Source:** Installation-and-Setup.

**Q: What does `scripts/instantiate.sh` do?**
- **Answer.** Substitutes placeholders in `CLAUDE.md.template`/`README.md.template`, initializes the wiki sub-repo via `init-wiki.sh`, strips KG sections if `scripts/kg/` is absent, configures the chosen agent overlay(s), then self-deletes after a successful run.
- **Must include:** substitutes placeholders; inits wiki sub-repo (init-wiki.sh); configures overlay; self-deletes.
- **Source:** Installation-and-Setup. **Caveat:** because it self-deletes, it is absent from already-instantiated projects.

**Q: What files land in a fresh project after instantiation?**
- **Answer.** A generated `CLAUDE.md` and `README.md`; the chosen overlay (Claude Code: `.claude/commands/wiki-*.md`, `.claude/skills/wiki-*.md`, `.claude/settings.json`, optional hooks); agent-agnostic policy files under `wiki/agents/`; and the wiki sub-repo at `wiki/<repo>.wiki/` seeded with Home, index, log, SCHEMA, Edge-Types.
- **Must include:** generated CLAUDE.md/README; overlay files; wiki/agents policy files; seeded wiki sub-repo.
- **Source:** Installation-and-Setup, Wiki-Structure-and-Conventions.

**Q: Why is the wiki a separate git repository?**
- **Answer.** Because it is durable memory with its own lifecycle, distinct from the code. As a sibling sub-repo at `wiki/<repo>.wiki/` it has its own history and remote (on GitHub, the built-in `<repo>.wiki.git`), so it can be pushed, cloned, and shared as a bundle independently, and wiki commits go in the wiki repo, not the project repo.
- **Must include:** own lifecycle/history/remote; sibling sub-repo; shareable independently as a bundle; wiki commits separate from project repo.
- **Source:** Installation-and-Setup.

**Q: How do I clone or bootstrap the wiki subdirectory?**
- **Answer.** `git clone https://github.com/<owner>/<repo>.wiki.git wiki/<repo>.wiki`, usually guarded by `[ -d wiki/<repo>.wiki ] ||` because the Claude Code SessionStart hook auto-clones it on first start. Teammates on other agents still get it via the explicit clone.
- **Must include:** git clone of the .wiki.git into wiki/<repo>.wiki; SessionStart hook auto-clones (so the guard); other agents clone explicitly.
- **Source:** Installation-and-Setup.

**Q: What does the SessionStart hook do (auto-clone the wiki)?**
- **Answer.** `ensure-wiki.py` runs on session start: if the wiki is absent it clones it non-interactively (30s timeout, no credential prompt) from the GitHub wiki URL derived from `origin`; if present and clean it fast-forwards it; on failure it falls back to nudging the agent to clone. A second hook, `session-start.sh`, surfaces the index and recent log. Installed by `setup.sh --hook`.
- **Must include:** ensure-wiki.py clones if absent / fast-forwards if present; non-interactive with timeout; derives URL from origin; second hook surfaces index+log.
- **Source:** Installation-and-Setup, Troubleshooting.

**Q: What is `init-wiki.sh` and when do I run it?**
- **Answer.** The agent-agnostic bootstrap/update tool for the wiki. `instantiate.sh` runs it during project creation; you run it directly only to scaffold a wiki manually or to bring an existing wiki's SCHEMA/CLAUDE.md up to current conventions. It is idempotent and auto-detects create-vs-update mode. Execute it; do not reimplement it.
- **Must include:** wiki bootstrap/update tool; idempotent, create-vs-update auto-detect; run by instantiate.sh; execute, don't reimplement.
- **Source:** Installation-and-Setup, Wiki-Structure-and-Conventions.

**Q: How do I set up the GitHub wiki remote?**
- **Answer.** Create the first "Home" page in the repo's wiki tab, which makes the `<repo>.wiki.git` remote exist; instantiating with `--github-wiki` wires it, and `ensure-wiki.py` derives the same URL from `origin` automatically. Push with `git -C wiki/<repo>.wiki push origin master` when publishing.
- **Must include:** create the Home page to make the wiki remote exist; --github-wiki wires it / hook derives from origin; push to origin master when publishing.
- **Source:** Installation-and-Setup.

**Q: How do I check the template version I am on?**
- **Answer.** Run `./scripts/check-template-version.sh` (read-only): it adds a `template` remote, fetches, and reports the template HEAD SHA, last sync, and per-file status (in sync / out of date / missing locally / not in template), pointing you at the update command if drift exists.
- **Must include:** check-template-version.sh; read-only; reports drift/per-file status; points to update-from-template.
- **Source:** Installation-and-Setup.

**Q: How do I pull template updates into an existing project?**
- **Answer.** Run `./scripts/update-from-template.sh` (preview with `--dry-run`). It syncs template improvements governed by a manifest (`scripts/lib/template-manifest.sh`) while preserving your `CLAUDE.md`, settings, hooks, wiki history, and source. A file not in the manifest does not propagate (which is why e.g. `scripts/kg/` may not arrive automatically).
- **Must include:** update-from-template.sh (--dry-run); manifest-governed; preserves CLAUDE.md/settings/wiki/code; non-manifest files don't propagate.
- **Source:** Installation-and-Setup, Extending-the-Template.

---

## Page 4: Everyday-Operations

**Q: How do I ingest a paper, article, or web page into the wiki?**
- **Answer.** Tell the agent to file it, or run `/wiki-source`: it reads the source, discusses takeaways, creates a `source-summary` page (with `up:`, `source:`, and clear typed edges), updates related pages and flags contradictions, fixes cross-references both ways, updates the index and log, optionally rebuilds the graph, runs the verification gate, and commits. Touches ~5-15 pages.
- **Must include:** /wiki-source or proactive; creates source-summary page; updates related pages + index + log; verification gate then commit.
- **Source:** Everyday-Operations.

**Q: How do I file the results of an experiment?**
- **Answer.** Run `/wiki-experiment` or ask the agent: read existing pages first, create/update a results page (config, headline metrics, what changed, what surprised, links to results/ and commit), update affected concept pages, fix cross-refs, update index/log, run the gate, commit. Honest reporting is mandatory: no metric from a projection.
- **Must include:** /wiki-experiment; record config/metrics/changes/surprises + links; honest reporting (no projections); gate then commit.
- **Source:** Everyday-Operations, Best-Practices.

**Q: How do I ask a question against my wiki?**
- **Answer.** Read the index, drill into relevant pages, synthesize with citations to page names. Use the KG for topology questions and file reads for content questions. If the answer is reusable, offer to file it back as a new page (often `type: analysis`).
- **Must include:** index → pages → synthesize with citations; topology→KG, content→file read; file reusable answers back.
- **Source:** Everyday-Operations.

**Q: How do I run a lint pass on the wiki?**
- **Answer.** Run `/wiki-lint` or ask for a health check: it scans for orphans, dead links, stale claims, missing frontmatter, untyped pages, missing concept pages, missing cross-references, index gaps, naming, and special-file integrity; reports grouped findings; asks which to fix (incremental); applies fixes with bidirectional cross-ref repair; updates index and log; commits.
- **Must include:** /wiki-lint; scans orphans/dead links/stale/missing frontmatter etc.; incremental (you pick fixes); logs the pass.
- **Source:** Everyday-Operations, Best-Practices.

**Q: What are the slash commands and what do they do?**
- **Answer.** Three, each a user-invokable front door to a model-side skill: `/wiki-source` (ingest an external source), `/wiki-experiment` (file experiment results), `/wiki-lint` (health-check and fix). They are a safety net for explicit invocation; the proactive default is that the agent runs the operations itself.
- **Must include:** /wiki-source, /wiki-experiment, /wiki-lint; each maps to a skill; safety net over a proactive default.
- **Source:** Everyday-Operations.

**Q: What does `/wiki-source` do, and when do I invoke it?**
- **Answer.** Runs the source-ingest procedure. Invoke it when a new external document should enter the project's memory and you want the ingest forced explicitly. Not for your own experiment results (use `/wiki-experiment`).
- **Must include:** ingest an external source; for external documents; not for experiment results.
- **Source:** Everyday-Operations.

**Q: What does `/wiki-experiment` do, and when do I invoke it?**
- **Answer.** Runs the experiment-ingest procedure. Invoke it after a run produces metrics/ablations/comparisons worth keeping. Skip a debug rerun with no new information or a config identical to one already filed.
- **Must include:** file experiment results; after a meaningful run; skip debug/duplicate runs.
- **Source:** Everyday-Operations.

**Q: What does `/wiki-lint` do, and when do I invoke it?**
- **Answer.** Runs the lint procedure. Invoke it every several sessions, after a major ingest that touched many pages, or when you notice a broken link or contradiction. It is incremental.
- **Must include:** health-check + fix; every several sessions / after big ingest / on noticing breakage; incremental.
- **Source:** Everyday-Operations, Best-Practices.

**Q: How do I add or edit a page by hand?**
- **Answer.** You can, following the SCHEMA: valid frontmatter with `type:`/`up:`, an opening summary line, a See also, and bidirectional cross-references; then run the verification gate and commit. Hand edits are fine, just held to the same conventions as the agent's writes.
- **Must include:** allowed; follow SCHEMA (frontmatter/type/up, See also, bidirectional links); run the gate and commit.
- **Source:** Everyday-Operations.

**Q: How do I get the LLM to update a page after new information arrives?**
- **Answer.** Tell it what changed; new information triggers an ingest. It updates the affected page, revises anything the change contradicts (flagging rather than silently overwriting), fixes cross-references, and logs it. The rule: trust what is observed now, update or flag the stale page.
- **Must include:** new info triggers ingest/update; flag contradictions rather than overwrite; trust current observation over stale claims.
- **Source:** Everyday-Operations, Best-Practices.

**Q: What is the Verification Gate and when does it fire?**
- **Answer.** A pre-commit checklist (`wiki/agents/verification-gate.md`) run after saving and before `git add`/`commit`: re-read each page, check corpus-tagged numbers, no cross-corpus gap arithmetic, every typed edge has a body back-reference, links resolve, valid frontmatter, analysis/decision required sections, index/log updated, Home for category changes, honest reporting. Fires on every ingest/experiment/lint write; fix and re-run until all pass.
- **Must include:** pre-commit checklist; re-read from disk; corpus tags / resolved links / back-references / index+log / honest reporting; fires before every commit.
- **Source:** Everyday-Operations, Best-Practices.

**Q: What is the wiki-write-protocol and when does it fire?**
- **Answer.** It governs pushing the wiki sub-repo when multiple agents may write concurrently, used in place of a plain `git push` (typically after an ingest/lint when you publish). It does an optimistic push with retry: index/log conflicts union-merge mechanically; genuine content conflicts are left with markers for the agent's next turn.
- **Must include:** governs push (not commit); optimistic push + retry; union-merge index/log, defer content conflicts; used instead of plain git push.
- **Source:** Everyday-Operations, Team-Workflow. **Caveat:** reference implementation shipped and CI-tested, but not wired into the overlay's default write path; invoke it deliberately when pushing.

---

## Page 5: Wiki-Structure-and-Conventions

**Q: What files exist in a new wiki after `init-wiki.sh`?**
- **Answer.** `Home_<project>.md` (human entry point), `Home.md` (GitHub redirect, never edited), `index_<project>.md` (catalog), `log_<project>.md` (append-only record), `SCHEMA_<project>.md` (conventions), and `Edge-Types.md` (typed-edge vocabulary). The `<project>` suffix namespaces special files for Obsidian-vault aggregation.
- **Must include:** Home_<project>, Home.md redirect, index_<project>, log_<project>, SCHEMA_<project>, Edge-Types; namespacing for vault aggregation.
- **Source:** Wiki-Structure-and-Conventions.

**Q: What is `Home_<project>.md` for?**
- **Answer.** The human-facing entry point: a project description plus a `## Categories` section mirroring the index's top-level categories with 1-3 representative links each. A curated nav surface, not a comprehensive catalog. Update it when a new top-level category emerges or a category-representative page lands.
- **Must include:** human entry point; Categories mirror index (1-3 links); curated not comprehensive; update on category-level changes.
- **Source:** Wiki-Structure-and-Conventions.

**Q: What is `index_<project>.md` for?**
- **Answer.** The content catalog: every page with a one-line description, organized by category. Updated on every ingest; read first when answering a query to find relevant pages. Replaces embedding-based RAG at moderate scale.
- **Must include:** catalog of every page + one-liner, by category; updated every ingest; read first on query.
- **Source:** Wiki-Structure-and-Conventions.

**Q: What is `log_<project>.md` for and how do I append to it?**
- **Answer.** The append-only chronological record. Each entry is `## [YYYY-MM-DD] <verb> | <Subject>` with a first bullet `- by: <human> via <agent>` (human = `git config user.name`, read not invented), then 2-5 bullets. Discipline: one commit per log entry, committed separately from page/index changes.
- **Must include:** append-only, dated verb|subject heading; first bullet is by: attribution; one commit per log entry.
- **Source:** Wiki-Structure-and-Conventions, Everyday-Operations.

**Q: What is `SCHEMA_<project>.md` and what does it define?**
- **Answer.** The authoritative conventions reference: page format, required/optional frontmatter, the analysis/decision structured page types, naming, cross-reference styles, edges-as-interface-operations, topology-vs-content guidance, log attribution, and the ingest/query/lint procedures. When any other doc disagrees, the SCHEMA wins for your project.
- **Must include:** authoritative conventions; frontmatter/page types/edges/procedures; SCHEMA wins on conflict.
- **Source:** Wiki-Structure-and-Conventions.

**Q: What is `Edge-Types.md` and how do I use it?**
- **Answer.** The canonical list of typed-edge predicates (16 forward: up, source, extends, supports, criticizes, concept, partOf, dependsOn, defines, resolvedBy, incorporatedInto, outOfScopeFor, precedes, feedsInto, related, mentions). Use it by choosing predicates for frontmatter and by inline Variant 1 body annotations. Inverses are materialized by the KG, never authored.
- **Must include:** canonical typed-edge vocabulary (16 forward predicates); used in frontmatter + inline Variant 1; inverses materialized by KG, not authored.
- **Source:** Wiki-Structure-and-Conventions, Knowledge-Graph.

**Q: What frontmatter fields are standard (type, up, area, source, related, extends, supports, criticizes)?**
- **Answer.** Required: `type:` and `up:`. Optional/common: `tags:` and typed edges `source:`, `extends:`, `supports:`, `criticizes:`, `related:` (plus `derived_from:` for analysis, `decided_at:` for decision). `area:` is not a standard authored field in this template (tags plays the topical role; area is KG-materialized). Every page gets frontmatter; use `type: untyped` rather than skip.
- **Must include:** required type + up; optional tags + typed edges; area is NOT standard-authored (tags instead); every page has frontmatter.
- **Source:** Wiki-Structure-and-Conventions. **Caveat:** do not claim `area:` is a standard authored field; correct the seed's list.

**Q: What node types are recognized (Concept, Synthesis, Entity, Index, SourceSummary, etc.)?**
- **Answer.** The SCHEMA `type:` vocabulary: concept, entity, source-summary, synthesis, analysis, decision, index, comparison, untyped. Most have no required structure; analysis (Question/Context/Analysis/Conclusion/Open follow-ups + `derived_from:`) and decision (Question/Options/Decision/Rejected alternatives/Revisit triggers + `decided_at:`) are the two structured ones.
- **Must include:** the type: values; analysis and decision have required sections; the KG ontology node names are near-equivalents.
- **Source:** Wiki-Structure-and-Conventions.

**Q: How do I link between pages (wikilinks vs `[Text](Target)` cross-references)?**
- **Answer.** Body text uses `[Display](Page-Name)` (GitHub-wiki style, emits a `mentions` edge); frontmatter edge fields use `[[Page-Name]]` (Obsidian style, emits the typed edge). Link concepts on first mention, aim for 2+ inbound and outbound, keep links bidirectional.
- **Must include:** body = [Display](Page-Name)=mentions; frontmatter = [[Page-Name]]=typed edge; bidirectional.
- **Source:** Wiki-Structure-and-Conventions.

**Q: Does the difference between a wikilink and a body cross-reference matter for the graph?**
- **Answer.** Yes. A `[[Page]]` in a frontmatter edge field carries that field's typed predicate; a `[Display](Page)` body link emits a generic `mentions` edge (RDF-star weighted). Frontmatter edges are the semantically rich, queryable relationships; body links are the navigational mesh. Inline Variant 1 can make a body link also carry a typed predicate.
- **Must include:** yes; frontmatter=typed predicate, body=mentions; frontmatter is the queryable semantics.
- **Source:** Wiki-Structure-and-Conventions, Knowledge-Graph.

**Q: What is a hub page and how does one become a hub?**
- **Answer.** A page with many inbound links, one others repeatedly reference (indexes, foundational concepts, heavily-cited findings). The KG materializes a hub flag so topology queries can find them. You don't declare a hub; it emerges from how often others link to it.
- **Must include:** many inbound links; emerges, not declared; KG materializes a hub flag.
- **Source:** Wiki-Structure-and-Conventions, Knowledge-Graph.

**Q: What is an orphan page and how do I fix one?**
- **Answer.** A page with no inbound links from any page or the index, invisible to navigation and retrieval. Fix it by linking it in from a relevant parent/sibling (and adding its index entry), or flag it for archival. Orphan detection is a standard lint check.
- **Must include:** no inbound links / invisible; fix by linking in + index entry (or archive); a lint check.
- **Source:** Wiki-Structure-and-Conventions, Everyday-Operations.

---

## Page 6: Best-Practices

**Q: What content belongs in the wiki?**
- **Answer.** Durable understanding a future session or teammate would benefit from: experiment results, decisions with reasons, reusable syntheses, source summaries, contradictions of prior claims, and reusable query answers.
- **Must include:** durable/reusable knowledge; experiments, decisions, syntheses, source summaries; things a future session needs.
- **Source:** Best-Practices.

**Q: What content should stay out of the wiki?**
- **Answer.** Routine debugging/code fixes (git history is enough), temporary analysis you won't reference again, unexecuted speculative plans, and anything that must not be in a shared versioned artifact (secrets, private data).
- **Must include:** routine debugging; throwaway/temporary; unexecuted speculation; secrets/private data.
- **Source:** Best-Practices, When-to-Use-When-Not.

**Q: How often should I commit? Should I let the LLM commit for me?**
- **Answer.** Commit every wiki edit; the agent commits without asking because local commits are trivially reversible. The discipline: run the verification gate, then commit pages+index as one commit and the log entry as its own separate commit. Letting the LLM commit is the intended default; you review the diff.
- **Must include:** commit every edit; agent commits without asking (reversible); one commit per log entry, separate from pages.
- **Source:** Best-Practices, Everyday-Operations.

**Q: Should I push the wiki, or keep it local until published?**
- **Answer.** Keep it local by default; pushes are explicit (human asks or agent asks first). Commit freely; push only to publish, and when you do, use the write protocol rather than a plain `git push`.
- **Must include:** local by default, explicit push; commit freely; use the write protocol to push.
- **Source:** Best-Practices, Team-Workflow.

**Q: How do I organize pages when the wiki gets larger?**
- **Answer.** Lean on index categories and the `up:` hierarchy; promote a repeatedly-mentioned concept to its own page; let hubs emerge as entry points; keep Home's Categories curated as top-level categories appear.
- **Must include:** index categories + up: hierarchy; promote recurring concepts to pages; use hubs; curate Home.
- **Source:** Best-Practices, Wiki-Structure-and-Conventions.

**Q: When should I use `extends:` versus `related:`?**
- **Answer.** Use the most specific edge you can justify; `related:` is the fallback. `extends:` = intellectual lineage (build on/refine the target, inheriting its claims as background). But when a note is written mid-work and the relation is genuinely uncertain, `related:` is the correct honest choice; don't manufacture crispness.
- **Must include:** most-specific edge; extends = lineage/inherit context; related = honest fallback when uncertain.
- **Source:** Best-Practices, Wiki-Structure-and-Conventions.

**Q: Is aggressive typed-edge discipline worth the effort for my project?**
- **Answer.** It depends on content shape. Bibliographic/review wikis (objectively typeable) reward aggressive typing; experimental/research wikis (provisional, in-progress) are where forcing crisp types backfires and downstream queries over-claim. Match the discipline to the material.
- **Must include:** depends on content shape; review/bibliographic → yes; experimental/provisional → no; match to material.
- **Source:** Best-Practices, Knowledge-Graph. **Caveat:** the review-vs-experimental distinction is vision-wiki framing.

**Q: How do I document a failed experiment honestly?**
- **Answer.** File it plainly, no polishing. Never report a number from a projection, only from a real script output, and tag every number with its corpus/config scope. An honestly recorded failure saves a future session from repeating it (the experience layer).
- **Must include:** file plainly, no hedging; no projected metrics; corpus-tag numbers; failures are high-value memory.
- **Source:** Best-Practices, Everyday-Operations.

**Q: How do I record decisions so my future self can find them?**
- **Answer.** Use a `type: decision` page with the required sections: Question, Options considered (pros/cons), Decision, Rejected alternatives (and why), Revisit triggers, plus `decided_at:`. Recording the rejected options and revisit triggers is what makes it useful later.
- **Must include:** type: decision page; Question/Options/Decision/Rejected alternatives/Revisit triggers + decided_at.
- **Source:** Best-Practices, Wiki-Structure-and-Conventions.

**Q: How do I keep the wiki healthy over months of use?**
- **Answer.** Run lint periodically, commit and cross-reference as you go rather than deferring ("later" is a named always-wrong rationalization), and update or flag pages when new work contradicts them. Health is a byproduct of not deferring the bookkeeping.
- **Must include:** periodic lint; don't defer cross-refs/commits; flag/update contradictions; health = no deferral.
- **Source:** Best-Practices, Team-Workflow.

**Q: Should I let the LLM auto-write pages, or approve every one?**
- **Answer.** A workflow choice. The proactive default is the agent writing and committing without asking; for high-stakes or shared bundles, review each page; for a fast personal deep-dive, let it run and review in batches. Commits are reversible, so over-delegating is cheap to undo.
- **Must include:** workflow choice; proactive default vs approve-each; reversible so low cost.
- **Source:** Best-Practices.

**Q: How do I review LLM-authored content critically?**
- **Answer.** Read for the discipline-gate failure modes: projection presented as fact, numbers without a corpus tag, cross-corpus gaps stated as direct, missing back-references, contradictions papered over. Check typed edges reflect real relationships. Trust current code/results over any wiki claim and flag stale pages.
- **Must include:** watch for projection-as-fact / untagged numbers / missing back-refs / hidden contradictions; verify edges; trust observation over stale claims.
- **Source:** Best-Practices, Team-Workflow.

**Q: How do I capture expertise and experience, not just facts?**
- **Answer.** Facts fall out of ingest by default; expertise and experience take deliberate prompting. Use the per-page checklist: knowledge check (facts/citations), expertise check (is my judgment visible, why this framing, are edges honest), experience check (concrete cases, what I tried, what surprised me). The experience check is most often skipped.
- **Must include:** deliberate prompting; knowledge/expertise/experience checks; synthesis pages, decision records, "considered and rejected", dated logs; experience most-skipped.
- **Source:** Best-Practices, Template-Philosophy. **Caveat:** the three-layer authoring checklist is vision-wiki framing.

**Q: Do I need to run `/wiki-lint` regularly, and when?**
- **Answer.** Yes, incrementally: every several sessions, when the wiki has grown ~10+ pages since the last pass, after a major ingest, or when you notice a broken link or contradiction. Fix what matters this pass and log it.
- **Must include:** yes, incremental; every several sessions / +10 pages / after big ingest / on noticing breakage.
- **Source:** Best-Practices, Everyday-Operations.

---

## Page 7: Knowledge-Graph

**Q: Why does the template build a knowledge graph from the wiki?**
- **Answer.** To answer topology questions the prose can't ("which pages cite X?", "what extends this transitively?"). The frontmatter typed edges already encode the relationships; the KG makes them queryable. Without typed edges it collapses to a flat `mentions` mesh; typing turns it from a navigation aid into a reasoning substrate.
- **Must include:** topology questions; typed edges → queryable; typing = reasoning substrate vs flat mentions.
- **Source:** Knowledge-Graph.

**Q: Do I need to know SPARQL to use the template?**
- **Answer.** No. The wiki works fully without the graph (index navigation + file reads). The KG is opt-in for topology/maintenance, and the template ships canned SPARQL queries so you rarely write SPARQL yourself.
- **Must include:** no; KG is opt-in; canned queries ship.
- **Source:** Knowledge-Graph.

**Q: How do I rebuild the graph after wiki edits?**
- **Answer.** Run `./scripts/kg/build-graph.sh` (idempotent). Flags: `--wiki=PATH`, `--refresh-spec`, `--stats`, `--help`. Rebuild after each ingest or periodically.
- **Must include:** ./scripts/kg/build-graph.sh; idempotent; after ingest.
- **Source:** Knowledge-Graph.

**Q: What does `scripts/kg/build-graph.sh` do?**
- **Answer.** A thin shell entry point over `build-graph.py`: walks the wiki, extracts frontmatter and body links (via `wiki-to-jsonld.py`), produces the graph as JSON-LD and Turtle, materializes inverses/hubs/area inheritance, and runs SHACL validation, all in-process Python (rdflib + pyshacl). It does not abort on validation failures; it writes the report.
- **Must include:** extract frontmatter+links; emit JSON-LD + Turtle; materialize + SHACL; in-process rdflib+pyshacl; does not abort on violations.
- **Source:** Knowledge-Graph.

**Q: What does `wiki-to-jsonld.py` extract from the wiki?**
- **Answer.** The frontmatter typed-edge fields (as typed edges) and body cross-references (as `mentions` edges), plus inline Variant 1 annotations and HTML-comment attributes. Pages without frontmatter are included as `untyped` nodes, so nothing is dropped.
- **Must include:** frontmatter typed edges + body mentions; recognizes Variant 1 annotations; untyped nodes for no-frontmatter pages.
- **Source:** Knowledge-Graph.

**Q: What outputs land in `scripts/kg/build/` and what is each for?**
- **Answer.** `graph.jsonld` (JSON-LD from extractor), `graph.ttl` (Turtle + RDF-star weights), `graph-weights.ttl` (weighted mentions), `graph-full.ttl` (graph.ttl + materialized inverses/hubs/area inheritance, the one to query), `validation-report.ttl` (SHACL report). The directory is gitignored/runtime-only.
- **Must include:** graph.jsonld / graph.ttl / graph-weights.ttl / graph-full.ttl / validation-report.ttl; graph-full is the query target; gitignored.
- **Source:** Knowledge-Graph.

**Q: What is RDF Turtle, and why does the template use it?**
- **Answer.** A compact, human-readable text serialization of an RDF graph as subject-predicate-object triples. The template uses it because it is the standard, tool-agnostic interchange format: rdflib reads/writes it natively, it loads into any triplestore, and it diffs in git. JSON-LD is the extractor's native output.
- **Must include:** text serialization of RDF triples; standard/interchange; rdflib-native, git-diffable; JSON-LD also emitted.
- **Source:** Knowledge-Graph, Concepts-Glossary.

**Q: What is materialized (inverses, area inheritance, hub flags) and why?**
- **Answer.** Derived triples computed once at build time (via SPARQL CONSTRUCT) so queries don't have to: inverse edges (each forward edge gets its inverse, so traversal works either direction, which is why agents never author inverses), area inheritance (a page inherits area/domain from its hierarchy), and hub flags (many-inbound pages flagged). 
- **Must include:** derived triples computed at build; inverses (both-direction traversal, not hand-authored); area inheritance; hub flags.
- **Source:** Knowledge-Graph.

**Q: What SPARQL queries ship with the template?**
- **Answer.** A curated set under `scripts/kg/sparql/` (11 in this bundle): ancestors-of, children-of, extension-chains, graph-stats, hub-notes, note-neighborhood, notes-by-tag, notes-by-type, orphan-notes, search-by-title, supports-criticizes. They cover common topology and maintenance questions without your writing SPARQL.
- **Must include:** curated set in scripts/kg/sparql/; hub/orphan/extension-chain/neighborhood etc.; cover common topology/maintenance.
- **Source:** Knowledge-Graph.

**Q: When would I write my own SPARQL query?**
- **Answer.** When your topology question isn't covered by the canned set: a domain-specific traversal, a multi-hop pattern particular to your edge vocabulary, or a custom health check. Only for topology; for content, read the file.
- **Must include:** uncovered topology question / custom traversal or health check; topology only, not content.
- **Source:** Knowledge-Graph.

**Q: What is SHACL validation and what does a failure mean?**
- **Answer.** SHACL is a constraint language for RDF; shapes describe what a conformant graph should look like (node types, required predicates, edge domain/range). `pyshacl` checks the graph against fetched `shapes.ttl` and writes `validation-report.ttl`. A failure (shape violation) means a page's frontmatter doesn't satisfy a shape. The build reports but does not abort.
- **Must include:** constraint language / shapes; violation = frontmatter doesn't conform; report written, build does not abort.
- **Source:** Knowledge-Graph, Troubleshooting.

**Q: Why is the pipeline in Python (rdflib + pyshacl) rather than Java (Jena)?**
- **Answer.** So the whole pipeline is a `pip install` away with no system-level dependencies: no Java, no Jena, no Fuseki by default. Parsing, serialization, materialization (SPARQL CONSTRUCT via rdflib), and SHACL validation all run in-process, keeping the agent-tool layer's graph calls in-process rather than subprocess CLIs.
- **Must include:** no Java/Jena/Fuseki dependency; pip-only; in-process (calls not subprocess).
- **Source:** Knowledge-Graph.

**Q: When would I switch to a Fuseki endpoint?**
- **Answer.** When you need a live SPARQL endpoint for multiple concurrent clients, agent-write via SPARQL UPDATE, federated queries across wikis, or a web dashboard. Jena Fuseki can host `graph-full.ttl` and rdflib talks to it via `SPARQLStore` with no tool-code change. Opt-in; the default is in-process.
- **Must include:** multi-client / SPARQL UPDATE / federation / dashboard; Fuseki hosts graph-full.ttl; opt-in over the in-process default.
- **Source:** Knowledge-Graph. **Caveat:** a future cross-session agent-memory feature is expected to depend on Fuseki; do not claim it is default.

---

## Page 8: Team-Workflow

**Q: Can multiple people edit the same wiki concurrently?**
- **Answer.** Yes; the wiki is a shared git repo, so people and their agents pull/edit/commit/push like any repo. The template adds a coordination layer (the write protocol) for the near-simultaneous-push case. Production wikis routinely have 3-4 writers.
- **Must include:** yes, shared git repo; write protocol coordinates concurrent pushes; multi-writer is the real case.
- **Source:** Team-Workflow.

**Q: How do we handle merge conflicts on the wiki?**
- **Answer.** Index and log files union-merge mechanically via `.gitattributes merge=union` (both writers' appended entries survive, in commit order). Content pages conflict only on the same lines of the same section; then a marked file is left for the resolving agent to reconcile (drop/adapt/supersede). Different pages/sections three-way-merge cleanly.
- **Must include:** index/log union-merge automatically; content conflicts only on same lines/section; agent resolves marked conflicts.
- **Source:** Team-Workflow, Troubleshooting.

**Q: What is the wiki-write-protocol (`wiki_push`), and why not just `git push`?**
- **Answer.** An optimistic-push-with-retry wrapper. Plain `git push` is rejected when someone pushed first, forcing manual back-out; `wiki_push` instead fetches, merges (union-merge for index/log), resolves content conflicts, and retries up to a cap, so only one ref-update lands at a time and `main` is never half-merged. From outside it is a normal git repo with merge commits.
- **Must include:** optimistic push + retry; avoids the plain-push rejection/back-out; union-merge + semantic resolve; atomic main.
- **Source:** Team-Workflow, Everyday-Operations. **Caveat:** reference impl shipped (9 CI scenarios) but not yet wired into the default write path; single-writer projects can push normally.

**Q: What is the discipline-gates document and how does it protect us?**
- **Answer.** `wiki/agents/discipline-gates.md`, the agent-agnostic enforcement layer shared across overlays. It names the "Universal Rationalizations (Always Wrong)" and their counters, plus three gate types (Design, Verification, Sequential) and a skill-dependency chain. It converts honesty rules into pre-write checks so one contributor's shortcut doesn't pollute shared memory.
- **Must include:** agent-agnostic; Universal Rationalizations table + gate types; pre-write enforcement of honesty; Verification Gate is its canonical instance.
- **Source:** Team-Workflow.

**Q: Can students see the faculty's wiki?**
- **Answer.** Yes, if published; a wiki is a git repo, so visibility is whatever the remote grants (public GitHub wiki or granted access on a private one). The intended student flow is exactly this: faculty publish a bundle, students clone or `ask` against it. There is no per-page access control; the unit of sharing is the repo.
- **Must include:** yes if published; visibility = git remote; unit of sharing is the repo, no per-page control.
- **Source:** Team-Workflow, Knowledge-Bundles-Overview. **Caveat:** fine-grained per-page/per-student access is not documented in the template.

**Q: How do we share wikis across labs or institutions?**
- **Answer.** Publish the wiki sub-repo to a remote the other group can clone; read-only (their wiki alongside yours) or merged (folded in with namespace prefixes and provenance). The `agent-comms` feature adds a federation index and an `ask` primitive so agents discover and query peer bundles cross-org via a trusted-owner allowlist.
- **Must include:** publish + clone; read-only vs merged composition; agent-comms federation index + ask (allowlist).
- **Source:** Team-Workflow, Knowledge-Bundles-Overview. **Caveat:** federation discovery is part of the agent-comms feature, not the base template.

**Q: Can I clone another group's wiki as a reference?**
- **Answer.** Yes: `git clone` and read directly, point an LLM at it, or use `agent-comms` `ask` (clones into a cache, runs an LLM query, returns the answer without involving the peer). Reference-only consumption requires no merge.
- **Must include:** yes, git clone; or ask (clone-and-invoke into cache); no merge needed.
- **Source:** Team-Workflow, Knowledge-Bundles-Overview.

**Q: What happens if two LLM agents write to the wiki at the same time?**
- **Answer.** The write protocol serializes them at the push level: first push wins; the second fetches, merges (index/log auto-merge), resolves any content overlap semantically, and retries. Same-new-page collisions: one becomes base, the other folds in. Hitting the retry cap halts and surfaces the situation, preserving un-pushed commits. It is OCC with the LLM as semantic resolver.
- **Must include:** serialize at push; first wins, second merges+retries; retry cap halts; OCC + LLM resolver.
- **Source:** Team-Workflow. **Caveat:** protocol is reference-impl, not default-wired.

**Q: How do we assign attribution when the LLM authors most of the content?**
- **Answer.** Via the log attribution convention: each log entry's first bullet is `- by: <human> via <agent>` (human = `git config user.name`, read not invented), and one-commit-per-log-entry keeps `git blame` a faithful per-author record. Attribution is to the directing human via the agent; git history is the verifiable copy.
- **Must include:** by: <human> via <agent>; human from git config; one commit per entry; git is the verifiable record.
- **Source:** Team-Workflow, Wiki-Structure-and-Conventions.

**Q: How does licensing work if we share the wiki publicly?**
- **Answer.** Not specified by the template. The wiki is a git repo of Markdown; licensing is whatever `LICENSE` you place in it. The template ships no default wiki license or guidance; add one explicitly when publishing. (The KG extractor code is separately MIT-derived from `LA3D/llm-wiki-colab`, which concerns tooling, not your content.)
- **Must include:** not specified by the template; add your own LICENSE; no default shipped.
- **Source:** Team-Workflow. **Caveat:** must state licensing is not documented/specified; do not invent a default license.

---

## Page 9: Knowledge-Bundles-Overview

**Q: What is a knowledge bundle in the llm-wiki context?**
- **Answer.** A portable, git-distributable, LLM-authored wiki on a specific topic, consumed through an LLM ask session. Bundles ship today as GitHub-wiki-format template instances (Markdown + frontmatter + wikilinks, their own index/log, optional extracted graph). The bundle format is the wire format; the template's contribution is the discipline layer, with the agent as primary maintainer. A good bundle carries knowledge, expertise, and experience.
- **Must include:** portable LLM-authored topical wiki; consumed via LLM ask; format=wire, discipline=contribution; agent is maintainer.
- **Source:** Knowledge-Bundles-Overview.

**Q: How is a bundle different from a wiki?**
- **Answer.** A bundle is a wiki viewed as a distributable product rather than a project's working memory; the difference is stance and packaging, not format. A wiki is primarily written/read by its own project; a bundle is curated on a topic and shared for others to consume, carrying its own index/log so it is self-describing when cloned.
- **Must include:** same format; difference is stance/packaging; bundle = shareable/self-describing product.
- **Source:** Knowledge-Bundles-Overview.

**Q: How do I create a bundle from my wiki?**
- **Answer.** Author the wiki with the normal operations; a bundle is what you have once it's worth sharing. Ensure it is a self-contained git repo (the sub-repo already is), that index/log are current, optionally build the graph, then `git push` the wiki sub-repo to a shareable remote.
- **Must include:** author via normal operations; self-contained sub-repo + current index/log; push to a shareable remote.
- **Source:** Knowledge-Bundles-Overview.

**Q: How do I consume a bundle authored by someone else?**
- **Answer.** Read-only (clone alongside your wiki as a separate graph; retrieval walks both) or merged (fold in with namespace prefixes and provenance to make a personalized derivative). At its simplest, point an LLM session at the cloned Markdown and ask, which is what the `ask` primitive does.
- **Must include:** read-only vs merged; walk both graphs / fork analogy; ask = point LLM at cloned bundle.
- **Source:** Knowledge-Bundles-Overview, Team-Workflow.

**Q: What existing topical bundles are available (knowledge engineering, LLMs, others)?**
- **Answer.** The vision wiki names topical bundles on knowledge engineering and LLMs (and "other domains") that students already use; the loop is described as operational, not aspirational. A precise current catalog is not enumerated in the template's own docs.
- **Must include:** knowledge engineering and LLMs named; student loop operational; no exhaustive catalog in the docs.
- **Source:** Knowledge-Bundles-Overview. **Caveat:** do not invent a specific bundle list beyond the named examples.

**Q: How do students consume a bundle via their own LLM?**
- **Answer.** They point their LLM at the faculty-authored bundle; ask sessions become grounded in its material because retrieval walks the bundle's graph alongside their own notes, and the LLM cites specific bundle pages leading back to faculty explanations. The `agent-comms` `ask` primitive operationalizes an agent-to-agent version (clone into cache, query, return).
- **Must include:** LLM grounded in the bundle; cites bundle pages back to faculty; ask primitive automates clone-and-query.
- **Source:** Knowledge-Bundles-Overview.

**Q: Can I extend a bundle with my own notes?**
- **Answer.** Yes; that is the merged-consumption pattern and the intended student workflow. You file your own notes/solutions/questions into your local wiki cross-referencing the bundle, producing a personalized derivative walked by the same retrieval. Faculty can absorb strong student contributions into the next version.
- **Must include:** yes, merged consumption; personalized derivative; bidirectional (faculty can absorb back).
- **Source:** Knowledge-Bundles-Overview.

**Q: Will the template support OKF (Google Open Knowledge Format) import/export? What for?**
- **Answer.** Planned, not yet shipped. The vision wiki says the template "will add OKF import and export"; the template wiki's OKF-Alignment-Ideas is an analysis of how, not a landed feature. Purpose: OKF v0.1 is a minimal permissive Markdown+frontmatter standard, so conforming lets any OKF-aware tool read the bundles and lets adopt/ask consume bundles authored elsewhere ("OKF + the discipline layer"). Internal storage stays GitHub wiki.
- **Must include:** planned/analysis stage, NOT shipped; OKF = minimal MD+frontmatter standard; interop purpose; storage stays GitHub wiki.
- **Source:** Knowledge-Bundles-Overview, Concepts-Glossary. **Caveat:** must state OKF import/export is not implemented; presenting it as shipped is a fail.

---

## Page 10: Troubleshooting

**Q: The wiki is not loading at session start. What do I check?**
- **Answer.** (1) origin remote exists and is GitHub (the hook is GitHub-only); (2) the wiki's Home page has been created (a GitHub wiki isn't clonable until it exists); (3) the clone is reachable non-interactively (no credential prompt / private access set up); (4) python3 is on PATH (the hook no-ops without it). Manual fix: `git clone <owner>/<repo>.wiki.git wiki/<repo>.wiki`.
- **Must include:** GitHub origin; Home page created; non-interactive/reachable clone; python3 present; manual clone fallback.
- **Source:** Troubleshooting, Installation-and-Setup.

**Q: The graph build failed. What is the first thing to look at?**
- **Answer.** Dependencies: Bash 4+ and Python 3 with PyYAML, rdflib, pyshacl (a missing package is the common cause). Then the wiki path (`--wiki=PATH`) and the spec fetch (`--refresh-spec`). The build does not abort on SHACL violations, so a "failure" is usually a dependency or path error, not a validation error.
- **Must include:** check deps (PyYAML/rdflib/pyshacl) first; then path/spec; SHACL violations don't fail the build.
- **Source:** Troubleshooting, Knowledge-Graph.

**Q: The LLM keeps writing pages without asking. How do I slow it down?**
- **Answer.** Proactive writing is the intended default (and it commits without asking because commits are reversible). To get approval-first behavior, instruct the agent to propose before writing, or invoke operations explicitly via the slash commands, or soften the wiki-maintenance guidance in your CLAUDE.md (keep edits outside the template's sentinel blocks). Over-eager writes undo cheaply with `git reset`.
- **Must include:** proactive is by design; ask for approval-first / use slash commands / edit CLAUDE.md guidance; reversible via git reset.
- **Source:** Troubleshooting, Best-Practices.

**Q: I have a merge conflict on the wiki. What is the safe recovery?**
- **Answer.** Index/log conflicts shouldn't reach you (union-merge). For a content page, read both sides, decide drop/adapt/supersede, write the merged content, add/commit, re-run the push. If mid-`wiki_push` at the retry cap, your un-pushed commits are preserved on local `main`: inspect, then retry, reset to abandon, or cherry-pick.
- **Must include:** index/log auto-merge; content: resolve markers (drop/adapt/supersede) then re-push; retry-cap preserves un-pushed commits.
- **Source:** Troubleshooting, Team-Workflow.

**Q: The wiki has grown too large to browse. How do I archive old content?**
- **Answer.** No built-in archival command; it is manual and git-native. Move superseded pages to an `archive/` subdir (fixing up: and cross-refs) or mark stale pages with a pointer to the superseding page during lint; git retains anything removed. Practically, lean on index categories and hubs rather than browsing everything.
- **Must include:** no built-in command / manual git-native; archive subdir or mark-stale-and-point; lean on index/hubs.
- **Source:** Troubleshooting, Wiki-Structure-and-Conventions. **Caveat:** do not claim an archival command exists.

**Q: The LLM is citing pages that no longer exist. What happened, and how do I fix it?**
- **Answer.** A page was renamed/removed but an inbound link or index entry wasn't updated, leaving a dead link the agent then cites. Run `/wiki-lint` (scans dead links and index gaps and repairs them) or fix the target by hand. The verification gate should catch this at write time, so a dead link usually means a write skipped the gate.
- **Must include:** dead link from rename/removal not propagated; fix via lint (or by hand); gate should prevent it.
- **Source:** Troubleshooting, Everyday-Operations.

**Q: SHACL validation is failing. What is a shape violation and how do I read the report?**
- **Answer.** A violation means a page's frontmatter doesn't satisfy a SHACL shape (edge pointing at the wrong target type, missing required field, constrained node type). The report is `scripts/kg/build/validation-report.ttl` (Turtle); read it for the focus node (which page), the path (which predicate), and the failed constraint. It is advisory: the build does not abort. Fix the frontmatter and rebuild.
- **Must include:** violation = frontmatter doesn't conform to a shape; report is validation-report.ttl (focus node/path/constraint); advisory, non-aborting.
- **Source:** Troubleshooting, Knowledge-Graph.

**Q: I accidentally committed private content to the wiki. How do I unwind?**
- **Answer.** If not pushed: `git -C wiki/<repo>.wiki reset` (soft/hard) before it leaves your machine, which is why commits stay local and pushes explicit. If pushed: treat it as a leaked secret (rotate anything sensitive), then rewrite history (`git filter-repo`) and force-push, coordinating with other writers. Prevention: keep secrets out of the wiki entirely.
- **Must include:** not pushed → git reset (local/reversible); pushed → rotate secrets + rewrite history + force-push + coordinate; prevention.
- **Source:** Troubleshooting, Best-Practices.

**Q: The `SessionStart` hook did not clone the wiki. What do I do?**
- **Answer.** Same causes as "wiki not loading": non-GitHub origin, Home page not created, unreachable/private clone, or missing python3. The hook fails quietly and nudges rather than blocking, so a silent non-clone is expected under those conditions. Manual remedy: the explicit `git clone`. If present but stale, it only fast-forwards when clean, so commit/stash local changes.
- **Must include:** GitHub origin / Home page / reachable clone / python3; fails quietly by design; manual clone; clean tree needed for fast-forward.
- **Source:** Troubleshooting, Installation-and-Setup.

**Q: `arq` or `rdflib` is not installed. Which error indicates which?**
- **Answer.** Correction: the default KG pipeline uses rdflib + pyshacl in-process Python, not `arq` (arq is Jena's SPARQL CLI). On the default path you'd only see a Python `ModuleNotFoundError`/`ImportError` naming rdflib/pyshacl/PyYAML (fix: `pip install rdflib pyshacl pyyaml`). An `arq: command not found` means you're on the optional Fuseki/Jena path, not the default.
- **Must include:** default uses rdflib+pyshacl NOT arq; rdflib missing = Python module error; arq missing = the optional Jena path.
- **Source:** Troubleshooting, Concepts-Glossary. **Caveat:** must correct the seed's premise that `arq` is part of the default pipeline.

---

## Page 11: Extending-the-Template

**Q: Can I add my own slash commands? Where do they go?**
- **Answer.** Yes: Claude Code slash commands live in `.claude/commands/<name>.md`, each referencing a model-side skill in `.claude/skills/<name>.md`. Model them on the shipped `wiki-*` pairs. Since sync only manages manifest-listed files, your own command/skill files survive `update-from-template.sh`.
- **Must include:** yes; .claude/commands/<name>.md (+ optional skill); untouched by template updates (not in manifest).
- **Source:** Extending-the-Template.

**Q: Can I add my own skills (model-side procedures)?**
- **Answer.** Yes: drop a `.claude/skills/<name>.md` file. Keep a skill and its slash command in sync if paired (parallel-file drift is a known footgun). For substantial, optional, removable capabilities prefer packaging as a feature.
- **Must include:** yes, .claude/skills/<name>.md; keep paired command/skill in sync; prefer a feature for big capabilities.
- **Source:** Extending-the-Template.

**Q: Can I add custom edge types beyond the standard vocabulary?**
- **Answer.** Yes, by editing `Edge-Types.md` to add the predicate (and its inverse convention). The vocabulary is meant to extend (heavy `related:` use is a signal to extend it). Caveat: the KG resolves predicates against the LA3D ontology and SHACL shapes, so a brand-new predicate is carried through but won't get a materialized inverse or shape-checking until the upstream spec knows it.
- **Must include:** yes, edit Edge-Types.md; vocabulary is extensible; caveat: no materialized inverse / SHACL check until upstream ontology recognizes it.
- **Source:** Extending-the-Template. **Caveat:** custom edges are locally usable but not fully KG-integrated without upstream ontology support.

**Q: Can I add custom node types?**
- **Answer.** Yes: `type:` is open, add a value and use it. Only analysis/decision carry required-section contracts; a custom type has no required structure. Unknown types are tolerated (carried through as-is), but only shape-validated to the extent the upstream SHACL spec knows them.
- **Must include:** yes, type: is open; custom types have no required structure; tolerated but limited SHACL validation.
- **Source:** Extending-the-Template.

**Q: Can I use a different LLM agent than the ones supported out of the box?**
- **Answer.** The template ships Claude Code (validated), Cursor (structural only), and `--agent=none`. For another agent, either use minimal mode (the agent reads CLAUDE.md/AGENTS.md and follows the procedures) or author a new overlay under `wiki/agents/<overlay>/` with that agent's surfaces plus a `setup.sh`. The core pattern is agent-agnostic; only the injection mechanism differs.
- **Must include:** minimal mode or author a new overlay under wiki/agents/<overlay>/; core is agent-agnostic.
- **Source:** Extending-the-Template, Installation-and-Setup. **Caveat:** whether a given non-instructed agent follows procedures is empirically open.

**Q: Can I add my own SPARQL queries to the library?**
- **Answer.** Yes: drop a `.rq` file into `scripts/kg/sparql/`. The shipped set is a starting library, not a ceiling; your queries run against the same `graph-full.ttl`.
- **Must include:** yes, add .rq to scripts/kg/sparql/; runs against graph-full.ttl.
- **Source:** Extending-the-Template, Knowledge-Graph.

**Q: Can I export the wiki to a different format?**
- **Answer.** Partly. Today the wiki is Markdown+frontmatter in git (any Markdown tool reads it), and the KG exports JSON-LD and Turtle. A dedicated OKF export is analyzed but not shipped (a `scripts/export-okf.sh` is discussed and deferred). For now, export means cloning the Markdown or using the emitted `.ttl`/`.jsonld`.
- **Must include:** Markdown + KG (JSON-LD/Turtle) today; OKF export analyzed but NOT shipped.
- **Source:** Extending-the-Template, Knowledge-Bundles-Overview. **Caveat:** OKF export is not implemented.

**Q: Can I add project-specific rules to `CLAUDE.md` without breaking template updates?**
- **Answer.** Yes: `CLAUDE.md` is host-owned; `update-from-template.sh` preserves it. The template injects its managed subsections behind paired HTML-comment sentinels (`<!-- lw:wiki-maintenance -->` ... `<!-- /lw:wiki-maintenance -->`) and only re-injects between its own sentinels. Keep your rules outside those blocks and they survive updates.
- **Must include:** CLAUDE.md host-owned/preserved; template edits only between its sentinels; put your rules outside them.
- **Source:** Extending-the-Template.

**Q: How do I add a `SessionStart` hook of my own?**
- **Answer.** Add your script under `.claude/hooks/` and register it in `.claude/settings.json` under `hooks.SessionStart` as its own matcher group (each hook is registered separately so matchers don't clobber). Model it on the shipped `ensure-wiki.py` (startup|resume) and `session-start.sh` (all sources). Use `.claude/settings.local.json` for a per-user, uncommitted hook.
- **Must include:** add to .claude/hooks/ + register in settings.json as its own SessionStart group; model on shipped hooks; settings.local.json for per-user.
- **Source:** Extending-the-Template, Installation-and-Setup.

**Q: Can I run the wiki without git?**
- **Answer.** Not really, and not recommended. Git is foundational: the wiki is a git sub-repo, the SessionStart hook clones with git, the write protocol is pure git mechanics, log attribution reconciles against `git blame`, and version history is a core value. You could keep the Markdown without a remote, but you'd lose auto-clone, the multi-writer protocol, attribution provenance, and history.
- **Must include:** no / not recommended; git is foundational (sub-repo, hook, write protocol, attribution, history); losing it loses most of the value.
- **Source:** Extending-the-Template.

---

## Page 12: When-to-Use-When-Not

**Q: When is this the right tool?**
- **Answer.** When you accumulate knowledge over time and future sessions or people benefit from it: research deep-dives, research-group institutional memory, reading a book/corpus, business/team knowledge, and topical teaching bundles. The common thread: many sources or sessions, a synthesis worth keeping, and a payoff to not re-deriving it.
- **Must include:** knowledge compounds over time; research/institutional-memory/book/team/teaching examples; many sources-or-sessions with a synthesis worth keeping.
- **Source:** When-to-Use-When-Not.

**Q: When is this the wrong tool?**
- **Answer.** One-shot QA where the answer is in one or two chunks (RAG is cheaper); throwaway analysis; fast-moving state better tracked elsewhere (tickets, spreadsheets); and content that must stay out of a shared versioned artifact.
- **Must include:** single-hop QA (use RAG); throwaway; operational/live state; secret/private content.
- **Source:** When-to-Use-When-Not, Best-Practices.

**Q: Is this overkill for a small personal project?**
- **Answer.** It can be; everything is optional and modular (a small project may need only the index and a few pages, no KG, no slash commands). The real question is whether anything will compound: skip it for an afternoon's work, use it for something running weeks.
- **Must include:** can be; optional/modular; decide by whether knowledge will compound.
- **Source:** When-to-Use-When-Not.

**Q: Do I need a lot of source material for the template to pay off?**
- **Answer.** No hard threshold, but value scales with sources and sessions; the index approach works well at moderate scale (~100 sources, hundreds of pages) with no embedding infrastructure. Below a handful of sources the compounding effect is weak.
- **Must include:** no hard threshold; scales with material; moderate scale (~100 sources) works; weak below a handful.
- **Source:** When-to-Use-When-Not.

**Q: Does this help for a single-book or single-paper project?**
- **Answer.** A single book: yes, a canonical use case (chapters, character/theme pages). A single paper: usually not on its own, that's a source-summary, not a wiki; it pays off once you relate the paper to others or track evolving understanding.
- **Must include:** single book yes; single paper usually no (just a source-summary) until related to others.
- **Source:** When-to-Use-When-Not.

**Q: Is this useful outside research (business, personal knowledge, hobby)?**
- **Answer.** Yes; the pattern is domain-agnostic: personal knowledge, competitive analysis, due diligence, trip planning, course notes, hobby deep-dives. The research framing is the headline use case, not a restriction.
- **Must include:** yes, domain-agnostic; personal/business/hobby examples; research is headline not a limit.
- **Source:** When-to-Use-When-Not.

**Q: What is the minimum team size that makes shared use worthwhile?**
- **Answer.** A team of one already benefits (durable memory across your own sessions/machines). Shared value starts at two or more contributors, where the coordination features (write protocol, union-merged index/log) become load-bearing; production wikis routinely have 3-4 writers.
- **Must include:** one benefits (own sessions/machines); 2+ makes coordination load-bearing; 3-4 typical in production.
- **Source:** When-to-Use-When-Not, Team-Workflow.

**Q: Does the template help students, or is it primarily for faculty and researchers?**
- **Answer.** Both, in different roles: faculty/researchers are primary authors (curate sources, direct the wiki); students are primary consumers and extenders (read a bundle through their own LLM with citations back to it, file their own notes into a personal derivative). The student loop is described as operational today.
- **Must include:** both; faculty author, students consume/extend; student loop operational.
- **Source:** When-to-Use-When-Not, Knowledge-Bundles-Overview.

---

## Page 13: Concepts-Glossary

**Q: What is a Markov chain in the context of retrieval?**
- **Answer.** A model of a walk over a graph where the next node depends only on the current node and edge weights; retrieval is framed as such a walk that returns a ranked neighborhood rather than an exact match, degrading gracefully as structure thins.
- **Must include:** walk where next depends on current + edge weights; returns ranked neighborhood; degrades gracefully.
- **Source:** Concepts-Glossary. **Caveat:** vision-wiki framing.

**Q: What is random walk with restart (RWR)?**
- **Answer.** A Markov walk that at each step either follows an edge or restarts to the seed with some probability, biasing the stationary distribution toward the seed's neighborhood so nodes rank by proximity. The retrieval primitive used at both wiki and corpus scale; restart probability and edge weights are tuning parameters. (Tong, Faloutsos, Pan, 2006.)
- **Must include:** walk with restart-to-seed probability; ranks by proximity to seed; the retrieval primitive.
- **Source:** Concepts-Glossary. **Caveat:** vision-wiki framing.

**Q: What is personalized PageRank?**
- **Answer.** PageRank computes a node's global importance from link structure; the personalized variant seeds the walk from specific nodes so ranking is relative to a query. Mathematically equivalent to RWR. (Page, Brin, Motwani, Winograd, 1999.)
- **Must include:** PageRank = global importance from links; personalized = query-seeded; equivalent to RWR.
- **Source:** Concepts-Glossary.

**Q: What is entity resolution, and why does the template avoid heavy versions of it?**
- **Answer.** Collapsing different surface forms of the same entity to a canonical node. The template avoids heavy versions because it's unreliable on real corpora: under-merging scatters an entity across forms; over-merging collapses distinct entities. Lightweight extraction keeps surface forms distinct and lets the walk propagate mass across them, so there's no resolution step to fail.
- **Must include:** collapse surface forms to canonical node; unreliable (under-/over-merging); template keeps forms distinct, walk propagates mass.
- **Source:** Concepts-Glossary, Template-Philosophy.

**Q: What is a structural graph versus a content graph?**
- **Answer.** A structural graph derives from layout/containment (chunks in documents, up: chains, wikilinks): unambiguous, cheap. A content graph derives from what the material means in a normalized ontology (resolved entities, formal typed cross-document assertions): more expressive but expensive and fragile. The template favors structural + lightweight content over heavy content-graph engineering.
- **Must include:** structural = layout/containment, cheap/unambiguous; content = normalized meaning, expensive/fragile; template favors structural + lightweight.
- **Source:** Concepts-Glossary, Knowledge-Graph.

**Q: What is the difference between vanilla RAG and graph-informed retrieval?**
- **Answer.** Vanilla RAG embeds chunks and retrieves by dense similarity (great single-hop, rank-collapses on deep multi-hop). Graph-informed retrieval walks an explicit node-edge structure to assemble the multi-hop context envelope. The template treats them as complementary: dense by default where it fits, graph-informed for evidence assembly.
- **Must include:** RAG = dense similarity, single-hop strong / multi-hop weak; graph-informed = walk structure for multi-hop; complementary.
- **Source:** Concepts-Glossary, When-to-Use-When-Not.

**Q: What is the extended-mind tradition and why does the template draw on it?**
- **Answer.** The lineage (Bush's Memex 1945, Licklider 1960, Engelbart 1962, Clark & Chalmers 1998) holding that cognition legitimately extends into external artifacts an agent reliably uses. The template draws on it because a knowledge bundle plus a local LLM is exactly such an artifact: rapid competence acquisition via the receiver's workflow, not their neurology.
- **Must include:** cognition extends into reliably-used external artifacts; Bush/Clark & Chalmers lineage; bundle+LLM is such an artifact.
- **Source:** Concepts-Glossary, Template-Philosophy.

**Q: What is the DIKW pyramid?**
- **Answer.** Ackoff's (1989) Data → Information → Knowledge → Wisdom hierarchy; the K layer maps loosely onto the wiki's knowledge layer, though DIKW does not map cleanly onto the three-layer framing.
- **Must include:** Data/Information/Knowledge/Wisdom hierarchy (Ackoff); K ~ knowledge layer; imperfect mapping.
- **Source:** Concepts-Glossary.

**Q: What is tacit knowledge?**
- **Answer.** Polanyi's (1966) knowledge that is hard to articulate ("we know more than we can tell"), the ground of expert judgment; corresponds most closely to the experience layer.
- **Must include:** Polanyi; hard-to-articulate knowledge; maps to experience layer.
- **Source:** Concepts-Glossary, Template-Philosophy.

**Q: What is procedural knowledge versus declarative knowledge?**
- **Answer.** Anderson's (1976) distinction: declarative = knowing that (facts); procedural = knowing how (skills, judgment in practice). The wiki's knowledge-vs-expertise axis echoes it.
- **Must include:** declarative = knowing-that/facts; procedural = knowing-how/skills; Anderson; maps to knowledge vs expertise.
- **Source:** Concepts-Glossary.

**Q: What is deliberate practice?**
- **Answer.** Ericsson and Charness's (1994) account of how expertise is acquired: gradual, effortful, feedback-driven practice. Cited to explain why instant skill download stays science fiction even as bundle+LLM approximates rapid competence acquisition another way.
- **Must include:** Ericsson & Charness; gradual/effortful/feedback-driven; why the Matrix mechanism is fiction.
- **Source:** Concepts-Glossary, Template-Philosophy.

**Q: What is RDF Turtle? RDF-star? JSON-LD?**
- **Answer.** RDF Turtle (`.ttl`) is a compact text serialization of an RDF graph as subject-predicate-object triples. RDF-star extends RDF so a triple can be the subject/object of another (statements about statements); the template uses it to weight `mentions` edges. JSON-LD is a JSON serialization of an RDF graph, the extractor's native output.
- **Must include:** Turtle = text triple serialization; RDF-star = statements about statements (weights mentions); JSON-LD = JSON serialization (extractor output).
- **Source:** Concepts-Glossary, Knowledge-Graph.

**Q: What is SHACL?**
- **Answer.** The Shapes Constraint Language for RDF: shapes describe what a conformant graph should look like (node types, required predicates, edge domain/range). `pyshacl` validates the extracted graph against fetched `shapes.ttl` and writes a report; the build reports violations but does not abort.
- **Must include:** constraint language / shapes for RDF; validates the graph (pyshacl); reports violations, non-aborting.
- **Source:** Concepts-Glossary, Knowledge-Graph.

---

## Grading summary (harness cheat-sheet)

- **Score** each answer as `key_facts_present / key_facts_total`.
- **Automatic fail** if the response violates a **Caveat**, i.e. it:
  - presents OKF import/export as shipped (it is planned/analysis stage);
  - presents the multi-agent write protocol as wired into the default path (it is a reference impl only);
  - claims the KG pipeline uses `arq` on the default path (it uses rdflib + pyshacl in-process);
  - claims Cursor or OpenCode is behaviorally validated (Cursor is structural-only);
  - lists `area:` as a standard authored frontmatter field (it is not; tags is);
  - invents a wiki license default, an archival command, or a bundle catalog the docs do not state;
  - pins a specific Python minor version (docs say "Python 3").
- These caveat checks are the point of the harness: they test whether the bundle preserves the honest-reporting discipline under `ask`.
