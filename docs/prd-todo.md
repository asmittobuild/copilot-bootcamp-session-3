# Product Requirements Document (PRD) - TODO App Upgrade (Due Dates, Priority, and Filters)

## 1. Overview

The current TODO app is intentionally basic (task title and completion status). This PRD defines a teachable, low-complexity upgrade that improves task organization while keeping implementation lightweight.

The MVP adds due dates, priority levels, and simple filters so users can quickly identify what needs attention today and what is overdue. The solution must remain local-only (no backend or external storage changes).

---

## 2. MVP Scope

- Add optional `dueDate` to each task using ISO date format `YYYY-MM-DD`.
- Add `priority` to each task with enum values `P1 | P2 | P3`.
- Default `priority` to `P3` when not provided.
- Add filters: `All`, `Today`, and `Overdue`.
- Keep data storage local only (no backend integration or external persistence).
- Data validation: `title` is required.
- Data validation: `priority` must be one of `P1`, `P2`, or `P3`.
- Data validation: `dueDate` is optional and must be valid ISO `YYYY-MM-DD`; invalid values are ignored and treated as absent.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks so they are easier to identify at a glance.
- Add sorting behavior: overdue tasks first.
- Add sorting behavior: then by priority (`P1` to `P3`).
- Add sorting behavior: then by due date ascending.
- Add sorting behavior: tasks without a due date last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user features.
- Keyboard navigation and additional accessibility enhancements.
- External storage or backend-based persistence.
