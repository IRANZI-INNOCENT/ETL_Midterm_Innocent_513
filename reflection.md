ETL Pipeline Project Reflection
Introduction
For the DSA 2040 Data Warehousing and Mining midterm exam, I developed an ETL (Extract, Transform, Load) pipeline to process sales data from raw_data.csv (100 rows) and incremental_data.csv (10 rows). The project involved loading and inspecting datasets, applying four meaningful transformations, loading results into SQLite databases, documenting the process in a README.md, and hosting the project in a public GitHub repository named DSA2040A_ETL_Midterm_Innocent_513. A visualization was included for bonus marks. This reflection discusses my approach, skills applied, challenges faced, lessons learned, and how the project deepened my understanding of data warehousing concepts.
Project Approach and Understanding
The ETL pipeline was modularized into three Jupyter notebooks (etl-extract.ipynb, etl_transform.ipynb, etl_load.ipynb) for clarity and ease of debugging. Each phase was designed to meet exam requirements while adhering to data engineering best practices.
Extract Phase
Objective: Load and inspect raw_data.csv and incremental_data.csv, document data quality issues, and save raw copies.
Approach:

Used pandas to load CSVs into DataFrames.
Displayed .head() and .info() to examine structure.
Checked for duplicates with duplicated() and missing values with isnull().
Observations: raw_data.csv had one duplicate (order_id 4) and missing values in customer_name, quantity, unit_price, order_date, and region. incremental_data.csv had similar missing values but no duplicates.
Saved raw copies to data/ to preserve originals.

Understanding:This phase emphasized data profiling. Identifying issues like missing values (e.g., 20% of customer_name in raw_data.csv) and duplicates ensured accurate downstream transformations. Documenting these issues informed the transformation strategy, highlighting the importance of early data quality checks in ETL pipelines.
Transform Phase
Objective: Apply four transformations (cleaning, enrichment, structural, categorization), show before-and-after states, save results, and create a visualization.
Approach:

Cleaning: Removed duplicates and filled missing values (customer_name → "Unknown", quantity and unit_price → median, region → "Unknown", order_date → mode).
Enrichment: Added total_price = quantity * unit_price for sales analysis.
Structural: Converted order_date to datetime and extracted month for temporal insights.
Categorization: Created price_category (Low: <500, Medium: 500-1500, High: >1500) to segment orders.


Printed before-and-after states using print() for transparency.
Saved results to data/transformed/transformed_full.csv and data/transformed/transformed_incremental.csv.
Bonus: Generated a bar chart of total sales by product using matplotlib, saved as data/transformed/sales_by_product.png.

Understanding:This phase was the most complex, requiring strategic transformation choices. Using the median for numerical missing values avoided outlier bias, while duplicate removal ensured data accuracy. The total_price column enabled financial analysis, and datetime conversion supported temporal queries. The visualization revealed product performance trends (e.g., Laptops vs. Tablets), demonstrating how transformations unlock analytical value.
Load Phase
Objective: Load transformed data into SQLite databases and verify with SQL queries.
Approach:

Used sqlite3 to create full_data.db and incremental_data.db in loaded/.
Loaded DataFrames using to_sql() with if_exists='replace'.
Verified with SELECT * FROM table LIMIT 5 queries, displaying results.

Understanding:This phase highlighted the role of structured storage in data warehousing. SQLite’s simplicity suited the project, and SQL verification ensured data integrity. The load phase bridged the pipeline to business intelligence applications, where databases enable efficient querying and reporting.
Documentation and Version Control
Objective: Create a clear README.md and host the project on GitHub with logical commits.
Approach:

Wrote a README.md with sections for overview, ETL phases, tools, run instructions, and visualization screenshot.
Initialized a Git repository and made logical commits (e.g., "Complete extract phase", "Add transformations and visualization").
Pushed to a public GitHub repository: DSA2040A_ETL_Midterm_Innocent_513.

Understanding:Clear documentation ensures reproducibility and accessibility. Logical Git commits tracked progress, making the project professional and organized, a critical skill for collaborative data engineering.
Skills Applied

Python and Pandas: Used read_csv(), fillna(), to_datetime(), groupby(), and other functions for data processing.
Matplotlib: Created a clear bar chart for sales analysis.
SQLite: Managed database creation and SQL querying.
Jupyter Notebooks: Organized code with Markdown headers for clarity.
Git and GitHub: Applied version control best practices with logical commits.
Data Quality Analysis: Addressed missing values and duplicates, ensuring robust ETL processes.

Challenges Faced

Data Quality: Significant missing values (e.g., customer_name) and a duplicate in raw_data.csv required careful handling. I chose median imputation for numerical columns to avoid outlier bias, which was a nuanced decision.
Transformation Design: Ensuring four distinct transformations (cleaning, enrichment, structural, categorization) was challenging. I selected transformations that added analytical value without overlap.
Visualization: Configuring matplotlib for a clear, saved bar chart required adjusting settings like figsize and tight_layout.
File Paths: Using relative paths (e.g., data/raw_data.csv) required ensuring folder structure with os.makedirs() to avoid errors.

Lessons Learned

ETL Importance: Each phase is critical—extract identifies issues, transform prepares data, and load enables querying.
Data Quality: Early profiling prevents downstream errors. For example, noting order_date as object prompted its conversion.
Transformation Strategy: Context-driven choices (e.g., median vs. mean) are key to maintaining data integrity.
Documentation: Clear Markdown and README.md enhance project accessibility, a vital data engineering skill.
Version Control: Logical commits improve traceability and collaboration.
Visualization: Visuals like sales by product provide actionable insights, reinforcing ETL’s business value.

Connection to Data Warehousing
This project mirrors real-world data warehousing:

Extract: Simulates pulling data from source systems (e.g., CRM).
Transform: Prepares data for consistency and analysis, a core warehousing task.
Load: Stores data in a structured format for querying, akin to a data warehouse.
Visualization: Supports business intelligence by revealing trends, a key warehousing outcome.

Handling issues like missing values and duplicates prepared me for building scalable data pipelines.
Improvements for Future Projects

Additional Transformations: Normalize product names or aggregate sales by region for deeper insights.
Error Handling: Add try-except blocks for robust file and database operations.
Advanced Visualization: Use Plotly for interactive plots.
Automation: Create a script to run the pipeline sequentially.

Conclusion
This ETL pipeline project was a valuable learning experience, reinforcing data warehousing concepts like data quality, transformation, and structured storage. By addressing challenges and producing a visualization, I gained practical skills in Python, Pandas, SQLite, and Git. The organized GitHub repository and clear documentation prepared me for professional data engineering tasks. I’m excited to apply these skills in future projects.
