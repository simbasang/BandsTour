# BandsTour / Concert Scout

Concert Scout bevakar valda artister och meddelar när nya konserter eller turnéer i Europa dyker upp.

## Arkitektur

- **TypeScript/Node + Fastify** – kärnlogik och API
- **PostgreSQL + Prisma** – source of truth
- **n8n** – schemaläggning, mailbox och notifieringar
- **Ticketmaster Discovery API** – första strukturerade eventkällan
- **Official artist sites/newsletters** – kompletterande officiella signaler
- **Bandsintown email** – extra signal, inte geografisk source of truth
- **LLM (OpenAI/Claude)** – används endast för ostrukturerad text

## Principer

1. Vanlig kod för deterministisk logik: Europa-filter, dedupe, databas, datumlogik och API-anrop.
2. AI endast när vanlig parsing inte räcker.
3. PostgreSQL är enda source of truth.
4. Raw source/evidence sparas innan tolkning när möjligt.
5. Varje GitHub issue ska vara en liten, testbar Claude Code-task.

## Börja här

Se GitHub-issuen **[PROJECT] Concert Scout roadmap** och arbeta därefter på exakt en `CS-xxx` issue åt gången.

Claude Code ska också läsa `CLAUDE.md` innan implementation.
