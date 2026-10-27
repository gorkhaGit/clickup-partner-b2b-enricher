# ClickUp Partner & Verified Consultant B2B Lead Enricher

> **Zero-Proxy Async Python B2B Scraper & Contact Enricher** for the official **ClickUp Partner Directory** (`clickup.com/partners`). Extracts Solution Partners, Global Partners, and Verified Consultants enriched with verified B2B emails, phone numbers, LinkedIn URLs, services, and locations.

---

## ⚡ Apify Cloud Production Benchmarks

| Metric | Production Benchmark |
| :--- | :--- |
| **Runtime Stack** | Python 3.12 (`httpx` + `BeautifulSoup4` + `selectolax` + `apify>=4.0.0`) |
| **Headless Browser Overhead** | **None (0 MB)** — 100% Native Async HTTP |
| **Memory Footprint** | **121.5 MB Avg / 188.9 MB Max** (Runs cleanly on **256 MB RAM** tier) |
| **Execution Speed** | **25 Enriched Partner Agencies in 47 seconds** |
| **Proxy Burn** | **$0.00** (100% Server-Rendered HTML + Direct Website Crawl) |
| **Cloud Verification Run** | `Succeeded` (`Build 0.1.1` / `Run ID: 77zXP86UXLg4WL7QI`) |

---

## 📊 Scraped Data Evidence (Sample Output)

Full sample files from live runs are included in this repository:
- **JSON Sample:** [`evidence/sample_leads.json`](./evidence/sample_leads.json)
- **CSV Sample:** [`evidence/sample_leads.csv`](./evidence/sample_leads.csv)

### Sample Enriched JSON Record
```json
{
  "partnerName": "Sharpflow Consulting",
  "slug": "sharpflow-consulting",
  "partnerTier": "Solution Partner",
  "headquarters": "Australia",
  "website": "https://sharpflowconsulting.com/",
  "primaryEmail": "",
  "emails": [],
  "phones": [],
  "linkedinUrl": "https://www.linkedin.com/company/sharpflow-consulting/",
  "twitterUrl": "",
  "contactPageUrl": "https://sharpflowconsulting.com/book-a-discovery-call",
  "services": [],
  "industries": [],
  "locations": [
    "Australia",
    "Canada",
    "Mexico",
    "Spain",
    "United Kingdom"
  ],
  "languages": [
    "Brazilian Portuguese",
    "English",
    "French",
    "Spanish"
  ],
  "summary": "We’re a British-led ClickUp only consultancy based in Mexico, working with teams around the world that need more than tidy dashboards. \n\nWe build operational systems that create structure, improve accountability, and support scalable growth.",
  "profileUrl": "https://clickup.com/partners/partner/sharpflow-consulting",
  "scrapedAt": "2026-10-27T03:48:12.093055+00:00"
}
```

---

## 🛠️ Engineering Architecture
1. **Paginated SSR Ingestion:** Crawls `clickup.com/partners?page=N` server-rendered HTML pages to discover Solution Partner and Verified Consultant profile slugs without browser automation.
2. **Dual-Layer Email & Social Enricher:** Extracts agency metadata, tier badges, headquarters, and LinkedIn links from `clickup.com/partners/partner/{slug}`, then concurrently crawls each agency's external website and `/contact` page to harvest verified business emails and phone numbers.
3. **Strict Schema Sanitization:** Enforces `100%` non-null field validation against `.actor/dataset_schema.json` and `.actor/output_schema.json` with native Pay-Per-Event (`partner-enriched`) charging.
