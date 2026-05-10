---
title: "Personal iOS Development with Claude and Cursor"
tags: [llm, workflow, ios]
source: "99_Archive/20260510-development_style_guide.md"
created: 2026-05-10
related: [ai-driven-development-overview, specification-first-ai-development, cursor-rules-context-management, ai-driven-implementation-cycle, ai-development-session-workflow, claude-project-instructions-cursor-handoff]
---

# Personal iOS Development with Claude and Cursor

This topic describes a reproducible solo workflow for taking a mobile idea to App Store release when you are learning Swift and SwiftUI but already know how to ship software in other ecosystems. It assumes personal-use quality goals, not a large team process, and it leans on two assistants with different jobs: a project-scoped model for thinking and writing, and Cursor for repository edits under rules you control.

The workflow begins by forcing the idea into three sentences: the problem, the audience, and the differentiated value. From there, progress is conversational but not delegated. You ask for options and trade-offs, then you choose and record rationale, following an order that reduces rework. Persistence, sync strategy, and file conventions come before core behaviors, screen structure, fine-grained UX, visual styling, and finally pricing and listing copy. Each batch of decisions is captured immediately in a lightweight specification document that uses short prose plus rationale sections, because downstream implementation quality in [[specification-first-ai-development]] depends on that record staying honest and current.

When the specification stabilizes, you translate it into durable AI context using [[cursor-rules-context-management]]. A common layout is a always-on `00_project.md` file plus phase files that each state goals, concrete deliverables, checklists, and explicit non-goals for that phase. Phases are sized to match app complexity; a typical solo sequence runs from toolchain setup through navigation skeletons, persistence and sync, core product behaviors, polish and accessibility, and finally store submission. Within a phase you still work in small steps so each Cursor session matches one verifiable slice, which is how this playbook aligns with [[ai-driven-implementation-cycle]] and [[ai-development-session-workflow]].

Tool boundaries are strict on purpose. Planning, review, and prompt drafting stay in the project assistant configured by [[claude-project-instructions-cursor-handoff]]. Cursor receives only scoped prompts that reference the active rules, then you read what changed, build in Xcode, run on a simulator or device, and commit. When specifications drift, you update the written spec, the rules, and the code together so prompts never chase stale intent. Git hygiene stays boring on purpose: one commit per coherent unit, imperative English messages, and pushes at natural checkpoints such as a finished screen or end of a work block.

Quality choices reflect solo bandwidth. Automated tests focus on deterministic business logic such as search, parsing, and graph-like relationships, while views and brittle I/O-heavy paths lean on manual verification. Simulator work is enough for much UI flow, but iCloud, security-scoped bookmarks, metadata queries, and similar platform behaviors need device truth. Code review checklists emphasize platform API correctness, memory lifetime in asynchronous Swift code, error handling, suspicious hard-coded locale or timezone assumptions, and drift from the specification.

App Store preparation is treated as engineering work, not marketing afterthought. You assemble required artwork sizes, localized listing text, privacy policy hosting, keyword limits, and support URLs early enough that missing assets do not block submission. Pricing often starts low to gather reviews, then moves up once credibility exists; paid-up-front pricing tends to match small utility apps better than aggressive free-to-play patterns unless the product truly needs ongoing service revenue.

How these pieces connect is the insight: the same methodology as generic [[ai-driven-development-overview]] becomes reliable on iOS when you add explicit platform validation gates, narrow automated testing to high-leverage logic, and treat Cursor prompts as compiled artifacts from specification and rules rather than improvised chat. The assistant’s job is to keep decisions legible; Cursor’s job is to mutate files under that legibility; Xcode’s job is to tell you whether reality agrees.

Open questions include how much of the phase template you keep for very small utilities versus multi-surface apps, and how aggressively you snapshot handoff context when model providers or pricing change. Further reading lives in the linked concept notes above, especially [[cursor-rules-context-management]] and [[specification-first-ai-development]].
