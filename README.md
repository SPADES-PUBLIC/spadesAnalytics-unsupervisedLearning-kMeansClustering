# spadesAnalytics-unsupervisedLearning-kMeansClustering
https://en.wikipedia.org/wiki/K-means_clustering

Description
-----------
The **SpadesAnalytics.jar** contains the Java source code and executables to run machine learning algorithms on data stored in mHealth format.  Specifically, the package **com.qmedic.spades.task.examples.spark** contains four algorithms implemented in Spark that take as input the feature extracted data (output of **com.qmedic.spades.task.examples.mapreduce.FeatureExtractor**).  

The algorithm takes five input parameters, which are passed as a string separated by commas:

1. Amazon key
2. Amazon secret key
3. Input data path (either on a local HDFS system or on Amazon S3)
4. Output data path (either on a local HDFS system or on Amazon S3)
5. Algorithm input parameters separated by a single dash

Usage
-----
Open a command prompt and type a command with the following usage pattern:

```ShellSession
java -cp SpadesAnalytics.jar [ALGORITHM] [AMAZON ACCESS KEY], [AMAZON SECRET KEY],[INPUT DATA PATH],[OUTPUT DATA PATH],[ALGORITHM PARAMETERS]
```

- **[ALGORITHM]**: (required) The desired algorithm to run on the data.  
- **[AMAZON ACCESS KEY]**: (required) The Amazon access key, needed particularly when the data is being retrieved from S3.  
- **[AMAZON SECRET KEY]**: (required) The Amazon secret key, needed particularly when the data is being retrieved from S3.
- **[INPUT DATA PATH]**: (required) The path for the input data.  This can be a local hdfs path or an S3 path.  
- **[OUTPUT DATA PATH]**: (required) The path for the output data. This can be a local hdfs path or an S3 path.  
- **[ALGORITHM PARAMETERS]**: (required) The parameters needed for the algorithm.  These are numerical parameters separated by a single dash.

Algorithm Background
--------------------
Parameters: numclusters, numiterations, x_index, y_index

Sample Input to Algorithm: 10-10-17-100

Parameter Explanations:

1. **numclusters**: The number of clusters.  For the Kmeans clustering algorithm, the number of clusters to generate.  The number of activities (estimated or actual) or fewer represented in dataset.  
2. **numiterations**: The number of times the Kmeans clustering algorithm should be run.  The greater the number of iterations, the better the results.  However, increasing the number of iterations beyond 20 will give diminishing returns.  
3. **x_index**: For the Kmeans clustering algorithm, the numerical index of the column/feature from the spades feature extractor that is desired for the x-axis for the clustering algorithm.  The first column has a numerical index of 0; the second column, 1; and so on.  
4. **y_index**: For the Kmeans clustering algorithm, the numerical index of the column/feature from the spades feature extractor that is desired for the y-axis for the clustering algorithm.  The first column has a numerical index of 0; the second column, 1; and so on.    

Suggested Parameter Values:

1. numclusters: number of activities represented in dataset (or fewer)
2. numiterations: 5-20
3. x_index: 1-256
4. y_index: 1-256

Example Command
---------------
```ShellSession
java -cp ~/SpadesAnalytics.jar com.qmedic.spades.task.examples.spark.LogisticRegressionHDFS yourAmazonAccessKey,yourAmazonSecretKey,hdfs://spades-data/development/InstitutionName/1/StudyName/1/MetaData-FeatureExtractor-2015-09-10-17-56-59.082/2010/07/21/*,hdfs://output-spark/output.csv,10-10
```

Output
------
Clustered data table: A table that shows the timestamp, x- and y-coordinates (selected by x_index and y_index) of the input data, the cluster prediction for that datapoint, and the x- and y-coordinates of the cluster center to which the datapoint belongs.

Example:
```ShellSession
HEADER_TIME_STAMP,MEAN_Wocket00066602fee4_1,CORR_Wocket00066602ff09_0_1,CLUSTER_ID,CLUSTER_X,CLUSTER_Y
2015-10-27 19:09:57.958,-1.3895878143332354,-4.169711291592983,4,-0.8081006299994251,-4.145899417430409
2015-10-27 19:09:57.958,-1.2442056100163699,-4.38401815905614, 4,-0.8081006299994251,-4.145899417430409
2015-10-27 19:09:57.958,1.4539831871118492,0.6307625395817607, 0,1.5938615175997668,0.43550517144866097
2015-10-27 19:09:57.958,1.7589860590549635,0.4164556721186023, 0,1.5938615175997668,0.43550517144866097
```
