# Tickets: "Anywhere" MVP (examples)

*Output of the [`spec-to-tickets`](SKILL.md) skill, run on the [functional requirements](../../02-design-prototype-booking-anywhere/3-requirements/frd.pdf) from homework 2 and the [roadmap](../1-roadmap/).*

The full run produced **8 epics and 23 tickets**, one epic per roadmap feature, with a coverage check showing every requirement became a ticket. Below are **3 examples**, one of each ticket type, plus the open questions the skill raised.

---

## Example 1 · Spike (an unknown is investigated first)

### E1-1 · Spike: check availability for ~350 destinations
Type: Spike   Size: S   Depends on: –
Source: R-1, open question 3

**What to find out**
- Can the availability system check ~350 destinations for one date range and group at once, fast enough for a results page?
- If not, what has to be pre-calculated (e.g. popular date ranges)?

**Acceptance criteria**
- [ ] A short written answer with the measured response time and a recommended approach (live check or pre-calculation).

---

## Example 2 · Story (a new piece of UI)

### E6-2 · Destination overview block
Type: Story   Size: S   Depends on: E2-2, E2-3, E2-4
Source: FR-3.3

As a traveller, I want a quick, factual sense of an unfamiliar place, so that I can decide if it suits me.

**Acceptance criteria**
- [ ] Shows photo, name, up to 3 summary lines, up to 4 tags and "Summary based on Booking.com bookings, property data and guest reviews".
- [ ] Given fewer than 50 reviews, then "Guests often mention" and "Guest rating" are hidden.

**Out of scope**
- Written destination descriptions.

---

## Example 3 · Task (taken straight from the spec's empty and error states)

### E5-5 · Empty, loading and error states (Screen 2)
Type: Task   Size: S   Depends on: E5-1, E5-2
Source: section 7 (rows 1–4)

**What to build**
- Messages inside the results area, no pop-ups: loading placeholders; "No destinations match your filters" with removable filters; "No destinations have availability…" with "Edit dates"; "We couldn't load destinations right now" with "Try again".

**Acceptance criteria**
- [ ] Given filters that remove all destinations, then each selected filter is listed with its own × and nothing is cleared automatically.
- [ ] Given "Edit dates", then the date picker opens with the current dates filled in.

---

## Open questions

| Question | Blocks | Who answers |
|---|---|---|
| Can the availability system check ~350 destinations at once? | E1-1 → all of E1, E3, E5 | Search engineering |
| Does Booking.com group review text by topic in every language? | E2-1 → E2-3, E2-4 | Data / reviews team |
| Should "Anywhere" be pre-selected, or only offered as the first option? | E7-1 | Product |
| Where do the destination photos come from, and who picks them? *(not in the spec)* | E5-1, E6-2 | Product + Design |
| What counts as "popularity" in the default ranking (R-3)? *(not defined in the spec)* | E3-1 | Product + Data |
| Is the "via Anywhere" tag shown again if the user returns to the destination later from history? *(not in the spec)* | E6-1 | Product |
