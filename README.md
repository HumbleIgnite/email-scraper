[Email Scraper](https://apify.com/c0nst/email-scraper?fpr=data)

# Email Scraper

Extract unique email addresses from a list of websites. The scraper visits each URL, follows internal links, and returns one result per site with all emails found — duplicates removed, known placeholder and schema emails excluded so you only pay for real results.

## What does Email Scraper do?

**Email Scraper** visits the URLs you provide, crawls their internal pages, and extracts every email address found in the raw HTML — including those inside `mailto:` links, plain text, and hidden fields. Results are grouped by site, deduplicated, and stored in a structured dataset you can download as JSON, CSV, or Excel.

Running on [Apify](https://apify.com/) gives you automatic proxy rotation, scheduling, API access, and cloud storage — no infrastructure to manage.

## Why use Email Scraper?

- **Lead generation** — collect contact emails from a list of target company websites
- **Sales prospecting** — find decision-maker emails from directories or partner pages
- **Data enrichment** — augment a list of domains with their publicly listed contact addresses
- **Outreach campaigns** — build verified email lists from niche industry sites
- **Research** — map contact information across a set of websites at scale

## How to use Email Scraper

1. Sign in to [Apify Console](https://console.apify.com) and open the Actor.
2. Paste your target URLs into the **Start URLs** field.
3. Click **Start** and wait for the run to finish.
4. Open the **Output** tab to view and download your results.

## Input

| Field | Type | Description |
| --- | --- | --- |
| `startUrls` | array | URLs to scrape (required) |

Example:

```
{
    "startUrls": [
        { "url": "https://acme.com" },
        { "url": "https://globex.com" },
        { "url": "https://initech.com" }
    ]
}
```

## Output

One dataset row is produced per input URL, containing all unique emails found across every page crawled under that site:

```
[
    {
        "startUrl": "https://acme.com",
        "emails": [
            "sales@acme.com",
            "support@acme.com",
            "ceo@acme.com"
        ],
        "emailCount": 3,
        "pagesScraped": 12,
        "scrapedAt": "2026-04-13T20:00:00.000Z"
    },
    {
        "startUrl": "https://globex.com",
        "emails": [
            "contact@globex.com"
        ],
        "emailCount": 1,
        "pagesScraped": 8,
        "scrapedAt": "2026-04-13T20:00:05.000Z"
    }
]
```

You can download the dataset in various formats such as JSON, HTML, CSV, or Excel from the **Output** tab or via the Apify API.

## Data table

| Field | Format | Description |
| --- | --- | --- |
| `startUrl` | URL | The input URL this result belongs to |
| `emails` | array | Unique, lowercased email addresses found across all crawled pages |
| `emailCount` | number | Total number of unique emails found |
| `pagesScraped` | number | Number of pages that contained at least one email |
| `scrapedAt` | ISO date | Timestamp of when post-processing completed |

## Pricing

This Actor uses **Pay per event** pricing — you are charged per site that returns at least one email. Sites that are crawled but yield no results are free.

| Event | When charged |
| --- | --- |
| `site-scraped` | Once per input URL that produced emails |

Your cost scales with useful output, not with how many pages were crawled. A run over 10 sites where 7 return emails = 7 charges.

## Advanced settings

For most use cases the defaults work well. If you need to fine-tune crawl behaviour, the following settings are available under **Advanced settings** in the Console:

| Field | Default | Description |
| --- | --- | --- |
| `maxDepth` | `1` | How many link-levels deep to follow. `0` = start URL only, `1` = all directly linked pages |
| `maxRequestsPerSite` | `100` | Max pages crawled per site. `0` = unlimited |

**Depth guide:**

- `0` — use when your URLs already point at a contact or about page
- `1` — recommended for most sites; covers Contact, About, Team pages linked from the homepage
- `2` — thorough crawl including blog posts, product pages and sub-sections; runs take longer

## FAQ and disclaimers

**Is this legal?**
Email Scraper only collects data that is publicly visible in the HTML of websites you provide. You are responsible for ensuring your use complies with the target site's Terms of Service, GDPR, CAN-SPAM, and any other applicable laws.

**Why are some emails missing?**
This Actor makes plain HTTP requests without running JavaScript. Emails injected into the page by JS (contact forms, dynamic "mailto" links, obfuscation scripts) won't be captured. If a site's Contact page scrapes clean but returns no emails, this is the likely cause. A future v2 will handle JS-rendered content.

**I'm seeing placeholder or test emails in the results.**
Common false positives (e.g. `user@example.com`, schema.org addresses, image filenames) are filtered out automatically. If you encounter others, open an issue.

**Need a custom solution?**
Open an issue in the repository or contact us for enterprise scraping requirements.