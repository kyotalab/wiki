---
title: "AI-Driven Development Prompt Pack"
tags: [llm, workflow, prompting]
source: "99_Archive/AI-driven-development-methodology-docs/01_spec_design.md, 99_Archive/AI-driven-development-methodology-docs/02_cursor_rules.md, 99_Archive/AI-driven-development-methodology-docs/03_ai_driven_dev.md"
created: 2026-05-06
related: [ai-driven-implementation-cycle, cursor-rules-context-management, specification-first-ai-development]
---

# AI-Driven Development Prompt Pack

Provides copy-paste prompt templates for specification-first, one-feature-at-a-time implementation in Cursor.

## Code

```markdown
## 1) Feature implementation prompt (default)
@00_project.md @0N_current_phase.md

Implement exactly one feature: <feature-name>.

## Requirements
- <requirement-1>
- <requirement-2>
- <requirement-3>

## Dependencies
- <file-or-symbol-1>
- <file-or-symbol-2>

## Constraints
- Do not change files outside: <scope>
- Keep existing architecture and naming conventions
- Add error handling for: <error-cases>

## Out of scope
- <what-not-to-do-1>
- <what-not-to-do-2>

## Acceptance checks
- Build passes
- Behavior matches requirements above
- Explain key changes briefly after implementation


## 2) Build error fix prompt
@00_project.md @0N_current_phase.md

Fix this build error without broad refactoring.

## Error output
<paste full error message exactly as-is>

## Relevant files
- <file-1>
- <file-2>

## Constraints
- Keep the fix minimal and localized
- Preserve current behavior except for the error fix
- If multiple fixes are possible, choose the lowest-risk option


## 3) Code understanding prompt (before next feature)
Review the code you just changed and explain:
1. What changed and why
2. How it satisfies each requirement
3. Risks or edge cases still remaining
4. What should be tested next


## 4) Spec decision prompt (before implementation)
I need to decide: <design-question>.

Give 3 options with:
- trade-offs
- implementation complexity
- long-term maintenance impact

Then recommend one option for this context:
<project constraints and goals>
```

## Usage Notes

- Replace placeholders (`<...>`) before sending any template.
- Use template 1 for normal progress, then template 3 before moving to the next feature.
- Use template 2 by pasting raw build errors verbatim; do not paraphrase.
- Use template 4 when requirements are still ambiguous, then update your spec/rules first.
- For deeper context, see [[ai-driven-implementation-cycle]], [[cursor-rules-context-management]], and [[specification-first-ai-development]].

## Related

- [[ai-driven-implementation-cycle]] — Defines the one-feature execution loop these prompts operationalize.
- [[cursor-rules-context-management]] — Explains why explicit `@rules` references improve response quality.
- [[specification-first-ai-development]] — Shows how decision prompts should precede implementation prompts.
