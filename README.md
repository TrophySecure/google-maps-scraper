[Google Maps Scraper](https://apify.com/scrape.badger/google-maps-scraper?fpr=data)

## What does Google Maps Scraper do?

Scrape [Google Maps](https://www.google.com/maps) at scale — search places by keyword and location, fetch full place details (hours, contact, rating breakdown, popular times), list reviews with topic filters, photos, and merchant posts.

## Why use Google Maps Scraper?

- **Five modes, one actor.** Search Places → Get Place Detail → List Reviews / Photos / Posts — the full Google Maps data surface.
- **GPS viewport targeting.** `@lat,lng,zoom` for pinpoint area searches.
- **Business-type filters.** `restaurant`, `hotel`, `coffee_shop`, `gas_station`, `gym` — 4,000+ Google categories.
- **200+ country domains.** Local rankings with `gl` + `hl` targeting.
- **Reviews sort + topic filter.** `newestFirst`, `highestRating`, filter by topic keyword.

## What data can Google Maps Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| title | string | Place name |
| place_id | string | Google Place ID (ChIJ…) |
| data_id | string | Google Maps data_id (0x…:0x…) |
| rating | number | Average star rating |
| reviews | number | Total review count |
| address | string | Formatted street address |
| phone | string | Phone number |
| website | string | Business website |
| gps_coordinates | object | `{lat, lng}` |
| hours | object | Weekly opening hours |
| type | array | Google category slugs |
| photos / reviews / posts | array | In per-mode calls — see the matching micro-actors for batch workflows |

## How to scrape Google Maps

1. Click **Try for free**.
2. Pick a `mode`: `Search Places`, `Get Place Detail`, `List Reviews`, `List Photos`, or `List Posts`.
3. Fill in the required input — `q` for Search Places, `place_id` for the detail / list modes.
4. Optional: set `gl`, `hl`, GPS `ll` viewport, `type` business category.
5. For list modes, set `max_pages` (1-20).
6. Click **Start** — results stream per-place into the dataset.

## How much will it cost?

**$0.003 per page (search / reviews / photos / posts) · $0.005 per Place Detail.** One credit-equivalent per API call. `List Reviews` with `max_pages: 10` is 10 calls = $0.03. `Get Place Detail` is a single richer call.

### Competitor benchmark

| Actor | Author | Price | Notes |
| --- | --- | --- | --- |
| compass/crawler-google-places | Compass | ~$7 / 1k places | Most popular, per-place pricing |
| apify/google-maps-scraper | Apify | ~$9 / 1k places | Official Apify actor |
| lukas_krivka/google-maps-with-contact-details | Lukas Krivka | ~$5 / 1k | Contact-focused |
| **scrape-badger/google-maps-scraper** | **ScrapeBadger** | **$3 / 1k pages** | **Undercuts every major** |

## Input

Configure the run in the **Input** tab above, or pass a JSON object matching the fields below when calling the Actor via the Apify API.

| Field | Required | Description |
| --- | --- | --- |
| mode | ✅ | `Search Places` / `Get Place Detail` / `List Reviews` / `List Photos` / `List Posts`. |
| q | Search only | Search query. |
| place_id | Detail / list modes | Google Place ID (ChIJ…). |
| data_id | — | Alternative to place_id for list modes. |
| ll | — | GPS viewport `@lat,lng,zoom`. |
| gl / hl | — | Country + language. |
| type | — | Business category (Search only). |
| sort_by / topic_id | — | Reviews-only filters. |
| max_pages | — | 1-20 for list modes. |

## Output

Every successful run streams records into the run's dataset. Download as JSON, CSV, XML, Excel, or HTML from the **Dataset** tab; consume programmatically via the Apify API or webhooks.

Example record:

```
{
  "title": "Blue Bottle Coffee",
  "place_id": "ChIJ_3Su08fj5UYRkFfNoiuWQUk",
  "rating": 4.6,
  "reviews": 1284,
  "address": "1 Rockefeller Plaza, New York, NY 10020",
  "phone": "+1 212-555-0198",
  "website": "https://bluebottlecoffee.com",
  "gps_coordinates": {
    "lat": 40.758,
    "lng": -73.978
  },
  "type": [
    "cafe",
    "coffee_shop"
  ]
}
```

## Tips / Advanced options

- **Pipe Search → List Reviews.** Run `Search Places` first, pipe each `place_id` through `google-maps-reviews-scraper` for 100% batch efficiency.
- **GPS viewport beats `q`-based searches for hyperlocal ranking.** Google ranks results differently when you pass `ll` vs. a text-based location in the query.
- **Reviews volume estimate.** Each reviews page ≈ 10 reviews. Budget `max_pages` accordingly.
- **Use micro-actors for single-purpose batch workflows.** `google-maps-reviews-scraper` and `google-maps-photos-scraper` accept many place_ids per run — one Apify job instead of N.

## FAQ, Disclaimers, Support

### What's the difference between `place_id` and `data_id`?

`place_id` starts with `ChIJ…` and is Google's durable place identifier. `data_id` (`0x…:0x…`) is Google Maps' internal ID. Either works for list modes; the actor normalises them.

### Does this include reviews?

Yes — use `mode: List Reviews` or the dedicated `google-maps-reviews-scraper` for batch workflows.

### Can I filter by opening hours?

Google doesn't expose that as a filter; you'll have to post-filter the output's `hours` field.

### What's `ludocid`?

Google's Location Document ID (the numeric ID in `cid=` URL parameters). Alternative to `place_id` for direct-lookup.

### Disclaimer

This Actor scrapes public Google data only. You're responsible for compliance with Google's Terms of Service and any applicable data-protection laws (GDPR, CCPA, etc.) in your jurisdiction. ScrapeBadger does not store the scraped results — they are delivered directly to your Apify dataset.

### Support

Something not working? Open a ticket in the **Issues** tab above — we triage within one business day. Full API reference: [docs.scrapebadger.com](https://docs.scrapebadger.com).

### Related Actors

- [`google-maps-reviews-scraper`](https://apify.com/scrape-badger/google-maps-reviews-scraper) — Reviews-only, batch place_ids
- [`google-maps-photos-scraper`](https://apify.com/scrape-badger/google-maps-photos-scraper) — Photos-only, batch place_ids

### Powered by

[ScrapeBadger](https://scrapebadger.com) — Google-optimised residential proxy pool + browser-farm fallback, 99.7% uptime, unmetered bandwidth. No CAPTCHAs reach you.