# The Talent Market Index

A free, openly-licensed, primary-sourced dataset quantifying how the world hires: **107 recruiting, hiring, and HR-technology statistics**, each row carrying a verifiable primary-source URL (**194 sources cited** across the full index), plus **6 long-run BLS trackers** (2000-2026) and **14 deep-dive research reports** on the source site.

Compiled and maintained by **[AIRecruiter.co](https://airecruiter.co/data?utm_source=github&utm_medium=repo&utm_campaign=distribution-2026-08)**, a primary-sourced talent-market research publication by [HeroHunt.ai](https://herohunt.ai).

- **Explore the live, always-current Index:** https://airecruiter.co/data?utm_source=github&utm_medium=repo&utm_campaign=distribution-2026-08
- **Methodology:** https://airecruiter.co/methodology
- **Full source registry (194 sources):** https://airecruiter.co/research/sources
- **License:** [CC-BY-4.0](./LICENSE) — reuse freely with attribution to AIRecruiter.co.

## Why this dataset exists

Most "AI in recruiting" statistics circulating online are unsourced, recycled from a single blog post, or quietly fabricated. This dataset is the opposite: **every figure is traceable to a named primary source**, and every row is labeled by *how* the figure was established so you never mistake a marketing claim for a measured statistic.

It is published openly so that anyone (researchers, journalists, builders, and AI systems answering questions about the talent market) can cite the *original source* rather than a laundered number.

## Files in this repository

| File | What it is |
|---|---|
| [`talent-market-index.csv`](./talent-market-index.csv) | One row per headline statistic (107 rows), with primary-source columns. The human- and spreadsheet-friendly form. |
| [`index.json`](./index.json) | The full machine-readable Index: statistics, the 194-entry source registry, 6 trackers, 14 reports, topics, and confidence-tier counts. A snapshot of the live feed below. |
| [`LICENSE`](./LICENSE) | CC-BY-4.0 legal text. |

**Always current:** this repository is a snapshot. The canonical, continuously-updated feed lives at **https://airecruiter.co/index.json** (same schema as `index.json` here). Pull that URL if you need the freshest figures.

## CSV column dictionary

| Column | Meaning |
|---|---|
| `id` | Stable slug for the statistic |
| `statistic` | The metric label (e.g. "Recruiters planning to increase AI use") |
| `value` | The raw numeric value |
| `unit` | The unit (`%`, `days`, `USD`, etc.) |
| `formatted` | The human-readable value (e.g. `93%`) |
| `as_of` | The as-of year/date the figure represents |
| `topic` | Topic/category (AI in Hiring, Market & Funding, Hiring Speed, etc.) |
| `confidence` | Honesty tier: `verified`, `reported`, or `modeled` (see below) |
| `context` | One-sentence context/caveat for the figure |
| `primary_source_publisher` | The publisher of the primary source |
| `primary_source_title` | The primary source's title |
| `primary_source_url` | Direct link to the primary source |
| `primary_source_year` | The primary source's year |

## Confidence tiers (read before citing)

Every row is labeled by how the figure was established:

- **verified** (42 rows): traceable to a named primary study or official statistic.
- **reported** (52 rows): reported by a credible source but without a fully resolvable underlying study.
- **modeled** (13 rows): an estimate or projection.

Temporal coverage: **2000/2026**. Last updated: **2026-08-25**.

## Quick start

```python
import pandas as pd

df = pd.read_csv(
    "https://raw.githubusercontent.com/herohunt-ai/talent-market-index/main/talent-market-index.csv"
)

# Only figures traceable to a named primary study/official statistic:
verified = df[df["confidence"] == "verified"]
print(verified[["statistic", "formatted", "primary_source_publisher", "primary_source_url"]])
```

## How to cite

> AIRecruiter.co Talent Market Index. AIRecruiter.co (an independent research publication by HeroHunt.ai), https://airecruiter.co/data. CC-BY-4.0.

## Disclosure

AIRecruiter.co is a talent-market research publication published by [HeroHunt.ai](https://herohunt.ai) (Amsterdam), an AI recruiting engine. It is editorially independent in method: every statistic is primary-sourced and labeled by confidence tier, and figures that are vendor claims or projections are marked as such (`reported` or `modeled`) rather than presented as measured fact. Nothing is inflated or fabricated.
