<a id="readme-top"></a>
# Implement and benchmark classification algorithms using Apache Spark
<!-- ABOUT-->
## Motivation
To implement ML classification algorithms from scratch using Apache Spark(PySpark), measure model performance and benchmark it against Spark’s built-in machine learning library MLlib.

## Algorithms and Techniques implemented:
- Algorithm used: Logistic Regression.
- Apache Spark is an open source cluster computing framework which has been built around speed, ease of use and streaming analytics. 
- Python is a high level programming language which provides a wide range of libraries majorly used for Machine Learning and real time data analytics. This makes PySpark, which is a Python API for Spark, harness the simplicity of Python and the high computing power of Apache Spark to process Big Data.
- Implemented Logistic Regression with Gradient Descent using PySpark. We
used Pipelines to tie the stages of categorical and numerical feature encoding
transformations. A pipeline chains multiple Transformations and Estimators together to
specify an ML workflow.

## Dataset
- The dataset used is [2015 Flight Delays and Cancellations](https://www.kaggle.com/datasets/usdot/flight-delays). It is collected from the U.S. Department of Transportation’s (DOT) Bureau of Transportation Statistics which contains information of flights in the year 2015, with respect to airline carrier, original airport, destination airport, distance traveled by the flight, time spent, departure delay time, arrival delay time, etc.
- The dataset is significantly large, with more than 1 million rows and 31 features, making it ideal for demonstrating the power of PySpark's distributed computing over Big Data. The rich feature set provided a good exercise in creating feature pipelines and integrating the stages together.

## Contents
1. Flights.py - Contains all the source code for the custom-built Logistic Regression algorithm, Logistic Regression using MLib, and Random Forest algorithm using MLib 
2. DataAnalysis.py - Contains code for analyzing 15000 random samples in the dataset
3. PlotResults.py - Predicted and actual label values for custom-built logistic regression algorithm and result graphs.
4. True_pred.txt - Output file of the Logistic regression algorithm executed for 15000 records for 500 iterations
5. True_pred100k.txt - output file of the Logistic regression algorithm executed for 100000 records for 100 iterations

## Instructions to run
1. Create an S3 bucket on AWS and upload source Flights.py file and datasets.
2. Create SparkCluster on AWS console with required number of m5.xlarge instances.
3. SSH to console and download source file and dataset file on the console from S3 bucket
4. Execute the following commands to download files from S3 bucket to local AWS console
```
aws s3 cp s3://BUCKET_NAME/Flights.py . 
aws s3 cp s3://BUCKET_NAME/randomData100k.csv . 
```
5. Copy files from the local file system to the Hadoop Distributed File System (HDFS)
```
hadoop fs -put randomData100k.csv /input/
```
6. Submit the Python script (Flights.py) with input and output directories specified in HDFS.
```
/usr/bin/spark-submit Flights.py /input/randomData100k.csv /output/
```
7. For adding the output to text file, execute this command - 
```
hadoop fs -cat output/* > output/true_pred100k.txt
```
8. Copy the output file to bucket and then downloaded directly from S3. For copying file to s3
```
aws s3 cp output/true_pred100k.txt s3://BUCKET_NAME/true_pred100k.txt
```
