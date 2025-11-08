# Rossmann Sales ETL Pipeline in Azure Data Factory

## Project Overview
This project demonstrates an **end-to-end ETL (Extract, Transform, Load) pipeline** built using **Azure Data Factory (ADF)**. The pipeline processes the Rossmann Store Sales dataset from Kaggle to produce a cleaned, analytics-ready dataset stored in **Azure Blob Storage**.  

The main goal is to demonstrate **processes in the Azure ecosystem**, including dataset ingestion, type conversion, filtering, and loading cleaned data for downstream analytics or machine learning.

**Source Dataset:** [Rossmann Store Sales - Kaggle Competition](https://www.kaggle.com/c/rossmann-store-sales/data)

---

## Architecture

![Architecture](https://github.com/temidataspot/rossman-etl-azure/blob/main/rossman_adf_architechture.png)

---

## Azure Setup & Getting to Azure Data Factory (ADF)

1. **Created a Resource Group**
   - In the Azure Portal, navigated to **Resource Groups → + Add** to hold all project resources
   - Named it: `priscilla`
   - Selected a supported region (e.g., `France Central`, `Italy North`)
   - **Review + Create → Create**

2. **Created a Storage Account**
   - Navigated to **Storage Accounts → + Add**
   - Named it: `priscillastorage`
   - Selected the same resource group (`priscilla`)
   - Chose a supported region
   - **Review + Create → Create**

3. **Created Blob Containers**
   - From the newly created storage account
   - Clicked **Containers → + Container**
     - Named one container `sales-raw` (for raw CSV files)
     - Named another `sales-clean` (for cleaned outputs)
       
![Containers](https://github.com/temidataspot/rossman-etl-azure/blob/main/az-setup.png)

4. **Accessed Azure Data Factory**
   - Navigated to **Data Factories → + Add**
   - Named it
   - Selected the resource group `priscilla` and region
   - **Review + Create → Create**
   - Once deployed, clicked **Launch Studio** to open the ADF UI where I built pipelines and Data Flows.


## Steps Implemented

### 1. Extract (Source)
- Created a **Linked Service** in ADF pointing to the Azure Storage account (`priscillastorage`).  
- Created a **Dataset** `TrainCSV_Raw` pointing to the raw CSV file container (`sales-raw`).  
- Verified connectivity and data preview inside ADF.

### 2. Transform (Data Flow)
- Added a **Select Transformation** to map and check all columns:
Store, DayOfWeek, Date, Sales, Customers, Open, Promo, StateHoliday, SchoolHoliday

![Select](https://github.com/temidataspot/rossman-etl-azure/blob/main/select_col.png)

- Added a **Derived Column Transformation** to convert text columns to numeric types:

Sales_num = toInteger(Sales)
Customers_num = toInteger(Customers)

![DerivedCol](https://github.com/temidataspot/rossman-etl-azure/blob/main/derived-col.png)

- Added a **Filter Transformation** to keep only valid records and verified transformations using Data Preview in ADF.

![Filter](https://github.com/temidataspot/rossman-etl-azure/blob/main/filter_col.png)

### 3. Load (Sink)
- Created a Sink Dataset TrainCSV_Clean pointing to the sales-clean container in Blob Storage.

- Configured the Data Flow Sink to write the transformed and filtered dataset into train_clean.csv.

- Ran the pipeline in Debug mode to validate the ETL workflow.

![Sink](https://github.com/temidataspot/rossman-etl-azure/blob/main/sink_c.png)





