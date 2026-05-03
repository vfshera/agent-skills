# Build Planning: Unit Decomposition

This guide helps you break a full project into scoped, verifiable units that can be built one at a time using the spec-driven workflow.

---

## What Is a Unit?

A unit is a **single, scoped, verifiable piece of work** that:

- Produces one visible, verifiable result
- Stays within one system boundary
- Has a clear checklist of completion conditions
- Can be built in one focused session

---

## Unit vs Phase

| Phase                 | Unit                                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| "Build the dashboard" | "Build the project sidebar with My Projects and Shared tabs, empty placeholder states, and open/close behavior. No API calls yet."                     |
| "Add authentication"  | "Create sign-in and sign-up pages using Clerk components with two-panel layout on desktop and form-only on mobile. Use proxy.ts for route protection." |
| "Build the canvas"    | "Set up React Flow canvas with pan/zoom controls and basic node rendering. Use placeholder data, no API integration yet."                              |

A **phase** is a collection of units. A **unit** is a single, deliverable piece.

---

## Rules for Decomposition

### 1. Dependencies First

If unit B requires unit A to exist, A comes first. Never build on top of something that doesn't exist yet.

```
Good:  Unit 1: Auth → Unit 2: Project CRUD → Unit 3: Canvas
Bad:   Unit 1: Canvas → Unit 2: Auth (canvas can't exist without auth)
```

### 2. Security Before Functionality

Auth and access control always come before the features they protect.

```
Good:  Unit 1: Auth + Route protection → Unit 2: Canvas
Bad:   Unit 1: Collaborative Canvas → Unit 2: Auth (building on unsecured foundation)
```

### 3. Backend Before Frontend Wiring

Build the API routes first, then wire the UI to them. Combining both in one unit gives the AI too much surface area to make assumptions.

```
Good:  Unit 1: POST /api/projects route → Unit 2: Create Project button + form
Bad:   Unit 1: Create project button + form + API route (too much at once)
```

### 4. UI Shells Before Real Data

Build the component structure with placeholder data first, then connect it to real API calls. This lets you verify the UI works before the data layer exists.

```
Good:  Unit 1: Sidebar with placeholder list → Unit 2: Wire to API
Bad:   Unit 1: Sidebar + API integration + loading states (too much)
```

### 5. Just-in-Time Dependencies

Only install a package in the unit where it first unlocks real behavior. Don't install everything upfront — it creates noise and can cause the AI to reach for tools it shouldn't use yet.

```
Good:  Install Clerk in Unit 1 (auth), not in Unit 0 (setup)
Bad:   Install all dependencies upfront, then build features
```

### 6. Merge When Appropriate

Units that are always done together in the same session with no standalone result should be merged.

```
Merge: "Create button component" + "Create button styles" → "Create button component with styles"
Keep:  "Create project sidebar" (standalone result) separate from "Wire sidebar to API"
```

---

## Sample Build Plan

For a project with: Auth, Projects, Canvas, AI Generation, Spec Export

```
Unit 01: Auth Setup
  - Clerk integration, sign-in/sign-up pages
  - Route protection for authenticated routes
  - Depends on: Nothing

Unit 02: Project CRUD
  - Create project page, project list
  - POST/GET /api/projects routes
  - Depends on: Unit 01

Unit 03: Canvas Setup
  - React Flow canvas with pan/zoom
  - Basic node rendering with placeholder data
  - Depends on: Unit 02

Unit 04: Canvas Integration
  - Connect canvas to Liveblocks for real-time
  - Presence indicators, cursors
  - Depends on: Unit 03

Unit 05: Starter Templates
  - Prebuilt template library
  - Import template into canvas
  - Depends on: Unit 04

Unit 06: AI Design Generation
  - Trigger.dev workflow for AI generation
  - Write nodes/edges to Liveblocks room
  - Depends on: Unit 04

Unit 07: AI Spec Generation
  - Convert canvas graph to Markdown
  - Save to blob storage
  - Link to project in database
  - Depends on: Unit 06

Unit 08: Spec Download
  - View and download generated specs
  - Depends on: Unit 07
```

---

## Validating the Build Order

For each unit, ask:

1. **Does everything this unit depends on exist in a previous unit?**
   - If no, reorder.

2. **Are any two adjacent units always done in the same session with no standalone result between them?**
   - If yes, merge them.

When the order is correct:

- Every unit builds cleanly on top of the previous one
- No unit requires jumping ahead
- No unit leaves something that doesn't work until three units later

---

## Save the Build Plan

Save as `context/specs/00-build-plan.md`. This file proves the entire system was designed before the first prompt was sent.

It should include:

1. **Project overview** — 1-2 sentences
2. **Ordered unit list** — number, name, what it builds, dependencies
3. **Total unit count** — for progress tracking

```
# Build Plan: [Project Name]

## Overview

[Brief project description]

## Units (N total)

| # | Unit | Output | Dependencies |
|---|------|--------|--------------|
| 01 | Auth Setup | Sign-in/sign-up pages with route protection | None |
| 02 | Project CRUD | Create/list projects with API routes | 01 |
| 03 | Canvas Setup | React Flow canvas with placeholder data | 02 |
...

## Progress

- Completed: 0
- In Progress: 0
- Remaining: N
```
