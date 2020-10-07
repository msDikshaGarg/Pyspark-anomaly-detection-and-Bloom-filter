# Pyspark-anomaly-detection-and-Bloom-filter
Implementation of  Anomaly detection  Bloom filters on the Hard Drive Failures dataset.  
<br>
Data: https://www.backblaze.com/blog/hard-drive-stats-q2-2019/  
<br>
## Data using Apache spark
* Create a single dataframe from all CSV files in the zip, with header information
* Show the dataframe columns
* Show the first 20 rows, sorted by (capacity descending, model ascending)
* Count the total number of rows
* Count the total number of rows, grouped by capacity
* Get the dataframe summary statistics
* Select the following columns: date, model, capacity
* Select the number of distinct models
* Calculate the pairwise frequency of this two columns (e.g. crosstab): capacity, smart_1_normalized
* Find the mean value of column capacity

## Anomaly detection
Anomaly detection is a technique used to identify unusual patterns that do not conform to expected behavior, called outliers. Point anomalies are a single instance of data is anomalous if it’s too far off from the rest. Example: Detecting credit card fraud based on “amount spent.”  
In this program we are implementing a point anomaly detector for:
* Annualized Failure Rate (by model) --target variable at 2%
* Normalized Read Error Rate, SMART attribute 1 --target variable at 100

## Bloom Filter
Bloom filters are efficient probabilistic data structures constructed of a set of values to be used for membership tests. It can tell you if an arbitrary element being tested might be in the set, or definitely not in the set, that is false positives are allowed, but false negatives are not.  
Consider, for example, if Table A has 100’s of millions of rows, while Table B has only a few thousands.
In cases like this, you might want to avoid the shuffle that the join operation introduces, especially if the dataset you want to use for filtering is significantly
smaller than the main dataset on which you will perform your further computation.  
In our program we ae using broadcast join and a bloom filter to filter all rows in Table A for only those containing ‘model’ in Table B. The common key is the ‘model’ column.
