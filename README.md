# Data Collection, Wrangling & Feature Engineering (Company & Industry Data)

## Overview

This project builds an end-to-end **data preparation pipeline** for company and
industry data. Starting from raw CSV files, it:

- standardises and cleans identifiers and text fields,
- joins company-level and industry-level datasets,
- engineers domain-relevant features (size buckets, sector groupings, ratios),
- and outputs **analysis-ready tables** that can be used in modelling,
  dashboarding or research (e.g. NLP, risk scoring, screening).

The focus is on the “unseen” but critical work that sits **before** any
machine learning, forecasting or valuation model.

---

## Business Context & Motivation

From the perspective of an **equity analyst, credit analyst or data team**,
there is often no value in more complex models if:

- company information is duplicated or inconsistent,
- sectors and industries are coded differently across sources,
- simple but important ratios and flags are missing.

This project answers questions like:

1. How do we create **a single, consistent view of companies and industries**?
2. Which **derived features** (size, sector, region, ratios) are useful to have
   baked into every downstream analysis?
3. How can we structure the wrangling process so it is **reproducible** and
   easy to extend?

The resulting dataset can feed into:

- valuation and screening models,
- NLP projects on company descriptions,
- dashboards and risk monitoring tools.

---

## Data

The core inputs are two CSV files:

- `companies_information.csv`  
  Basic company-level information such as:
  - company name and ID
  - sector / industry tags
  - region / country
  - selected financial fields or KPIs (depending on the source)

- `industries_information.csv`  
  Higher-level industry metadata such as:
  - industry codes and descriptions
  - sector groupings
  - optional mappings to broader themes (e.g. “Consumer”, “Financials”, etc.)

> In this repo, these files act as a **proxy for a fundamentals universe**
> (e.g. listed companies in a given market with industry classifications).

---

## Approach

The notebook **`Data Collection, Wrangling & Feature Engineering.ipynb`**
follows a structured workflow:

1. **Data Loading**
   - Import both CSV files with correct encodings and data types.
   - Basic sanity checks on row counts, unique IDs, and key columns.

2. **Cleaning & Standardisation**
   - Trim and normalise text fields (names, sectors, industries).
   - Handle missing values and obvious inconsistencies.
   - Ensure a consistent key to join company and industry tables.

3. **Joining Company & Industry Data**
   - Merge company-level and industry-level information into a single table.
   - Validate joins (e.g. how many companies fail to match an industry).

4. **Feature Engineering**
   - Create **size buckets** (e.g. small / mid / large) based on a size metric
     such as revenue, assets or market cap.
   - Build **sector / super-sector groupings** to reduce noise in very granular
     industry codes.
   - Compute basic **ratio features** where available (e.g. margins or simple
     efficiency indicators).
   - Generate flags for:
     - region / listing location,
     - sectors of interest (e.g. financials, consumer, industrials),
     - any custom themes used elsewhere in the portfolio.

5. **Output & Documentation**
   - Produce a clean, analysis-ready dataframe.
   - Optionally write the result to a CSV or parquet file for use in other
     projects (e.g. NLP, forecasting, dashboards).
   - Document the steps so the pipeline is reproducible.

---

## Repository Structure

> This is the structure the project is moving towards. Your current layout may
> be a subset of this.

- `notebooks/`
  - `Data Collection, Wrangling & Feature Engineering.ipynb` – main notebook
    implementing the pipeline.
- `data/`
  - `companies_information.csv` – raw company information.
  - `industries_information.csv` – raw industry metadata.
- `README.md` – project overview and usage instructions.

---

## Tools & Libraries

- **Language:** Python 3.x  
- **Core libraries:**
  - `pandas` – data loading, cleaning and feature engineering
  - `numpy` – numerical helpers
  - `matplotlib` / `seaborn` – optional exploratory plots
- **Environment:** Jupyter Notebook

---

## How to Use

1. Clone the repository:

   ```bash
   git clone https://github.com/Kimuyu-Charles/Data-Collection-Wrangling-Feature-Engineering.git
   cd Data-Collection-Wrangling-Feature-Engineering
