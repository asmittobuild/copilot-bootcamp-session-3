# Cloud Architecture Overview

This document provides a simple cloud/system context for the TODO monorepo and a request sequence for creating a TODO.

## System Context

```mermaid
flowchart LR
    U[User]
    FE[React Frontend<br/>packages/frontend]
    API[Express API<br/>packages/backend]
    DB[(In-Memory SQLite Store)]

    U -->|Uses in browser| FE
    FE -->|HTTP JSON<br/>/api/tasks| API
    API -->|SQL read/write| DB
```

## Sequence: User Creates a TODO

```mermaid
sequenceDiagram
    actor U as User
    participant FE as React Frontend (TaskForm/App)
    participant API as Express API
    participant DB as In-Memory SQLite

    U->>FE: Enter title/description/due date and submit
    FE->>FE: Validate title is not empty
    FE->>API: POST /api/tasks { title, description, due_date }
    API->>API: Validate title
    API->>DB: INSERT INTO tasks (...)
    DB-->>API: lastInsertRowid
    API->>DB: SELECT * FROM tasks WHERE id = ?
    DB-->>API: created task row
    API-->>FE: 201 Created + task JSON
    FE->>FE: Increment refreshKey
    FE->>API: GET /api/tasks
    API->>DB: SELECT * FROM tasks ORDER BY due_date, created_at
    DB-->>API: task list
    API-->>FE: 200 OK + tasks JSON
    FE-->>U: Updated task list rendered
```

## Assumptions and Constraints

- This architecture reflects the current monorepo implementation and is intended for development/local runtime.
- Task data is stored in an in-memory SQLite database (`:memory:`), so all task data is lost when the backend process restarts.
- The system is a single backend service boundary (Express API) with no external queue, cache, or separate database service.
- The frontend communicates with the backend using JSON over HTTP at `/api/tasks` endpoints.
- No authentication/authorization flow is currently implemented in the frontend or backend code paths.