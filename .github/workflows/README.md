# CI/CD Workflows

Automated CI/CD workflows via GitHub Actions are currently not implemented for this repository.

## Rationale

This project is a dedicated Data Engineering and Analytics Engineering portfolio demonstration developed and executed interactively within a Databricks Lakehouse workspace using Databricks Notebooks, Unity Catalog Volumes, and Delta Lake.

## Potential Future CI/CD Integrations

Future production-grade automation enhancements could include:

1. **Databricks Asset Bundles (DABs):** Automating deployment of workspace assets, permissions, and job schedules across staging and production environments.
2. **Databricks CLI / GitHub Actions Runners:** Triggering automated integration runs of `notebooks/sales_payments_data_modeling.ipynb` on dedicated test compute pools upon pull requests.
3. **Data Quality & Testing CI Gate:** Integrating schema assertion checks, data contracts, and transformation unit tests using frameworks such as `pytest` and `Great Expectations` before merging changes.
