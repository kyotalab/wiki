# LLM Wiki

A personal knowledge wiki built with the help of LLMs, covering technical topics across software engineering, machine learning, and adjacent fields.

---

## Overview

This wiki is a curated collection of technical knowledge, constructed by processing web sources through LLM-assisted workflows. Raw material — primarily from Japanese-language sources — is translated, synthesized, and organized into structured English notes.

The goal is not to mirror the web, but to build a personal knowledge base where concepts are understood, connected, and expressed in my own words.

---

## Scope

- **Domain**: Technology in general — with a focus on LLMs, machine learning, and software systems
- **Language**: English (source material may be in Japanese)
- **Depth**: Concept-level understanding, not exhaustive documentation

---

## Structure

```
Wiki/
├── _templates/      # Note templates used during processing.
├── 00_Inbox/           # Raw web captures. Temporary — not for reading.
├── 01_Concepts/        # One concept per file. Definitions and mechanisms.
├── 02_Topics/          # Multi-concept synthesis. How ideas connect.
├── 03_Atlas/           # Index notes and concept maps (Mermaid).
├── 04_Snippets/        # Copy-paste ready code. Minimal explanation.
└── 99_Archive/         # Processed Inbox files. Read-only.
```

### Note Types

| Type | Location | Purpose |
|------|----------|---------|
| Concept | `01_Concepts/` | Defines a single idea: what it is, how it works, why it matters |
| Topic | `02_Topics/` | Synthesizes multiple concepts around a theme |
| MOC | `03_Atlas/` | Map of Content — navigation index for a domain or tag |
| Snippet | `04_Snippets/` | Copy-paste ready code with minimal explanation |

---

## Workflow

```
Web source (Japanese or English)
        ↓
  Captured as Markdown → Inbox/
        ↓
  Processed by Cursor (.cursorrules)
        ↓
  Translated, paraphrased, structured → Concepts/ or Topics/
        ↓
  Linked and indexed → Atlas/
        ↓
  Browsed in Obsidian / Published via Quartz (future)
```

### Capture Tools
- **MarkDownload** — browser extension for one-click Markdown capture
- **Jina Reader** (`r.jina.ai/URL`) — URL-to-Markdown API, callable from Cursor

### Processing Tools
- **Cursor** — LLM-assisted note generation, translation, and linking
- **Obsidian** — local browsing, graph view, and backlink navigation

### Version Control
- **Git / GitHub** — change history and future publishing base

---

## Note Conventions

### Frontmatter
Every Concept and Topic note includes:

```yaml
---
title: ""        # Title Case, English
tags: []         # max 3 tags, lowercase, hyphenated
source: ""       # original URL(s)
created: YYYY-MM-DD
related: []      # linked note slugs
---
```

### File Naming
- Lowercase slugs with hyphens only
- Example: `transformer-architecture.md`, `retrieval-augmented-generation.md`

### Tagging
- Maximum 3 tags per note
- Tag categories: domain (`llm`, `nlp`, `cv`), type (`architecture`, `training`, `evaluation`), status (`stub`)

### Wikilinks
- Internal links use `[[slug]]` format
- Unwritten notes are linked as stubs and tracked in Atlas MOCs

---

## Cursor Commands

These prompts are defined in `.cursorrules` and can be used directly in Cursor:

| Command | Action |
|--------|--------|
| `Process this inbox note` | Run full Inbox → Wiki pipeline on the current file |
| `Create concept note: [topic]` | Generate a new Concept note |
| `Create topic note: [theme]` | Generate a new Topic note |
| `Create snippet note: [use case]` | Generate a new Snippet note with working code |
| `Update atlas for [tag]` | Regenerate the MOC for a given tag |
| `Find related notes: [concept]` | List notes that should link to this concept |
| `Generate mermaid map: [theme]` | Create a Mermaid concept map for Atlas/ |

---

## Status

This wiki is actively maintained as a private knowledge base, with potential future publication via [Quartz](https://quartz.jzhao.xyz/).

---

## License

All notes are original writing. Source URLs are cited in frontmatter. This repository does not reproduce copyrighted content.