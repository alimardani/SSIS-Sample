# SSIS Package: CSV File Importer with Table Row Count Check

This SSIS package is designed to import data from CSV files into a SQL Server database. It includes logic to handle scenarios where data already exists in the target table, ensuring that the table is truncated before new data is imported.

## Features

- **Table Row Count Check**: 
  - The package starts by checking the row count of the target table using an **Execute SQL Task** component.
  - If the row count is greater than zero, the table is truncated.
  - If the row count is zero, the package skips truncation and proceeds directly to the import section.

- **CSV File Import with Foreach Loop**:
  - The package uses a **Foreach Loop Container** to loop through all CSV files in the specified Data folder.
  - For each CSV file found, the package performs the following operations.

- **Data Flow Task**:
  - The **Data Flow Task** handles the import of data from the CSV files into the database.
  - **Flat File Source**: Reads data from the CSV file.
  - **OLE DB Destination**: Inserts the data into the target SQL Server database table.

- **Post-Import File Handling**:
  - After successfully importing the data, a **File System Task** moves the processed CSV file to a designated **Processed** folder, ensuring that it is not reprocessed in subsequent runs.

## Folder Structure

- **Data Folder**: This is where the package looks for CSV files to import.
- **Processed Folder**: After processing, CSV files are moved here.

## Package Flow

1. **Row Count Check**: The package first checks the row count of the target table.
   - If rows exist, the table is truncated.
   - If no rows exist, the package skips truncation.

2. **Foreach Loop**: Iterates over each CSV file in the Data folder.

3. **Data Flow**:
   - Reads the CSV file.
   - Imports the data into the SQL Server table.

4. **File System Task**: Moves the processed CSV file to the Processed folder.

## How to Run

1. Ensure that the Data folder contains the CSV files you want to import.
2. Configure the connection strings in the SSIS package to point to your SQL Server instance and the appropriate database.
3. Run the SSIS package.

## Requirements

- **SQL Server**: The package requires SQL Server with SSIS enabled.
- **SSIS**: SQL Server Integration Services (SSIS) must be installed.
