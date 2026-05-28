<div align="center">

# 📡 RSS Feeds Configuration

**Feed definitions for the open-news package**

This branch contains curated RSS feed configurations used by the `open-news` package.

[Feed Structure](#-feed-structure) • [Adding Feeds](#-adding-feeds) • [Feed Format](#-feed-format) • [Back to Main](https://github.com/alphap365/open-news)

</div>

---

## 📋 Overview

This branch (`rss-feeds`) maintains the RSS feed definitions that power the `get_live_news()` function in the main `open-news` package. Feed configurations are stored as JSON files and are automatically fetched and cached by the package.

**Key features:**
- ✅ Independent from code updates
- ✅ 50+ country-specific feeds
- ✅ Category-based news feeds
- ✅ Version controlled for transparency
- ✅ Easy community contributions

---

## 🗂️ Feed Structure

```
feeds/
├── news.json              # General news feeds
├── business.json          # Business & finance news
├── politics.json          # Political news
├── geopolitics.json       # Geopolitical analysis
├── country/
│   ├── india.json         # India-specific feeds
│   ├── usa.json           # United States feeds
│   ├── uk.json            # United Kingdom feeds
│   ├── pakistan.json      # Pakistan-specific feeds
│   └── ...                # Other countries
└── metadata.json          # (Optional) Feed metadata
```

---

## 📝 Feed Format

Each JSON file follows this structure:

```json
{
  "feeds": [
    {
      "name": "BBC News",
      "url": "https://feeds.bbc.co.uk/news/rss.xml",
      "description": "BBC News RSS Feed"
    },
    {
      "name": "Reuters",
      "url": "https://www.reuters.com/rssFeed/worldNews",
      "description": "Reuters World News"
    }
  ]
}
```

### Field Descriptions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | ✅ Yes | Feed source name (e.g., "BBC News") |
| `url` | string | ✅ Yes | RSS feed URL (must be valid and accessible) |
| `description` | string | ❌ Optional | Human-readable description of the feed |

---

## ➕ Adding Feeds

### Step 1: Fork & Branch
```bash
git clone https://github.com/alphap365/open-news.git
cd open-news
git checkout rss-feeds
git pull origin rss-feeds
```

### Step 2: Edit the Appropriate JSON File

For example, to add a feed to India news:

```bash
# Open feeds/country/india.json
# Add your feed to the "feeds" array:
{
  "name": "The Hindu",
  "url": "https://feeds.thehindu.com/news/national/?format=feed&type=rss",
  "description": "The Hindu - National News"
}
```

### Step 3: Validate JSON

Ensure the JSON is valid:
```bash
python3 -m json.tool feeds/country/india.json
```

### Step 4: Test the Feed

Verify the RSS feed is accessible:
```bash
curl -s "https://feeds.thehindu.com/news/national/?format=feed&type=rss" | head -20
```

### Step 5: Commit & Push

```bash
git add feeds/country/india.json
git commit -m "Add The Hindu news feed to India feeds"
git push origin rss-feeds
```

### Step 6: Create a Pull Request

Submit your PR on the `rss-feeds` branch with:
- Description of feeds added
- Rationale (why this feed is relevant)
- Verification that feeds are working

---

## 🔍 Feed Guidelines

### What Makes a Good Feed?

✅ **Good Feeds:**
- Regularly updated (daily or more frequent)
- Returns complete article titles
- Provides publication dates
- Maintains feed for 6+ months
- Accessible without authentication

❌ **Avoid:**
- Paywalled or limited access feeds
- Feeds with truncated content
- Dead or inactive feeds
- Feeds requiring API keys

### Best Practices

1. **Test before submitting:** Verify the feed URL works and returns data
2. **No duplicates:** Check existing feeds to avoid adding the same source twice
3. **Country-specific feeds:** Place country feeds in `feeds/country/{country}.json`
4. **Category feeds:** Use the main category files (`news.json`, `business.json`, etc.)
5. **Descriptive names:** Use official source names (e.g., "BBC News" not "BBC")

---

## 📤 How Package Uses These Feeds

The main `open-news` package fetches feeds from this branch via:

```
https://raw.githubusercontent.com/alphap365/open-news/rss-feeds/feeds/
```

### Usage Example

```python
from open_news import get_live_news

# Fetches from feeds/country/india.json
india_news = get_live_news(country="india", limit_per_feed=5)

# Fetches from feeds/business.json
business = get_live_news(category="business", limit_per_feed=3)

# Fetches from feeds/news.json
general = get_live_news(limit_per_feed=2)
```

---

## 📊 Feed Categories

### Countries
- `country/india.json` – India
- `country/usa.json` – United States
- `country/uk.json` – United Kingdom
- `country/pakistan.json` – Pakistan
- `country/{country}.json` – Add more as needed

### News Categories
- `news.json` – General news
- `business.json` – Business & finance
- `politics.json` – Politics & government
- `geopolitics.json` – International relations

---

## 🔄 Maintenance

### Regular Updates

Feed maintenance is community-driven. Please:
- Report broken feeds as [GitHub issues](https://github.com/alphap365/open-news/issues)
- Remove feeds that haven't been updated in 3 months
- Test feeds occasionally to ensure they're still active
- Update feed URLs if sources change

### Broken Feed Protocol

If a feed is broken:
1. Open a GitHub issue with the feed name and URL
2. Include error details (404, timeout, etc.)
3. Maintainers will remove or update within a week

---

## 🤝 Contributing

We welcome contributions! To add feeds:

1. **Read the guidelines** above
2. **Test your feeds** thoroughly
3. **Create a pull request** with clear descriptions
4. **Be patient:** PRs are reviewed within 2-3 days

### PR Checklist
- [ ] JSON is valid (`python3 -m json.tool` passes)
- [ ] Feed URLs are tested and accessible
- [ ] No duplicate feeds
- [ ] Appropriate category/country folder
- [ ] Descriptive commit message

---

## ⚡ Caching

The main package caches these feeds for **24 hours** to minimize network requests. Force refresh by clearing:

```bash
rm -rf ~/.open_news/feeds_cache/
```

---

## 📄 License

Feed configurations are part of the **open-news** project, licensed under MIT. See [main LICENSE](https://github.com/alphap365/open-news/blob/main/LICENSE).

---

<div align="center">

**[← Back to Main Repository](https://github.com/alphap365/open-news)**

Made with ❤️ by the [open-news](https://github.com/alphap365/open-news) community

</div>
