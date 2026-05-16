# CSV Audit Tool

A browser-based data quality auditor for CSV files. Drop in a file, get an instant report.

**[Try it live →](https://michaelf-pm.github.io/csv-audit-tool)**

---

## What it does

Paste a CSV in and get a report covering:

- **Completeness** – null and empty value rates, per column and overall
- **Duplicates** – exact duplicate row detection
- **Type inference** – automatically classifies columns as numeric, date, boolean, or text
- **Outlier detection** – flags statistical outliers in numeric columns using the IQR method
- **Negative values** – surfaces unexpected negatives that may indicate data entry errors
- **Mixed delimiters** – detects and normalises rows using semicolons instead of commas
- **Currency symbols** – identifies `$`-prefixed numeric fields that need cleaning
- **Date format inconsistency** – flags columns with mixed date formats and recommends ISO 8601

Everything runs locally in the browser. No data is uploaded anywhere.

---

## Why I built this

Data quality is one of the most persistent and expensive problems in martech and fintech data stacks. Dirty CRM exports, inconsistent pipeline outputs, and malformed ETL feeds are a daily reality for data and ops teams – but most quality issues aren't caught until they've already propagated downstream.

This tool was built to answer a simple question: *can a non-engineer quickly audit a CSV before it enters a pipeline or gets loaded into a system?*

The answer turned out to be yes – with a clean interface that surfaces the right signals without requiring SQL, Python, or a data engineering ticket.

---

## Product decisions worth noting

**Why browser-only?**
The target user is an ops manager or analyst, not a developer. Requiring a server, a login, or an install creates friction that kills adoption. Running everything client-side also removes the data privacy concern entirely – a real consideration when the files contain PII or financial data.

**Why not just use Excel?**
Excel will open a CSV and show you the data. It won't tell you your null rate, flag mixed delimiters, or detect that one column has three different date formats. This tool is opinionated about *what matters for data quality* rather than being a general-purpose viewer.

**Why IQR for outlier detection?**
IQR is robust to skewed distributions and doesn't assume normality, which makes it more reliable than z-score methods for the kind of transactional data (purchase amounts, order values) common in martech and fintech contexts.

**The v1 → v2 lesson**
The first version scored a genuinely messy test file as "Good" because semicolon-delimited rows were being parsed as single-column blobs, which masked the real null picture and inflated uniqueness counts. This is a good illustration of why tools that process real-world data need to be tested against real-world mess, not clean synthetic samples.

---

## Built with

- Vanilla HTML, CSS, and JavaScript – no frameworks, no dependencies
- [Tabler Icons](https://tabler.io/icons) for iconography
- Built iteratively using [Claude](https://claude.ai) as a coding assistant

---

## Running locally

No build step required. Clone the repo and open `index.html` in a browser:

```bash
git clone https://github.com/Michael-Fehle-PM/csv-audit-tool.git
cd csv-audit-tool
open index.html
```

---

## Potential next iterations

- **Export** – download the audit report as PDF or CSV
- **Column-level detail** – value frequency distributions, min/max/mean for numeric columns
- **Fuzzy duplicate detection** – catch near-duplicates (`Bob Lee` vs `Bob  Lee`)
- **Schema validation** – validate a file against a defined expected schema
- **Multi-file comparison** – diff two versions of the same dataset

---

## About

Built by [Michael F](https://github.com/Michael-Fehle-PM) as part of a portfolio of data tooling projects. Background in SaaS product management across martech and fintech, with a focus on data quality, ETL pipelines, and operational tooling.
