[Google Maps Scraper](https://apify.com/lulzasaur/google-maps-scraper?fpr=data)

Extract business leads from Google Maps including emails, phone numbers, addresses, ratings, opening hours, and reviews.

## Key Features

- **Email extraction** — Automatically crawls business websites to find contact emails
- **Full business data** — Name, address, phone, website, rating, reviews, category, coordinates
- **Multiple queries** — Run multiple search queries in a single run
- **Review scraping** — Optionally extract review text and ratings
- **Smart caching** — Avoids re-crawling the same business website domains

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| searchQueries | string[] | ["plumbers in Denver, CO"] | Google Maps search queries |
| maxResults | integer | 100 | Max businesses per query (0 = unlimited) |
| scrapeEmails | boolean | true | Crawl websites for emails |
| scrapeReviews | boolean | false | Extract review text |
| maxReviews | integer | 5 | Reviews per business (1-50) |
| language | string | "en" | Maps interface language |
| proxyConfiguration | object | Residential | Proxy settings (residential required) |

## Output

Each result contains:

```
{
    "businessName": "Denver Plumbing Co",
    "placeId": "ChIJ...",
    "address": "123 Main St, Denver, CO 80202",
    "phone": "+1 303-555-0100",
    "website": "https://denverplumbing.com",
    "emails": ["info@denverplumbing.com", "jobs@denverplumbing.com"],
    "rating": 4.7,
    "reviewCount": 234,
    "category": "Plumber",
    "priceLevel": "$$",
    "latitude": 39.7392,
    "longitude": -104.9903,
    "openingHours": {"Monday": "8 AM–6 PM", "Tuesday": "8 AM–6 PM"},
    "plusCode": "QRVW+XY Denver, CO",
    "reviews": [{"author": "John", "rating": 5, "text": "Great service!", "time": "2 months ago"}],
    "searchQuery": "plumbers in Denver, CO",
    "scrapedAt": "2026-04-20T12:00:00.000Z"
}
```

## Usage Tips

- Use specific location queries for best results (e.g., "dentists in Austin, TX" not just "dentists")
- Email extraction adds ~1-2 seconds per business but provides high-value lead data
- Set `maxResults` to control run time and cost
- Residential proxies are required — Google blocks datacenter IPs

## Proxy

This scraper requires **residential proxies**. The default configuration uses Apify's RESIDENTIAL proxy group. Google Maps will block requests from datacenter IPs.

## Cost

Pricing: $0.005 per result (Pay Per Event). A typical run of 100 businesses costs ~$0.50.

Memory recommendation: 4096 MB for optimal performance with Playwright browser.