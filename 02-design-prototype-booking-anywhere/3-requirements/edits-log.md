# FRD: AI first draft vs. my edits

**AI tool used:** Claude (Anthropic)
**Prompt:** [paste or summarise the prompt]

The first AI draft was a 16-page FRD. Below is what I changed while reviewing it, and why. The result is the [6-page FRD](frd.pdf).

## What I changed and why

| # | What the AI draft had | What I changed | Why |
|---|---|---|---|
| 1 | Destination overview with a written description ("Sunny beaches, a historic old town…"), assuming a content team would write it | Summary built only from existing data: what guests mention in reviews, most booked areas, guest rating, plus rule-based tags (R-4, R-5) | Booking.com has no written content about cities. Writing it for ~350 destinations in every language is a hidden cost bigger than the UI, and AI-written text risks invented claims |
| 2 | A new "Neighbourhood" filter on Screen 3 | Screen 3 uses Booking.com's standard filter panel, unchanged (FR-3.5) | A custom panel costs more to build and test, and users expect the filters they know |
| 3 | A "Popular nearby" line in the destination overview | Removed | Not needed to decide on a destination; one less data dependency |
| 4 | A "Mild weather" theme tag | Removed (replaced by "Family-friendly", based on family rooms) | Booking.com has no weather data of its own; every tag must come from existing data |
| 5 | A "What are you in the mood for?" theme filter in the prototype | Removed; tags are for display only | Booking.com has no theme filters. A new filter is extra scope the MVP doesn't need |
| 6 | Screen 3 with "Why it fits your trip" and "Similar for your dates" blocks | Removed from the MVP, moved to the future-vision moodboard | Keep the MVP focused; both are closer to personalisation, which was cut |
| 7 | A 16-page FRD with an API sketch, caching rules, glossary and a traceability matrix | Shortened to 6 pages: requirements with a one-line check each, business rules, empty and error states, analytics | Easier to read and review; technical design such as APIs belongs to engineering |
| 8 | Feature shown only to a test group (A/B test with a control group) | Released to all users at once; success measured by bookings through "Anywhere" plus a before/after check | Avoids extra work for the dev team. Trade-off: we can't prove the bookings are incremental |
| 9 | Destinations shown only with at least 3 available stays | Shown with at least 1 available stay (FR-2.1) | The "3" was arbitrary and hid real, bookable options; one house that fits a family is enough |
| 10 | Empty states with "Clear all filters" | Filters are never cleared automatically; selected filters are listed and removed one at a time; "Edit dates" keeps the current dates | Users shouldn't lose or forget what they selected |

## What I learned

- [e.g. AI is fast at structure and coverage, but invents details the product doesn't have (city descriptions, weather data). Every claim needs a data source.]
