# Clickable prototype: "Anywhere"

** [Open the clickable prototype](https://yufokina.github.io/product-manager-portfolio/02-design-prototype-booking-anywhere/2-prototype/)** (the file itself: [index.html](index.html))

**Built with:** Claude

## Flows

| # | Flow | Steps |
|---|---|---|
| 1 | **Search without a destination** | Home > "Where are you going?" > "Anywhere" > dates & guests > Search |
| 2 | **Compare destinations** | Destination results > filter by budget / property type / popular filters → sort > open a destination |
| 3 | **Explore stays and hand off to booking** | Destination page ("via Anywhere" tag, data-based summary) > standard filters > "See availability" |

> Concept prototype for a learning exercise, not affiliated with Booking.com. Hotel names, prices and counts are invented.

## Prompt I used

```
As a Senior UX/UI Designer and Frontend Developer with experience in travel products and booking platforms.
**Context**:
I am working on a Product Management case study for Booking.com as part of the Product Academy.
The feature is called "Anywhere" - a date-led destination discovery experience that helps travellers discover destinations based on their travel dates and group size, without having to select a destination first.
I will provide a Functional Requirements Document containing the product scope, user stories, functional requirements, business rules, and acceptance criteria.
**Task**:
Create a clickable desktop prototype based on the attached FRD.

The prototype should demonstrate the following three screens:
1. Anywhere Search
- Destination field with "Anywhere" as the first option.
- Fixed check-in and check-out dates.
- Guest and room selection.
- Search validation.
2. Destination Results
- Destination cards with images, country, availability, average nightly price and total stay price.
- Sorting by Best Match, Lowest Price and Most Stays.
- Filters for budget, property type and popular preferences.
- Ability to show more destinations.
3. Explore Stays
- Destination overview with image, summary and tags.
- Breadcrumb navigation and "Back to all destinations".
- Property cards with ratings and total prices.
- Existing booking journey entry point.

**Interaction requirements**:
- Make navigation between all three screens clickable.
- Preserve dates, guests and selected filters when navigating.
- Simulate property selection and preserve the src=anywhere attribution.
- Make the prototype usable in a desktop browser.

**Design requirements**:
- Use Booking.com's visual language and design patterns.
- Use sample destinations, property data and illustrative prices where real data is unavailable.

**Technical requirements**:
- Deliver a standalone HTML prototype.
- Use HTML, CSS and JavaScript.
- Avoid requiring a backend or database.
- Make the prototype easy to publish using GitHub Pages.

**Important**:
Use the attached FRD as the primary source of truth. Do not introduce features outside the defined MVP scope. 
```
