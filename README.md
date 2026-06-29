
<div align="center">

# 📡 Open Feeds

**Curated RSS feed definitions for news aggregation**

[📚 Feed Structure](#-feed-structure) • [➕ Adding Feeds](#-adding-feeds) • [📝 Feed Format](#-feed-format) • [🤝 Contributing](#-contributing)

</div>

---

## 📋 Overview

**Open Feeds** is a community-maintained repository of curated RSS feed definitions. These feeds are designed to be used by news aggregation tools, scrapers, and Python packages like [open-news-api](https://pypi.org/project/open-news-api).

This repository maintains:
* ✅ 50+ country-specific feeds
* ✅ Category-based news feeds (business, politics, geopolitics, general news)
* ✅ Version controlled for full transparency
* ✅ Easy community contributions
* ✅ Regularly maintained and validated feeds

---

## 🗂️ Feed Structure

```text
feeds/
├── news.json             # General news feeds
├── business.json         # Business & finance news
├── politics.json         # Political news
├── geopolitics.json     # Geopolitical analysis
└── country/
    ├── usa.json          # United States
    ├── india.json        # India
    ├── uk.json           # United Kingdom
    ├── pakistan.json     # Pakistan
    └── ...               # Other countries

templates/template.json   # Template for new feed files

```

The root `index.json` serves as a registry that lists all available feed files, their type (category or country), and their path.

---

## 📝 Feed Format

Each JSON file follows this **versioned schema**:

```json
{
  "schema_version": 2,
  "category": null,                 // or "news", "business", "politics", "geopolitics"
  "country": null,                  // or "usa", "india", "uk", etc.
  "last_updated": "2026-06-28T00:00:00Z",
  "max_articles_per_feed": 8,       // maximum articles to fetch from each feed
  "feeds": [
    {
      "id": "bbc-news",             // unique identifier for the feed
      "name": "BBC News",           // display name
      "url": "[https://feeds.bbci.co.uk/news/rss.xml](https://feeds.bbci.co.uk/news/rss.xml)",
      "type": "rss",                // "rss" or "google_news_rss" (or others)
      "lang": "en",                 // language code
      "country": "uk",              // primary country (may be null for global feeds)
      "tags": ["general"],          // array of tags (e.g., "general", "state-media", "aggregator")
      "active": true                // whether the feed is currently live
    }
  ]
}

```

### Field Descriptions

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `schema_version` | integer | ✅ Yes | Version of the schema (currently 2) |
| `category` | string or null | ❌ No | If the file is a category file (e.g., "news", "business") |
| `country` | string or null | ❌ No | If the file is a country file (e.g., "usa", "india") |
| `last_updated` | string (ISO 8601) | ✅ Yes | Date when the file was last modified |
| `max_articles_per_feed` | integer | ✅ Yes | Number of latest articles to fetch per feed (default usually 8) |
| `feeds` | array | ✅ Yes | List of feed objects |
| `feeds[].id` | string | ✅ Yes | Unique identifier for this feed (within the repository) |
| `feeds[].name` | string | ✅ Yes | Human‑readable name of the source |
| `feeds[].url` | string | ✅ Yes | RSS/Atom feed URL (must be valid and accessible) |
| `feeds[].type` | string | ✅ Yes | Feed format (currently "rss" or "google_news_rss") |
| `feeds[].lang` | string | ✅ Yes | Language code (e.g., "en", "fr") |
| `feeds[].country` | string or null | ❌ No | Primary country of the feed (if applicable) |
| `feeds[].tags` | array of strings | ✅ Yes | Descriptive tags (e.g., `["general"]`, `["state-media"]`) |
| `feeds[].active` | boolean | ✅ Yes | `true` if the feed is active and should be used |

---

## ➕ Adding Feeds

### 1. Fork & Clone the Repository

```bash
git clone [https://github.com/alphap365/open-feeds.git](https://github.com/alphap365/open-feeds.git)
cd open-feeds

```

### 2. Choose the Appropriate File

* **Country feeds** → edit `feeds/country/<country>.json`
* **Category feeds** → edit `feeds/<category>.json` (e.g., `news.json`)
* **New country** → copy `templates/template.json` to `feeds/country/<country>.json` and fill in the details.

### 3. Add Your Feed Entry

Inside the `feeds` array, add a new object with all required fields. For example, to add a new Indian news source:

```json
{
  "id": "the-hindu",
  "name": "The Hindu",
  "url": "[https://www.thehindu.com/news/feeder/default.rss](https://www.thehindu.com/news/feeder/default.rss)",
  "type": "rss",
  "lang": "en",
  "country": "india",
  "tags": ["general"],
  "active": true
}

```

### 4. Validate the JSON

Make sure the file is valid JSON:

```bash
python3 -m json.tool feeds/country/india.json

```

### 5. Test the Feed

Verify the feed URL works:

```bash
curl -s "[https://www.thehindu.com/news/feeder/default.rss](https://www.thehindu.com/news/feeder/default.rss)" | head -20

```

### 6. Update `index.json` (if adding a new file)

If you create a new country or category file, add an entry in `index.json` under the registry array.

For a new country file:

```json
{
  "key": "mynewcountry",
  "kind": "country",
  "path": "feeds/country/mynewcountry.json"
}

```

For a new category file:

```json
{
  "key": "technology",
  "kind": "category",
  "path": "feeds/technology.json"
}

```

### 7. Commit & Push

```bash
git add feeds/country/india.json
git add index.json   # if changed
git commit -m "Add The Hindu news feed to India feeds"
git push origin add-feeds/india-news

```

### 8. Create a Pull Request

Submit your PR with:

* **A clear title:** `Add [Feed Name] to [Category/Country]`
* Description of the added feeds
* Rationale for inclusion
* Verification that feeds are working

---

## 🔍 Feed Guidelines

### ✅ Good Feeds

* Regularly updated (daily or more)
* Complete article titles and links
* Publication dates included
* Stable feed URL for 6+ months
* Accessible without authentication
* Valid RSS/Atom format

### ❌ Avoid

* Paywalled or limited‑access feeds
* Truncated content or summaries only
* Dead or inactive feeds (no updates in 3+ months)
* Feeds requiring API keys or authentication
* Feeds with excessive redirects or errors

### 💡 Best Practices

* **Test before submitting** – always verify the URL works.
* **No duplicates** – search existing files to avoid adding the same source twice.
* **Use official names** – e.g., "BBC News" instead of "BBC".
* **Choose correct tags** – use `["general"]`, `["state-media"]`, `["aggregator"]`, or custom tags as needed.
* **Set active status** – set `"active": true` only if the feed is currently live; set to `false` if it’s temporarily broken.

---

## 📊 Feed Categories

| File | Type | Description |
| --- | --- | --- |
| `news.json` | Category | General / breaking news |
| `business.json` | Category | Business, finance, economics |
| `politics.json` | Category | Politics & government |
| `geopolitics.json` | Category | International relations, geopolitical analysis |
| `country/*.json` | Country | Feeds specific to a country (e.g., `india.json`) |

---

## 🔄 Maintenance

* Report broken feeds via GitHub Issues.
* Remove feeds that haven’t been updated in 3+ months.
* Update feed URLs if sources change their feed endpoints.
* Set `"active": false` for temporarily unavailable feeds.

---

## 🤝 Contributing

We welcome contributions! Please follow the steps above and check the PR checklist:

### PR Checklist

* [ ] JSON is valid (`python3 -m json.tool` passes)
* [ ] Feed URLs are tested and accessible
* [ ] No duplicate feeds in the repository
* [ ] Feed placed in appropriate category/country file
* [ ] `index.json` updated if a new file is added
* [ ] Descriptive commit message and PR description
* [ ] Feed follows the format specification

---

GitHub • Issues • Discussions

Made with ❤️ by the community
