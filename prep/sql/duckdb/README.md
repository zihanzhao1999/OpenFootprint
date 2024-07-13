[Open Data Panels](../../../) and [International Trade Flow](../../../../useeio.js/footprint/)

# DuckDB Data Loader

Also see our [Supabase Data Loader page](../../sql/supabase)

## Overview
The [load\_data.py script](https://github.com/ModelEarth/OpenFootprint/tree/main/prep/sql) is designed to load data from a CSV file into a DuckDB database. It provides flexibility in loading data from both a URL and a local file, dynamically creating a table in [DuckDB](https://duckdb.org/docs/api/r.html) based on the columns of the input data, and allowing users to choose whether to append new data to an existing table or replace existing data.

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
