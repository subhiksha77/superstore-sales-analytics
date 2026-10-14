# Superstore Sales Analytics | SQL, Python & Power BI

An end-to-end retail sales analytics portfolio project exploring sales performance, profitability, product mix, customer segments, geography, order trends, and shipping behavior using **MySQL, Python (Pandas/Matplotlib/Seaborn), and Power BI**.

> **Project status:** Source materials have been organized. Validate the analysis and add the final Power BI `.pbix` file and dashboard preview before presenting this as a finished portfolio project.

## Business objective

Turn transactional sales data into practical answers for business stakeholders:
- Which product categories and sub-categories contribute most to sales and profit?
- Which regions and states lead sales or profitability?
- What are the monthly sales trends?
- Which products and customers contribute the most sales?
- Which products generate losses or relatively weak profit despite sales?
- Which customer segments and shipping modes are most common?
- How are quantity sold and returns represented in the supplied data?

## Technology stack

- **SQL:** MySQL 8+ for aggregation, ranking, grouping, filtering, and business-question analysis.
- **Python:** Pandas for data loading and grouping; Matplotlib/Seaborn for charts.
- **BI:** Power BI for interactive KPI reporting and dashboard exploration.
- **Data source:** Excel workbook included under `data/raw/`.


## Dataset overview

The supplied workbook contains **5,901 rows and 23 columns**, with order dates from **2019-01-01 through 2020-12-31**. Fields cover order and shipping dates, shipping mode, customer and segment, location, product hierarchy, sales, quantity, profit, returns, and payment mode.

Please see [`data/README.md`](data/README.md) for observed data-quality caveats. The source workbook has blank values in `Returns`, `ind1`, and `ind2`; the first column header also appears malformed. These should be resolved or explicitly documented before treating the results as production-quality.

## Analytical workflow

1. Inspect the source** — examine row/column counts, data types, date fields, missing values, and unusual headers.
2. **Prepare the data** — validate data types, determine how blank return values should be interpreted, and exclude unusable fields only with a documented reason.
3. **Analyze in Python** — summarize sales by category and region, monthly sales, profit distribution, top products by quantity, and sales-versus-profit patterns.
4. **Answer business questions in SQL** — aggregate sales and profit by category, region, state, sub-category, customer, segment, product, month, shipping mode, and return status.
5. **Communicate in Power BI** — add the validated `.pbix` file and an exported dashboard screenshot after checking the visuals and KPI definitions.

## Business questions currently represented in the SQL/Python source

| Area | Questions / analysis |
|---|---|
| Overall performance | What are total sales and total profit? |
| Product mix | Which category has the highest sales? Which sub-category has the highest profit? |
| Geography | Which region and state lead sales? |
| Time series | How do sales change by month? |
| Product performance | Which products rank highest by sales or quantity? Which products have negative total profit? |
| Customer analysis | Which customers contribute the highest sales? |
| Segments | Which customer segment contributes the most sales? |
| Fulfilment | Which shipping mode appears most frequently? |
| Profitability | Which products have high sales but comparatively low profit? |
| Returns | How many records have each `Returns` value? Interpretation depends on the data dictionary. |

## Key findings

**Final numerical findings are intentionally not asserted in this README yet.** The supplied files contain analysis code and questions, but the notebook's outputs were not used as verified business conclusions here. Run the notebook and SQL against the same validated dataset, cross-check totals, then replace this section with 3–5 evidence-backed findings.

Use this format for each finding:
- **Finding:** [specific result with value and unit]
- **Evidence:** [query, chart, or KPI used]
- **Business implication:** [what a sales/operations team could do next]

Avoid claiming that one category, region, or product is the “best” without specifying whether the metric is sales, profit, margin, quantity, or order count.

## How to run

### Python notebook
1. Install Python 3.10+ and Jupyter.
2. Install dependencies:
   ```bash
   pip install pandas openpyxl matplotlib seaborn jupyter
   ```
3. From the repository root, launch Jupyter:
   ```bash
   jupyter notebook notebooks/superstore_sales_analysis.ipynb
   ```
4. Confirm the dataset path and run cells from top to bottom. The notebook uses a relative path to the source workbook; do not add machine-specific file paths.

### MySQL
1. Use MySQL 8+.
2. Import the workbook into a table named `sales` using MySQL Workbench's Table Data Import Wizard or a documented ETL process.
3. Confirm the table schema and row count before running `sql/superstore_sales_analysis.sql`.
4. Review the SQL script and run it in a test schema first. The script assumes that a `sales` table with compatible column names and data types already exists.

### Power BI
Open the verified `sales_analysis.pbix` file in Power BI Desktop. The uploaded dashboard attachment is an archive of Power BI package internals; see [`powerbi/README.md`](powerbi/README.md) for the required validation step.

## KPI definitions to document

- **Total Sales** = `SUM(Sales)`
- **Total Profit** = `SUM(Profit)`
- **Total Quantity** = `SUM(Quantity)`
- **Profit Margin (%)** = `SUM(Profit) / SUM(Sales) × 100` (guard against zero sales)
- **Order Count** = preferably `DISTINCTCOUNT(Order ID)` in Power BI or `COUNT(DISTINCT \`Order ID\`)` in SQL; do not use row count as order count when an order can contain multiple product rows.

Use consistent filters and the same validated source when comparing Python, SQL, and Power BI results.

## Limitations and next steps

- Confirm the intended meaning of blank `Returns` values.
- Investigate the unusual first column header and document any renamed field.
- Remove the all-empty `ind1` and `ind2` fields from analysis only after recording the decision.
- Add a data dictionary and a reproducible import/cleaning step.
- Reconcile headline metrics across Python, SQL, and Power BI.
- Add 3–5 verified findings, dashboard screenshots, and the working `.pbix` file.
- Consider adding tests or validation queries for row count, nulls, duplicate identifiers, date ranges, and metric totals.

## Security

Never commit database passwords, API keys, or personal credentials. Configure database access locally through environment variables or an ignored local configuration file. If a real password was previously committed to a public repository, rotate it immediately and remove it from the repository history.

## Author / attribution

