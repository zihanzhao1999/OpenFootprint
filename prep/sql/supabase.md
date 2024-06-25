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