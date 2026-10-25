---
layout: page
title: Hepsiemlak Web Scraping
description: A Python Scrapy crawler for extracting structured apartment listing data from a Turkish real-estate platform
img: assets/img/hepsiemlak.jpg
importance: 3
category: work
related_publications: false
---

This Python project uses **Scrapy** to crawl apartment listings from [Hepsiemlak](https://www.hepsiemlak.com/), a Turkish real-estate platform, and extract structured property information for analysis and data collection.

The scraper starts from Istanbul apartment sale listings, navigates through paginated results, follows individual advertisement links, and collects property attributes from each listing.

## Extracted Property Information

The spider extracts a range of real-estate attributes, including:

- **Listing details:** Title, price, and listing URL.
- **Property characteristics:** Room count, gross and net area, floor, building age, and total number of floors.
- **Interior features:** Heating type, furnishing status, and bathroom count.
- **Property status:** Usage status and title deed status.
- **Location:** District and neighborhood.

The extracted information is stored as structured Python dictionaries, making it suitable for exporting to JSON, CSV, or XML for subsequent processing.

## Scraping Logic & Workflow

The `apartmentspider.py` spider implements the crawling workflow using Scrapy's request and response handling.

1. **Initial Request:** Starts from the Istanbul apartment sale listings page.
2. **Pagination:** Navigates through listing result pages to discover additional advertisements.
3. **Link Extraction:** Identifies individual property listing URLs on each results page.
4. **Data Extraction:** Visits each advertisement and parses its specification section to retrieve property attributes.
5. **Structured Output:** Yields the extracted fields as dictionaries that Scrapy can export into different data formats.

The project also configures a download delay to make requests more conservative and reduce the likelihood of rate limiting.

## Example Output

Each scraped listing is represented as a structured record containing the relevant property details.

```python
{
    "Başlık": "2+1 Daire",
    "Fiyat": "₺3.500.000",
    "Oda + Salon Sayısı": "2+1",
    "Brüt / Net M2": "75 / 68",
    "Bulunduğu Kat": "5. Kat",
    "Bina Yaşı": "10",
    "Isınma Tipi": "Kömür",
    "Kat Sayısı": "12",
    "Eşya Durumu": "Eşyalı",
    "Banyo Sayısı": "2",
    "İlçe": "Kadıköy",
    "Mahalle": "Moda",
    "Link": "https://www.hepsiemlak.com/..."
}
```

## Usage

Install Scrapy in your Python environment:

```bash
pip install scrapy
```

Run the spider from the project root:

```bash
scrapy crawl apartmentspider
```

To save the collected listings, use Scrapy's built-in export functionality:

```bash
# Export to JSON
scrapy crawl apartmentspider -o apartments.json

# Export to CSV
scrapy crawl apartmentspider -o apartments.csv
```

## Technologies

**Python · Scrapy · Web Scraping · HTML Parsing · JSON · CSV · Data Collection**

This project demonstrates how web crawling can transform unstructured real-estate listing pages into structured datasets for further analysis. Potential extensions include database integration, configurable location filters, data validation, and improved handling of changes in page structure.

The scraper is intended for educational, research, and personal data collection. Responsible use requires checking the website's terms, applicable access restrictions, and relevant legal requirements before crawling.
