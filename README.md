# RetailHub Analytics Lakehouse

An end-to-end retail analytics lakehouse built with Azure Databricks, PySpark, Delta Lake, SQL, and Power BI.

## Project Overview

RetailHub is a fictional retail business that operates through physical stores and online channels. Its operational data is distributed across multiple entities, including customers, products, stores, orders, payments, and returns.

This project aims to build a scalable data engineering solution that ingests raw data, applies data quality rules, processes incremental changes, and transforms the data into analytics-ready datasets for business reporting.

The project follows the Medallion Architecture, separating data processing into Bronze, Silver, and Gold layers.

## Business Objectives

- Consolidate retail data from multiple source entities.
- Build reliable batch and incremental data pipelines.
- Implement data validation, deduplication, and error quarantine.
- Apply dimensional modeling for analytical workloads.
- Develop reusable SQL-based business metrics.
- Enable business reporting through Power BI.
- Demonstrate data engineering best practices through a documented, testable, version-controlled project.

## Architecture

**Planned data flow:**

Python Synthetic Data Generator → Azure Data Lake Storage Gen2 → Azure Databricks Auto Loader → Bronze Delta Tables → Silver Delta Tables → Gold Dimensions and Facts → Databricks SQL → Power BI

The implementation will include incremental processing, data quality checks, pipeline orchestration, and reconciliation.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Synthetic data generation and supporting utilities |
| Azure Data Lake Storage Gen2 | Source file storage |
| Azure Databricks | Distributed data processing |
| PySpark | Data transformations and validation |
| Delta Lake | Reliable lakehouse tables and merge operations |
| Spark SQL / Databricks SQL | Transformations and analytical queries |
| Unity Catalog | Data governance and organization |
| Databricks Workflows | Pipeline orchestration |
| Power BI | Business intelligence and reporting |
| Git and GitHub | Version control and project documentation |

## Data Sources

The project uses seven synthetic source entities:

1. Customers
2. Products
3. Stores
4. Orders
5. Order Items
6. Payments
7. Returns

The generator will produce reproducible development data, configurable larger datasets, and controlled data-quality issues for testing.

## Medallion Architecture

### Bronze Layer

- Ingest raw source files into Delta tables.
- Preserve source values and ingestion metadata.
- Support traceability and reprocessing.

### Silver Layer

- Apply data types and standardization.
- Deduplicate records using defined business rules.
- Validate business keys and relationships.
- Derive financial amounts and quarantine invalid records.

### Gold Layer

- Build analytical dimensions and fact tables.
- Implement historical dimension tracking where required.
- Publish datasets for sales, customers, products, stores, payments, and returns analysis.

## Planned Analytics

The solution will support analysis of:

- Gross merchandise value and net sales.
- Order volumes, units sold, and average order value.
- Product, category, and brand performance.
- Customer purchasing and repeat-order behavior.
- Store, region, and sales-channel performance.
- Return rates, refund amounts, and return reasons.
- Payment success and failure rates.

Business metric definitions and exclusions will be documented to avoid inconsistent reporting.

## Repository Structure

```text
retail-analytics-databricks/
├── README.md
├── docs/
├── data_generator/
├── config/
├── notebooks/
├── sql/
├── tests/
└── .github/
    └── workflows/
```

The detailed documentation and implementation files will be added as the project progresses.

## Implementation Roadmap

1. Document business requirements and data architecture.
2. Define source schemas, data models, and business rules.
3. Implement and validate the Python synthetic data generator.
4. Ingest source files into Bronze Delta tables.
5. Build Silver transformations and data quality checks.
6. Implement incremental processing and historical tracking.
7. Build Gold dimensions and fact tables.
8. Develop analytical SQL views and validate business metrics.
9. Orchestrate the pipeline and connect Power BI.
10. Add automated tests and document the completed implementation.

## Data and Security

All generated data is synthetic and intended for learning and demonstration. No real customer records or production credentials should be committed to the repository.

Environment-specific configuration and credentials will be kept separate from source code.

## Project Status

**Current stage:** Documentation and design.

Implementation details, test results, architecture diagrams, and dashboard screenshots will be added as they are completed and validated.
