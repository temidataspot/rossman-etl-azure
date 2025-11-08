# Rossmann Sales ETL Pipeline in Azure Data Factory

## Project Overview
This project demonstrates an **end-to-end ETL (Extract, Transform, Load) pipeline** built using **Azure Data Factory (ADF)**. The pipeline processes the Rossmann Store Sales dataset from Kaggle to produce a cleaned, analytics-ready dataset stored in **Azure Blob Storage**.  

The main goal is to demonstrate **processes in the Azure ecosystem**, including dataset ingestion, type conversion, filtering, and loading cleaned data for downstream analytics or machine learning.

**Source Dataset:** [Rossmann Store Sales - Kaggle Competition](https://www.kaggle.com/c/rossmann-store-sales/data)

---

## Architecture

https://github.com/temidataspot/rossman-etl-azure/blob/main/rossman_adf_architechture.png

---

## Steps Implemented

### Azure Setup
→ Created a Resource Group, 'priscilla', in Azure to hold all project resources.
→ Created a Storage Account 'priscillastorage' within the resource group.
→ Created two Blob Containers:
    - sales-raw → for raw input CSV files
    - sales-clean → for storing cleaned data outputs
    
https://github.com/temidataspot/rossman-etl-azure/blob/main/az-setup.png

### 1. Extract (Source)
- Created a **Linked Service** in ADF pointing to the Azure Storage account (`priscillastorage`).  
- Created a **Dataset** `TrainCSV_Raw` pointing to the raw CSV file container (`sales-raw`).  
- Verified connectivity and data preview inside ADF.

### 2. Transform (Data Flow)
- Added a **Select Transformation** to map and check all columns:
Store, DayOfWeek, Date, Sales, Customers, Open, Promo, StateHoliday, SchoolHoliday

https://github.com/temidataspot/rossman-etl-azure/blob/main/select_col.png

- Added a **Derived Column Transformation** to convert text columns to numeric types:
```text
Sales_num = toInteger(Sales)
Customers_num = toInteger(Customers)

https://github.com/temidataspot/rossman-etl-azure/blob/main/rossman_adf_architechture.png

- Added a **Filter Transformation** to keep only valid records and verified transformations using Data Preview in ADF.

https://github.com/temidataspot/rossman-etl-azure/blob/main/filter_col.png

### 3. Load (Sink)
- Created a Sink Dataset TrainCSV_Clean pointing to the sales-clean container in Blob Storage.

- Configured the Data Flow Sink to write the transformed and filtered dataset into train_clean.csv.

- Ran the pipeline in Debug mode to validate the ETL workflow.

https://github.com/temidataspot/rossman-etl-azure/blob/main/sink_c.png



