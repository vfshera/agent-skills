# Context File Templates

Copy these templates to a `context/` folder in your project. Rename them with the numbering convention shown below.

---

## context/01-project-overview.md

```markdown
# [Project Name]

## Overview

[One paragraph describing what this application does,
who it's for, and what problem it solves.]

## Goals

1. [Goal one — specific and measurable]
2. [Goal two]
3. [Goal three]

## Core User Flow

1. [Step one — e.g. User signs in]
2. [Step two]
3. [Step three]
4. [Continue until the core flow is complete]

## Features

### [Feature Category One]

- [Feature description]
- [Feature description]

### [Feature Category Two]

- [Feature description]
- [Feature description]

## Scope

### In Scope

- [What you are building]
- [What you are building]

### Out of Scope

- [What you are explicitly not building]
- [What you are explicitly not building]

## Success Criteria

1. [Specific, verifiable condition — e.g. A signed-in
   user can create and open a project]
2. [Condition two]
3. [Condition three]
```

---

## context/02-architecture.md

```markdown
# Architecture

## Stack

| Layer | Technology | Role |
|-------|------------|------|
| Framework | [e.g. Next.js 16 + TypeScript] | [Role description] |
| UI | [e.g. Tailwind + shadcn/ui] | [Role description] |
| Auth | [e.g. Clerk] | [Role description] |
| Database | [e.g. Prisma + PostgreSQL] | [Role description] |
| [Layer name] | [Technology] | [Role description] |

## System Boundaries

- `[folder]` — [Responsibility description]
- `[folder]` — [Responsibility description]
- `[folder]` — [Responsibility description]

## Storage Model

- **Database**: [What goes here]
- **[Storage service]**: [What goes here]
- **Cache**: [What goes here if applicable]

## Auth and Access Model

[Describe authentication approach, ownership model, and access control rules]

## [Additional sections as needed]

### [Section Name]

[Description]

## Invariants

1. [Rule the codebase must never violate]
2. [Rule]
3. [Rule]
4. [Rule]
```

---

## context/03-code-standards.md

```markdown
# Code Standards

## General

- [Principle one]
- [Principle two]
- [Principle three]

## TypeScript

- [Convention one]
- [Convention two]
- [Convention three]

## [Framework, e.g. Next.js]

- [Convention one]
- [Convention two]

## Styling

- [Convention one]
- [Convention two]

## API Routes

- [Convention one]
- [Convention two]

## Data and Storage

- [Convention one]
- [Convention two]

## File Organization

- `[folder]` — [Responsibility]
- `[folder]` — [Responsibility]
```

---

## context/04-ai-workflow-rules.md

```markdown
# Development Workflow

## Approach

[Describe the overall development approach, e.g. spec-driven, incremental]

## Scoping Rules

- [Rule one]
- [Rule two]
- [Rule three]

## When To Split Work

[Describe conditions that require splitting implementation into smaller steps]

## Handling Missing Requirements

- [What to do when a requirement is ambiguous]
- [What to do when a requirement is missing]

## Protected Foundation Components

Do not modify generated third-party foundation components unless explicitly instructed.

This includes:

- `[component category]`
- `[component category]`

## Keeping Docs In Sync

Update the relevant context file whenever implementation changes:

- [Condition one]
- [Condition two]

## Before Moving To The Next Unit

1. [Verification step one]
2. [Verification step two]
3. [Verification step three]
```

---

## context/05-ui-context.md

> **Note:** This file is optional. Skip if the project already has an established UI.

```markdown
# UI Context

## Theme

[Theme description, e.g. Dark only. No light mode. The visual language is a dark technical workspace]

### Color Palette

| Role | Token Name | Hex / Value |
|------|------------|-------------|
| [e.g. Page background] | [e.g. --bg-base] | [#080809] |
| [Surface] | [--bg-surface] | [#111114] |
| [Elevated surface] | [--bg-elevated] | [#18181c] |
| [Primary text] | [--text-primary] | [#f0f0f4] |
| [Secondary text] | [--text-secondary] | [#c0c0cc] |
| [Brand accent] | [--accent-primary] | [#00c8d4] |
| [Error] | [--state-error] | [#ff4d4f] |
| [Success] | [--state-success] | [#34d399] |

## Typography

| Role | Font | CSS Variable |
|------|------|--------------|
| UI text | [e.g. Geist Sans] | [--font-geist-sans] |
| Code/mono | [e.g. Geist Mono] | [--font-geist-mono] |

## Border Radius

| Context | Class |
|---------|-------|
| Inline / small UI | [e.g. rounded-xl] |
| Cards / panels | [e.g. rounded-2xl] |
| Modal / overlay | [e.g. rounded-3xl] |

## Component Library

[Component library name and usage conventions]

## Layout Patterns

[Describe layout structure, e.g. sidebar behavior, modal patterns, navbar structure]

## Icons

[Icon library and usage conventions, e.g. Lucide React, stroke-based only]
```

---

## context/06-progress-tracker.md

```markdown
# Progress Tracker

Update this file after every meaningful implementation change.

## Current Phase

- [phase name, e.g. Not started / In progress / Complete]

## Current Goal

- [What you are building right now]

## Completed

- [Completed item one]
- [Completed item two]

## In Progress

- [Item currently being built]

## Next Up

- [Next unit to build]

## Open Questions

- [Any unresolved decisions]

## Architecture Decisions

- [Decisions made that affect the system design or data model — include why the decision was made]

## Session Notes

- [Context needed to resume work in the next session]
```

---

## CLAUDE.md (Entry Point)

Place this in the project root:

```markdown
## Application Building Context

Read the following files in order before implementing
or making any architectural decision:

1. `context/01-project-overview.md` — product definition,
   goals, features, and scope
2. `context/02-architecture.md` — system structure,
   boundaries, storage model, and invariants
3. `context/05-ui-context.md` — theme, colors, typography,
   and component conventions
4. `context/03-code-standards.md` — implementation rules
   and conventions
5. `context/04-ai-workflow-rules.md` — development workflow,
   scoping rules, and delivery approach
6. `context/06-progress-tracker.md` — current phase,
   completed work, open questions, and next steps

Update `context/06-progress-tracker.md` after each
meaningful implementation change.

If implementation changes the architecture, scope, or
standards documented in the context files, update the
relevant file before continuing.
```