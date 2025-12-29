# Movie Data Analysis

A focused, reproducible data-analysis project that integrates multiple movie data sources (IMDb, Rotten Tomatoes, and financial records) to produce a cleaned, analysis-ready dataset and notebooks for exploration, visualization and basic modeling.

## Project Summary

- Purpose: Integrate and clean movie metadata and financials, produce derived features (ROI, normalized ratings, decade, genre flags), and analyze relationships between budget, ratings and box-office performance.
- Status: Notebooks and cleaned CSVs are present in the repo under the `data/` folder and top-level notebooks; update and extend as needed.

## Repository Structure

- `data/` — raw and processed CSVs:
  - `imdb_data.csv`
  - `rotten_tomatoes_movies.csv`
  - `movies_financial.csv`
  - `movies_dataset_final.csv`
  - `movies_project_final_dataset.csv`
- Notebooks:
  - `web_scrapping.ipynb` — optional code used to fetch supplemental data.
  - `data_integration.ipynb` — main integration and reconciliation pipeline that produces `movies_dataset_final.csv`.
  - `Data_preprocessing.ipynb` — cleaning, imputations, normalization, and feature engineering.
  - `Analysis.ipynb` — exploratory analysis, plots, summary tables and answers to analytical questions.
- `README.md` — this document.

## How to Reproduce (Workflow)

Run notebooks in this order:

1. `web_scrapping.ipynb` (optional) — refresh external scraping sources only if needed.
2. `data_integration.ipynb` — harmonize sources, match titles/years, resolve duplicates, and create unified dataset.
3. `Data_preprocessing.ipynb` — standardize types, handle missingness, convert currencies/units, and compute derived fields.
4. `Analysis.ipynb` — produce charts, tables and findings.

Notebooks are designed so that outputs of integration → preprocessing are consumed by analysis for reproducibility.

## Datasets & Key Fields

**Source files:**
- IMDb extract: basic metadata (title, year, runtime, genres, IMDb rating, votes).
- Rotten Tomatoes: critic and audience scores and counts.
- Financials: production budget, domestic/international box office, distributor/studio info.

**Typical columns included or derived:**
- `title`, `year`, `original_title`
- `imdb_rating`, `imdb_votes`
- `rt_critic_score`, `rt_critic_count`, `rt_audience_score`, `rt_audience_count`
- `budget`, `box_office_domestic`, `box_office_international`, `revenue_total`
- `ROI` (derived; e.g., (revenue - budget) / budget)
- `genres` (comma-separated), `genre_<name>` flags (exploded/one-hot)
- `runtime_minutes`, `release_date`, `decade`
- `production_companies`, `director`, `top_cast` (as available)

Note: column names may vary between source files; check the integration notebook for exact schema used in this project.

## Integration & Preprocessing Highlights

- **Title/ID matching**: fuzzy title matching combined with year matching to align records across sources.
- **Normalization**: standardize currency (USD), numeric types, and rating scales.
- **Missing data**: documented imputation strategies (median/mean for numeric fields, "Unknown" for categorical, or drop where appropriate) and removal thresholds are in `Data_preprocessing.ipynb`.
- **De-duplication**: prioritize entries with richer metadata or higher vote counts when duplicates exist.
- **Derived features**: ROI, normalized rating (combined score), release decade, genre flags, and budget buckets.

## Analyses Included

- Revenue vs. ratings (IMDb vs. RT vs. audience)
- Budget vs. ROI distribution and budget buckets analysis
- Genre trends over time and ROI by genre
- Studio/distributor profitability and consistent performers
- Basic predictive experiments (e.g., simple regression/classifier for revenue/ROI using pre-release features)

## Visualizations & Outputs

The `Analysis.ipynb` generates:
- Time series of production counts and median budgets per decade
- Scatter plots of budget vs. revenue and budget vs. ROI
- Boxplots of ROI by genre and by budget bucket
- Correlation heatmaps for numeric features
- Exported figures and summary CSVs as artifacts for reporting

## Recommendations & Next Steps

- Add a `requirements.txt` to pin library versions (pandas, numpy, matplotlib, seaborn, scikit-learn, jupyter, beautifulsoup4, requests, tqdm, openpyxl).
- Add a `LICENSE` (MIT suggested) and `CONTRIBUTING.md` if you plan to accept external contributions.
- Add lightweight data validation tests (e.g., assert non-negative budgets where present, check date ranges) and a CI workflow that runs core notebook cells or scripts.
- Consider exposing a small script that runs the integration + preprocessing pipeline headlessly (a Python script or Makefile) to avoid manual notebook execution.

## Contributing

- To propose changes: open an issue describing the change, fork the repo, create a feature branch, update notebooks or code, and submit a PR.
- When adding data sources or dependencies, update `README.md` and `requirements.txt` accordingly.

## License & Attribution

- Add a `LICENSE` file when publishing (MIT recommended for general sharing).
- Respect data source terms of use and include attribution for IMDb, Rotten Tomatoes and other sources where required.

## Contact / Author

- Your Name — update this with your GitHub profile or preferred contact method.
