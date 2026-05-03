# AI Prompts to Generate Context Files

These prompts use the confirmed answers from Phase 1 (Grilling). Since the context files are ordered, each prompt can reference previously generated files.

---

## 1. project-overview.md

```
Help me write a project-overview.md file for my project.
It should include:

- A one paragraph overview of what the application does
- A numbered list of goals
- A step-by-step core user flow from start to finish
- A features section broken down by category
- An in-scope section listing what we are building
- An out-of-scope section listing what we are not building
- A success criteria section defining what done looks like

Base this on the confirmed Phase 1 answers for this project.

Write it in plain Markdown. Be specific and concrete.
Avoid vague language.
```

### What Good Output Looks Like

- Goals are measurable, not aspirational
- User flow is step-by-step with no gaps
- Out-of-scope list is explicit and detailed
- Success criteria are verifiable (e.g., "a signed-in user can create and open a project")

---

## 2. architecture.md

```
Help me write an architecture.md file for my project.
It should include:

- A stack table with each layer, technology, and its role
- System boundaries which folder owns which responsibility
- Storage model what goes in the database vs file storage vs cache
- Auth and access model how authentication and ownership work
- Any AI or background task models if relevant
- Invariants rules the codebase must never violate

Base this on the confirmed Phase 1 answers and align with
01-project-overview.md goals and scope.

Write it in plain Markdown with tables where appropriate.
Be specific. The invariants section should have at least
four rules.
```

### What Good Output Looks Like

- Stack table is complete with a clear role for every technology
- System boundaries specify exact folder names and responsibilities
- Storage model is explicit, no ambiguity about what lives where
- Invariants are stated as rules, not guidelines

---

## 3. code-standards.md

```
Help me write a code-standards.md file for my project.
It should include:

- General code quality principles
- TypeScript conventions (strict mode, type usage, interfaces)
- Framework patterns (React Server Components, when to use client)
- API route structure and conventions
- File organization rules
- Styling approach (CSS tokens, component patterns)
- Data and storage conventions

Base this on the confirmed Phase 1 answers and align with
02-architecture.md system boundaries and invariants.

Write it in plain Markdown. Be specific and concrete.
```

### What Good Output Looks Like

- TypeScript rules are explicit (no any, use interfaces, strict mode)
- Framework patterns are clear (when to use client components)
- File organization rules specify folder responsibilities
- Styling conventions reference design tokens

---

## 4. ai-workflow-rules.md

```
Help me write an ai-workflow-rules.md file for my project.
It should define how an AI coding agent should behave
while building this project. Include:

The overall approach (spec-driven, incremental)
Scoping rules (one unit at a time, no speculative changes)
When to split work into smaller steps
How to handle missing or ambiguous requirements
Which files should not be modified without explicit
instruction (e.g. generated UI library components)
How to keep documentation in sync with implementation
Verification checklist before moving to the next unit

Base this on the confirmed Phase 1 answers and align with
02-architecture.md invariants and 03-code-standards.md conventions.

Write it as direct instructions to the agent. Not guidelines —
rules. Use imperative language.
```

### What Good Output Looks Like

- Written as direct commands, not suggestions
- "Work on one feature unit at a time" not "try to keep scope small"
- Missing requirements section tells the agent exactly what to do

---

## 5. ui-context.md

```
Help me write a ui-context.md file for my project.
It should include:

- Color palette with semantic token names and hex values
- Typography (font families, sizes, weights)
- Border radius scale
- Component library conventions
- Layout patterns (sidebar, modals, navigation)
- Icon usage

Base this on the confirmed Phase 1 design answers. If the
project has an existing UI, reference the established design system.

Write it in plain Markdown with tables where appropriate.
```

**Note:** This is optional. Skip if the project already has an established UI. Confirm with the user before generating.

### What Good Output Looks Like

- Every color is a named token, not a raw hex value
- Agent should never need to invent a color
- Layout patterns describe the actual structure

---

## 6. progress-tracker.md

The progress tracker starts empty. Copy this template:

```markdown
# Progress Tracker

Update this file after every meaningful implementation change.

## Current Phase

- [phase name]

## Current Goal

- [what you are building right now]

## Completed

- None yet.

## In Progress

- None yet.

## Next Up

- [first unit to build]

## Open Questions

- [any unresolved decisions]

## Architecture Decisions

- [decisions made that affect the system design]

## Session Notes

- [context needed to resume in the next session]
```

Fill in the first two sections based on Phase 3 (Build Planning) results.

The agent updates this file after every unit. Update it when architectural decisions are made or open questions are resolved.

---

## Entry Point File ( AGENTS.md / CLAUDE.md)

After generating all context files, add this to the project root:

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
