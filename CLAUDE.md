# Claude Code instructions – BandsTour / Concert Scout

## Working rule

Work on **one GitHub issue at a time**. The active issue defines the complete scope.

Before changing code:
1. Read this file, `README.md`, and the active GitHub issue.
2. Inspect relevant existing files.
3. State a short implementation plan.
4. Do not implement future issues early.

During implementation:
- Keep changes small and directly related to the active issue.
- Prefer simple, explicit TypeScript over abstraction without a current need.
- Reuse existing project patterns.
- Do not make unrelated refactors.
- Do not add dependencies unless clearly necessary for the active issue.
- Never commit API keys, passwords, tokens, mailbox credentials or other secrets.
- Keep business logic out of n8n Code nodes; n8n should orchestrate.
- Keep LLMs out of deterministic logic such as Europe filtering, deduplication and persistence rules.
- Validate external inputs and LLM outputs at runtime with Zod where applicable.

Testing:
- Add/update automated tests for changed behavior.
- Run relevant tests.
- Run type checking.
- Run linting when configured.

When finished:
1. Summarize what changed.
2. List changed files.
3. Report test/typecheck/lint results.
4. Mention limitations or follow-up work.
5. Stop. Do not continue with the next issue.

## Target stack

- Node.js
- TypeScript (strict)
- pnpm
- Fastify
- Prisma
- PostgreSQL
- Zod
- Vitest
- Docker / Docker Compose
- n8n for orchestration

## System boundaries

The backend owns:
- artist/domain rules
- source integrations
- normalization
- Europe filtering
- deduplication
- persistence
- scan logic
- notification state
- signal processing

n8n owns:
- schedules
- mailbox triggers
- calling backend endpoints
- sending notifications
- workflow retries/integration plumbing

LLMs may:
- classify unstructured text
- extract explicitly stated tour/event facts

LLMs must not:
- invent missing dates/cities
- decide Europe membership
- directly mutate persistence without validated application logic
- replace deterministic deduplication

## Definition of Done

An issue is done when its acceptance criteria are met, relevant tests pass, TypeScript passes, no secrets are committed, and unrelated changes are excluded.
