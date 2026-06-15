[Email Scraper](https://apify.com/ib4ngz/email-scraper?fpr=data)

This actor scrapes email addresses from a list of provided URLs. It recursively crawls pages, extracts unique email addresses, and stores them in a dataset. The actor supports DNS validation to ensure domain authenticity and allows filtering based on custom crawling depth. Only unique email addresses are saved, preventing duplicates during the scraping process.

## Features

- **Email Extraction**: Extracts email addresses from a list of provided URLs and recursively explores linked pages to gather additional emails.
- **Recursive Crawling**: Crawls web pages to a user-defined maximum depth, enabling thorough exploration while managing resource usage.
- **DNS Validation**: Validates email domains using DNS records to ensure authenticity and exclude invalid domains.
- **Unique Dataset**: Ensures only unique email addresses are saved by preventing duplicates during the crawling process.

## Input Schema

- **Start URLs** (required): A list of URLs to start crawling from.
- **Maximum Depth**: The maximum depth for crawling, defining how deep the crawler should explore.
- **DNS Lookup**: Option to enable or disable DNS validation for email domains.
- **Proxy Configuration**: Configuration settings for selecting and using proxies during crawling.
- **Minimum Concurrency**: The minimum number of concurrent requests or pages to process.
- **Maximum Concurrency**: The maximum number of concurrent requests or pages to process.

## Dataset Schema

- **email**: The extracted email address.
- **dnsLookup**: Indicates whether the email domain passed DNS validation.

## How to Use

1. **Set up the Actor**

Start by providing a list of URLs to begin the crawling process. You can either manually input the URLs or provide a list in the actor configuration.
2. **Configure the Input Parameters**

- **Start URLs**: Provide the initial URLs from which the crawler will start.
- **Maximum Depth**: Define how deep the crawler should explore.
- **DNS Lookup**: Choose whether to validate email domains using DNS records.
- **Proxy Configuration**: If necessary, configure the proxy settings for your crawler.
- **Concurrency**: Adjust the minimum and maximum concurrency based on your needs.
3. **Run the Actor**

Once the input parameters are configured, run the actor to start the crawling process. The actor will crawl the pages, extract unique email addresses, and store the results in the dataset.
4. **View Results**

After the actor finishes running, you can view the extracted email addresses in the dataset. The data will be displayed in a table format with the following fields:

- Email Address
- DNS Lookup Status
5. **Export Data**

You can export the dataset for further processing or analysis. The results are saved in a structured format for easy integration with other tools.
6. **Modify Parameters**

Adjust the configuration and rerun the actor as needed to gather additional data or refine the crawling process.

## Conclusion

This actor provides an efficient solution for scraping and extracting unique email addresses from a list of URLs. It recursively crawls the provided pages, extracts emails, and stores them in a dataset. By respecting a defined maximum depth and supporting DNS validation, it ensures only authentic and relevant emails are captured.

The actor is optimized to prevent duplicates by saving only unique email addresses during the crawling process. This makes it a valuable tool for anyone looking to gather email data in a structured and efficient manner, while maintaining control over the types of emails collected.