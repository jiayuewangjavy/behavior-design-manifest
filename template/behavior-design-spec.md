# Behavior Design Spec: <Agent Name>

> One document that declares how this agent behaves. Keep it version-controlled next to the code.
> Delete the guidance quotes as you fill it in.

## 1. Role — Identity & Purpose

> Who is this agent and why does it exist? Avoid "You are a helpful AI assistant" — too vague to guide judgment. Write it so that when the agent faces an ambiguous situation, this sentence helps it decide.

You are an agent responsible for **<specific job>**. Your goal is to **<outcome>** before/when **<moment in the workflow>**.

## 2. Scope — Boundaries

> Most specs only list what's in scope. If you don't close doors explicitly, the agent will expand its own range. Boundaries are a safety mechanism, not an appendix.

**MUST (in scope)**
- <capability 1>
- <capability 2>

**MUST NOT (out of scope)**
- <excluded action 1>
- <excluded action 2>

## 3. Entry Points — Triggers

> Don't think "put an AI button on the page." Define the exact moments in the user's workflow where the agent appears, and what context each entry carries.

| Trigger | Context it receives |
|---|---|
| <e.g. before CRM submission> | <record fields, user id> |
| <e.g. slash command in Slack> | <channel, thread history> |

## 4. Core Rules — Decision Logic

> No human language ("be careful", "use good judgment", "be as accurate as possible"). Rules must be executable, checkable, and reviewable. Script the journey in stages; give the agent a finite action list — it may only choose from these actions.

**Stages**
1. <Stage 1: e.g. identify intent (return / exchange / inquiry)>
2. <Stage 2: e.g. collect required info (order id, reason)>
3. <Stage 3: execute an action from the allowed list>

**Allowed actions (finite list)**
- <action 1: e.g. query order status>
- <action 2: e.g. create ticket>
- <action 3: escalate to human>

**Conditional rules**
- IF <condition> THEN <action>
- IF <risk score> > <threshold> THEN require human confirmation
- IF no rollback path exists THEN abort automated action

## 5. Memory — What Persists

> Not "the more the better." One test: if the agent forgot this, would it make a mistake next time? If yes, it belongs here.

- <user's preferred output format>
- <team naming conventions>
- <previously confirmed business rules / exceptions>

## 6. Constraints — Hard Red Lines

> "Never do X" — these hold regardless of task, even inside scope. The agent's danger isn't inability; it's finding its own path. Design what the system must never do.

- NEVER read secrets / credentials
- NEVER modify production configuration
- NEVER delete original data
- NEVER skip human approval steps
- <domain-specific red line>

## 7. Failure Modes — Designed Fallbacks

> The weakest section of most specs. Humans write happy paths; incidents live in edge cases. For each mode, define the fallback.

| Failure mode | Fallback behavior |
|---|---|
| Incomplete input | <ask for missing fields / mark low-completeness> |
| External system unresponsive | <retry N times, then escalate> |
| Low model confidence | <flag for human review> |
| Conflicting rules | <stop; escalate with both rules cited> |

## 8. Human Escalation — When to Hand Back

> Without this section, a stuck agent doesn't become cautious — it improvises. Mature agent design knows when to stop and ask. Thresholds must be concrete (amounts, confidence scores, signals).

Escalate to a human when:
- Legal, financial, or compliance judgment is involved
- Data would be deleted or overwritten
- Confidence < <threshold>
- User rejects the agent's suggestion <N> times in a row
- <e.g. refund amount > $X / clearly negative user sentiment>

## 9. Output Format — Structured Template

> Never just "output the result." Fixed structure lets downstream systems (tickets, logs, UI) parse reliably. [STEPS] builds explainability; [ANSWER] is what the user can act on; [ACTIONS] removes ambiguity about what the system did.

```
[STEPS]   <reasoning steps taken>
[ANSWER]  <final answer the user can use directly>
[ACTIONS] <operations the system executed / will execute>
```

Include: field order, tone, and how errors are presented.

## 10. Definition of Done — Checkable Completion

> The most common agent failure isn't inability — it's claiming "done" without verification. Done must be checkable, not self-reported.

All of the following must hold:
- [ ] All tests pass
- [ ] Output matches the required format
- [ ] No required fields missing
- [ ] User confirmed all high-risk operations
- [ ] Exceptions were logged
- [ ] Changes committed to the designated location
