# ETL Pipeline Project Reflection

## Introduction

This project details the development of an ETL (Extract, Transform, Load) pipeline for the DSA 2040 Data Warehousing and Mining midterm exam. The pipeline processes sales data from `raw_data.csv` (100 rows) and `incremental_data.csv` (10 rows). The core tasks included:

* Loading and inspecting datasets.
* Applying four meaningful data transformations.
* Loading the transformed results into SQLite databases.
* Documenting the entire process in this `README.md` file.
* Hosting the project in a public GitHub repository named `DSA2040A_ETL_Midterm_Innocent_513`.
* Including a data visualization for bonus marks.

This reflection discusses the project's approach, skills applied, challenges faced, lessons learned, and how it deepened my understanding of data warehousing concepts.


## Project Approach and Understanding

The ETL pipeline was modularized into three distinct Jupyter notebooks for clarity and ease of debugging:

* `etl-extract.ipynb`
* `etl_transform.ipynb`
* `etl_load.ipynb`

Each phase was designed to meet exam requirements while adhering to data engineering best practices.

### Extract Phase

**Objective:** Load and inspect `raw_data.csv` and `incremental_data.csv`, document data quality issues, and save raw copies.

**Approach:**

* Used **pandas** to load CSVs into DataFrames.
* Displayed `.head()` and `.info()` to examine dataset structure.
* Checked for duplicates with `.duplicated()` and missing values with `.isnull().sum()`.
* Saved raw copies to the `data/` directory to preserve originals.

**Observations:**

* `raw_data.csv` had one duplicate (`order_id 4`) and missing values in `customer_name`, `quantity`, `unit_price`, `order_date`, and `region`.
* `incremental_data.csv` had similar missing values but no duplicates.

**Understanding:** This phase emphasized **data profiling**. Identifying issues like missing values (e.g., 20% of `customer_name` in `raw_data.csv`) and duplicates was crucial for accurate downstream transformations. Documenting these issues informed the transformation strategy, highlighting the importance of early data quality checks in ETL pipelines.

### Transform Phase

**Objective:** Apply four distinct transformations (cleaning, enrichment, structural, categorization), show before-and-after states, save results, and create a visualization.

**Approach:**

* **Cleaning:**
    * Removed duplicates.
    * Filled missing values: `customer_name` → "Unknown", `quantity` and `unit_price` → median, `region` → "Unknown", `order_date` → mode.
* **Enrichment:** Added `total_price` = `quantity` * `unit_price` for sales analysis.
* **Structural:** Converted `order_date` to datetime objects and extracted the `month` for temporal insights.
* **Categorization:** Created `price_category` (Low: <500, Medium: 500-1500, High: >1500) to segment orders.

* Printed before-and-after states using `print()` for transparency.
* Saved transformed results to `data/transformed/transformed_full.csv` and `data/transformed/transformed_incremental.csv`.
* **Bonus:** Generated a bar chart of total sales by product using **matplotlib**, saved as `data/transformed/sales_by_product.png`.

**Understanding:** This was the most complex phase, requiring strategic transformation choices. Using the median for numerical missing values avoided outlier bias, while duplicate removal ensured data accuracy. The `total_price` column enabled financial analysis, and datetime conversion supported temporal queries. The visualization revealed product performance trends (e.g., Laptops vs. Tablets), demonstrating how transformations unlock analytical value.

### Load Phase

**Objective:** Load transformed data into SQLite databases and verify with SQL queries.

**Approach:**

* Used **sqlite3** to create `full_data.db` and `incremental_data.db` in the `loaded/` directory.
* Loaded DataFrames using `to_sql()` with `if_exists='replace'`.
* Verified data integrity with `SELECT * FROM table LIMIT 5` queries, displaying the results.

**Understanding:** This phase highlighted the role of structured storage in data warehousing. SQLite's simplicity suited the project, and SQL verification ensured data integrity. The load phase bridged the pipeline to business intelligence applications, where databases enable efficient querying and reporting.


## Documentation and Version Control

**Objective:** Create a clear `README.md` and host the project on GitHub with logical commits.

**Approach:**

* Wrote a comprehensive `README.md` with sections for project overview, ETL phases, tools used, run instructions, and a visualization screenshot.
* Initialized a Git repository and made logical, descriptive commits (e.g., "Complete extract phase", "Add transformations and visualization").
* Pushed the project to a public GitHub repository: [DSA2040A\_ETL\_Midterm\_Innocent\_513](https://github.com/Innocent-Chibike/DSA2040A_ETL_Midterm_Innocent_513).

**Understanding:** Clear documentation ensures reproducibility and accessibility. Logical Git commits tracked progress effectively, making the project professional and organized—a critical skill for collaborative data engineering.


## Skills Applied

This project allowed me to apply and strengthen several key skills:

* **Python and Pandas:** Proficiently used functions like `read_csv()`, `fillna()`, `to_datetime()`, `groupby()`, and more for robust data processing.
* **Matplotlib:** Created a clear and insightful bar chart for sales analysis.
* **SQLite:** Managed database creation and performed SQL querying for data verification.
* **Jupyter Notebooks:** Organized code effectively with Markdown headers for enhanced readability and clarity.
* **Git and GitHub:** Applied version control best practices, including logical commits and repository management.
* **Data Quality Analysis:** Addressed missing values and duplicates systematically, ensuring robust ETL processes.


## Challenges Faced

During the project, I encountered and successfully navigated several challenges:

* **Data Quality:** Significant missing values (e.g., in `customer_name`) and a duplicate entry in `raw_data.csv` required careful handling. My decision to use median imputation for numerical columns, rather than the mean, was a nuanced choice made to avoid outlier bias.
* **Transformation Design:** Ensuring four distinct and meaningful transformations (cleaning, enrichment, structural, categorization) was challenging. I focused on selecting transformations that added clear analytical value without significant overlap.
* **Visualization:** Configuring **matplotlib** to produce a clear, properly sized, and saved bar chart required adjustments to settings like `figsize` and `tight_layout`.
* **File Paths:** Using relative paths (e.g., `data/raw_data.csv`) necessitated ensuring the correct folder structure with `os.makedirs()` to prevent runtime errors.


## Lessons Learned

This project provided invaluable lessons that significantly deepened my understanding of data warehousing principles:

* **ETL Importance:** Each phase of the ETL process is critical—**extract** identifies initial data issues, **transform** prepares and refines the data, and **load** enables efficient querying and reporting.
* **Data Quality:** Early data profiling is paramount for preventing downstream errors. For instance, observing `order_date` as an object type in the extract phase immediately prompted its conversion during transformation.
* **Transformation Strategy:** Context-driven choices (e.g., using median vs. mean for imputation) are key to maintaining data integrity and accuracy.
* **Documentation:** Clear and comprehensive Markdown documentation, especially in the `README.md` file, significantly enhances project accessibility and reproducibility, a vital skill in data engineering.
* **Version Control:** Logical and descriptive Git commits greatly improve project traceability and facilitate collaboration.
* **Visualization:** Visualizations, such as the "sales by product" chart, provide actionable insights, reinforcing the direct business value derived from well-executed ETL processes.


## Connection to Data Warehousing

This project directly mirrors real-world data warehousing processes:

* **Extract:** Simulates the process of pulling raw data from various source systems (e.g., a CRM or transactional database).
* **Transform:** Represents the core warehousing task of cleaning, standardizing, and preparing data for consistency and analytical use.
* **Load:** Analogous to storing the prepared data in a structured format within a data warehouse for efficient querying.
* **Visualization:** Supports **business intelligence** by revealing trends and patterns, which is a key outcome of a well-designed data warehouse.

Handling issues like missing values and duplicates in this project provided practical experience crucial for building scalable and reliable data pipelines.


## Improvements for Future Projects

Based on this experience, I've identified several areas for improvement in future ETL projects:

* **Additional Transformations:** Explore normalizing product names or aggregating sales data by region for even deeper insights.
* **Error Handling:** Implement `try-except` blocks to create more robust file and database operations, making the pipeline more resilient to unexpected issues.
* **Advanced Visualization:** Utilize libraries like **Plotly** for interactive and more dynamic data visualizations.
* **Automation:** Develop a script to automate the sequential execution of the entire ETL pipeline, improving efficiency and repeatability.


## Conclusion

This ETL pipeline project was an invaluable learning experience that significantly reinforced my understanding of fundamental data warehousing concepts, including data quality, transformation methodologies, and structured data storage. By actively addressing real-world challenges and producing a meaningful visualization, I gained practical proficiency in key tools like **Python**, **Pandas**, **SQLite**, and **Git**. The organized GitHub repository and clear documentation further prepared me for professional data engineering tasks. I am excited to apply these enhanced skills in future data projects.
