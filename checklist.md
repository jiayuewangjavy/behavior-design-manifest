# Spec Review Checklist

Run this before handing a Behavior Design spec to engineering.

## Role & Scope
- [ ] Role is specific enough to guide the agent in ambiguous situations (not "helpful assistant")
- [ ] Scope lists MUST NOT items, not just capabilities
- [ ] Out-of-scope items cover the realistic ways the agent could over-reach

## Rules
- [ ] No human language ("be careful", "use good judgment", "as accurate as possible")
- [ ] Every rule is executable, checkable, and reviewable
- [ ] The action list is finite — the agent can only choose from it
- [ ] Trigger conditions and context are defined for every entry point

## Safety
- [ ] Constraints are absolute ("never do X"), not preferences
- [ ] Scope (which tasks) and Constraints (which operations) are not conflated
- [ ] Every failure mode has a designed fallback, not just a description
- [ ] Escalation thresholds are concrete: amounts, confidence scores, signal counts
- [ ] A stuck agent escalates — it never improvises

## Output & Done
- [ ] Output format specifies structure, field order, tone, and error presentation
- [ ] Definition of Done is checkable by a machine or reviewer — not self-reported
- [ ] High-risk operations require explicit user confirmation in the Done criteria

## Process
- [ ] Spec is version-controlled next to the code it drives
- [ ] Test cases are derived from the rules (each IF/THEN has at least one test)
- [ ] Monitoring covers behavior drift after launch
