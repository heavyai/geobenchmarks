# geobenchmarks
Short snippets of python testing various geo-enrichment examples and timing the results.

The initial benchmark is for two flavors of geo-enrichment done using "point in polygon" spatial joins. In the first case, we enrich points by adding column attributes from the polygons they fall within.  For example here, the census block groups of the points.  In the second case, we enrich the polygons with summary metrics based on the points.  Most simply for example, how many Uber rides ended in a particular census block over the full period of record. 

Supporting ETL scripts are provided for open data files which don't directly load in OmniSci.  To start, we have 4.5m NYC Uber dropoff points from Kaggle.  These don't load directly because they are zipped into a file archive with multiple CSV with different schema, only some of which represent the primary data.  So the ETL script separates the wheat from the chaff and loads multiple months of data into a single table.

We also use US Census block groups as polygons.  The pre-2020 versions of these are available in a single file which loads directly.  Since these are what has been used elsewhere, they form the current best basis for benchmarking.  

The census has released new geometries for 2020 by state.  We will eventually add a script demonstrating how to loop through and load those into a single table.  For now probably enough to say that "COPY * FROM 'foo' WITH (geo='true')" appends by default and accepts http(s) and s3 paths directly.

