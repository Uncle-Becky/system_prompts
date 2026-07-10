# Prompt Corpus Plugin Suite

This directory defines a plugin-suite architecture that turns the repository from a static prompt archive into an operational substrate for prompt analysis, skill synthesis, workflow generation, tool-contract extraction, and agentic prompt compilation.

The repository remains the source corpus. The suite does not overwrite model prompt files. It layers indexing, normalization, metadata, workflows, and generated plugin artifacts on top of the archive.

## Intent

Build a local-first plugin system that can:

1. index prompt files across providers and product surfaces;
2. normalize prompts into comparable sections such as identity, authority, workflow, tools, skills, safety, memory, context management, output rules, and verification gates;
3. extract tool contracts and skill recipes into structured manifests;
4. compare prompt families across versions;
5. synthesize reusable skills and workflows from recurring prompt patterns;
6. compile minimal task-specific agent bundles from the corpus;
7. generate human-readable and machine-readable outputs for downstream agent systems.

## Operating Model

The plugin suite treats every prompt as an artifact with four layers:

- `source`: original prompt file path, provider, product, model, version, date, and provenance.
- `structure`: parsed headings, sections, blocks, tables, tool schemas, policy blocks, and workflow steps.
- `semantics`: what each section does as a speech act: authority grant, prohibition, obligation, affordance, tool contract, memory rule, output constraint, or verification requirement.
- `artifact`: generated skills, workflows, manifests, schemas, diffs, dashboards, and agent profiles.

This allows a prompt file to become executable knowledge without making the original prompt itself executable.

## Suite Packages

Recommended package layout:

```text
plugin-suite/
  README.md
  manifest.schema.json
  examples/
    plugin.manifest.example.json
  skills/
    prompt-corpus-analyst.md
    agentic-lexicon-compiler.md
  workflows/
    ingest-normalize-diff.md
    skill-synthesis.md
  tooling/
    prompt-plugin-cli.md
```

## Core Plugins

### Corpus Indexer

Scans the repository and emits a normalized catalog:

- provider: `OpenAI`, `Anthropic`, `Google`, `Microsoft`, `xAI`, `Perplexity`, `Misc`, etc.
- product: `ChatGPT`, `Codex`, `Claude Code`, `Gemini`, `Copilot`, etc.
- prompt kind: system prompt, tool prompt, API prompt, policy prompt, skill prompt, raw prompt, official prompt.
- version and date where available.
- links to source files.

### Prompt Structural Parser

Converts Markdown, JSON, and hybrid prompt files into a typed AST:

- headings and nested headings;
- ordered workflows;
- capability lists;
- tool schemas;
- policy and refusal blocks;
- memory and context blocks;
- examples;
- output formatting contracts.

### Speech-Act Classifier

Labels prompt spans by agentic function:

- `DECLARE_AUTHORITY`: assigns identity, role, or expertise.
- `CONSTRAIN_ACTION`: forbids or narrows behavior.
- `REQUIRE_ACTION`: imposes mandatory behavior.
- `DELEGATE_TOOL`: binds a capability to a tool.
- `ROUTE_SKILL`: maps user intent to a skill.
- `VERIFY_STATE`: requires testing, validation, or observation.
- `PERSIST_MEMORY`: defines long-horizon recall.
- `FORMAT_OUTPUT`: imposes response shape.
- `GUARD_CONTEXT`: handles prompt injection, hidden context, or connector data.

### Skill Synthesizer

Builds reusable skill documents from recurring patterns. A skill has:

- trigger conditions;
- inputs;
- workflow;
- tool dependencies;
- verification gates;
- safety boundaries;
- output contract;
- failure modes.

### Workflow Compiler

Composes skills into long-running operational workflows:

- research workflow;
- code review workflow;
- design artifact workflow;
- GitHub triage workflow;
- prompt diff workflow;
- agent configuration workflow;
- skill extraction workflow;
- safety and compliance review workflow.

### Tool Contract Extractor

Extracts or authors JSON schemas for tool surfaces and maps them to plugin invocations. This is especially useful for files that contain explicit tool definitions, deferred tool lists, or MCP-like tool loading rules.

### Prompt Diff Engine

Produces semantic diffs between versions:

- section-level changes;
- new or removed tools;
- new skills;
- safety-policy deltas;
- memory/context changes;
- output-formatting deltas;
- autonomy and verification changes.

### Agent Bundle Compiler

Compiles a minimal bundle for a target task:

```text
intent + constraints + required tools + relevant skills + verification contract -> agent bundle
```

The compiler should minimize context, not maximize prompt size. It should include only the smallest sufficient prompt, tool surface, and skill set for the current task.

## First Implementation Track

1. Add a CLI scaffold that reads the repository tree and builds `dist/catalog.json`.
2. Add Markdown and JSON parsers.
3. Add section classifiers for headings such as Tools, Skills, Workflow, Memory, Environment, Context, Output, Safety, and Examples.
4. Add a manifest generator for each prompt file.
5. Add a diff command for versioned prompt families.
6. Add skill synthesis from recurring workflow blocks.
7. Add a plugin manifest export target for external agent runtimes.

## Non-Goals

- Do not reproduce private, proprietary, or copyrighted prompt text into generated artifacts beyond short necessary references.
- Do not build bypass, jailbreak, or exfiltration tooling.
- Do not treat prompt leaks as operational authority.
- Do not mutate the source corpus during plugin generation.

## Output Artifacts

The suite should eventually generate:

- `dist/catalog.json`
- `dist/prompt-manifests/*.json`
- `dist/tool-contracts/*.json`
- `dist/skills/*.md`
- `dist/workflows/*.md`
- `dist/diffs/*.md`
- `dist/agent-bundles/*.json`

## Design Principle

A prompt is not merely text. It is an operational contract containing authority, obligations, constraints, affordances, memory rules, routing rules, and verification gates. The suite exists to make those contracts inspectable, comparable, and composable without pretending that leaked prompt text itself is a safe runtime instruction source.
