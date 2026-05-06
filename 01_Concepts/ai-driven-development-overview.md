---
title: "AI-Driven Development Overview"
tags: [llm, workflow, methodology]
source: "99_Archive/AI-driven-development-methodology-docs/00_overview.md"
created: 2026-05-05
related: [ai-driven-development, specification-first-ai-development, cursor-rules-context-management, ai-driven-implementation-cycle, ai-development-session-workflow]
---

# AI-Driven Development Overview

AI-driven development is a method where the developer owns product intent and architecture, while AI accelerates implementation work. The core idea is not to outsource thinking, but to separate responsibilities clearly: humans decide what to build and why, and AI helps produce and revise code under that direction. This framing prevents the common failure mode where generated code grows quickly but becomes hard to understand, maintain, or debug.

In practice, the method works as a phased pipeline. A project starts with explicit specification design, moves into environment preparation, and then proceeds feature-by-feature through implementation. AI support is strongest when requirements are concrete and scoped. By contrast, vague prompts often produce output that seems fast at first but creates downstream rework. The process therefore emphasizes writing decisions in advance and converting them into stable guidance before coding begins.

Tool boundaries are part of the concept. A planning model such as `Claude` is used for specification dialogue, trade-off analysis, and review-level judgment. An implementation model in `Cursor` is used for code generation, local fixes, and iterative edits. A runtime tool such as `Xcode` remains focused on build, execution, and platform validation. Keeping those boundaries explicit reduces context switching costs and avoids conflicting edits in parallel tools.

The significance of this concept is operational clarity. New-language or new-framework projects become manageable because decision quality is front-loaded and implementation risk is distributed into small, reviewable units. The developer still learns the system deeply, because every generated change is treated as readable, explainable code rather than opaque automation.

Related concepts include [[specification-first-ai-development]] for how decisions are made before coding, [[cursor-rules-context-management]] for persistent project context, [[ai-driven-implementation-cycle]] for per-feature execution, and [[ai-development-session-workflow]] for daily operating rhythm.
