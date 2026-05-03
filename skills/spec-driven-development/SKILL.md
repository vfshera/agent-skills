---
name: spec-driven-development
description: Use when the user explicitly invokes "spec driven development" or "spec-driven development" methodology. This implements the Six-File Context System with a mandatory grilling phase to ensure the developer has clarified their thinking before generating any context files.
---

# Spec-Driven Development

A methodology for building software with AI that actually works. Instead of vague prompts producing broken code, this skill implements the Six-File Context System — a documented foundation that keeps every AI session consistent and aligned.

## When to Use This Skill

Use this skill when you want to:

- Start a new project with proper AI development infrastructure
- Resume work on an existing project and restore full context
- Break down features into scoped, verifiable units
- Prevent "vibe coding collapse" or "feature drift" in AI-assisted builds

## The Core Principle

You are the architect. AI is the execution engine.

Before you write any prompt, you must know what you're building, how it fits together, and what rules the code must follow. The Six-File Context System documents that knowledge so every AI session starts with the same foundation.

---

## Phase 1: Grilling (Required Before Generating Files)

Before generating any context files, you must validate that the user has clarity on their project. Use the questions below to "grill" the user until they can answer each one clearly and specifically.

### Product Questions

Grill the user until they can answer ALL of these:

1. **What does this application do in one sentence?**
   - If they can't describe it in one sentence, they don't understand it well enough yet.

2. **Who is the primary user and what is their core need?**
   - Who is building for? What problem does it solve for them?

3. **What is the step-by-step flow from sign-up to core value?**
   - Walk through the complete user journey. Every step matters.

4. **What are the three most important features for the first version?**
   - Not everything — just the three that deliver the core value.

5. **What is explicitly out of scope?**
   - Explicitly list what you are NOT building. This prevents the AI from suggesting unnecessary dependencies.

### Technical Questions

Grill the user until they can answer ALL of these:

1. **What is the full technology stack and why each choice?**
   - For every technology, the user must state why it was chosen over alternatives.

2. **Where does data live — database, file storage, cache?**
   - Be explicit: metadata in the database, generated artifacts in blob storage, nothing in memory.

3. **How does authentication and access control work?**
   - Who can see what? Who can modify what? How is ownership enforced?

4. **What are the system boundaries — which folder owns what responsibility?**
   - Name the folders and state their exact responsibilities.

5. **What are the rules the codebase must never violate?**
   - These are invariants. Example: "Request handlers do not run long-lived AI work" or "Auth is enforced at every mutation boundary."

### Design Questions

Grill the user until they can answer ALL of these:

1. **What is the visual language — colors, typography, spacing?**
   - If the project already has established UI, confirm this and skip ui-context.md generation.

2. **What UI component library are you using?**
   - shadcn/ui, Radix, custom, etc.

3. **What does the layout look like at a high level?**
   - Sidebar? Top nav? Modal-based? Full-screen canvas?

### Process Questions

Grill the user until they can answer ALL of these:

1. **What are the major features broken into buildable units?**
   - A "unit" is a single, scoped, verifiable piece of work. Not "build the dashboard" — that's a phase. A unit is: "Build the project sidebar with My Projects and Shared tabs, empty placeholder states, and open/close behavior. No API calls yet."

2. **In what order should those units be built?**
   - Dependencies first. Security before functionality. Backend before frontend wiring. UI shells before real data.

3. **What does done look like for each unit?**
   - Specific, verifiable conditions. Not "looks good" but "a signed-in user can create and open a project."

### Validation Checkpoint

Before proceeding to Phase 2, confirm the user can answer EVERY question above clearly and specifically. If any answer is vague, incomplete, or missing, continue grilling until clarity is achieved.

> **This is the critical step most developers skip.** The quality of what AI produces is entirely determined by the quality of the thinking you bring to it.

---

## Phase 2: Generate Context Files

Once the user has been properly grilled and has clear answers, generate the six context files using the prompts in [prompts.md](references/prompts.md).

### The Six Context Files

| File                     | Purpose                                             | Required?           |
| ------------------------ | --------------------------------------------------- | ------------------- |
| **project-overview.md**  | Product definition, goals, features, scope          | Always              |
| **architecture.md**      | Tech stack, boundaries, storage, auth, invariants   | Always              |
| **code-standards.md**    | TypeScript conventions, patterns, file organization | Always              |
| **ai-workflow-rules.md** | How the AI should behave while building             | Always              |
| **ui-context.md**        | Colors, typography, component conventions           | Only if new project |
| **progress-tracker.md**  | Current phase, completed work, next steps           | Always              |

### Confirmation Step

Before generating any files, summarize the clarified answers from Phase 1 and confirm with the user:

```
Based on Phase 1 grilling, here are your clarified answers:

**Product:**
- One-sentence description: [user's answer]
- Primary user and core need: [user's answer]
- Core user flow: [user's answer]
- Top 3 features for v1: [user's answer]
- Out of scope: [user's answer]

**Technical:**
- Tech stack: [user's answer]
- Data storage: [user's answer]
- Auth model: [user's answer]
- System boundaries: [user's answer]
- Invariants: [user's answer]

**Design:**
- Visual language: [user's answer or "existing UI confirmed"]
- Component library: [user's answer]
- Layout: [user's answer]

**Process:**
- Buildable units: [user's answer]
- Build order: [user's answer]
- Completion criteria: [user's answer]

Do you want to add or clarify anything before I generate the context files?
```

After the user confirms (or makes edits), proceed to generate the files.

### How to Generate

1. Copy [templates.md](references/templates.md) to a `context/` folder in the project
2. For each file, use the corresponding prompt from [prompts.md](references/prompts.md) — the prompts now reference the confirmed Phase 1 answers automatically
3. Review the generated output — refine until it accurately represents the project

### Context File Naming Convention

```
context/
├── 01-project-overview.md
├── 02-architecture.md
├── 03-code-standards.md
├── 04-ai-workflow-rules.md
├── 05-ui-context.md          # optional
└── 06-progress-tracker.md
```

### Entry Point File

Create `AGENTS.md`or `CLAUDE.md` in the project root:

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

---

## Phase 3: Build Planning

With context files in place, decompose the full build into scoped, verifiable units.

### Unit Definition

A unit is:

- **Single** — produces one visible result
- **Scoped** — stays within one system boundary
- **Verifiable** — has a clear checklist of completion conditions
- **Buildable** — can be completed in one focused session

### Bad vs Good Units

| Bad                   | Good                                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| "Build the dashboard" | "Build the project sidebar with My Projects and Shared tabs, empty placeholder states, and open/close behavior. No API calls yet."                     |
| "Add authentication"  | "Create sign-in and sign-up pages using Clerk components with two-panel layout on desktop and form-only on mobile. Use proxy.ts for route protection." |

### Decomposition Rules

1. **Dependencies first** — if unit B requires unit A, A comes first
2. **Security before functionality** — auth comes before the features it protects
3. **Backend before frontend** — build API routes first, then wire UI to them
4. **UI shells before real data** — build component structure with placeholder data first
5. **Just-in-time dependencies** — only install a package in the unit where it first unlocks real behavior

### How to Decompose

Use the guidance in [build-planning.md](references/build-planning.md) to help the user break their project into units. For each unit, generate a spec file using [spec-template.md](references/spec-template.md).

---

## Phase 4: Execute with Specs

Each unit gets a spec file that serves as a contract with the AI.

### Spec File Structure

See [spec-template.md](references/spec-template.md) for the full template. Each spec includes:

1. **Goal** — One or two sentences, specific and concrete
2. **Design** — Visual and structural decisions, reference ui-context.md tokens
3. **Implementation** — Broken into sub-sections, one per component or system boundary
4. **Dependencies** — Packages to install (with reason)
5. **Verification checklist** — Specific conditions that must be true before the unit is complete

### Execution Prompts

**To implement a unit:**

```
Read context/specs/NN-feature-name.md.
Update context/06-progress-tracker.md to mark this as in progress.
Implement it exactly as specified.
Do not go beyond the scope of this unit.
```

**To correct something off-spec:**

```
The [specific element] does not match the spec.
Expected: [what the spec says].
Current: [what was built].
Fix only this. Do not change anything else.
```

**To close a unit:**

```
Implementation is complete and verified.
Mark unit NN complete in context/06-progress-tracker.md.
```

---

## Key Principles

1. **Think before build** — The grilling phase is not optional. Clarity before code.

2. **Spec as contract** — The spec file is the source of truth. The AI executes what is written, no more, no less.

3. **No vibe coding** — Don't let the AI guess. Every decision belongs in the context files or spec files.

4. **Progress tracking** — Update progress-tracker.md after every meaningful change. This is how the AI restores context in new sessions.

5. **Update on change** — If implementation reveals something that should change in the context files, update them immediately. The documentation must reflect reality.

---

## Reference Files

- [prompts.md](references/prompts.md) — AI prompts to generate each context file
- [templates.md](references/templates.md) — Blank templates for all six context files
- [spec-template.md](references/spec-template.md) — Feature spec file template
- [build-planning.md](references/build-planning.md) — Unit decomposition rules and guidance
