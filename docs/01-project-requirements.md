# Project Requirements — RetailHub Analytics Lakehouse

## 1. Business Background

RetailHub is a fictional retail company that sells products through physical stores and an online channel.

The business generates operational data across customers, products, stores, orders, order items, payments, and returns. This data must be consolidated and transformed into reliable analytical datasets to support business decision-making.

The project simulates a real-world data engineering environment in which source data arrives in batches, records may be updated or delivered late, and data quality issues must be identified before the data reaches reporting layers.

## 2. Problem Statement

RetailHub requires a centralized analytical platform to integrate operational data, maintain data quality, process changes efficiently, and provide consistent business metrics.

Without a structured data pipeline, the business may experience:

- Inconsistent sales and order reporting.
- Duplicate or incomplete records.
- Incorrect financial calculations.
- Unresolved relationships between source entities.
- Difficulty processing new and updated records.
- Limited visibility into product, customer, store, and return performance.

The solution will implement a lakehouse architecture that addresses these challenges through staged data processing, validation, incremental updates, dimensional modeling, and analytics-ready outputs.

## 3. Project Objectives

The primary objectives are to:

1. Generate realistic, reproducible synthetic retail datasets.
2. Ingest source files into a Bronze layer while preserving raw data and lineage.
3. Clean, standardize, deduplicate, and validate records in the Silver layer.
4. Quarantine invalid records with traceable failure reasons.
5. Implement incremental processing for inserts, updates, and late-arriving data.
6. Build Gold dimension and fact tables for analytical queries.
7. Apply consistent definitions for sales, orders, returns, and payments.
8. Orchestrate data processing through Databricks Workflows.
9. Expose reusable analytical views for reporting.
10. Connect the analytical layer to Power BI.
11. Validate correctness through automated tests and reconciliation checks.

## 4. Project Scope

### 4.1 In Scope

- Seven synthetic source entities: customers, products, stores, orders, order items, payments, and returns.
- Configurable development and scale-test data volumes.
- File-based batch ingestion from Azure Data Lake Storage Gen2.
- Bronze, Silver, and Gold Delta tables.
- Schema enforcement and data type standardization.
- Business-key deduplication and deterministic record selection.
- Data quality checks and invalid-record quarantine.
- Incremental processing and Delta Lake merge operations.
- Slowly Changing Dimension Type 2 for selected dimensions.
- Star-schema dimensional modeling.
- Sales, customer, product, store, payment, and returns analytics.
- Databricks Workflows orchestration.
- Databricks SQL views and Power BI reporting.
- Automated tests, reconciliation, and GitHub documentation.

### 4.2 Out of Scope for the Initial Implementation

- Integration with real production retail systems.
- Real customer information or payment credentials.
- Production financial accounting or tax compliance.
- Real-time streaming as a mandatory requirement.
- Machine learning, demand forecasting, and recommendation engines.
- Production-grade disaster recovery and enterprise service-level commitments.

These features may be considered as future enhancements.

## 5. Source Data Requirements

The solution will process the following entities:

| Entity | Purpose |
|---|---|
| Customers | Customer profiles and segmentation |
| Products | Product catalog, categories, brands, and pricing |
| Stores | Store locations, regions, and operational status |
| Orders | Order dates, channels, statuses, and customer relationships |
| Order Items | Product-level quantities, discounts, taxes, and sales amounts |
| Payments | Payment transactions, amounts, and outcomes |
| Returns | Returned quantities, refund amounts, and reasons |

Each entity will have a defined business key and documented schema. Related records must be validated against their parent entities.

## 6. Functional Requirements

### FR-01: Synthetic Data Generation

The system must generate configurable, reproducible datasets with valid entity relationships and realistic business distributions.

### FR-02: Raw Data Ingestion

The system must ingest source files into Bronze Delta tables and preserve source-file and ingestion metadata.

### FR-03: Data Transformation

The system must standardize data types, clean values, derive financial measures, and prepare validated Silver datasets.

### FR-04: Data Quality Management

The system must detect duplicates, invalid values, missing mandatory fields, and broken relationships. Invalid records must be quarantined with actionable failure reasons.

### FR-05: Incremental Processing

The system must support new records, updated records, duplicate deliveries, and late-arriving data without unnecessarily reprocessing the entire dataset.

### FR-06: Historical Tracking

Selected dimensions must maintain historical versions using SCD Type 2 where business history is required.

### FR-07: Analytical Modeling

The system must produce dimension and fact tables with explicitly defined grain, keys, relationships, and measures.

### FR-08: Business Metrics

The system must implement documented calculations for sales, orders, units sold, average order value, returns, refunds, and payment outcomes.

### FR-09: Pipeline Orchestration

The system must execute processing stages in the correct dependency order and make failures observable.

### FR-10: Reporting

The system must expose analytics-ready datasets for Databricks SQL and Power BI.

### FR-11: Testing and Reconciliation

The system must validate record counts, key uniqueness, referential integrity, financial calculations, and incremental-processing correctness.

## 7. Non-Functional Requirements

### NFR-01: Scalability

The design must support small development datasets and larger scale-test datasets without requiring a redesign of the entire pipeline.

### NFR-02: Reliability

Rerunning a batch must not create duplicate business records or double-count financial measures.

### NFR-03: Data Traceability

Records must be traceable to their source files and ingestion batches wherever the source provides sufficient information.

### NFR-04: Maintainability

Code must be organized into reusable modules with clear configuration, documented business rules, and consistent naming conventions.

### NFR-05: Data Quality

Critical validation failures must be detectable and must not silently flow into trusted analytical outputs.

### NFR-06: Security

The repository must not contain production credentials, secrets, or real personal data.

### NFR-07: Reproducibility

Synthetic datasets and automated tests must use controlled configuration and random seeds.

### NFR-08: Observability

Pipeline runs should report processed counts, rejected records, duplicate counts, reconciliation outcomes, execution duration, and failures.

## 8. Development Data Volumes

| Entity | Development | Scale Test |
|---|---:|---:|
| Customers | 1,000 | 50,000 |
| Products | 500 | 5,000 |
| Stores | 20 | 100 |
| Orders | 10,000 | 1,000,000 |
| Order Items | 25,000–40,000 | 2,500,000–4,000,000 |
| Payments | Approximately 10,000 | Approximately 1,000,000 |
| Returns | 1,000–1,500 | 100,000–150,000 |

Development data will be validated first. Scale testing will begin only after the smaller dataset passes the required checks.

## 9. Acceptance Criteria

The project will be considered functionally complete when the following criteria are demonstrated:

- [ ] All seven source entities can be generated with the documented schemas.
- [ ] Source data can be ingested into Bronze tables with lineage metadata.
- [ ] Silver transformations enforce the defined business rules.
- [ ] Invalid records are quarantined with traceable reasons.
- [ ] Valid records satisfy key uniqueness and relationship checks.
- [ ] Gold facts and dimensions follow their documented grains.
- [ ] Sales and financial metrics reconcile with their source calculations.
- [ ] Incremental inserts and updates are processed correctly.
- [ ] Repeated delivery of the same data does not double-count records.
- [ ] Late-arriving records are handled according to the documented strategy.
- [ ] Historical dimension changes are correctly represented where SCD Type 2 applies.
- [ ] Analytical SQL queries return results consistent with the documented KPI definitions.
- [ ] Power BI can consume the intended analytical datasets.
- [ ] Automated tests and pipeline validation results are documented.

## 10. Assumptions and Constraints

- All source data is synthetic.
- The initial ingestion pattern is file-based batch processing.
- Azure and Databricks resource availability may affect which cloud features can be demonstrated.
- Actual scale-test performance will depend on compute configuration and data layout.
- Source-file arrival does not automatically imply that a record has been deleted.
- Business rules for cancellations, returns, refunds, and sales eligibility must remain consistent across the Gold layer and reporting.

## 11. Expected Deliverables

1. Project requirements and architecture documentation.
2. Python synthetic data generator.
3. Source data dictionary and dimensional model.
4. Bronze, Silver, and Gold processing notebooks or scripts.
5. Data quality and quarantine implementation.
6. Incremental-processing logic and tests.
7. Databricks SQL analytical views and queries.
8. Power BI report.
9. Automated tests and reconciliation results.
10. GitHub repository containing implementation code, documentation, and evidence of completed testing.
