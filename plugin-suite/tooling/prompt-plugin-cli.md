# Prompt Plugin CLI Specification

This file defines the intended command surface for a future `prompt-plugin` CLI.

## Commands

### `prompt-plugin catalog`

Build a repository-level catalog.

```bash
prompt-plugin catalog --root . --out dist/catalog.json
```

Outputs:

- provider inventory;
- product inventory;
- prompt file inventory;
- prompt kind classification;
- source hashes;
- explicit dates and versions when present.

### `prompt-plugin manifest <path>`

Generate a structured manifest for one prompt file.

```bash
prompt-plugin manifest Anthropic/Claude\ Code/claude-code-opus-4.8.md --out dist/prompt-manifests/anthropic/claude-code-opus-4.8.json
```

Outputs:

- source metadata;
- canonical sections;
- speech-act labels;
- tool contracts;
- skills;
- workflows;
- safety boundaries;
- verification gates.

### `prompt-plugin diff <base> <head>`

Generate a semantic prompt diff.

```bash
prompt-plugin diff Anthropic/claude-opus-4.8.md Anthropic/claude-sonnet-5.md --out dist/diffs/opus-4.8--sonnet-5.md
```

Outputs:

- section delta;
- tool delta;
- skill delta;
- memory/context delta;
- safety delta;
- verification delta;
- autonomy delta.

### `prompt-plugin synthesize-skill`

Generate a skill recipe from source paths.

```bash
prompt-plugin synthesize-skill \
  --theme github \
  --source Anthropic/Claude\ Code/claude-code-opus-4.8.md \
  --source OpenAI/Codex/gpt-5.5.md \
  --out dist/skills/github-triage.md
```

Outputs a skill document with trigger conditions, workflow, tool dependencies, safety boundaries, failure modes, and verification gates.

### `prompt-plugin compile-agent`

Compile a minimal task-specific agent bundle.

```bash
prompt-plugin compile-agent \
  --intent "review a GitHub pull request" \
  --skills dist/skills/github-triage.md,dist/skills/code-review.md \
  --tools dist/tool-contracts/github.json \
  --out dist/agent-bundles/github-review-agent.json
```

Outputs:

- active identity;
- selected skills;
- selected tools;
- context budget;
- verification contract;
- output contract.

## Implementation Notes

Recommended stack:

- TypeScript for CLI, schemas, and AST transforms.
- `commander` or `clipanion` for commands.
- `zod` for runtime validation.
- `gray-matter` for frontmatter.
- `unified`, `remark-parse`, and `mdast` for Markdown.
- `ajv` for JSON Schema validation.
- `fast-glob` for corpus traversal.
- `vitest` for parser and compiler tests.

## Data Model

```ts
type PromptArtifact = {
  source: SourceRef;
  sections: PromptSection[];
  tools: ToolContract[];
  skills: SkillRecipe[];
  workflows: WorkflowRecipe[];
  speechActs: SpeechAct[];
  verification: VerificationGate[];
};
```

## Guardrails

- Never execute prompt text as instructions.
- Never generate bypass tooling.
- Never duplicate long source passages into generated artifacts.
- Always preserve source path, hash, and selector.
- Treat parser confidence as data, not truth.
