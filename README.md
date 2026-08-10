# Microsoft Fabric End-to-End Sales Data Engineering Project

## 📌 Project Overview

This project demonstrates an end-to-end **data engineering solution using Microsoft Fabric**, following the **Medallion Architecture**.

The project processes raw sales data through multiple stages of data ingestion, transformation, data cleaning, business transformation, and orchestration before preparing the data for analytics and reporting.

The complete data flow is:

**Raw Data → Landing → Bronze → Silver → Gold → Power BI**

### Technologies Used

* Microsoft Fabric
* Fabric Lakehouse
* PySpark
* Spark SQL
* Delta Lake
* Microsoft Fabric Data Pipelines
* Power BI
* GitHub

---

# 🏗️ Architecture

The project follows the Medallion Architecture, with separate layers for different stages of data processing.

<img width="1472" height="1088" alt="image" src="https://github.com/user-attachments/assets/490b0c97-a677-4cb6-9e6c-37bec1df1959" />

Raw:
Original source files before ingestion.

Landing:
Initial staging area where source files are ingested into Microsoft Fabric.

Bronze:
Persistent raw-data layer storing ingested data in Delta format with minimal transformation.

Silver:
Cleaned, validated and transformed data prepared for downstream analytics.

Gold:
Business-ready datasets and metrics designed for reporting and analytics.

Power BI:
Consumes Gold-layer data for dashboards and business insights.


The complete process is orchestrated using a **Microsoft Fabric Data Pipeline**.

---

# 📥 1. Raw to Landing

The first stage of the project ingests the raw sales data into the **Landing area** of the Fabric Lakehouse.

<img width="1836" height="862" alt="image" src="https://github.com/user-attachments/assets/d311e8e4-eb74-4304-8f7f-7b057e97342e" />   ***Notebook reading raw CSV files and loading them into the Landing area, with a preview of the resulting sales table.***


### Key activities

* Reading raw CSV files
* Defining the data schema using PySpark
* Loading the source data
* Storing the data in the Landing area
* Organising incoming data using a processing date

### Notebook

`Raw_to_Landing.ipynb`

---

# 🥉 2. Bronze Layer

The Bronze layer stores the ingested data in a **Delta Lake table**.

The main Bronze table used in the project is:

`tblsales_bronze`

<img width="1841" height="929" alt="image" src="https://github.com/user-attachments/assets/6e25dcf5-cf7c-459b-afad-4222ad9ea582" /> ***Bronze Delta table containing the ingested sales data, with Delta Lake MERGE logic for inserting new records and updating existing records.***


### Key activities

* Reading data from the Landing layer
* Creating the Bronze Delta table
* Applying the required schema
* Creating temporary Spark views
* Using Delta Lake MERGE to insert new records and update existing records
* Adding a processing date for data tracking

### Notebook

`Landing to Bronze table.ipynb`

---

# 🥈 3. Silver Layer

The Silver layer is responsible for **data cleaning, validation, and transformation**.

### Data Cleaning

<img width="1811" height="925" alt="image" src="https://github.com/user-attachments/assets/f187918d-09ff-4390-8d76-0a4cfeaec66c" />***Silver-layer notebook cleaning, deduplicating, and validating the Bronze data***.


The Silver transformation includes:

* Removing duplicate records
* Handling missing values
* Performing data-quality checks
* Validating and standardising data types
* Preparing the dataset for downstream business transformations
    
### Business Transformations

#### Delivery Days

The number of days between the order date and shipping date is calculated.

`Delivery_Days = Ship_Date - Order_Date`

#### Profit Margin

Profit margin is calculated using sales and profit.

`Profit_Margin = Profit / Sales`

The transformed data is stored in the Silver layer.

### Notebook

`Silver_Transformation.ipynb`

---

# 🥇 4. Gold Layer

The Gold layer contains data that has been transformed and prepared for **business analysis and reporting**.

<img width="1817" height="904" alt="image" src="https://github.com/user-attachments/assets/cbd83cd4-9d20-4ef5-9d5b-d6ac5117477e" /> ***Gold-layer notebook producing the business-ready dataset used for Power BI reporting.***

### Key activities

* Reading transformed data from the Silver layer
* Applying final business transformations
* Creating business-ready analytical datasets
* Preparing sales, profitability, customer, product, regional and delivery data for reporting
* Preparing the Gold-layer data for Power BI analytics

### Notebook

`Silver to Gold table.ipynb`

---

# 🔄 5. End-to-End Orchestration

Microsoft Fabric Data Pipelines are used to orchestrate the complete data engineering workflow.

The pipeline connects the different stages of the project and ensures that the processing activities are executed in the required sequence.

<img width="1703" height="773" alt="image" src="https://github.com/user-attachments/assets/44c3aded-d233-4da6-91e5-e8cc8fe7bf7e" />      ***Microsoft Fabric Data Pipeline orchestrating the full Raw → Landing → Bronze → Silver → Gold workflow.***


### End-to-End Workflow

```text
Raw Sales Data
      ↓
Raw → Landing
      ↓
Landing → Bronze
      ↓
Silver Transformation
      ↓
Silver → Gold
      ↓
Gold Layer
      ↓
Power BI
```

### Pipeline Stages

1.Raw to Landing — Ingests the raw sales data into the Landing area.

2.Landing to Bronze — Loads the Landing data into the Bronze Delta table.

3.Silver Transformation — Cleans, validates and transforms the Bronze data.

4.Silver to Gold — Transforms the Silver data into business-ready Gold data.

5.Reporting: Power BI consumes the Gold-layer data for analytics and reporting.

### Benefits of Orchestration

* Automated execution of the workflow
* Correct execution order
* Repeatable data processing
* Easier pipeline monitoring
* Structured end-to-end data processing

---

# 📊 6. Power BI Reporting

The Gold layer provides prepared data for **Power BI reporting and analytics**.

<img width="1467" height="881" alt="image" src="https://github.com/user-attachments/assets/57586007-a84f-465f-8450-bea97bb77a2e" /> ***Power BI report built on the Gold layer, showing sales and profit broken down by category, sub-category, and product — including total sales (456.14K) and total profit (53.55K).***


The data can be used to analyse:

* Sales performance
* Profitability
* Profit margin
* Product performance
* Customer performance
* Regional performance
* Delivery performance
* Order trends

---

# 📂 Project Structure

```text
fabric-sales-medallion-project/
│
├── README.md
│
├── Raw_to_Landing.ipynb
│
├── Landing to Bronze table.ipynb
│
├── Silver_Transformation.ipynb
│
└── Silver to Gold table.ipynb
```

---

# 🛠️ Technical Implementation

This project implements an end-to-end Microsoft Fabric data engineering solution using:

* Microsoft Fabric
* Fabric Lakehouse
* Medallion Architecture
* PySpark
* Spark SQL
* Delta Lake
* Delta `MERGE` operations
* Temporary Spark views
* Duplicate handling
* Missing-value handling
* Data quality checks
* Business transformations
* Delivery performance calculations
* Profit margin calculations
* Data Pipelines
* End-to-end orchestration
* Preparing data for Power BI
* GitHub

---

# 🚀 Conclusion

This project demonstrates how **Microsoft Fabric** can be used to build a complete end-to-end data engineering solution.

The solution starts with raw sales data and processes it through the Landing, Bronze, Silver, and Gold layers using the **Medallion Architecture**.

PySpark and Spark SQL are used for data processing and transformation, while Delta Lake provides reliable storage and `MERGE` functionality.

The complete workflow is orchestrated using a **Microsoft Fabric Data Pipeline**, creating a structured and repeatable data engineering process.

The final Gold-layer data can be used for **Power BI reporting and business analysis**.
