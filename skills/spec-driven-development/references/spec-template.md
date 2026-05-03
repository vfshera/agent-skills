# Feature Spec Template

Each unit in your build plan gets its own spec file. This is the complete instruction set for that unit — it replaces the vague prompt.

## File Location

Place specs in `context/specs/` with numbered naming:

```
context/specs/
├── 00-build-plan.md
├── 01-authentication.md
├── 02-project-creation.md
├── 03-canvas-setup.md
└── ...
```

## Template

```markdown
# Unit NN: [Feature Name]

## Goal

One or two sentences describing the concrete output
of this unit. Be specific and concrete.

_Example: "Create sign-in and sign-up pages using Clerk
components with a two-panel layout on desktop and
form-only on mobile. Use proxy.ts for route protection,
not middleware.ts."_

## Design

Visual and structural decisions specific to this unit.
Reference ui-context.md tokens where relevant.

### Layout

[Describe the layout behavior, responsiveness requirements]

### Components

[Describe component choices, any specific component library usage]

### Interactions

[Describe user interactions, states, transitions]

## Implementation

### [Component or Sub-section Name]

Detailed description of what to build. Enough detail
that there is no ambiguity about what done looks like.

### [Next sub-section]

Description.

## Dependencies

- [package-name](https://...) — [reason why needed]
- [package-name](https://...) — [reason why needed]

## Verify when done

- [ ] Condition one
- [ ] Condition two
- [ ] No TypeScript errors
- [ ] No console errors
- [ ] Responsive at mobile and desktop
- [ ] npm run build passes
- [ ] [Other specific verification conditions]
```

## Good vs Bad Spec Examples

### Goal

| Bad | Good |
|-----|------|
| "Create the auth pages" | "Create sign-in and sign-up pages using Clerk components with a two-panel layout on desktop and form-only on mobile. Use proxy.ts for route protection, not middleware.ts." |

### Design

| Bad | Good |
|-----|------|
| "Use the theme" | "Use bg-base for page background, bg-surface for cards, text-primary for headings. Border radius: rounded-xl for buttons, rounded-2xl for cards." |

### Implementation

| Bad | Good |
|-----|------|
| "Add authentication" | "Create auth/ directory with sign-in/page.tsx and sign-up/page.tsx. Use Clerk's <SignIn> and <SignUp> components. Wrap pages in AuthLayout component that centers content vertically. On mobile, hide the left panel and show only the form." |

### Verification

| Bad | Good |
|-----|------|
| "Works" | "Signed-in user can access /dashboard. Unsigned-in user redirected to /sign-in. No console errors on page load. Build passes." |

---

## How to Generate Specs

When you're ready to build a unit, have a quick conversation with your planning AI first. Share:

- Your `01-project-overview.md` and `02-architecture.md` for context
- What you want to build in this unit
- Any specific decisions or constraints that apply

Then ask it to write the spec file:

```
Here is my project overview: [paste project-overview.md]
Here is my architecture: [paste architecture.md]
I want to implement: [describe the feature]
Write a detailed spec file for this feature following
this structure:

- Goal (1-2 sentences, specific and concrete)
- Design (visual and structural decisions)
- Implementation (broken into sub-sections)
- Dependencies (packages to install)
- Verification checklist

Be as specific as possible. If anything is unclear,
ask me questions before writing the spec.
```

---

## Execution Prompts

### To implement a unit:

```
Read context/specs/NN-feature-name.md.
Update context/06-progress-tracker.md to mark this as in progress.
Implement it exactly as specified.
Do not go beyond the scope of this unit.
```

### To correct something off-spec:

```
The [specific element] does not match the spec.
Expected: [what the spec says].
Current: [what was built].
Fix only this. Do not change anything else.
```

### To close a unit:

```
Implementation is complete and verified.
Mark unit NN complete in context/06-progress-tracker.md.
Push branch feat/NN-feature-name to GitHub.
```

---

## One Feature, Multiple Specs

One feature might need one spec file or it may need multiple. Let the complexity of the feature decide, not a fixed rule.

For example:

- `01-authentication.md` — single spec for auth pages
- `02-project-creation.md` — single spec for project CRUD
- `03-canvas-setup.md` — might need three specs:
  - 03-canvas-layout.md
  - 04-canvas-nodes.md
  - 05-canvas-edges.md