---
id: ingest-normalize-diff
name: Ingest, Normalize, Diff
description: Convert prompt corpus files into structured manifests and semantic diffs.
---

# Ingest, Normalize, Diff

## Trigger

Use this workflow when adding new prompt files, refreshing the corpus index, or comparing prompt versions.

## Inputs

- `paths`: source paths or provider folders.
- `mode`: `catalog`, `manifest`, `diff`, or `all`.
- `base`: optional base prompt path for comparison.
- `head`: optional head prompt path for comparison.

## Steps

1. Discover source files.
2. Classify each file by provider, product, model, prompt kind, date, and version.
3. Parse content into an AST:
   - Markdown headings;
   - tables;
   - code fences;
   - JSON tool schemas;
   - XML-like tags;
   - ordered workflows;
   - bullet constraints.
4. Normalize each AST into canonical sections:
   - identity;
   - workflow;
   - tools;
   - skills;
   - memory;
   - environment;
   - safety;
   - formatting;
   - verification.
5. Extract tool contracts where schemas appear.
6. Extract skill recipes where trigger/action instructions appear.
7. Classify speech acts.
8. Write prompt manifests.
9. When `base` and `head` are provided, produce a semantic diff:
   - added, removed, and changed sections;
   - new or removed tools;
   - new or removed skills;
   - autonomy changes;
   - safety changes;
   - memory/context changes;
   - verification changes.
10. Validate all manifests against `plugin-suite/manifest.schema.json`.

## Outputs

- `dist/catalog.json`
- `dist/prompt-manifests/<provider>/<name>.json`
- `dist/tool-contracts/<provider>/<tool>.json`
- `dist/diffs/<base>--<head>.md`

## Failure Modes

- Ambiguous model/version metadata: mark as `unknown` rather than guessing.
- Invalid JSON schema: preserve raw span and emit a parser warning.
- Oversized prompt passage: store selectors and hashes rather than long duplicated text.
- Missing dates: infer only from explicit source text or git metadata, and record provenance.

## Verification

The workflow passes only when:

- every manifest validates;
- every source path exists;
- every diff references two concrete sources;
- every generated claim includes a source selector;
- no generated artifact contains unnecessary long copied prompt passages.
