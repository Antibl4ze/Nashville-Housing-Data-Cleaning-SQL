# Nashville Housing Data Cleaning (SQL)

Raw data is rarely ready for analysis. This project takes a messy public dataset of about 56,000 property sales in Nashville, Tennessee (2013–2016) and cleans it in Microsoft SQL Server, step by step, so it can be used for reporting and analysis.

## The problems in the raw data
| Problem | Example |
|---|---|
| Sale dates stored as text | `April 9, 2013` |
| Missing property addresses | 29 sales had no property address |
| Addresses packed into one column | `1808 FOX CHASE DR, GOODLETTSVILLE` |
| Inconsistent yes/no values | `SoldAsVacant` contained `Yes`, `No`, `Y` and `N` |
| Duplicate sales | The same parcel, address, price, date and legal reference appearing more than once |
| Columns no longer needed | Original address and date columns, tax district |

## What I did
1. **Standardised the sale date:** added a `SaleDateConverted` column with `CONVERT(date, SaleDate)`.
2. **Filled missing property addresses:** properties with the same `ParcelID` share an address, so a self-join on `ParcelID` with `ISNULL()` filled all 29 missing values.
3. **Split addresses into separate columns:**
   - Property address → street and city, using `SUBSTRING` and `CHARINDEX`
   - Owner address → street, city and state, using `PARSENAME` on a comma-replaced string
4. **Made SoldAsVacant consistent:** a `CASE` statement turned the 451 `Y`/`N` values into Yes/No.
5. **Removed about 100 duplicate sales:** used a CTE with `ROW_NUMBER() OVER (PARTITION BY ...)` and deleted every row numbered above 1.
6. **Dropped unused columns:** `OwnerAddress`, `PropertyAddress`, `SaleDate` and `TaxDistrict`.

After every change the SQL includes a check query, such as confirming no duplicates remain.

## SQL techniques used
`CONVERT` · self `JOIN` · `ISNULL` · `SUBSTRING` / `CHARINDEX` · `PARSENAME` / `REPLACE` · `CASE` · CTE · `ROW_NUMBER()` window function · `ALTER TABLE` / `UPDATE` / `DELETE`

## Data
`Nashville Housing Data for Data Cleaning.csv`: 56,477 property sales with 19 columns, including parcel ID, land use, address, sale date and price, owner, acreage, land and building values, year built, bedrooms and bathrooms.

## Files
| File | Description |
|---|---|
| `Data cleaning.sql` | All cleaning queries, commented step by step |
| `Nashville Housing Data for Data Cleaning.csv` | Raw data |
| `UPDATED_EXCEL` | Link to the cleaned data as an Excel file on [Google Drive](https://drive.google.com/drive/folders/17A6UGAwJq5nAwxsQWzmnnrlOK0mhyUuF?usp=sharing) |

## Tools
SQL Server (SSMS), Excel
