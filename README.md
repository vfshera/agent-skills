# 🤖 Agent Skills

A curated collection of high-performance AI agent skills designed for modern web development workflows. These skills provide precise, actionable guidelines for performance optimization, architecture, and best practices across JavaScript, React, and React Router.

# Installation

```sh
pnpx skills add vfshera/agent-skills --skill='*'
```

or to install all of them globally:

```sh
pnpx skills add vfshera/agent-skills --skill='*' -g
```

Learn more about the CLI usage at [skills](https://github.com/vercel-labs/skills?tab=readme-ov-file#skills).

## 🛠️ Available Skills

### 🟨 [JavaScript Best Practices](https://github.com/vfshera/agent-skills/blob/main/skills/js-best-practices/SKILL.md)

Performance optimization and code style patterns for JavaScript and TypeScript.

- **Rules**: 21 focused on loops, data structures, and DOM manipulation.
- **Triggers**: Tasks involving array operations, Map/Set usage, direct DOM styling, or general JS/TS optimization.

### ⚛️ [React Best Practices](https://github.com/vfshera/agent-skills/blob/main/skills/react-best-practices/SKILL.md)

Advanced performance and composition patterns for React components.

- **Rules**: 47 covering bundle size, re-render avoidance, and React 19 APIs.
- **Triggers**: Creation/refactor of React components, hook implementation, memoization, or accessibility (a11y) improvements.

### 🛣️ [React Router Best Practices](https://github.com/vfshera/agent-skills/blob/main/skills/react-router-best-practices/SKILL.md)

Modern architecture and data patterns for React Router / Remix applications.

- **Rules**: 66 focusing on Single Fetch, loaders/actions, and internationalization.
- **Triggers**: Routing setup, server-side data fetching, form mutations, or `i18n` integration.

## 🚀 How to Use

AI Agents should automatically trigger these skills based on the context of the task.

1. **Trigger**: When a task matches a skill's description (e.g., "Optimizing React re-renders").
2. **Consult**: The agent reads the corresponding `SKILL.md` to identify relevant rules.
3. **Apply**: Rules are applied directly to the codebase with preference for the provided best-practice examples.

## License

MIT
