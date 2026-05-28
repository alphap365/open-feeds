<div align="center">

# 📡 Open Feeds

**Curated RSS feed definitions for news aggregation**

[📚 Feed Structure](#-feed-structure) • [➕ Adding Feeds](#-adding-feeds) • [📝 Feed Format](#-feed-format) • [🤝 Contributing](#-contributing)

</div>

---

## 📋 Overview

**Open Feeds** is a community-maintained repository of curated RSS feed definitions. These feeds are designed to be used by news aggregation tools, scrapers, and Python packages like `open-news`.

This repository maintains:
- ✅ 50+ country-specific feeds
- ✅ Category-based news feeds (business, politics, geopolitics)
- ✅ Version controlled for full transparency
- ✅ Easy community contributions
- ✅ Regularly maintained and validated feeds

---

## 🗂️ Feed Structure

```
feeds/
├── news.json              # General news feeds
├── business.json          # Business & finance news
├── politics.json          # Political news
├── geopolitics.json       # Geopolitical analysis
└── country/
    ├── india.json         # India-specific feeds
    ├── usa.json           # United States feeds
    ├── uk.json            # United Kingdom feeds
    ├── pakistan.json      # Pakistan-specific feeds
    └── ...                # Other countries
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

### Step 1: Fork & Clone
```bash
git clone https://github.com/alphap365/open-feeds.git
cd open-feeds
```

### Step 2: Create a Feature Branch
```bash
git checkout -b add-feeds/<feed-category>
# Example: git checkout -b add-feeds/india-news
```

### Step 3: Edit the Appropriate JSON File

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

### Step 4: Validate JSON

Ensure the JSON is valid:
```bash
python3 -m json.tool feeds/country/india.json
```

### Step 5: Test the Feed

Verify the RSS feed is accessible and returns data:
```bash
curl -s "https://feeds.thehindu.com/news/national/?format=feed&type=rss" | head -20
```

### Step 6: Commit & Push

```bash
git add feeds/country/india.json
git commit -m "Add The Hindu news feed to India feeds"
git push origin add-feeds/india-news
```

### Step 7: Create a Pull Request

Submit your PR with:
- Clear title: `Add [Feed Name] to [Category/Country]`
- Description of feeds added
- Rationale: Why this feed is relevant
- Verification: Confirmation that feeds are working

---

## 🔍 Feed Guidelines

### What Makes a Good Feed?

✅ **Good Feeds:**
- Regularly updated (daily or more frequent)
- Returns complete article titles and links
- Provides publication dates
- Maintains stable feed URL for 6+ months
- Accessible without authentication or paywall
- Valid and well-formed RSS/Atom format

❌ **Avoid:**
- Paywalled or limited access feeds
- Feeds with truncated content or summaries only
- Dead or inactive feeds (no updates in 3+ months)
- Feeds requiring API keys or authentication
- Feeds with excessive redirects or errors

### Best Practices

1. **Test before submitting:** Always verify the feed URL works and returns articles
2. **No duplicates:** Search existing JSON files to avoid adding the same source twice
3. **Country-specific feeds:** Place country feeds in `feeds/country/{country}.json`
4. **Category feeds:** Use the main category files (`news.json`, `business.json`, etc.)
5. **Descriptive names:** Use official source names (e.g., "BBC News" not "BBC")
6. **Categorize correctly:** Ensure the feed matches its file category

---

## 📊 Feed Categories

### Countries
- `country/india.json` – India
- `country/usa.json` – United States
- `country/uk.json` – United Kingdom
- `country/pakistan.json` – Pakistan
- `country/{country}.json` – Add more as needed

### News Categories
- `news.json` – General/Breaking news
- `business.json` – Business, finance & economics
- `politics.json` – Politics & government
- `geopolitics.json` – International relations & geopolitical analysis

---

## 🔄 Maintenance

### Regular Updates

Feed maintenance is community-driven. Please:
- **Report broken feeds** as [GitHub issues](https://github.com/alphap365/open-feeds/issues)
- **Remove feeds** that haven't been updated in 3+ months
- **Test feeds** occasionally to ensure they're still active
- **Update feed URLs** if sources change their feed endpoints

### Broken Feed Protocol

If a feed is broken:
1. Open a GitHub issue with the feed name and URL
2. Include error details (404, timeout, malformed XML, etc.)
3. Maintainers will remove or update the feed within 1 week

---

## 🤝 Contributing

We welcome contributions! To contribute feeds:

1. **Read the [guidelines](#-feed-guidelines) above**
2. **Test your feeds** thoroughly before submitting
3. **Create a pull request** with a clear description
4. **Be patient:** PRs are reviewed within 2-3 days

### PR Checklist
- [ ] JSON is valid (`python3 -m json.tool` passes)
- [ ] Feed URLs are tested and accessible
- [ ] No duplicate feeds in the repository
- [ ] Feed placed in appropriate category/country folder
- [ ] Descriptive commit message and PR description
- [ ] Feed follows the format specification above

---

## 📄 License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<div align="center">

**[GitHub](https://github.com/alphap365/open-feeds) • [Issues](https://github.com/alphap365/open-feeds/issues) • [Discussions](https://github.com/alphap365/open-feeds/discussions)**

Made with ❤️ by the community

</div>
