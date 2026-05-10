---
title: "Claude Project Instructions for Cursor Handoff"
tags: [llm, workflow, ios]
source: "99_Archive/20260510-claude_project_instructions.md"
created: 2026-05-10
related: [ai-driven-development-overview, specification-first-ai-development, cursor-rules-context-management, ai-driven-implementation-cycle, personal-ios-development-claude-cursor-playbook]
---

# Claude Project Instructions for Cursor Handoff

Claude project instructions for Cursor handoff means a fixed system-level brief you keep in a project-scoped assistant so planning, teaching, and review stay in that chat while file-level implementation and repair are deliberately pushed into Cursor through copy-ready prompts.

The mechanism is a role contract plus routing rules. The assistant behaves as a senior mentor: it explains why before what, surfaces options in a structured layout, names a single recommended path with rationale, and advances work in one small step at a time instead of dumping large multi-file changes. Technical answers carry explicit decision rationale, and code snippets are expected to be complete enough to run when they appear. Parallel to that, the instructions name which tool owns which risk. The assistant owns specification dialogue, trade-off analysis, documentation, code review, and the generation of Cursor prompts (including error-fix prompts that carry raw logs and localized snippets). Cursor owns implementation, refactors, and iterative fixes against active rule files. Xcode owns compile-run-debug cycles and store submission mechanics. When a new implementation slice is ready, the assistant emits a prompt shaped like a miniature spec: reference the active rules file with `@`, state a one-line objective, list concrete requirements, call out anti-patterns, and restate shared conventions such as localized comments for explanation and English for user-visible strings. Phase and step boundaries are treated as hard scope so the assistant does not propose work outside the current milestone. For continuity across chat resets, a handoff block summarizes product identity, toolchain versions, phase progress, architecture layout, known pitfalls, open issues, and the next concrete Cursor action.

This pattern matters because mixed-responsibility chats often blur diagnosis and editing. Separating “think and specify” from “mutate the repo” keeps error signals clean (paste compiler output verbatim into the implementation tool), reduces contradictory edits, and preserves learning velocity for developers who are new to a stack but experienced elsewhere. It also pairs naturally with [[cursor-rules-context-management]] and [[specification-first-ai-development]] because the instructions constantly steer decisions back to written specs and synchronized rules before code changes land.

Related concepts include [[ai-driven-development-overview]] for the broader split between human intent and AI acceleration, [[ai-driven-implementation-cycle]] for the implement-review-build loop that follows each Cursor task, and [[personal-ios-development-claude-cursor-playbook]] for how this handoff pattern fits an end-to-end iOS shipping path.
