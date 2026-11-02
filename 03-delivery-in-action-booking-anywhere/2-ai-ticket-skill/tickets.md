# Tickets: "Anywhere" MVP

*Output of the [`spec-to-tickets`](SKILL.md) skill, run on the [functional requirements](../../02-design-prototype-booking-anywhere/3-requirements/frd.pdf) from homework 2 and the [roadmap](../1-roadmap/).*

## Summary

**8 epics, 23 tickets** (2 of them spikes). Build order follows the roadmap: data and tracking first (E1–E4), then screens (E5–E6), then the entry point and analytics (E7), and the optional map last (E8).

| Epic | Name | Tickets | Roadmap size |
|---|---|---|---|
| E1 | Destination availability & price engine | 3 | XL |
| E2 | Destination summary & tags job | 4 | L |
| E3 | Ranking & sorting | 2 | M |
| E4 | Source tracking to booking | 2 | M |
| E5 | Screen 2: destination results | 5 | L |
| E6 | Screen 3: destination stays | 3 | M |
| E7 | Screen 1 entry + analytics | 3 | S |
| E8 | Map view (optional) | 1 | M |

---

## E1 · Destination availability & price engine

### E1-1 · Spike: check availability for ~350 destinations
Type: Spike   Size: S   Depends on: –
Source: R-1, open question 3

**What to find out**
- Can the availability system check ~350 destinations for one date range and group at once, fast enough for a results page?
- If not, what has to be pre-calculated (e.g. popular date ranges)?

**Acceptance criteria**
- [ ] A short written answer with the measured response time and a recommended approach (live check or pre-calculation).

### E1-2 · Count available stays per destination
Type: Task   Size: L   Depends on: E1-1
Source: R-1, FR-2.1

**What to build**
- For each destination, count properties with at least one room offer bookable for the exact dates that fits all guests.
- Return only destinations with at least 1 available stay.

**Acceptance criteria**
- [ ] Given 2 adults + 2 children, when the count runs, then properties that can't fit 4 guests are not counted.
- [ ] Given a destination with 0 available stays, then it is not returned.

**Out of scope**
- Flexible dates; mobile.

### E1-3 · Calculate destination price
Type: Task   Size: M   Depends on: E1-2
Source: R-2, FR-2.2

**What to build**
- For each available stay, take its cheapest offer for the whole stay, including taxes.
- Destination total = average of these; per night = total ÷ number of nights.

**Acceptance criteria**
- [ ] Given a 7-night search, then per night × 7 = total (rounded to whole currency units).
- [ ] Given a budget filter, then only stays within the budget are used in the average.

---

## E2 · Destination summary & tags job

### E2-1 · Spike: review topics in every language
Type: Spike   Size: S   Depends on: –
Source: R-4, R-5, open question 2

**What to find out**
- Does Booking.com already group review text by topic (food, beach, …) in every language?

**Acceptance criteria**
- [ ] A written answer: available / partly available (which languages) / not available, with a recommendation.

### E2-2 · Nightly job: guest rating and most booked areas
Type: Task   Size: M   Depends on: –
Source: R-4

**What to build**
- Nightly, for each destination: average guest rating and review count; top 3 districts by bookings.

**Acceptance criteria**
- [ ] Given fewer than 50 reviews, then no guest rating is stored for that destination.
- [ ] The job runs every night and stores the result per destination.

### E2-3 · Nightly job: "guests often mention"
Type: Task   Size: M   Depends on: E2-1
Source: R-4

**What to build**
- Nightly, for each destination: top 3 topics in reviews, filled into a fixed sentence template.

**Acceptance criteria**
- [ ] Given fewer than 50 reviews, then the line is not generated.
- [ ] The text uses only the fixed template; no free or AI-generated text.

### E2-4 · Rule-based tags
Type: Task   Size: S   Depends on: E2-2, E2-3
Source: R-5

**What to build**
- Calculate tags from simple rules, e.g. Beaches (≥ 20% of stays near a beach), Great food (food in ≥ 15% of reviews), Family-friendly (≥ 25% of stays with family rooms). Max 4 per destination.

**Acceptance criteria**
- [ ] Given a destination meeting 6 rules, then only 4 tags are stored.
- [ ] No weather-based tags exist.

**Out of scope**
- Using tags as filters.

---

## E3 · Ranking & sorting

### E3-1 · Default ranking "Top picks…"
Type: Task   Size: S   Depends on: E1-2, E1-3
Source: R-3, FR-2.3

**What to build**
- Score each destination: availability 40%, price 30%, popularity 30%. Weights adjustable without a release.

**Acceptance criteria**
- [ ] Given two destinations equal on price and popularity, then the one with more stays ranks higher.
- [ ] No personal data is used in the score.

### E3-2 · Sort options for destinations
Type: Story   Size: S   Depends on: E3-1
Source: FR-2.3

As a traveller, I want to sort destinations by price or reviews, so that I can compare them my way.

**What to build**
- Options with Booking.com's labels: default (same label as Booking.com's default for the trip length, e.g. "Top picks for long stays"), Price (lowest first), Price (highest first), Top reviewed, Best reviewed & lowest price.

**Acceptance criteria**
- [ ] Given "Price (lowest first)", then the cheapest destination is first.
- [ ] No property-level options (stars, distance from downtown, property type, traveller groups) are shown.

---

## E4 · Source tracking to booking

### E4-1 · Carry `src=anywhere` to the booking
Type: Task   Size: S   Depends on: –
Source: R-6, FR-2.7, FR-3.6

**What to build**
- Add `src=anywhere` when moving from Screen 2 to Screen 3 and keep it through the property page and checkout.

**Acceptance criteria**
- [ ] Given a user who opens a property from Screen 3, then `src=anywhere` is still present at checkout.
- [ ] Given a user who switches to a normal city search, then the tag is removed.

### E4-2 · Save the source on the booking
Type: Task   Size: M   Depends on: E4-1 · *needs the booking team*
Source: R-6, section 8

**What to build**
- Store source "anywhere" on the booking record and add it to the existing `booking_completed` and `booking_cancelled` events.

**Acceptance criteria**
- [ ] Given a booking made via Anywhere, then the booking record has source "anywhere".

**Out of scope**
- Any other change to the property page or checkout.

---

## E5 · Screen 2: destination results

### E5-1 · Destination card and list
Type: Story   Size: M   Depends on: E1-3, E2-2, E2-4
Source: FR-2.1, FR-2.2

As a traveller, I want to see destinations that fit my dates, group and budget, so that I know where I could go.

**What to build**
- Card: photo, name and country, short data summary, up to 4 tags, "{n} stays available", average price per night, total price, "Explore stays".

**Acceptance criteria**
- [ ] Given a 7-night search, then each card's total = average per night × 7.
- [ ] Given a summary line without enough data, then it is hidden.

### E5-2 · Filters on Screen 2
Type: Story   Size: M   Depends on: E5-1
Source: FR-2.4

**What to build**
- Budget per night, property type, popular filters (e.g. free cancellation, pool). List and URL update without a page reload.

**Acceptance criteria**
- [ ] Given budget max €80, then stay counts include only stays up to €80 per night.
- [ ] Given a refresh, then the same filters are still applied.

### E5-3 · "Show more" and URL state
Type: Task   Size: S   Depends on: E5-1
Source: FR-2.5, FR-1.3

**Acceptance criteria**
- [ ] Given 20 cards, when "Show more" is clicked, then 40 cards are shown and the scroll position is kept.
- [ ] Given a shared link, then the same results open.

### E5-4 · Open a destination
Type: Task   Size: XS   Depends on: E5-1, E4-1
Source: FR-2.7

**Acceptance criteria**
- [ ] Given filters on Screen 2, when a card is clicked, then Screen 3 opens with the same dates, guests and filters, and `src=anywhere`.

### E5-5 · Empty, loading and error states (Screen 2)
Type: Task   Size: S   Depends on: E5-1, E5-2
Source: section 7 (rows 1–4)

**What to build**
- Messages inside the results area, no pop-ups: loading placeholders; "No destinations match your filters" with removable filters; "No destinations have availability…" with "Edit dates"; "We couldn't load destinations right now" with "Try again".

**Acceptance criteria**
- [ ] Given filters that remove all destinations, then each selected filter is listed with its own × and nothing is cleared automatically.
- [ ] Given "Edit dates", then the date picker opens with the current dates filled in.

---

## E6 · Screen 3: destination stays

### E6-1 · Anywhere context on the results page
Type: Story   Size: S   Depends on: E5-4
Source: FR-3.1, FR-3.2, FR-3.4

**What to build**
- Reuse the existing search results page. Add the "via Anywhere" tag in the search bar, the breadcrumb Home › Explore anywhere › Results › {Destination}, and "Back to all destinations".

**Acceptance criteria**
- [ ] Given guests changed to 4, then the same destination reloads and the tag is still shown.
- [ ] Given card 30 was opened, when "Back to all destinations" is clicked, then Screen 2 shows card 30 with the same filters.

### E6-2 · Destination overview block
Type: Story   Size: S   Depends on: E2-2, E2-3, E2-4
Source: FR-3.3

As a traveller, I want a quick, factual sense of an unfamiliar place, so that I can decide if it suits me.

**Acceptance criteria**
- [ ] Shows photo, name, up to 3 summary lines, up to 4 tags and "Summary based on Booking.com bookings, property data and guest reviews".
- [ ] Given fewer than 50 reviews, then "Guests often mention" and "Guest rating" are hidden.

**Out of scope**
- Written destination descriptions.

### E6-3 · Standard filters, sorting and property cards
Type: Task   Size: S   Depends on: E6-1, E4-1
Source: FR-3.5, FR-3.6, section 7 (rows 5–6)

**What to build**
- Reuse Booking.com's standard filter panel, sorting and property cards, unchanged. Pre-apply filters from Screen 2. Show only stays that fit the whole group, with the total price. Add the "just sold out" notice.

**Acceptance criteria**
- [ ] Given budget €150 + Apartments on Screen 2, then both are pre-selected and all standard filters are available.
- [ ] Given the destination sold out since Screen 2, then the notice "Stays in {Destination} just sold out for these dates" is shown with "Back to all destinations".

**Out of scope**
- New filters or sort options on Screen 3.

---

## E7 · Screen 1 entry + analytics

### E7-1 · "Anywhere" option in the search box
Type: Story   Size: S   Depends on: E5-1, E6-1
Source: FR-1.1, FR-1.2, FR-1.3

As a traveller, I want to search without choosing a place, so that I can see where I could go.

**Acceptance criteria**
- [ ] Given an empty destination field, when it's clicked, then "Anywhere" is the first option.
- [ ] Given no dates, when Search is clicked, then the date picker opens and no results are loaded.

### E7-2 · Analytics events
Type: Task   Size: S   Depends on: E5-1, E6-1, E7-1
Source: section 8

**What to build**
- Events `anywhere_selected`, `anywhere_search_submitted`, `destination_results_viewed`, `explore_stays_clicked`, `property_opened`, each with user and session.

**Acceptance criteria**
- [ ] Given one full flow from Screen 1 to a property, then all 5 events are recorded once, in order.

### E7-3 · Launch report: main metric and before/after
Type: Task   Size: S   Depends on: E4-2, E7-2
Source: section 8

**What to build**
- Weekly report: completed (not cancelled) bookings with source "anywhere"; total bookings and search-to-booking conversion 4 weeks before vs. after launch, plus the same period last year; guardrails (normal search conversion, cancellation rate).

**Acceptance criteria**
- [ ] The "before" baseline is recorded before launch.
- [ ] The report shows all four numbers for each week after launch.

---

## E8 · Map view (optional, *Should*)

### E8-1 · Map with destination pins
Type: Story   Size: M   Depends on: E1-3, E5-1
Source: FR-2.6

**Acceptance criteria**
- [ ] Each destination is a pin with its average price per night.
- [ ] Clicking a pin opens the same destination as its card.

---

## Coverage

| Source | Ticket(s) |
|---|---|
| FR-1.1, FR-1.2 | E7-1 |
| FR-1.3 | E7-1, E5-3 |
| FR-2.1 | E1-2, E5-1 |
| FR-2.2 | E1-3, E5-1 |
| FR-2.3 | E3-1, E3-2 |
| FR-2.4 | E5-2 |
| FR-2.5 | E5-3 |
| FR-2.6 | E8-1 |
| FR-2.7 | E4-1, E5-4 |
| FR-3.1, FR-3.2, FR-3.4 | E6-1 |
| FR-3.3 | E6-2 |
| FR-3.5 | E6-3 |
| FR-3.6 | E6-3, E4-1 |
| R-1 | E1-2 |
| R-2 | E1-3 |
| R-3 | E3-1 |
| R-4 | E2-2, E2-3 |
| R-5 | E2-4 |
| R-6 | E4-1, E4-2 |
| Section 7, rows 1–4 | E5-5 |
| Section 7, rows 5–6 | E6-3 |
| Section 8, events | E7-2, E4-2 |
| Section 8, metric and before/after | E7-3 |

All requirements, rules, states and events are covered.

## Open questions

| Question | Blocks | Who answers |
|---|---|---|
| Can the availability system check ~350 destinations at once? | E1-1 → all of E1, E3, E5 | Search engineering |
| Does Booking.com group review text by topic in every language? | E2-1 → E2-3, E2-4 | Data / reviews team |
| Should "Anywhere" be pre-selected, or only offered as the first option? | E7-1 | Product |
| Where do the destination photos come from, and who picks them? *(not in the spec)* | E5-1, E6-2 | Product + Design |
| What counts as "popularity" in the default ranking (R-3)? *(not defined in the spec)* | E3-1 | Product + Data |
| Is the "via Anywhere" tag shown again if the user returns to the destination later from history? *(not in the spec)* | E6-1 | Product |
