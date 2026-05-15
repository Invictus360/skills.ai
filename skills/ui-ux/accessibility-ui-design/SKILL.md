---
name: accessibility-ui-design
description: When designing and implementing web interfaces to ensure they are usable by everyone.
version: 1.0.0
tags: [ui-ux, a11y, inclusive-design]
---

# Accessibility (a11y) UI Design

## When to use
- Writing HTML markup for UI components.
- Designing complex interactive widgets (modals, dropdowns, tabs).
- Auditing existing user interfaces for compliance.

## What it does
Ensures web interfaces comply with WCAG standards, making them operable via keyboard and understandable by screen readers.

## Workflow
1. **Semantic HTML First**: Use native elements (`<button>`, `<nav>`, `<dialog>`) before building custom `<div>` components.
2. **Keyboard Navigation**: Ensure all interactive elements are reachable via the `Tab` key and operable via `Enter` or `Space`.
3. **Focus Management**: Trap focus inside open modals and return focus to the trigger element when closed.
4. **ARIA Attributes**: Apply `aria-expanded`, `aria-hidden`, and `aria-live` to dynamic content only when native HTML is insufficient.
5. **Color Contrast**: Verify foreground/background colors meet the WCAG AA 4.5:1 contrast ratio.

## Rules
- All `<img>` tags must have an `alt` attribute (even if empty `alt=""` for decorative images).
- Forms must have explicitly associated `<label>` elements.
- Do not outline: `none` without providing custom visual focus states.

## Anti-patterns
- **Div Buttons**: Using `<div onClick={...}>` instead of `<button>`.
- **Relying solely on Color**: Communicating error states purely through red text without an icon or textual indicator.

## Output format
HTML/JSX markup that passes automated accessibility tools (like axe-core) and can be fully navigated without a mouse.
