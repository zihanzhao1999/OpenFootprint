# Supabase

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

