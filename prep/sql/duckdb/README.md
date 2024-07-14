[Open Data Panels](../../../) and [International Trade Flow](../../../../useeio.js/footprint/)

# DuckDB Data Loader

Also see our [Supabase Data Loader page](../../sql/supabase)

## Overview
The <!-- Loren couldn't find load_data.py, so he's guessing duckdb-db-loader.py is the new name. -->[duckdb-db-loader.py](https://github.com/ModelEarth/OpenFootprint/blob/main/prep/sql/duckdb/duckdb-db-loader.py)  script is designed to load data from a CSV file into a DuckDB database. It provides flexibility in loading data from both a URL and a local file, dynamically creating a table in [DuckDB](https://duckdb.org/docs/api/r.html) based on the columns of the input data, and allowing users to choose whether to append new data to an existing table or replace existing data.

Table migrations and column names are set in [create-database.yaml](https://github.com/ModelEarth/OpenFootprint/blob/main/impacts/exiobase/US-source/create-database.yaml)

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
3. Run the script `duckdb-db-loader.py`:
   ```sh
   python duckdb-db-loader.py
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

---

** When loading local CSV files, provide paths using slashes (/) rather than a backslashes (\\).


<br>
<div style="height:8px; background-color:orange"></div>
<br>

Please edit: Move anything missing above, and delete redundant text.

## Overview

This Python script loads data from CSV files into a DuckDB database based on configurations provided in a YAML file. It allows users to choose between loading data from URLs or local files and supports dynamic column mapping and data manipulation before insertion into DuckDB tables.
Features

Loads data from CSV files into DuckDB tables.
Supports configuration through a YAML file for specifying data sources and table mappings.
Allows users to choose between loading data from URLs or local file paths.
Provides options to delete existing data or append to it when tables already exist in the DuckDB database.

### Prerequisites

Python 3.6 or higher installed.
Required Python packages:

requests
yaml
pandas
duckdb

### Setup

Install Python Dependencies:

Install required Python packages using pip:

pip install requests yaml pandas duckdb

Clone the Repository:

Clone this repository to your local machine:

bash

    git clone https://github.com/your_username/your_repo.git

Download DuckDB:

Download and install DuckDB from DuckDB website.

Prepare Data and Configuration:
Ensure your CSV files are accessible either via URLs or locally.
Prepare a create-database.yaml file specifying the source and configuration of your CSV files.

Usage

Navigate to the directory containing the script and run:

    python duckdb_data_loader.py

Follow the Prompts:
Choose whether to load data from URLs or local file paths.
Provide paths or URLs as required.
Follow prompts to delete existing data or append to it for existing DuckDB tables.

Monitor Progress:

The script will output status messages indicating the loading and transformation of data, as well as any errors encountered.

YAML Configuration (create-database.yaml):

Modify to specify:
source: CSV file names or URLs.
columns: Column mappings for renaming.
omit: Columns to omit from CSV files.

