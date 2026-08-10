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

```text
Raw Sales Data
      ↓
   Landing
      ↓
   Bronze
      ↓
   Silver
      ↓
    Gold
      ↓
  Power BI
```

The complete process is orchestrated using a **Microsoft Fabric Data Pipeline**.

---

# 📥 1. Raw to Landing

The first stage of the project ingests the raw sales data into the **Landing area** of the Fabric Lakehouse.

<img width="1804" height="877" alt="image" src="https://github.com/user-attachments/assets/78d14857-7128-4fdd-b8e0-51e010f237b9" />   ***Notebook reading raw CSV files and loading them into the Landing area, with a preview of the resulting sales table.***


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
<img width="1841" height="929" alt="image" src="https://github.com/user-attachments/assets/6e25dcf5-cf7c-459b-afad-4222ad9ea582" /> ***Bronze Delta table creation and MERGE logic for updating and inserting sales records***.
**

### Key activities

* Reading data from the Landing layer
* Creating the Bronze Delta table
* Applying the required schema
* Creating temporary Spark views
* Using Delta Lake `MERGE`
* Updating existing records
* Inserting new records
* Adding a processing date

### Notebook

`Landing to Bronze table.ipynb`

---

# 🥈 3. Silver Layer

The Silver layer is responsible for **data cleaning, validation, and transformation**.

### Data Cleaning

<img width="1811" height="925" alt="image" src="https://github.com/user-attachments/assets/f187918d-09ff-4390-8d76-0a4cfeaec66c" />


The Silver transformation includes:

* Removing duplicate records
* Handling missing values
* Performing data quality checks
* Ensuring appropriate data types

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

<img width="1817" height="904" alt="image" src="https://github.com/user-attachments/assets/cbd83cd4-9d20-4ef5-9d5b-d6ac5117477e" />

### Key activities

* Reading Silver-layer data
* Applying business transformations
* Preparing analytical datasets
* Creating business-ready data
* Preparing data for reporting and visualisation

### Notebook

`Silver to Gold table.ipynb`

---

# 🔄 5. End-to-End Orchestration

Microsoft Fabric **Data Pipelines** are used to orchestrate the complete data engineering workflow.

The pipeline connects the different stages of the project and ensures that the processing activities are executed in the required sequence.

<img width="1703" height="773" alt="image" src="https://github.com/user-attachments/assets/44c3aded-d233-4da6-91e5-e8cc8fe7bf7e" />


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

1. **Raw to Landing**
   Ingests the raw sales data into the Landing area.

2. **Landing to Bronze**
   Loads the Landing data into the Bronze Delta table.

3. **Silver Transformation**
   Cleans and transforms the Bronze data.

4. **Silver to Gold**
   Transforms the Silver data into business-ready Gold data.

5. **Power BI**
   Uses the Gold layer for reporting and analytics.

### Benefits of Orchestration

* Automated execution of the workflow
* Correct execution order
* Repeatable data processing
* Easier pipeline monitoring
* Structured end-to-end data processing

---

# 📊 6. Power BI Reporting

The Gold layer provides prepared data for **Power BI reporting and analytics**.
<img width="1392" height="907" alt="image" src="https://github.com/user-attachments/assets/da3da99b-ae35-408e-a174-40ea78bf3f78" />


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

# 🎯 Key Learning Outcomes

Through this project, I gained practical experience with:

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
