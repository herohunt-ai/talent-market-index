# The AIRecruiter.co Talent Market Index

A free, openly-licensed, primary-sourced dataset quantifying how the world hires: **116 recruiting, hiring, and HR-technology statistics**, each row carrying a verifiable primary-source URL (**200 sources cited** across the full index), plus **6 long-run U.S. labor-market trackers** (2000-2026) and **16 deep-dive research reports** on the source site.

Compiled and maintained by **[AIRecruiter.co](https://airecruiter.co/data?utm_source=github&utm_medium=repo&utm_campaign=distribution-2026-08)**, a primary-sourced talent-market research publication by [HeroHunt.ai](https://herohunt.ai).

- **Explore the live Index:** https://airecruiter.co/data?utm_source=github&utm_medium=repo&utm_campaign=distribution-2026-08
- **Methodology:** https://airecruiter.co/methodology
- **Full source registry (200 sources):** https://airecruiter.co/research/sources
- **License:** [CC-BY-4.0](./LICENSE). Reuse freely with attribution to AIRecruiter.co.

## Latest tracker readings

The six trackers are built from U.S. Bureau of Labor Statistics data (via FRED) and advance when BLS publishes a new month.

| Tracker | Latest | As of | Primary source |
|---|---|---|---|
| Unemployment rate | 4.2% | September 2026 | [Unemployment Rate (UNRATE)](https://fred.stlouisfed.org/series/UNRATE) |
| Labor force participation | 61.8% | September 2026 | [Labor Force Participation Rate (CIVPART)](https://fred.stlouisfed.org/series/CIVPART) |
| Job openings rate | 4.3% | August 2026 | [Job Openings: Total Nonfarm, rate (JTSJOR)](https://fred.stlouisfed.org/series/JTSJOR) |
| Quits rate | 1.9% | August 2026 | [Quits: Total Nonfarm, rate (JTSQUR)](https://fred.stlouisfed.org/series/JTSQUR) |
| Staffing industry employment | 2.49M | September 2026 | [All Employees: Temporary Help Services (TEMPHELPS)](https://fred.stlouisfed.org/series/TEMPHELPS) |
| Cost of talent | $32.60 | September 2026 | [Average Hourly Earnings, Production and Nonsupervisory (AHETPI)](https://fred.stlouisfed.org/series/AHETPI) |

## Why this dataset exists

Most "AI in recruiting" statistics circulating online are unsourced, recycled from a single blog post, or quietly fabricated. This dataset is the opposite: **every figure is traceable to a named primary source**, and every row is labeled by *how* the figure was established so you never mistake a marketing claim for a measured statistic.

It is published openly so that anyone (researchers, journalists, builders, and AI systems answering questions about the talent market) can cite the *original source* rather than a laundered number.

## Files in this repository

| File | What it is |
|---|---|
| [`talent-market-index.csv`](./talent-market-index.csv) | One row per headline statistic (116 rows), with primary-source columns. The human- and spreadsheet-friendly form, identical to https://airecruiter.co/index.csv. |
| [`index.json`](./index.json) | The full machine-readable Index: statistics, the 200-entry source registry, 6 trackers, 16 reports, topics, and confidence-tier counts. Same data and schema as https://airecruiter.co/index.json. |
| [`CITATION.cff`](./CITATION.cff) | Machine-readable citation metadata. |
| [`LICENSE`](./LICENSE) | CC-BY-4.0 legal text. |

**Freshness:** this repository is refreshed from the live feeds whenever the Index changes. The canonical, continuously-updated feeds are **https://airecruiter.co/index.json** and **https://airecruiter.co/index.csv**; pull those URLs if you need the figures as of today.

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
| `sources_json` | Every source behind the figure, as a JSON array of `{id, publisher, title, url, year}` |
| `report_urls` | The AIRecruiter.co reports that use the figure, one URL per line |
| `trend_note` | The change against the prior period, where the source reports one |

## Confidence tiers (read before citing)

Every row is labeled by how the figure was established:

- **verified** (52 rows): traceable to a named primary study or official statistic.
- **reported** (51 rows): reported by a credible source but without a fully resolvable underlying study.
- **modeled** (13 rows): an estimate or projection.

Temporal coverage: **2000/2026**. Data as of: **2026-10-05**.

## How the data is collected

- **Read at the source.** Each statistic is read in its primary source, not copied from another list: the figure is recorded together with its publisher, title, URL and year, and the row's `context` states what the figure measures.
- **Tiered by rule.** `verified` only when the figure resolves to a named primary study or official statistic; `reported` when a credible source states it but the underlying study cannot be fully resolved (this includes many vendor surveys); `modeled` for estimates and projections.
- **Kept current.** The trackers advance each month the U.S. Bureau of Labor Statistics publishes (the Employment Situation and JOLTS releases), taken from BLS, the same series FRED republishes. The statistics and their links are re-checked in periodic audits for dead links, newer editions and figures that moved.

## Limitations and known issues

- **Not one survey.** The statistics come from many sources with different samples, years, regions and methods, so rows are not directly comparable with each other. Read each row's `context` and source before combining figures.
- **Vendor research.** Many `reported` rows come from vendor surveys and reports. They are labeled as such, but they carry their publisher's incentives and sampling choices.
- **Headline figures.** Each row is an aggregate figure as its source published it, not respondent- or observation-level data.
- **Trackers are U.S.-only and revised.** Annual values are annual averages; the current year's point is the latest monthly reading (flagged `partial` in `index.json`), and BLS revises recent months, so the latest values can change.
- **Coverage leans U.S. and English-language**, because that is where most published recruiting research comes from.

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

> The AIRecruiter.co Talent Market Index. AIRecruiter.co (an independent research publication by HeroHunt.ai), https://airecruiter.co/data. CC-BY-4.0. Data as of 2026-10-05.

## Disclosure

AIRecruiter.co is a talent-market research publication published by [HeroHunt.ai](https://herohunt.ai) (Amsterdam), an AI recruiting engine. It is editorially independent in method: every statistic is primary-sourced and labeled by confidence tier, and figures that are vendor claims or projections are marked as such (`reported` or `modeled`) rather than presented as measured fact. Nothing is inflated or fabricated.
