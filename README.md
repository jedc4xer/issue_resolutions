# issue_resolutions
Repository containing resolutions to various issues surrounding Data Science

Managing Nulls with PySpark in DataBricks:

  - Problem:
   -- I was unable to use simple functions to count nulls. 
   -- Resolution:
   --- I learned that I needed to import the "when", "count", and "isnull" from pyspark
   -----from pyspark.sql.functions import when, count, isnull
        df.select([count(when(isnull(col), True)).alias(col) for col in df.columns]).show()
