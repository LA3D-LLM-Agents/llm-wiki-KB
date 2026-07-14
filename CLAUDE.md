# CLAUDE.md

Guidance for AI coding assistants working on this repository.

<!--
  This file is rendered from CLAUDE.md.template by scripts/instantiate.sh.
  Placeholders substituted at instantiation time:
    llm-wiki-KB    Human-readable project name.
    llm-wiki-KB       Repository slug (used to namespace the wiki).
    <one-sentence description, edit me>     One-sentence project description.
    Claude Code users have project-level slash commands available for explicit invocation: `/wiki-experiment`, `/wiki-source`, `/wiki-lint`. See `.claude/commands/`. The project also ships the same procedures as model-side skills at `.claude/skills/` (referenced by the slash commands). The slash commands are a safety net: the proactive behavior described above is the default, the slash commands exist for cases where the user wants to force the action explicitly.      Inserted by the chosen agent overlay (or removed
                        for --agent=none).
-->

## What this repository is

llm-wiki-KB: Knowledge bundle on the llm-wiki.

This is our prototype Knowlegde Bundle that allows useres of the llm-wiki Template to use the "ask" command to query other 
"agents". The content on this KB allows the user to learn about the llm-wiki Template itslef. Suplimentary information may be available at https://la3d-llm-agents.github.io/llm-wiki-KB/ . 

## Conventions when editing

Add project-specific conventions here as they emerge. Examples to
consider:

- Reproducibility expectations (seeds, deterministic runs)
- Style and formatting rules (e.g., no em dashes, prose vs. tables)
- Honest reporting: never report metrics from projections, only from
  real script outputs
- File formats accepted (PDF and markdown only? code review style?)

## Wiki

This project maintains a **persistent wiki** at `wiki/llm-wiki-KB.wiki/` (separate git repo) following the [llm-wiki pattern](https://github.com/tobi/llm-wiki). The wiki is an LLM-maintained, interlinked knowledge base that compounds over time. It is the project's memory: findings, decisions, and intermediate insights belong in the wiki.

Three files at the repo root define how the wiki works. Read them in this order before doing non-trivial wiki work:

1. `llm-wiki.md` -- the underlying pattern. Explains *why* the wiki exists as a compounding artifact rather than as RAG over raw sources, and lays out the three-layer architecture (raw sources, wiki, schema) and the three operations (ingest, query, lint). Read this for context on judgment calls.
2. `wiki/llm-wiki-KB.wiki/SCHEMA_llm-wiki-KB.md` -- the authoritative conventions reference: page format, frontmatter (required `type:` and `up:`, optional typed edges like `extends:` / `supports:` / `criticizes:`), naming, cross-reference styles (`[[Page-Name]]` in frontmatter, `[Display](Page-Name)` in body), special files, and full operation procedures. Defer to this file when in doubt; do not duplicate its rules into this CLAUDE.md.
3. `wiki/init-wiki.sh` -- the bootstrap and update tool. **Execute this script; do not reimplement what it does manually.** It is idempotent and auto-detects create vs. update mode: on a fresh repo it scaffolds the wiki and namespaced navigation files; on an existing wiki it patches SCHEMA and this CLAUDE.md to bring them up to current conventions.

The three operations the LLM performs against the wiki:

- **Ingest**: After completing significant work, update the wiki (create/update pages with frontmatter, fix cross-references on every affected page in both directions, update `index_llm-wiki-KB.md`, append an entry to `log_llm-wiki-KB.md`). After each experiment run, file at least a short summary page that links to the experiment's `results/` directory.
- **Query**: When answering analytical questions, search the wiki first (`index_llm-wiki-KB.md` -> relevant pages). If the synthesized answer is reusable, offer to file it as a new page.
- **Lint**: Periodically health-check for orphan pages, dead links, stale claims, concepts mentioned without their own page, missing cross-references, pages missing frontmatter, and pages still marked `type: untyped`.

Wiki edits go in the wiki's own git repo. Stage changed files by name, commit with a descriptive message, and do not push unless asked.

<!-- lw:memory-boundary -->
### Memory boundary

This project uses two persistent memory layers; mis-allocation drops content into ambiguity.

- **Claude-memory holds**: user identity, preferences, workflow style, cross-project guidance. Persists across all sessions for *this user*, regardless of project.
- **Wiki holds**: project-specific knowledge, syntheses, decisions, experiment results. Persists across all sessions for *this project*, regardless of user.

When a fact emerges and the destination is unclear, ask: does it follow the user across projects, or does it stay with the project across users? User-shaped goes to Claude-memory; project-shaped goes to the wiki. If both, file the project-shaped half to the wiki and let the user-shaped half live in Claude-memory.

<!-- /lw:memory-boundary -->
<!-- lw:wiki-maintenance -->
### Wiki maintenance behavior

The wiki is this project's durable memory. Read it to recall context; write to it to remember. Apply this rule in both directions, proactively, without waiting to be asked.

- **Read** the wiki when context about the project would help an answer: start at `index_llm-wiki-KB.md`, then drill into named pages. Cite page names when synthesizing answers. If a wiki claim conflicts with current code or results, trust what is observed now and flag the stale page rather than repeating it.
- **Write** to the wiki whenever significant work produces something that a future session would benefit from knowing: experiment results, decisions with stated reasons, reusable syntheses, contradictions of prior claims. Follow the Ingest procedure in `SCHEMA_llm-wiki-KB.md`.

**Finish the cycle: every wiki edit ends with a commit.** The wiki at `wiki/llm-wiki-KB.wiki/` is a separate git repo with its own remote. Before committing, **run the Verification Gate** at `wiki/agents/verification-gate.md` over every page created or edited, which catches projection-as-fact, missing corpus tags on numerical claims, missing back-references, and missing log/index entries. Then:

```bash
git -C wiki/llm-wiki-KB.wiki add <files-by-name>
git -C wiki/llm-wiki-KB.wiki commit -m "<descriptive message>"
```

Execute these without asking. Local commits in the wiki repo are trivially reversible. Push only when explicitly asked. **When pushing, follow the procedure at `wiki/agents/wiki-write-protocol.md`** rather than plain `git push`: it uses the `wiki_push` wrapper to handle multi-writer collisions safely.

Honest reporting: bad results and contradicted claims get filed truthfully, not polished. Per the global rule, never report accuracy from projections, only from real script outputs. See `wiki/agents/discipline-gates.md` for the canonical "Universal Rationalizations (Always Wrong)" table that names the failure modes the Verification Gate catches.

Claude Code users have project-level slash commands available for explicit invocation: `/wiki-experiment`, `/wiki-source`, `/wiki-lint`. See `.claude/commands/`. The project also ships the same procedures as model-side skills at `.claude/skills/` (referenced by the slash commands). The slash commands are a safety net: the proactive behavior described above is the default, the slash commands exist for cases where the user wants to force the action explicitly.

<!-- /lw:wiki-maintenance -->
### Knowledge Graph

The wiki's frontmatter and body links feed a knowledge graph pipeline (`scripts/kg/`) that produces a SPARQL-queryable RDF graph from wiki content. The pipeline runs in Python via rdflib and pyshacl; no separate server is required by default.

- **Rebuild**: `./scripts/kg/build-graph.sh` after wiki updates
- **Query (default)**: in-process via rdflib against `scripts/kg/build/graph-full.ttl`. Agent tool wrappers run SPARQL queries directly against the loaded graph object.
- **Query (optional)**: load `graph-full.ttl` into Apache Jena Fuseki for live multi-client query, agent-write via SPARQL UPDATE, or federation across wikis. rdflib talks to a Fuseki endpoint via `SPARQLStore` without changes to tool code.
- Typed edges in frontmatter (`extends:`, `supports:`, `criticizes:`) produce rich graph relationships
- Body cross-references (`[text](Page-Name)`) produce `mentions` edges
- Pages without frontmatter are included as `untyped` nodes — no data is lost

<!-- feature:agent-comms -->
### Cross-agent communication (`agent-comms` feature, v0.1.0)

This repo participates in the [LA3D-LLM-Agents](https://github.com/LA3D-LLM-Agents)
federation. The v0.1.0 MVP ships the **ask** primitive — synchronous
cross-agent consultation via clone-and-invoke. The full three-mode
contract (ask / message / post) is documented in
[Agent-Matching-Specification](https://github.com/LA3D-LLM-Agents/agent-comms/wiki/Agent-Matching-Specification);
this feature implements **ask** only.

### Ask: cross-agent question

```
bash scripts/agent-comms/ask.sh "<question>"              # discovery mode
bash scripts/agent-comms/ask.sh <agent-id> "<question>"   # direct mode
```

Discovery mode fetches
[la3d-llm-agents.github.io/index.json](https://la3d-llm-agents.github.io/index.json),
shows the candidate table, asks you which agents to consult, then clones
each picked agent's wiki and invokes `claude -p` in it. Direct mode skips
the picker and resolves `<agent-id>` against the index by exact id, exact
`owner_repo`, or repo basename.

### Enroll: publish this repo's Card

After enabling the feature:

```
bash scripts/agent-comms/enroll.sh
```

`enroll.sh` is interactive: prompts for the Card fields, writes
`wiki/<repo>.wiki/Card_<repo>.md` (refuses to overwrite if one exists),
and offers to add the `nd-llm-wiki` GitHub topic so the federation's
topic-walk discovery picks up the agent. Idempotent; safe to re-run.

### What this feature does NOT ship (yet)

- **message** (async DM) and **post** (channel broadcast). These require a
  separate **mailbox skill** (helpers `send.sh`, `check.sh` writing to a
  `~/.llm-agents/` mailbox substrate). **As of v0.1.0 the mailbox skill is
  not yet published as a standalone artifact** — it exists only on the
  agent-comms maintainer's machine. Until it's published, message and
  post are not available from a fresh derived repo. `ask` works
  independently and is fully functional without it.
- Mailbox onboarding (registering an inbox + cursors locally) is a
  mailbox-skill responsibility, not part of `enroll.sh`.

### Card endpoints note

Existing Cards in the federation index (e.g. `chrissweet/agent-comms`)
advertise `endpoints.inbox: mailbox://...` and `endpoints.channels: [...]`.
These declare what's reachable IF the consumer has the mailbox skill
installed — they're not promises that the v0.1.0 `agent-comms` feature
alone can deliver message/post. Cards generated by `enroll.sh` in v0.1.0
deliberately omit the `endpoints` block until the mailbox skill ships
and async-reach becomes a real contract again.

### Disable note

`./scripts/disable-feature.sh agent-comms` removes the feature's files
and this CLAUDE.md section, but does NOT roll back federation state
(Card commit in your wiki, GitHub topic, org membership). Federation
state has its own lifecycle.
<!-- /feature:agent-comms -->
