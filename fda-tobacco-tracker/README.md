# FDA Tobacco Product Directory Tracker

A static GitHub Pages site that fetches the [FDA Searchable Tobacco Products Database](https://www.accessdata.fda.gov/scripts/searchtobacco/) daily and lets you search the directory and flag newly authorized products.

## Features

- **Full-text search** across company name, product name, STN, and MRTP numbers
- **Filter** by product category and submission type
- **"New products" quick filters** — last 30 / 60 / 90 days, or products added since your last visit
- **Color-coded rows** — green for recently authorized products, purple for new-since-last-visit
- **Document links** — direct links to Order Letters, Decision Summaries, Environmental Assessments, and FONSI documents
- **Sortable columns**, pagination, and CSV export of filtered results
- **Auto-updates daily** via GitHub Actions

---

## Setup (takes ~5 minutes)

### 1. Fork this repository

Click **Fork** at the top right of this page. The repo must be **public** to use GitHub Pages for free.

### 2. Enable GitHub Pages

Go to your fork: **Settings → Pages → Source → Deploy from a branch → main / (root) → Save**

After saving, your site will be available at:
```
https://<your-username>.github.io/<repo-name>/
```

### 3. Enable GitHub Actions

Go to **Actions** tab → click **"I understand my workflows, go ahead and enable them"** if prompted.

### 4. Fetch initial data

Go to **Actions → Update FDA Tobacco Data → Run workflow → Run workflow**.

This fetches the full FDA CSV (~10,000+ products) and commits it to `data/tobacco.csv`. Wait about 30 seconds, then reload your GitHub Pages URL.

From now on the workflow runs automatically every day at noon UTC.

---

## How "New Since Last Visit" works

The first time you open the page, your browser saves a snapshot of all current product STN numbers to `localStorage`. On your next visit, anything in the live data that wasn't in your saved snapshot is flagged purple as "New Visit." Your snapshot is updated each time you load the page.

---

## File structure

```
/
├── index.html                         ← the tracker app (self-contained)
├── data/
│   └── tobacco.csv                    ← populated daily by GitHub Action
└── .github/
    └── workflows/
        └── update-data.yml            ← daily fetch workflow
```

---

## Data source

FDA Searchable Tobacco Products Database  
https://www.accessdata.fda.gov/scripts/searchtobacco/

Products in the database are legally marketable because they are authorized through one of three pathways (PMTA, SE, EXREQ), established as pre-existing tobacco products (PTP), or provisional products removed from review (SE - Removed From Review).

> No tobacco product is safe. It is illegal to sell tobacco products to anyone under 21.
