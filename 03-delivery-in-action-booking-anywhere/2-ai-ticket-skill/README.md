# AI skill: from spec to tickets

**Task:** design my own AI skill that creates tickets, describe how it works, and share its output on the spec from homework 2.

| | |
|---|---|
| **The skill** | [SKILL.md](SKILL.md): the actual instructions the AI follows |
| **Its output on "Anywhere"** | [tickets.md](tickets.md): 3 example tickets and the open questions the skill raised |

## The skill: `spec-to-tickets`

**What it does:** turns a functional requirements document into development-ready tickets, grouped into epics, with testable acceptance criteria, sizes and dependencies.

**Built for:** Claude (as a Skill, a reusable instruction file). The same text works as a custom GPT or a saved prompt in other AI tools.

**Input**
- Required: the spec (FRD/PRD) with requirement IDs.
- Optional: the roadmap, so the skill reuses its epics, sizes and order.

**How it works (6 steps)**
1. Reads the whole spec and lists every requirement, business rule, empty/error state and analytics event.
2. Groups them into epics (the roadmap's epics if given).
3. Splits each epic into tickets one developer can finish in about 1–5 days.
4. Writes each ticket with a fixed template.
5. Checks coverage: every source ID must appear in at least one ticket.
6. Lists open questions instead of guessing, and links each one to the tickets it blocks.

**Ticket template**
- Title, type (Story / Task / Spike), size, dependencies, source IDs
- User story (for Stories)
- What to build
- Acceptance criteria (testable "Given / when / then")
- Out of scope

**Rules** (most of them come from my lessons in homework 2, see the [edits log](../../02-design-prototype-booking-anywhere/3-requirements/edits-log.md))
- **Never invent:** anything missing from the spec becomes an open question.
- **Reuse before new:** if the spec reuses an existing component, the ticket says "reuse".
- **Testable acceptance criteria only:** no "fast" or "user-friendly".
- **Respect scope:** out-of-scope items never become tickets.
- **Unknowns become spikes:** a short, time-boxed investigation before the real work.
- **Traceable IDs:** every ticket lists its source; a coverage table proves nothing was missed.

## Output on the "Anywhere" spec

Run on the [6-page FRD](../../02-design-prototype-booking-anywhere/3-requirements/frd.pdf) and the [roadmap](../1-roadmap/), the skill produced **8 epics and 23 tickets**, covering every requirement. [tickets.md](tickets.md) shows 3 examples, one of each type (Spike, Story, Task). The skill also found 3 gaps the spec doesn't answer (photo source, the definition of "popularity", the tag on returning visits).

## What I changed in the output and why

- [add after reviewing tickets.md: e.g. a ticket that was too big, a wrong dependency, an unclear acceptance criterion]
