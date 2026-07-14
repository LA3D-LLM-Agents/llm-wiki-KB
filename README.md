# llm-wiki-KB

A knowledge bundle (an LLM-authored, interlinked wiki) that teaches you about the [llm-wiki-memory-template](https://github.com/crcresearch/llm-wiki-memory-template): what it is, how to install and operate it, its wiki conventions, the knowledge-graph pipeline, how to extend it, and how teams collaborate on it. It doubles as the **exemplar bundle** for the [LA3D-LLM-Agents](https://la3d-llm-agents.github.io/) federation: a worked model others can copy when creating their own bundles.

- **Read the bundle:** [wiki Home](https://github.com/LA3D-LLM-Agents/llm-wiki-KB/wiki/Home_llm-wiki-KB) (start at [What-is-the-llm-wiki-Template](https://github.com/LA3D-LLM-Agents/llm-wiki-KB/wiki/What-is-the-llm-wiki-Template))
- **Front door and supplementary site:** https://la3d-llm-agents.github.io/llm-wiki-KB/
- **Build your own:** [Creating a Knowledge Bundle](https://github.com/LA3D-LLM-Agents/llm-wiki-KB/wiki/Creating-a-Knowledge-Bundle) (how-to)

## Consume it via an LLM

With the `agent-comms` feature enabled in your own template project, ask this bundle directly. Two equivalent forms:

```bash
# slash command (Claude Code): the question needs no quotes
/ask llm-wiki-KB What is the llm-wiki template and how do I install it?

# underlying script: the question is a single quoted argument
bash scripts/agent-comms/ask.sh llm-wiki-KB "What is the llm-wiki template and how do I install it?"
```

Omit the bundle name to use discovery mode, which reads the federation's agent Cards to find a match. You can also just clone the wiki and point any LLM session at the directory.

## This repository uses LLM wiki memory

llm-wiki-KB keeps a persistent, LLM-maintained knowledge base under `wiki/llm-wiki-KB.wiki/` (a separate git repo), following the [llm-wiki pattern](https://github.com/tobi/llm-wiki). It is the project's durable memory: findings, decisions, and syntheses belong in the wiki and accumulate over time. Three operations, **Query** (read it), **Ingest** (write to it), and **Lint** (health-check it), are codified in `CLAUDE.md`, in `wiki/llm-wiki-KB.wiki/SCHEMA_llm-wiki-KB.md`, and in the `.claude/commands/` slash commands (`/wiki-source`, `/wiki-experiment`, `/wiki-lint`). See [llm-wiki.md](llm-wiki.md) for the underlying pattern.

## Quick start for collaborators

```bash
git clone https://github.com/LA3D-LLM-Agents/llm-wiki-KB.git
cd llm-wiki-KB
[ -d wiki/llm-wiki-KB.wiki ] || \
    git clone https://github.com/LA3D-LLM-Agents/llm-wiki-KB.wiki.git wiki/llm-wiki-KB.wiki
./wiki/agents/claude-code/setup.sh --seed-memory
```

The wiki at `wiki/llm-wiki-KB.wiki/` is a separate git repo with its own history and remote. After any wiki edit, commit in the wiki repo (not the project repo), and push only to publish:

```bash
git -C wiki/llm-wiki-KB.wiki add <files>
git -C wiki/llm-wiki-KB.wiki commit -m "..."
git -C wiki/llm-wiki-KB.wiki push origin master
```

## About the template

This project was instantiated from [crcresearch/llm-wiki-memory-template](https://github.com/crcresearch/llm-wiki-memory-template). Maintainers who need to pull template updates, add an agent overlay, or understand the instantiate/update scripts should read the template repo's documentation.

## License

Created by Chris Sweet ([@chrissweet](https://github.com/chrissweet)), authored with Claude Code, under [LA3D-LLM-Agents](https://github.com/LA3D-LLM-Agents).

The **bundle content** authored here (the wiki under `wiki/llm-wiki-KB.wiki/`, the `docs/` material, and the GitHub Pages site) is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). Reuse and adapt it freely with attribution to: **llm-wiki-KB, created by Chris Sweet (@chrissweet), authored with Claude Code**.

The **template scaffolding** in this repo (`scripts/`, `.claude/`, `wiki/agents/`, `wiki/init-wiki.sh`, `features/`) derives from [crcresearch/llm-wiki-memory-template](https://github.com/crcresearch/llm-wiki-memory-template) and is subject to that project's license; the knowledge-graph extractor under `scripts/kg/` is MIT-derived from [LA3D/llm-wiki-colab](https://github.com/LA3D/llm-wiki-colab) (see its file headers).
