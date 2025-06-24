ETL Pipeline Midterm Project
Project Overview
This project implements an ETL (Extract, Transform, Load) pipeline for processing sales data as part of the DSA 2040 Data Warehousing and Mining midterm exam. It processes raw_data.csv (100 orders) and incremental_data.csv (10 orders), addressing data quality issues, enriching data, and loading results into SQLite databases for analysis. A visualization of sales by product provides insights.
ETL Phases
Extract (etl-extract.ipynb)

Tasks:
Loads raw_data.csv and incremental_data.csv.
Inspects with head() and info().
Observes missing values (e.g., customer_name, quantity), duplicates (order ID 4 in raw data), and incorrect data types (order_date as object).
Saves raw copies to data/.


Output: Datasets saved, issues documented.

Transform (etl_transform.ipynb)

Tasks:
Applies four transformations:
Cleaning: Fills missing values (customer_name → “Unknown”, quantity → 1, unit_price → median, order_date → “2024-01-01”, region → “Unknown”); removes duplicates.
Enrichment: Adds total_price = quantity * unit_price.
Structural: Converts order_date to datetime, extracts month.
Categorization: Creates price_category (Low: <500, Medium: 500-1499, High: ≥1500).


Shows before-and-after for each transformation.
Visualizes total sales by product (bonus).


Output: Saves transformed_full.csv and transformed_incremental.csv to data/transformed/.
Visualization:

Load (etl_load.ipynb)

Tasks:
Loads transformed data into SQLite databases (full_data.db, incremental_data.db).
Verifies with SQL queries (SELECT * FROM table LIMIT 5).


Output: Databases saved to loaded/.

Tools Used

Python: Core programming.
Pandas: Data manipulation.
SQLite3: Database storage.
Matplotlib: Visualization.
Jupyter Notebook: Development environment.

How to Run

Clone the repository:git clone https://github.com/<your-username>/DSA2040A_ETL_Midterm_Innocent_513.git


Install dependencies:pip install pandas matplotlib


Navigate to ETL_Midterm_Innocent_513/.
Run notebooks in order:
etl-extract.ipynb
etl_transform.ipynb
etl_load.ipynb


Verify outputs in data/transformed/, loaded/, and sales_by_product.png.

Screenshot
