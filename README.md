# Behavior Design Toolkit

A practical toolkit for designing AI agents with **Behavior Design specs** — instead of PRDs and screen mockups.

From the talk **"The Full-Stack Era of AI Product Designers"** (PM-Summit 2026) by Javy Wang.

## Why this exists

The most successful AI products are the ones users don't notice. Adoption is driven by friction, not features. That changes what designers and PMs produce:

- **Old workflow:** requirements doc → prototype → UI spec → code (information lost at every handoff)
- **New workflow:** Behavior Design spec → agent design → test cases → code → monitoring

A Behavior Design spec declares — in one version-controlled, testable document — how an agent behaves: what it is, what it must never do, when it escalates to a human, and what "done" means.

## 5-minute quickstart

1. Pick one user request and copy the [spec template](template/behavior-design-spec.md).
2. Write three rules: what the agent can do now, when it must ask, and what it must never do. For example: “Draft a shipping update; ask before sending; never change the order.”
3. Define what counts as done. “Draft is ready for review” and “Message sent with a receipt” are two different outcomes.
4. Test two paths: a routine request the agent can handle and a boundary case where it should stop. Then use the [review checklist](checklist.md) to fill out the rest of the spec.

## What's inside

| Path | What it is |
|---|---|
| `template/behavior-design-spec.md` | The 10-element spec template, ready to fill in |
| `examples/sales-lead-agent.md` | Example: a sales-lead completeness checker |
| `examples/customer-service-agent.md` | Example: a customer-service agent with staged rules |
| `checklist.md` | Definition-of-Done review checklist |

## The 10 elements

1. **Role** — identity & purpose; the agent's highest-order instruction
2. **Scope** — MUST / MUST NOT boundaries of responsibility
3. **Entry Points** — when it's triggered, and with what context
4. **Core Rules** — decision logic as a finite action list (prevents hallucination)
5. **Memory** — what persists across turns (test: would forgetting cause a mistake?)
6. **Constraints** — hard "never do X" red lines, regardless of task
7. **Failure Modes** — designed fallbacks for edge cases, not just the happy path
8. **Human Escalation** — concrete thresholds for handing back to a human
9. **Output Format** — strict structured template ([STEPS] / [ANSWER] / [ACTIONS])
10. **Definition of Done** — checkable completion criteria, not self-reported success

> Scope vs. Constraints: Scope limits *which tasks* the agent takes on; Constraints limit *which operations* are forbidden even inside scope. One is a door, the other is a lock.

## How to use

1. Copy `template/behavior-design-spec.md` into your project.
2. Fill in the 10 sections for one feature of your product. Start small — even just Role, Core Rules, Escalation and Output Format says more than a prototype.
3. Review with the `checklist.md` before handing to engineering.
4. Version-control the spec next to the code it drives. Iterate on it like source.

## License

MIT — use freely, attribution appreciated.
