---
id: agentic-lexicon-compiler
name: Agentic Lexicon Compiler
description: Compile recurring prompt patterns into compact agentic operators, tags, and reusable syntax.
triggers:
  - convert prompts into operators
  - build an agentic lexicon
  - compress a prompt into shorthand
  - compile XML-like tags into workflow semantics
  - design a prompt programming language
---

# Agentic Lexicon Compiler

## Purpose

Use this skill to convert verbose prompt patterns into a compact operational lexicon. The compiler is inspired by stenographic compression: short operators carry the semantic weight of larger prompt structures.

The output is not merely shorter wording. It is a typed vocabulary for agent behavior.

## Core Idea

A prompt span can be represented as:

```text
operator + target + constraint + evidence gate
```

Examples:

```text
@role(senior.fullstack)
@read(repo).before(plan)
@tool(github).when(url.github)
@gate(verify).requires(test || screenshot || diff)
@memory(project).write(nonobvious && durable)
```

Each operator expands into a deterministic instruction block during compilation.

## Operator Classes

- `@role(...)`: declares identity, expertise, posture, or scope.
- `@intent(...)`: binds the user objective.
- `@read(...)`: requires source inspection before synthesis.
- `@plan(...)`: requests decomposition, sequencing, or architecture.
- `@act(...)`: authorizes implementation or mutation.
- `@tool(...)`: delegates capability to a tool surface.
- `@skill(...)`: selects a skill recipe.
- `@workflow(...)`: selects or composes a multi-step procedure.
- `@gate(...)`: requires validation evidence.
- `@cite(...)`: requires source-grounded claims.
- `@memory(...)`: governs persistence and recall.
- `@guard(...)`: applies safety, privacy, or context-boundary rules.
- `@format(...)`: binds output shape.

## Compilation Pipeline

1. Parse raw prompt or XML-like markup.
2. Identify speech acts and role claims.
3. Collapse repeated phrase patterns into operators.
4. Attach constraints and evidence gates.
5. Generate expanded instructions only for the active task state.
6. Emit both compact source and expanded runtime form.

## Example Input

```xml
<intent>
Act as a senior engineer. Read the repo first. Build the smallest scalable implementation. Verify before final.
</intent>
```

## Example Compiled Form

```text
@role(engineer.senior)
@read(repo).before(@plan)
@act(minimal && scalable)
@gate(verify).before(final)
```

## Example Expansion

```text
You are operating as a senior engineer for this task. Inspect the actual repository before proposing or changing architecture. Prefer the smallest implementation that preserves credible scalability. Before final response, verify the result with the strongest available evidence for the task.
```

## Output Contract

Return:

- a compact operator version;
- an expansion table;
- a runtime-expanded instruction block;
- any unresolved ambiguity;
- verification rules.

## Verification Gates

- Every operator must have a defined expansion.
- Every expansion must preserve the original intent.
- No operator may silently remove a safety constraint.
- Runtime compilation must be context-minimal: only active operators expand.
