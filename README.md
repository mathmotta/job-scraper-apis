# Job Scraper APIs: Greenhouse, Lever, Ashby, Workday & more

Ready-to-use scrapers for company career pages and applicant tracking systems (ATS), running on [Apify](https://apify.com/arcaedion).
They need no setup, proxies or browsers. Call them from the Apify UI, the REST API, Python, Node.js, Zapier, Make or n8n.

| Actor | What it returns | Price |
|---|---|---|
| [Multi-ATS Jobs Scraper](https://apify.com/arcaedion/ats-jobs-scraper) | Jobs from **Greenhouse, Lever, Ashby, Workday, SmartRecruiters, Workable, Recruitee, Personio**. Input a domain, careers URL or company name, and the ATS is detected automatically. | $1.50 / 1,000 jobs |
| [Workday Jobs Scraper](https://apify.com/arcaedion/workday-jobs-scraper) | Jobs from any `myworkdayjobs.com` career site | $1.50 / 1,000 jobs |
| [Greenhouse Jobs Scraper](https://apify.com/arcaedion/greenhouse-jobs-scraper) | Greenhouse job boards, including published salary ranges | $1.50 / 1,000 jobs |
| [Ashby Jobs Scraper](https://apify.com/arcaedion/ashby-jobs-scraper) | Ashby job boards, including compensation | $1.50 / 1,000 jobs |
| [Company Hiring Signals](https://apify.com/arcaedion/company-hiring-signals) | One record per company: open roles, 30-day hiring velocity, engineering/sales/marketing mix and tech-keyword counts. Hiring-intent data for B2B lead generation. | $0.02 / company |

## Features
- **New jobs only:** monitor mode remembers what it has already returned, so scheduled runs deliver (and bill) only fresh postings.
- **One normalized schema** for every ATS: title, company, locations, remote flag, department, seniority, salary min/max/currency, posting date and URLs.
- **Fast and cheap:** official public job-board APIs, so most runs finish in seconds.
- **Pay per result:** failed companies, duplicates and filtered-out jobs are free.

## Quick start (Python)
```python
from apify_client import ApifyClient

client = ApifyClient("<YOUR_APIFY_TOKEN>")
run = client.actor("arcaedion/ats-jobs-scraper").call(run_input={
    "companies": ["stripe.com", "https://jobs.lever.co/spotify", "Notion"],
    "keywords": ["engineer"],
    "onlyNewJobs": True,
})
for job in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(job["company"], "|", job["title"], "|", job["url"])
```

## Quick start (cURL)
```bash
curl -X POST "https://api.apify.com/v2/acts/arcaedion~ats-jobs-scraper/run-sync-get-dataset-items?token=<YOUR_APIFY_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"companies": ["stripe.com", "notion.so"], "keywords": ["engineer"]}'
```

## Example output
```json
{
  "title": "Senior Software Engineer, Payments",
  "company": "Stripe",
  "source": "greenhouse",
  "locations": ["Remote - US"],
  "remote": true,
  "department": "Engineering",
  "seniority": "senior",
  "salaryMin": 180000,
  "salaryMax": 260000,
  "salaryCurrency": "USD",
  "postedAt": "2026-10-20T00:00:00.000Z",
  "url": "https://stripe.com/jobs/listing/..."
}
```
*(Illustrative record; field names match the real output.)*

## Use cases
Niche job boards and aggregators, recruiting agencies tracking target companies, job-alert bots,
salary and labor-market research, sales prospecting (hiring = buying intent), and AI agents or RAG pipelines.

## Support
Missing an ATS or a field? Open an issue on the actor's Apify page.
