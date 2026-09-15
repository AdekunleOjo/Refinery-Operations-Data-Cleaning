# Dangote Refinery Operations Data Cleaning

## Overview

This project demonstrates the cleaning and validation of a synthetic refinery operations dataset using **Python, Pandas, and Jupyter Notebook**.

The raw Excel workbook contains multiple operational tables with data-quality issues. The objective was to investigate these issues, apply appropriate cleaning decisions, and produce a validated cleaned Excel workbook without unnecessarily altering valid operational information.

## Data Cleaning Approach

The cleaning process followed four questions:

> **What problem was found?**  
> **How was it investigated?**  
> **What decision was made?**  
> **How was it validated?**

### Duplicate Records

**Problem:**  
`Refinery_Production` contained **120 exact duplicate rows**.

**Investigation:**  
Full-row duplicate detection was used to identify exact duplicate records.

**Decision:**  
The 80 confirmed duplicate rows were removed.

**Validation:**  
The production table decreased from **15,120 to 15,000 records**, while the original 21 columns were retained.

### Missing Values

**Problem:**  
Missing values were identified in `Shift`, `Product`, and `Processing_Unit`.

**Investigation:**  
Missing counts and percentages were calculated for each column.

**Decision:**  
Missing operational attributes were not blindly replaced with artificial values where the correct value could not be reliably determined.

**Validation:**  
Missing-value profiling was used to confirm the affected fields and quantify the remaining missing data.

### Inconsistent Categories

**Problem:**  
Fields such as `Product` and `Status` contained variations caused by capitalization and whitespace.

**Investigation:**  
Unique values were inspected before standardization.

**Decision:**  
Unnecessary whitespace was removed and text values were standardized.

**Validation:**  
Unique values were checked again after transformation to confirm that inconsistent representations had been consolidated.

### Data Types and Dates

**Problem:**  
`Crude_Input_Bbl` was stored as an `object` even though it represents a numerical measure.

**Investigation:**  
Column data types were inspected before conversion.

**Decision:**  
The field was converted to numeric using `pd.to_numeric()`. Date fields were also converted to Pandas datetime format.

**Validation:**  
Data types, null counts, and date boundaries were checked after conversion.

### Operational Data-Quality Checks

**Problem:**  
Some records contained logically questionable combinations, including **zero operating hours with positive production** and utilization values above 100%.

**Investigation:**  
Business-rule conditions were used to isolate the affected records.

**Decision:**  
These records were **flagged rather than automatically overwritten or deleted**, preserving the underlying values for further review.

**Validation:**  
The flagged records were queried again to confirm that the data-quality rules correctly identified the exceptions.

### Outlier Investigation

**Problem:**  
Some production and downtime observations were statistically unusual.

**Investigation:**  
Descriptive statistics and the **Interquartile Range (IQR)** method were used to identify potential outliers.

**Decision:**  
Statistical outliers were treated as investigation candidates rather than automatically classified as errors.

**Validation:**  
The identified observations were isolated and reviewed alongside their data-quality classifications.

## Dataset Structure

The original workbook contains the following operational tables:

| # | Table |
|---|---|
| 1 | `Refinery_Production` |
| 2 | `Equipment_Data` |
| 3 | `Maintenance_Data` |
| 4 | `Downtime_Data` |
| 5 | `Product_Quality` |
| 6 | `Inventory_Data` |
| 7 | `Logistics_Data` |
| 8 | `Energy_Utilities` |
| 9 | `HSSE_Data` |
| 10 | `Workforce_Data` |

The cleaning process focused on the tables requiring data-quality treatment, while the remaining tables were reviewed and confirmed to be suitable for use.

## Final Output

The project produces:

- **Raw Excel workbook** — original uncleaned data
- **Jupyter Notebook** — complete cleaning and validation process
- **Cleaned Excel workbook** — processed data after the documented transformations

The raw dataset is preserved separately from the cleaned dataset so that the entire cleaning process remains **reproducible and auditable**.

## Tools

- **Python**
- **Pandas**
- **NumPy**
- **Jupyter Notebook**
- **OpenPyXL**
- **Microsoft Excel**

## Key Data Quality Principles Applied

The project followed a controlled approach to data cleaning:

- Remove confirmed duplicates
- Investigate missing values before deciding how to handle them
- Standardize inconsistent categorical values
- Correct inappropriate data types
- Convert date fields to appropriate datetime formats
- Apply business-rule checks
- Flag questionable operational records rather than blindly deleting them
- Investigate statistical outliers before classifying them as errors
- Preserve the original dataset for reproducibility

## Disclaimer

This dataset is **synthetic** and created for educational and portfolio purposes. It is inspired by publicly available information about Dangote Petroleum Refinery & Petrochemicals and does not represent actual confidential, proprietary, or operational data from Dangote Refinery.
