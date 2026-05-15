---
name: state-management-patterns
description: When deciding where and how to store data in a modern web application.
version: 1.0.0
tags: [frontend, state, architecture]
---

# State Management Patterns

## When to use
- Adding new interactive features that require data persistence across views.
- Refactoring an app suffering from excessive re-renders.
- Integrating external data fetching with local UI state.

## What it does
Dictates the optimal location to store application state (URL, local state, global store, or server cache) to minimize complexity and maximize performance.

## Workflow
1. **Assess State Scope**: Determine if the state is local (UI only), global (user session/theme), server (database data), or URL-driven (filters/search).
2. **URL First**: Move sort, filter, and pagination parameters to URL search params.
3. **Server State Separation**: Use tools like React Query or SWR for caching server responses instead of storing them in global state.
4. **Localize UI State**: Keep form inputs, modal visibility, and toggles in local component state (`useState`).
5. **Global Fallback**: Only use Context/Redux/Zustand for truly global client state (e.g., Auth, Theme).

## Rules
- Server data must not be manually synced to a global UI store.
- Shareable application states (like search queries) must exist in the URL.

## Anti-patterns
- **Mirroring State**: Copying props into local state (`const [val, setVal] = useState(props.val)`).
- **Global Everything**: Storing UI-only state (like a dropdown toggle) in Redux/Zustand.

## Output format
Refactored logic separating data into URL parameters, Server Cache hooks, and localized component state.
