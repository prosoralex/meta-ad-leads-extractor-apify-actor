# META Ad Leads Extractor — Apify Actor usage guide

[![Run for free on Apify](https://img.shields.io/badge/Apify-Run%20it%20free%20%E2%80%94%20%245%2Fmo%20credit-24C1E0)](https://console.apify.com/sign-up?fpr=aupara)

Extract enriched leads from Facebook Ad Library. Enter a keyword + country → get email, phone, website, adress, Instagram & more for every advertiser found. Powered by Leadsbrary.com. Pay only for results.

> **This repository does not contain the Actor's source code.** The Actor
> itself is closed-source and runs on Apify's infrastructure — this repo is
> just documentation and example client code showing how to call it via the
> Apify API/SDK with your own Apify API token. Think of it as a "cookbook"
> repo, not the product itself.

**Run it on Apify →** [https://apify.com/leadsbrary/meta-ad-leads-extractor?fpr=aupara](https://apify.com/leadsbrary/meta-ad-leads-extractor?fpr=aupara)

## What it does

A Facebook Ads Lead Extractor that searches the Meta Ad Library and the Meta Graph API to find advertisers by keyword and country, then scrapes Facebook business pages to extract and enrich advertiser contact data. The Actor identifies advertiser page IDs from ad search results, scrapes JSON-encoded profile data to capture emails, phone numbers, websites and physical addresses, enriches records with Instagram profile and follower information via a typeahead API, and applies post-search filters and keyword-intersection logic to produce structured lead records containing page metadata, contact details, social handles, audience/follower metrics, advertiser verification and ad timing information.…

## Pricing

Pay-per-event pricing — you only pay for what the Actor actually delivers:

- **Lead** — $0.0035. Enriched Facebook Ads lead (email, phone, website, Instagram)
- **Actor Start** — $0.00005 (one-time, per run). Charged when the Actor starts running. Number of events charged depends on Actor memory (one event per GB, minimum one event).

*(Apify may also charge a small amount for the platform compute the Actor
uses while running — see the [pricing tab](https://apify.com/leadsbrary/meta-ad-leads-extractor?fpr=aupara) on the Actor page
for exact current numbers.)*

## Quick start

You need an Apify account and API token (`console.apify.com` → Settings →
Integrations). Don't have one yet? See the signup section below — new
accounts get **$5 of free usage credit every month**.

### cURL

```bash
curl -X POST "https://api.apify.com/v2/acts/leadsbrary~meta-ad-leads-extractor/runs?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "keywords": "dental clinic",
  "country": "FR",
  "adStatus": "ACTIVE",
  "maxLeads": 5,
  "matchAllKeywords": false
}'
```

### Python (`apify-client`)

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")

run_input = {
  "keywords": "dental clinic",
  "country": "FR",
  "adStatus": "ACTIVE",
  "maxLeads": 5,
  "matchAllKeywords": False
}

run = client.actor("leadsbrary/meta-ad-leads-extractor").call(run_input=run_input)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### JavaScript (`apify-client`)

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });

const runInput = {
  "keywords": "dental clinic",
  "country": "FR",
  "adStatus": "ACTIVE",
  "maxLeads": 5,
  "matchAllKeywords": false
};

const run = await client.actor('leadsbrary/meta-ad-leads-extractor').call(runInput);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

See [`example.py`](./example.py) in this repo for a complete runnable script.

## Don't have an Apify account yet?

[Sign up here](https://console.apify.com/sign-up?fpr=aupara) — new accounts get **$5 of free platform credit
every month**, enough to try most Actors without paying anything upfront.
Browsing for other tools? The full [Apify Store](https://apify.com/store?fpr=aupara) has thousands
of ready-made Actors.

## Links

- Actor page (run it, see live pricing/reviews): [https://apify.com/leadsbrary/meta-ad-leads-extractor?fpr=aupara](https://apify.com/leadsbrary/meta-ad-leads-extractor?fpr=aupara)
- All Actors from this developer: [https://apify.com/leadsbrary?fpr=aupara](https://apify.com/leadsbrary?fpr=aupara)
- Apify API docs: [https://docs.apify.com/api/v2](https://docs.apify.com/api/v2)

## License

The example code in this repository (README snippets, `example.py`) is
released under the MIT License — see [LICENSE](./LICENSE). This does not
cover the Actor itself, which remains closed-source and is operated by its
developer on the Apify platform.
