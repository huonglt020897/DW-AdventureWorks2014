# AdventureWorks2014 – End-to-End Business Intelligence Project

## Overview

This project implements a complete Business Intelligence (BI) pipeline using the AdventureWorks2014 database, following a classical data warehouse architecture:

Operational Database → Staging → Data Warehouse → SSAS Tabular → Power BI

The solution delivers interactive dashboards focused on sales performance, profitability, channel comparison, territory analysis, and employee payment management.

---

## Tech Stack

- **Database:** SQL Server 2025  
- **ETL:** SQL Server Integration Services (SSIS)  
- **Data Warehouse:** Dimensional Modeling (Star Schema)  
- **Semantic Layer:** SQL Server Analysis Services (SSAS) Tabular  
- **Reporting:** Power BI (Live Connection)  
- **Development Tools:** Visual Studio, SSMS  

---

## Architecture

### 1. Source Layer
- Restored `AdventureWorks2014` as transactional source system.

### 2. Staging Layer 
- SQL script 1_AWN_STG_Demo was executed to create schemas, tables, and views in the staging database.
- Built SSIS packages to extract and load:
  - Master data (Business_Entity, Currency, Customer, Person, Product, ProductCategory, ProductSubCategory, Store, PersonAddress, SalesTerritory)
  - Transactional data (SalesHeader, SalesOrderDetails)
  - HR data (Employee, EmployeeDepartmentHistory, EmployeePayHistory)
- Added metadata columns (`CreatedDate_dt`, `SSISTrackID`)
- Validated row counts and data integrity in SSMS
<img width="609" height="321" alt="image" src="https://github.com/user-attachments/assets/b98ababf-e294-4e3f-b8b8-6e882959ae6f" />
<img width="606" height="317" alt="image" src="https://github.com/user-attachments/assets/92376689-af99-4b5f-87c1-55d0e90c5fb7" />

### 3. Data Warehouse Layer 
- SQL script 2_AWN_DW_Demo was executed up to line 326 to create the core data warehouse schema.
- SQL script 2_AWN_DW_Demo was executed up from line 326 to end to create procedures.
#### Dimensions
- DimDate  
- DimCustomer  
- DimProduct  
- DimCurrency  
- DimSalesTerritory  
- DimReseller  
- DimEmployee (Slowly Changing Dimension)

#### Fact Tables
- FactInternetSales  
- FactResellerSales  
- FactEmployeePay  

Key practices:
- Stored procedures for repeatable loads  
- Lookup transformations for surrogate key mapping  
- SCD implementation for historical tracking  
- Post-load validation  

---

## Semantic Model (SSAS Tabular)

- Imported fact and dimension tables
- Defined relationships (cardinality + filter direction)
- Deployed to SSAS
- Enabled live connection from Power BI
<img width="609" height="338" alt="image" src="https://github.com/user-attachments/assets/34b06ae5-c057-4a41-9063-27da7ae832f1" />

---

## Power BI Dashboard

### Business Questions Addressed
- Sales performance by channel (Internet vs Reseller)
- Sales trends over time
- Product category performance
- Geographic performance by territory
- Employee payment analysis

### DAX Measures

Core KPIs:
- TotalSales
- TotalCost
- TotalProfit
- ProfitMargin
- OrderCounts
- AvgProfitPerOrder

Time Intelligence:
- Sales LY
- Sales YoY %
- AverageDailySales
- AverageWeeklySales
- AverageMonthlySales
- AverageQuarterlySales

### Report Pages
1. Overview
<img width="609" height="340" alt="image" src="https://github.com/user-attachments/assets/1160d0ab-e31d-4be3-a010-65be4b48c228" />

2. Reseller Sales
<img width="609" height="338" alt="image" src="https://github.com/user-attachments/assets/777f370b-8f27-4a80-a844-f5237084d3ec" />

3. Internet Sales  
<img width="609" height="339" alt="image" src="https://github.com/user-attachments/assets/a7dd6463-48d9-4982-a8d4-4deebf17083b" />

---


## Outcome

Delivered a scalable and maintainable BI solution that transforms raw transactional data into executive-level, interactive insights aligned with enterprise best practices.
