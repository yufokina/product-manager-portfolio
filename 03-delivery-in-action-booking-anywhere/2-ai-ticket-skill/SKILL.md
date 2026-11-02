---
name: spec-to-tickets
description: Turn a product spec (FRD/PRD) into development-ready tickets grouped into epics, with testable acceptance criteria, sizes, dependencies and a coverage check. Use when someone asks to create, draft or split tickets from a spec or requirements document.
---

# Spec to tickets

Turn a functional requirements document into tickets a development team can pick up without a walkthrough.

## Input

- **Required:** the spec (FRD/PRD). Requirements should have IDs (e.g. FR-2.1, R-3). If they don't, number them yourself and say so.
- **Optional:** a roadmap with epics, T-shirt sizes and dependencies. If given, use its epics and order.

If the spec is missing, ask for it. Don't start from memory or assumptions.

## Steps

1. **Read the whole spec** and list every requirement (FR-…), business rule (R-…), empty/error state and analytics event. Note what is in and out of scope.
2. **Group into epics.** Use the roadmap epics if provided. Otherwise group by deliverable chunks a team can build and test on their own (back-end data first, then screens, then entry point and tracking).
3. **Split each epic into tickets.** One ticket = one developer can finish and test it in about 1–5 days. Split by screen element, rule or state, not by technical layer only.
4. **Write each ticket** with the template below.
5. **Check coverage.** Every requirement, rule, state and event must appear in at least one ticket. Show a coverage table. Anything not covered is listed as a gap.
6. **List open questions:** everything the spec doesn't answer and the developer would need to decide. Include the spec's own open questions and link them to the tickets they block.

## Ticket template

```
### [EPIC-ID]-[n] · Title (verb + object, max ~8 words)
Type: Story | Task | Spike        Size: XS | S | M | L        Depends on: …
Source: FR-… / R-… / section …

As a … I want … so that …   (Stories only)

What to build
- 2–5 bullets. Concrete, no implementation details the spec doesn't give.

Acceptance criteria
- [ ] Given … when … then …   (each one testable by QA, taken from the spec's "How we check it" where possible)

Out of scope
- what this ticket must NOT do (taken from the spec's out-of-scope list where relevant)
```

## Rules

- **Never invent.** Every behaviour, number, label and text must come from the spec. If something is missing, add an open question instead of guessing.
- **Reuse before new.** If the spec says an existing component or flow is reused, the ticket says "reuse"; don't create tickets for redesigning it.
- **Testable acceptance criteria only.** No "works well", "fast", "user-friendly". Use numbers and observable results from the spec.
- **Respect scope.** Out-of-scope items never become tickets.
- **Unknowns become spikes.** If a ticket depends on an open technical question, create a short Spike ticket first (time-boxed, with a clear question to answer).
- **Keep IDs traceable.** Every ticket lists its source IDs; every source ID appears in the coverage table.
- **Plain language.** Short sentences; a new developer should understand each ticket on its own.

## Output format

1. Summary: number of epics and tickets, and the suggested build order.
2. Epics, each with its tickets (template above).
3. Coverage table: source ID → ticket(s).
4. Open questions: question → which ticket it blocks → who should answer.
