# E-Commerce Sales Data Warehouse

**Microsoft SQL Server · T-SQL · ETL · Data Warehousing · Data Quality**

## Overview

An end-to-end SQL Server data warehouse project designed to demonstrate practical Data Engineering concepts including dimensional modeling, ETL transformations, incremental data loading, data-quality validation, audit logging, analytical SQL, and business reporting.

## Architecture

```text
Source / Raw Data
       ↓
Staging Layer
       ↓
Data Transformation
       ↓
Data Quality Checks
       ↓
Data Warehouse
       ↓
Reporting Views
       ↓
Business Analytics
```

## Warehouse Design

The warehouse follows a star-schema-style model:

```text
                    DimCustomer
                         │
                         │
DimProduct ──────── FactSales ──────── DimPayment
                         │
                         │
                      DimDate
```

### Core warehouse tables

- `Warehouse.FactSales`
- `Warehouse.DimCustomer`
- `Warehouse.DimProduct`
- `Warehouse.DimPayment`
- `Warehouse.DimDate`

`FactSales` stores transactional sales data including order, customer, product, date, payment, quantity, unit price, discount amount, sales amount and load date.

## ETL and Incremental Loading

The project uses a staging layer to represent incoming source-system data. The ETL process cleans and standardizes inconsistent source data, then incrementally updates or inserts customer records into the warehouse.

Key transformations include:

- `LTRIM()` / `RTRIM()` for whitespace cleanup
- `UPPER()` for name standardization
- `LOWER()` for email standardization
- `TRY_CAST()` for ID/date conversion
- Location standardization

Incremental loading is based on the `CustomerID` business key.

The reusable stored procedure is:

```sql
Staging.usp_LoadDimCustomer
```

## Audit Logging

Each ETL execution is recorded in:

```text
Staging.ETL_AuditLog
```

The log captures:

- ETL process name
- Start time
- End time
- Rows inserted
- Rows updated
- Execution status
- Error message

## Data Quality

The project includes:

- NULL-value checks
- Duplicate `OrderID` checks
- Quantity and price validation
- Discount validation
- Sales-amount validation
- Foreign-key integrity checks
- Overall data-quality reporting
- Production-quality health checks

## Validation Metrics

| Warehouse table | Records |
|---|---:|
| DimCustomer | 500 |
| DimProduct | 100 |
| DimPayment | 15 |
| DimDate | 1,096 |
| FactSales | 10,000 |

The repository reports successful validation for NULL values, duplicates, quantity, unit price, discount, sales amount, foreign-key integrity, overall data quality and the production quality check.

## Business Analytics

The project answers questions around:

- Total revenue and orders
- Monthly sales
- Top products
- Top customers
- Category performance
- City performance
- Payment analysis
- Year-over-year sales
- Customer ranking

Analytical techniques include aggregations, joins, CTEs, window functions, `RANK()`, `NTILE()` and `LAG()`.

A reporting view, `Reporting.vw_CompletedSales`, filters reporting to completed payments.

## Technology Stack

- Microsoft SQL Server
- T-SQL
- SQL Server Management Studio (SSMS)
- Common Table Expressions (CTEs)
- Window Functions
- Stored Procedures
- Views
- Git
- GitHub

## GitHub

[View the complete source code](https://github.com/SDK-13/Project-1-E-Commerce-Sales-Data-Warehouse)

## Portfolio note

This is a personal portfolio project and is separate from my professional Cognizant experience. It demonstrates hands-on SQL Server, T-SQL, ETL and data-warehouse engineering skills.
