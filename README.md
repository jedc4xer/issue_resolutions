# issue_resolutions
Repository containing resolutions to various issues surrounding Data Science

Managing Nulls with PySpark in DataBricks:

  - Problem:
   -- I was unable to use simple functions to count nulls. 
   -- Resolution:
   --- I learned that I needed to import the "when", "count", and "isnull" from pyspark
   -----from pyspark.sql.functions import when, count, isnull
        df.select([count(when(isnull(col), True)).alias(col) for col in df.columns]).show()

Writing Single Files to Blob:

  - Problem:
    Any time I attempted to write a single file to a blob, I would get multiple extensions added. 
    I realized that my problem was rooted in creating the initial file dump folder with an extension on its name.
    
    ''' 
        final_path = write_path + "/" + getArgument('filename')
        combined_df.repartition(1).write.format("com.databricks.spark.csv") \
        .mode('overwrite').option("header", "True") \
        .csv(final_path[:-4])
        files = dbutils.fs.ls(write_path + '/' + getArgument('filename')[:-4])
        csv_file = [x.path for x in files if x.path.endswith(".csv")][0]
        dbutils.fs.mv(csv_file, final_path)
        dbutils.fs.rm(write_path + '/' + getArgument('filename')[:-4], recurse = True)
        '''
