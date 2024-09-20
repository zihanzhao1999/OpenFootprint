[Active Projects](../../projects/)
<h1>International Trade Flow</h1>

<b>Exiobase International Trade Data + US Bureau of Economic Analysis (BEA)</b>
Our SQL Team has been generating <a href="/OpenFootprint/prep/sql/supabase/">Supabase</a> and <a href="/OpenFootprint/prep/sql/duckdb/">DuckDB</a> databases for comparing industries and identifying imports with positive environmental impacts.

We're imitating the data migration in [generate\_import\_factors.py](https://github.com/ModelEarth/USEEIO/blob/import_factors/import_factors_exio/generate_import_factors.py) but we're push directly to Supabase (avoiding csv files).  We're changing FlowUUID to FactorID to reduce the data size.

TO DO: Pulling from Exiobase directly to Supabase.  
We're working in a [ExiobaseSupabase CoLab](https://colab.research.google.com/drive/1LsEDmXrAAGs40OiAKWH48K63E_2bMGBb?usp=sharing). - Himanshu, Sahil, Ben, Parth, Jack, Satwik, Indrasenareddy

TO DO: Update the ExiobaseSupabase CoLab above to pull the same data as <a href="https://github.com/ModelEarth/USEEIO/tree/import_factors/import_factors_exio">generate\_import\_factors.py</a>. Test with the US.  Later we'll add send about 7 countries to unique Supabase instances. - Yuhao, Ruolin, Nancy

TO DO: Experiment in our [Pymiro CoLab](https://colab.research.google.com/drive/1Q9_1AhdY8uPUfLVUN71X6mKbEy_kqPuQ?usp=sharing) using the [Pymiro for Exiobase library](https://pymrio.readthedocs.io/en/latest/).

Jaya and Satwick are investigating using .feather within the Pymiro CoLab.

The [Big Sankey](https://github.com/baptiste-an/Application-mapping-GHG) ([view chart](https://sankey.theshiftproject.org/)) uses Plotly with .feather files. We could do the same with [Anvil](https://anvil.works). 

<!--
In the CoLab, add the [Sector table output](https://github.com/ModelEarth/USEEIO/commit/c10d087d916477b3335127de560d4689fa5818ea) Ben created.
-->

TO DO: Create [interactive versions](/OpenFootprint/impacts/) of the [three Exiobase charts](https://exiobase.eu)  
See our [SQL Project Overview](/OpenFootprint/prep/) - Three Charts using International Exiobase Data


TO DO: <a href="/OpenFootprint/prep/">Create International Industry Reports</a> - like Energy Consumption in Drying

TO DO: Generate SQL for [US States from Matrix table files](/io/about/) with new [50 State USEEIO json](https://github.com/ModelEarth/OpenFootprint/tree/main/impacts/2020)


<!--<a href="#reports">Our Javascript USEEIO TO DOs</a>-->
<!--<a href="/io/charts/">Our React USEEIO widget TO DOs</a>-->

<b>Pulling data into state SQL databases</b>
New simple table names - for use by elementary school students
<a href="/OpenFootprint/prep/sql/supabase/">Supabase from .csv files</a>
<a href="/OpenFootprint/prep/sql/duckdb/">DuckDB from .csv files</a>
<a href="/requests/products/">Harmonized System (HS) codes</a> - <a href="https://colab.research.google.com/drive/1etpn1no8JgeUxwLr_5dBFEbt8sq5wd4v?usp=sharing">Our HS CoLab</a>

<b>View SQL Data</b>
[Javascript with Supabase](/OpenFootprint/impacts) and [Just Tables](/OpenFootprint/prep/sql/supabase/SupabaseWebpage.html)
Our DuckDB parquet tables in [ObservableHQ Dashboard](https://observablehq.com/d/2898d01446cefef1) and [Static Framework](/data-commons/dist/innovation/)
<a href="/OpenFootprint/impacts/">Sample of JavaScript joining DuckDB Parquet tables</a>
<a href="https://model.earth/storm/impact/process.html">SQL Documentation Sample - Storm Tweet Data</a>

<b>Python to pull CSV files into SQL</b>
<a href="https://colab.research.google.com/drive/1qWgO_UjeoYYB3ZSzT3QdXSfVZb7j09_S?usp=sharing">Generate Supabase Exiobase (Colab)</a> - <a href="https://github.com/ModelEarth/OpenFootprint/tree/main/impacts/exiobase/US-source">Bkup</a>
<a href="https://colab.research.google.com/drive/1Wm9Bvi9pC66xNtxKHfaJEeIYuXKpb1TA?usp=sharing">Generate DuckDB Exiobase (CoLab) - <a href="https://github.com/ModelEarth/OpenFootprint/tree/main/impacts/exiobase/US-source">Bkup</a>


# Our Trade Data Pipeline

We first generate six [US-2020-17schema CSV files](https://github.com/ModelEarth/OpenFootprint/tree/main/impacts/exiobase/US-source/2022) by running <a href="https://github.com/ModelEarth/USEEIO/tree/import_factors/import_factors_exio">generate\_import\_factors.py</a>. The merge combines US BEA and <a href="https://exiobase.eu">EXIOBASE</a> data emissions factors for annual trade data. (The ExiobaseSupabase CoLab above aims to send the same Exiobase data directly to Supabase and DuckDB for each country and year.)

Exiobase provides the equivalent to <a href="https://github.com/USEPA/useeior/blob/master/format_specs/Model.md">M, N, and x</a> which is used in the <a href="/io/about/">USEEIO models</a> for import emissions factors. Exiobase also provides gross trade data which has no equivalent in USEEIO.



**Data Prep Notes**
- We remove underscores and use CamelCase for column names.
- We exclude the Year columns because each database is a different year.
- Commodity refers to the 6-character detail sectors.
- Sector refers to the 5-character and fewer sectors.
- Region is referred to as Import.
- National is omitted from the table names.
- Country abbreviations (Example: US) are appended to country-specific tables.
This structure supports pulling all the country data into one database.