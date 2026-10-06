# Nashville Housing Data Cleaning (SQL)

Cleaning a raw dataset of about 56,000 Nashville property sales in Microsoft SQL Server so it can be used for analysis.

## What I did
- Converted the sale date from text to a proper date column
- Filled missing property addresses with a self-join on ParcelID
- Split property and owner addresses into address, city and state columns (SUBSTRING, CHARINDEX, PARSENAME)
- Standardised the SoldAsVacant field from Y/N to Yes/No with CASE
- Removed duplicate sales with a ROW_NUMBER() CTE
- Dropped columns that were no longer needed

## Files
- `Data cleaning.sql` – all cleaning queries, commented step by step
- `Nashville Housing Data for Data Cleaning.csv` – raw data
- `UPDATED_EXCEL` – link to the cleaned Excel file

## Tools
SQL Server (SSMS), Excel
