[Email Scraper](https://apify.com/dominic-quaiser/email-scraper?fpr=data)

# Email Scraper

A powerful Apify Actor designed to crawl websites and extract email addresses using advanced detection methods. Simply provide a list of starting URLs, configure crawling depth and behavior, and the actor will automatically discover and extract email addresses from across the website—even those hidden behind obfuscation or CloudFlare protection.

⚠️ **Pre-Release Version**: This is a release candidate. Features are complete but may contain bugs. Feedback and issue reports are welcome!

## 🚀 Features

- **Intelligent Email Discovery**: Finds email addresses using multiple sophisticated detection methods, including:

- Standard text pattern matching
- Mailto links extraction
- CloudFlare-protected emails
- RTL (Right-to-Left) Unicode obfuscation
- Common text obfuscation patterns
- **Configurable Crawl Depth**: Control how deep the crawler follows links from your starting URLs (0-10 levels).
- **Domain-Focused or Broad Crawling**: Choose to stay on the same domain or explore external links.
- **Lightweight HTTP Crawling**: Fast, efficient method using HTTP requests without the overhead of a browser.
- **Anti-Detection Features**: Built-in measures to avoid blocking, including user agent rotation, request delays, and robots.txt compliance.
- **Proxy Support**: Integrates seamlessly with Apify's proxy service for IP rotation and avoiding rate limits.
- **Structured JSON Output**: Delivers clean, well-structured data with full context about where and how each email was discovered.

## 📥 Input Parameters

Configure the actor's behavior using these fields in the Apify Console Input tab or via API:

| Field | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `start_urls` | Array | The URLs to start crawling from. The scraper will extract emails from these pages and follow links up to the specified depth. | `[{ "url": "https://www.katjes.de/" }]` | Yes |
| `max_depth` | Integer | Maximum depth of links to follow from start URLs. 0 = only start URLs, 1 = start URLs + one level of links, etc. Range: 0-10. | `2` | No |
| `stay_on_domain` | Boolean | Only follow links that stay on the same domain as each start URL. When enabled, the crawler won't visit external sites. | `true` | No |
| `max_concurrent_pages` | Integer | Maximum number of pages to process simultaneously. Leave empty for auto-tuning (recommended: 50). Range: 1-100. | Auto | No |
| `max_pages_per_domain` | Integer | Maximum number of pages to crawl from each individual domain. Leave empty for unlimited. This limit applies separately to each domain. | `200` | No |
| `max_requests_per_run` | Integer | Maximum number of pages to crawl globally across all domains. Leave empty for unlimited. | Unlimited | No |
| `request_delay_min` | Number | Minimum delay in seconds between requests to avoid detection. Recommended: 1-2 seconds. Range: 0-60. | `1` | No |
| `request_delay_max` | Number | Maximum delay in seconds between requests. A random delay between min and max will be used. Range: 0-60. | `3` | No |
| `respect_robots_txt` | Boolean | Honor robots.txt directives including crawl delays and disallowed paths. | `false` | No |
| `rotate_user_agents` | Boolean | Use a pool of realistic user agents to appear as different users. | `true` | No |
| `proxy_configuration` | Object | Proxy settings to avoid being blocked. Apify Proxy is recommended for large crawls. | `{}` | No |

## 📤 Output Data Structure

The actor outputs one record per unique email address found during the crawl.

### Example Output

```
[
  {
    "email": "info@example-company.com",
    "found_on_url": "https://www.example-company.com/contact",
    "start_url": "https://www.example-company.com",
    "extraction_method": "mailto_link",
    "depth": 1
  },
  {
    "email": "support@example-company.com",
    "found_on_url": "https://www.example-company.com/about",
    "start_url": "https://www.example-company.com",
    "extraction_method": "text_standard",
    "depth": 1
  },
  {
    "email": "sales@example-company.com",
    "found_on_url": "https://www.example-company.com/impressum",
    "start_url": "https://www.example-company.com",
    "extraction_method": "cloudflare_protected",
    "depth": 2
  }
]
```

## 📧 Extraction Methods Explained

The actor uses multiple sophisticated techniques to find email addresses, even when websites try to hide them from bots:

| Method | Description |
| --- | --- |
| **`mailto_link`** | Email addresses found in standard `mailto:` links in the HTML. |
| **`text_standard`** | Email addresses found in plain text using standard pattern matching. |
| **`text_obfuscated`** | Email addresses that use common text obfuscation like "info [at] example [dot] com". |
| **`cloudflare_protected`** | Email addresses protected by CloudFlare's email obfuscation that are decoded from the page. |
| **`rtl_obfuscated`** | Email addresses hidden using Right-to-Left (RTL) Unicode characters to confuse simple scrapers. |

### 💡 Performance Tips

- **For small sites**: Keep the default settings for optimal speed.
- **For large crawls**: Use proxy rotation to avoid blocking and rate limits.
- **Memory constraints**: Set `max_concurrent_pages` to a lower value (2-5) if running on limited memory.
- **Faster crawling**: Increase `max_concurrent_pages` if you have sufficient resources.

## 🎯 Use Cases

- **Lead Generation**: Build targeted contact lists for sales and marketing outreach.
- **Competitive Research**: Discover contact information for companies in your industry.
- **Data Enrichment**: Enhance existing company databases with email addresses.
- **Market Analysis**: Gather communication channels for businesses in specific sectors or regions.
- **Recruitment**: Find contact emails for potential candidates or hiring managers.
- **Partnership Development**: Identify contact points for potential business partnerships.

## 🛠️ Maintainer

- **Author**: Dominic M. Quaiser
- **Contact**: [mail@dominic-quaiser.io](mailto:mail@dominic-quaiser.io)
- **Website**: [dominic-quaiser.io](https://dominic-quaiser.io/)

---

## 🔧 Troubleshooting

### No Emails Found

- Check if the website contains any publicly visible emails
- Try increasing `max_depth` to crawl more pages
- Verify that `stay_on_domain` isn't preventing you from reaching contact pages on subdomains
- Check if the website might be blocking the scraper (try enabling proxies)

### Actor Running Out of Memory

- Decrease `max_concurrent_pages` to process fewer pages simultaneously
- Use `max_requests_per_run` to limit the total crawl size
- Upgrade to a larger memory tier on Apify

### Getting Blocked by Websites

- Enable proxy rotation via `proxy_configuration`
- Increase `request_delay_min` and `request_delay_max`
- Enable `rotate_user_agents` and `use_stealth_mode`
- Consider enabling `respect_robots_txt` to honor crawl delays