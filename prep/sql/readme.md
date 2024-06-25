[Open Data Panels](../../)
Documentation of our DuckDB and Supabase SQL

# DuckDB Data Loader

## Overview
This script is designed to load data from a CSV file into a DuckDB database. It provides flexibility in loading data from both a URL and a local file, dynamically creating a table in DuckDB based on the columns of the input data, and allowing users to choose whether to append new data to an existing table or replace existing data.

## Requirements
- Python 3.x
- DuckDB
- pandas

## Usage
1. Clone or download the repository to your local machine.
2. Install the required Python libraries (`duckdb` and `pandas`) using pip:
   ```sh
   pip install duckdb pandas
   ```
3. Run the script `load_data.py`:
   ```sh
   python load_data.py
   ```
4. Follow the prompts:
   - Choose whether to load data from a URL or a local file.
   - Provide the URL or the path to the local CSV file.
   - If the table already exists in the DuckDB database, choose whether to delete existing data and add new data, or append new data to the existing data.

## Script Breakdown

### 1. Loading Data
- The script prompts the user to choose between loading data from a URL or a local file.
- Depending on the user's choice, the script loads the data into a pandas DataFrame using `pd.read_csv()` from either the provided URL or the local file path.

### 2. Dynamically Creating the DuckDB Table
- The script dynamically infers the column types from the DataFrame and creates the DuckDB table using a `CREATE TABLE` statement.
- Column types are inferred as INTEGER, DOUBLE, or VARCHAR based on the data types in the DataFrame.

### 3. Handling Existing Tables
- If the table already exists in the DuckDB database, the script prompts the user to choose whether to delete existing data and add new data, or append new data to the existing data.

### 4. Loading Data into DuckDB
- The script loads the data into the DuckDB table using an `INSERT INTO` statement.
- Depending on the user's choice, it either appends the new data to the existing table or replaces existing data with the new data.

### 5. Verification
- After loading the data, the script verifies the number of rows loaded into the DuckDB table and displays the count to the user.

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

---------------------------------------------------------------------------------------------------------------------------------------------------

# Supabase Database Loader

This script allows you to load data from a CSV file into a Supabase database table. It provides options to choose between loading data from a URL or a local file, and also gives the flexibility to delete existing data before adding new data or to append new data to the existing records.

## Requirements

- Python 3.x
- `psycopg2-binary` library
- `pandas` library

You can install the required libraries using pip:

```
pip install psycopg2-binary pandas
```

## Usage

1. Clone the repository to your local machine:

   ```
   git clone https://github.com/your-username/your-repo.git
   ```

2. Navigate to the directory where the script is located:

   ```
   cd your-repo
   ```

3. Run the script:

   ```
   python supabase_db_loader.py
   ```

4. Follow the prompts to choose the data source and specify the URL or file path accordingly.

5. Choose whether to delete existing data before adding new data or to append new data to the existing records.

6. The script will connect to your Supabase database, create the required table if it does not exist, and then load the data from the CSV file.



## Indexes and Keys

We explored the following indexes for optimizing the data in the Supabase database:

B-tree Index: Good for general-purpose indexing.
Hash Index: Best for equality comparisons.
GIN (Generalized Inverted Index): Useful for full-text search.
GiST (Generalized Search Tree): Used for geometric data types.
Partial Index: Indexes only a portion of the table.
Composite Index: Indexes multiple columns together.

Currently, we have focussed on adding B-tree indexes to the potential primary keys for each table.

1. Commodity: CommodityID
2. CommodityUS: Sector and FlowUUID
3. Flow: Flowable & FlowUUID
4. ImportCommodityUS: Region & Sector
5. ImportContributionsUS: BeaDetail & CountryCode
6. ImportMultiplierUS: BeaDetail, CountryCode, FlowUUID
7. ImportSectorUS: Region, Sector, FlowUUID
8. SectorUS: Sector, FlowUUID

For multiple primary keys, we have added separate B-tree indexes instead of a common composite key because it is not sure whether the data will be queried using a filter on both columns simultaneously. For such cases, a B-tree index provides the best optimization.


