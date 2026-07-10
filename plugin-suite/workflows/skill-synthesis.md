---
id: skill-synthesis
name: Skill Synthesis
description: Generate reusable skills from recurring prompt workflow and tool patterns.
---

# Skill Synthesis

## Trigger

Use this workflow when the corpus reveals repeated patterns that should become explicit skills.

Examples:

- a design artifact workflow appearing with starter components and export gates;
- a code review workflow with severity-first findings and file references;
- a research workflow with source fan-out and citation verification;
- a tool-loading workflow with deferred schema discovery;
- a memory workflow with persistent file rules.

## Inputs

- `sourcePaths`: prompt files to mine.
- `theme`: target skill theme, such as `design`, `code-review`, `research`, `memory`, `github`, `tool-routing`, or `safety`.
- `targetRuntime`: optional output runtime, such as `claude-code`, `chatgpt`, `mcp`, `custom-agent`, or `provider-neutral`.

## Steps

1. Read selected source files.
2. Extract recurring blocks:
   - trigger conditions;
   - workflow steps;
   - tools;
   - routing rules;
   - verification gates;
   - output expectations;
   - safety boundaries.
3. Convert blocks into a skill recipe.
4. Remove provider-specific implementation details unless `targetRuntime` requires them.
5. Preserve provenance with source selectors.
6. Add failure modes and verification gates.
7. Validate the skill against the manifest schema where possible.
8. Emit the skill under `dist/skills/` or a target plugin package.

## Skill Document Shape

```markdown
---
id: <skill-id>
name: <Human Name>
description: <one-line purpose>
triggers:
  - <trigger>
---

# <Skill Name>

## Purpose
## Inputs
## Workflow
## Tool Dependencies
## Output Contract
## Safety Boundaries
## Failure Modes
## Verification Gates
```

## Synthesis Rules

- A skill must be narrower than an agent identity and broader than a single prompt trick.
- A skill must have clear trigger conditions.
- A skill must include enough workflow to be executable.
- A skill must not depend on hidden provider behavior.
- A skill must cite or point to the source patterns it came from.
- A skill must preserve safety constraints from its source.

## Verification

A synthesized skill is acceptable only when:

- it can be invoked by an intent router;
- it names required tools or states that no tools are required;
- it has explicit stopping conditions;
- it has a validation or evidence rule;
- it does not duplicate long source prompt text.
