# Data Loader for Supabase

This script loads data into a Supabase PostgreSQL database from CSV files based on a configuration specified in a YAML file. It provides options to load data either from URLs or local file paths and allows the user to either delete existing data in a table or append to it if the table already exists.

## Features

- Load CSV files from URLs or local file paths.
- Configure data loading via a YAML file.
- Option to delete existing data or append to it if the table already exists.
- Handles large datasets by inserting data in batches.

## Requirements

- Python 3.6 or later
- Required Python packages:
  - requests
  - PyYAML
  - pandas
  - psycopg2
  - supabase-py

## Installation

1. Clone the repository or download the script.
2. Install the required Python packages using pip:

```sh
pip install requests pyyaml pandas psycopg2 supabase
```

## Usage

1. Ensure you have your Supabase credentials (URL and key) and PostgreSQL connection details.
2. Prepare your YAML configuration file that specifies the tables and corresponding CSV files.
3. Prepare your CSV files if using local paths.

### Running the Script

Run the script and follow the prompts:

```sh
python supabase-db-loader.py
```

### Prompts

1. **Data Source:** The script will ask if you want to load data from URLs. Answer `yes` or `no`.
2. **Local YAML File Path:** If you chose `no` for the previous prompt, provide the path to your local `create-database.yaml` file.
3. **Local CSV Files Directory:** If you chose `no` for the data source prompt, provide the path to your local CSV files directory.
4. **Table Exists:** If a table already exists, the script will ask if you want to delete existing data or append to it. Answer `delete` or `append`.

## Configuration File Format

The YAML configuration file should specify each table and the corresponding CSV file along with any column mappings and columns to omit. Here is an example:

```yaml
table1:
  source: "file1.csv"
  columns:
    original_col1: new_col1
    original_col2: new_col2
  omit:
    - col_to_omit1
    - col_to_omit2
table2:
  source: "file2.csv"
  columns:
    original_col1: new_col1
  omit:
    - col_to_omit1
```

## Example YAML File

```yaml
Commodity:
  source: "Commodity.csv"
  columns:
    old_name: new_name
  omit:
    - column_to_omit
```

## Script Details

### Importing Required Modules

```python
import requests
import yaml
import pandas as pd
import psycopg2
from supabase import create_client, Client
from io import StringIO
import psycopg2.extras
```

### Loading YAML Configuration

The `load_yaml` function loads the configuration file from a URL or local path.

### Supabase and PostgreSQL Connection

The script establishes a connection to Supabase and PostgreSQL using the provided credentials.

### Data Processing and Table Creation

For each table specified in the YAML configuration:
- The CSV file is loaded from the specified source.
- Columns are renamed or omitted as specified.
- If the table already exists, the user is prompted to either delete existing data or append to it.
- The table is created if it does not exist.
- Data is inserted in batches of 10,000 rows.

### Closing the Connection

The PostgreSQL connection is closed at the end of the script.

## Notes

- Ensure your Supabase credentials and PostgreSQL connection details are correct.
- The script assumes that the CSV files and the YAML configuration file are formatted correctly.
- Handle any exceptions or errors as needed, based on your specific requirements.


----------------------------------------------------------------

Indexes and Keys

We explored the following indexes for optimizing the data in the Supabase database:

B-tree Index: Good for general-purpose indexing.
Hash Index: Best for equality comparisons.
GIN (Generalized Inverted Index): Useful for full-text search.
GiST (Generalized Search Tree): Used for geometric data types.
Partial Index: Indexes only a portion of the table.
Composite Index: Indexes multiple columns together.

Currently, we have focussed on adding B-tree indexes to the potential primary keys for each table.

    Commodity: CommodityID
    CommodityUS: Sector and FlowUUID
    Flow: Flowable & FlowUUID
    ImportCommodityUS: Region & Sector
    ImportContributionsUS: BeaDetail & CountryCode
    ImportMultiplierUS: BeaDetail, CountryCode, FlowUUID
    ImportSectorUS: Region, Sector, FlowUUID
    SectorUS: Sector, FlowUUID

For multiple primary keys, we have added separate B-tree indexes instead of a common composite key because it is not sure whether the data will be queried using a filter on both columns simultaneously. For such cases, a B-tree index provides the best optimization.

----------------------------------------------------------------

DuckDB Data Loader
Overview

This Python script loads data from CSV files into a DuckDB database based on configurations provided in a YAML file. It allows users to choose between loading data from URLs or local files and supports dynamic column mapping and data manipulation before insertion into DuckDB tables.
Features

    Loads data from CSV files into DuckDB tables.
    Supports configuration through a YAML file for specifying data sources and table mappings.
    Allows users to choose between loading data from URLs or local file paths.
    Provides options to delete existing data or append to it when tables already exist in the DuckDB database.

Prerequisites

    Python 3.6 or higher installed.
    Required Python packages:
        requests
        yaml
        pandas
        duckdb

Setup

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

    Run the Script:

    Navigate to the directory containing the script and run:

    python duckdb_data_loader.py

    Follow the Prompts:
        Choose whether to load data from URLs or local file paths.
        Provide paths or URLs as required.
        Follow prompts to delete existing data or append to it for existing DuckDB tables.

    Monitor Progress:

    The script will output status messages indicating the loading and transformation of data, as well as any errors encountered.

Configuration

    YAML Configuration (create-database.yaml):

    Modify this file to specify:
        source: CSV file names or URLs.
        columns: Column mappings for renaming.
        omit: Columns to omit from CSV files.


** In the case of loading CSV files from local, please provide path with backslash (/) instead of forward slash (\)