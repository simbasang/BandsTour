# Concert Scout – project plan

## Goal

Monitor selected artists and notify when concerts or tour announcements relevant to Europe are discovered.

## Data flow

```text
Ticketmaster API --------------------┐
Official artist tour pages ----------|
Official newsletters ----------------|--> Raw signals / canonical events
Bandsintown email -------------------┘              |
                                                    v
                                           Parse / LLM when needed
                                                    |
                                                    v
                                          Normalize + deduplicate
                                                    |
                                                    v
                                             Europe filter
                                                    |
                                                    v
                                                Postgres
                                                    |
                                                    v
                                             Notifications
```

## Release sequence

### v0.1 – Core scanner without AI
CS-001 through CS-013.

Result: artists can be stored, resolved against Ticketmaster, scanned for upcoming events, filtered to Europe and persisted without duplicates.

### v0.2 – Automated daily notifications
CS-014 through CS-016.

Result: n8n runs a daily scan and sends one digest only for previously unnotified events.

### v0.3 – Email intelligence
CS-017 through CS-022.

Result: newsletters and Bandsintown emails can be ingested as raw evidence and interpreted using a validated LLM extraction layer.

### v0.4 – Additional official sources and onboarding
CS-023 through CS-029.

Result: official tour pages can be monitored and artist onboarding can track source discovery/review.

### v0.5 – UI and operations
CS-030 through CS-033.

Result: basic admin UI, collector health, deployment and backup documentation.

## Scope deliberately excluded from early versions

Do not add these until a later issue explicitly asks for them:
- autonomous/multi-agent architecture
- vector database / RAG
- Kafka or event streaming infrastructure
- Kubernetes
- advanced crawler platform
- fuzzy cross-source event matching beyond the defined task
- advanced UI

## Guiding rule

The GitHub issue is the unit of work. Claude Code should be given one issue number, complete it, verify it, and stop.
