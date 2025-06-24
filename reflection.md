ETL Pipeline Project Reflection
Introduction
As part of the DSA 2040 Data Warehousing and Mining midterm exam, I developed an ETL (Extract, Transform, Load) pipeline to process sales data from two datasets: raw_data.csv (100 rows) and incremental_data.csv (10 rows). This project required loading and inspecting the datasets, applying at least four meaningful transformations, loading the results into SQLite databases, documenting the process in a clear README.md, and hosting the project in a public GitHub repository (DSA2040A_ETL_Midterm_Innocent_513). Additionally, I included a visualization for bonus marks. This reflection outlines my approach, the skills I applied, challenges faced, lessons learned, and how the project deepened my understanding of data warehousing concepts.
Project Approach and Understanding
The ETL pipeline was structured into three Jupyter notebooks (etl-extract.ipynb, etl_transform.ipynb, etl_load.ipynb) to modularize the process, making it easier to debug and present. Each phase was designed to meet specific requirements while demonstrating best practices in data engineering.
Extract Phase
Objective: Load and inspect raw_data.csv and incremental_data.csv, document data quality issues, and save raw copies.Approach: I used pandas to read the CSV files into DataFrames, leveraging head() and info() to preview the data and assess its structure. I checked for duplicates using duplicated() and noted issues like missing values and incorrect data types. For example, I observed that raw_data.csv had a duplicate order_id (ID 4) and missing values in columns like customer_name and unit_price, while incremental_data.csv had similar issues but no duplicates. Saving raw copies ensured data integrity.Understanding: This phase taught me the importance of data profiling. By examining the datasets’ structure (e.g., 100 rows in raw data, object-type order_date), I identified issues that could affect downstream analysis, such as missing values skewing calculations or duplicates inflating sales figures. Documenting these observations was critical for planning transformations.
Transform Phase
Objective: Apply four transformations (cleaning, enrichment, structural, categorization), show before-and-after, save transformed data, and create a visualization.Approach: I implemented:

Cleaning: Filled missing values (e.g., customer_name → “Unknown”, unit_price → median) and removed duplicates to ensure data quality.
Enrichment: Added total_price = quantity * unit_price to enable sales analysis.
Structural: Converted order_date to datetime and extracted month for temporal analysis.
Categorization: Created price_category (Low, Medium, High) based on total_price thresholds to segment orders.I used print statements to show column states and data snippets before and after each transformation, ensuring transparency. The transformed data was saved to data/transformed/. For the bonus, I created a bar chart of total sales by product using matplotlib, saved as sales_by_product.png.Understanding: This phase was the most complex, requiring thoughtful transformation choices. Cleaning missing values with the median for unit_price avoided bias, while removing duplicates ensured accuracy. The total_price column added analytical value, and datetime conversion enabled time-based insights. The visualization revealed product performance (e.g., Laptops vs. Tablets), highlighting the power of data transformation in uncovering trends.

Load Phase
Objective: Load transformed data into SQLite databases and verify with SQL queries.Approach: I used sqlite3 to create two databases (full_data.db and incremental_data.db) in the loaded/ folder. The to_sql() method stored the DataFrames, and I verified the data with SELECT * FROM table LIMIT 5 queries, displaying results to confirm successful loading.Understanding: Loading data into a database emphasized the importance of structured storage for querying. SQLite’s lightweight nature made it ideal for this project, and verifying with SQL queries ensured the data was accessible and correct. This phase connected the pipeline to real-world applications, where databases support business intelligence.
Documentation and Version Control
Objective: Create a clear README.md and host the project on GitHub with logical commits.Approach: The README.md included sections for overview, ETL phases, tools, run instructions, and the visualization screenshot. I initialized a Git repository, made incremental commits (e.g., “Complete extract phase”), and pushed to a public GitHub repository (DSA2040A_ETL_Midterm_Innocent_513).Understanding: Clear documentation and version control are essential for collaboration and reproducibility. The README.md served as a guide for graders, while Git commits tracked my progress, making the project professional and organized.
Skills Applied

Python and Pandas: Used for data loading, transformation, and analysis. I leveraged pandas functions like read_csv(), fillna(), to_datetime(), and groupby() effectively.
Matplotlib: Created a bar chart to visualize sales, enhancing interpretability.
SQLite: Managed database creation and querying, reinforcing database skills.
Jupyter Notebooks: Structured the pipeline into clear, executable cells with Markdown for documentation.
Git and GitHub: Applied version control best practices, ensuring logical commits and a clean repository.
Data Quality Analysis: Identified and addressed issues like missing values and duplicates, critical for ETL pipelines.

Challenges Faced

Data Quality Issues: The datasets had significant missing values (e.g., 20% of customer_name in raw data) and a duplicate order_id. Deciding how to handle missing values (e.g., median for unit_price vs. mean) required balancing data integrity and analysis needs. I chose the median to avoid outliers’ influence.
Transformation Design: Selecting four meaningful transformations was challenging. I ensured each transformation (cleaning, enrichment, structural, categorization) added value and met the requirement for distinct types, avoiding overlap.
Visualization: Ensuring the bar chart was clear and saved correctly for the README.md required tweaking matplotlib settings (e.g., figsize for readability).
File Paths: Relative paths (data/raw_data.csv) needed careful setup to avoid FileNotFoundError. Creating folders (transformed/, loaded/) with os.makedirs() prevented issues.

Lessons Learned

ETL Importance: The project highlighted ETL’s role in preparing raw data for analysis. Each phase builds on the previous one, requiring careful planning to ensure a seamless pipeline.
Data Quality: Inspecting data early (extract phase) prevents issues later. For example, noting order_date as object prompted its conversion in the transform phase.
Transformation Strategy: Choosing appropriate transformations (e.g., median for unit_price) requires understanding the data’s context and analytical goals.
Documentation: Clear Markdown cells and a detailed README.md make the project accessible to others, a key skill in data engineering.
Version Control: Logical Git commits (e.g., one per phase) made the project traceable, reinforcing the value of version control in collaborative settings.
Visualization: Visualizing data (e.g., sales by product) not only earned bonus marks but also provided actionable insights, showing the practical impact of ETL.

Connection to Data Warehousing
This project directly applies data warehousing concepts:

Extract: Mirrors extracting data from source systems (e.g., CRM databases).
Transform: Reflects cleaning and enriching data for a data warehouse, ensuring consistency and usability.
Load: Simulates loading data into a data warehouse for querying and reporting.
Visualization: Aligns with business intelligence, where transformed data drives decision-making.

By addressing real-world issues like missing values and duplicates, the project prepared me for building scalable data pipelines in professional settings.
Improvements for Future Projects

Additional Transformations: I could add more transformations, like normalizing product names or aggregating sales by region, to deepen analysis.
Error Handling: Incorporating try-except blocks for file loading or database connections would make the pipeline more robust.
Advanced Visualization: Including interactive plots (e.g., using Plotly) could enhance insights.
Automation: Scripting the entire pipeline to run sequentially would streamline execution.

Conclusion
Completing this ETL pipeline was a rewarding experience that deepened my understanding of data warehousing. I learned to systematically extract, transform, and load data, addressing quality issues and adding value through transformations. The visualization provided practical insights, and the GitHub repository ensured professional delivery. This project has equipped me with skills to tackle real-world data engineering challenges, and I’m excited to apply these lessons in future coursework and professional projects.
Marks Achieved:
