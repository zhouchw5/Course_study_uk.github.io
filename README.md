# First Dance with PySpark                   
- Buckets and clusters conctruction in Google Cloud Platform                       
- VM SSH connection and browser configuration                    
- 'Local repository' constructed in Hadoop, upload/download files to/from the bucket                   
- Coding performance in PySpark using jupyter                
- Creation and performance on various transformations of resilient distributed datasets (RDD) in PySpark           
                              
## Buckets and clusters construction in Google Cloud Platform                    
This part can be finished in PowerShell (Windows System) or Google Cloud SDK Shell.                  
```python
# Create a bucket, for example creating a bucket named chuwei:                    
gsutil mb gs://chuwei/          
# cluster construction and SSH configuration
gcloud dataproc clusters create chuweizhou --bucket chuwei --subnet default --zone europe-west3-a --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 1.3-deb9 --project curious-ocean-228920 --initialization-actions gs://dataproc-initialization-actions/jupyter/jupyter.sh
```
Sometimes if the zone we have selected has no enough space, we can switch to us-east1-b, europe-west1-b, europe-west1-c, europe-west3-b, etc.                 
```python
gcloud dataproc clusters create chuweizhou --bucket chuwei --subnet default --zone europe-west3-b --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 1.3-deb9 --project curious-ocean-228920 --initialization-actions gs://dataproc-initialization-actions/jupyter/jupyter.sh
```                   
![VM SSH](https://github.com/zhouchw5/Course_study_uk.github.io/blob/First-Dance-with-PySpark/VM%20SSH.png)
## VM SSH connection and browser configuration                   
Actually we have finished some parts of VM SSH connection when creating the cluster above. But before configuring our browser so that we can get access to different ports based on our browser, like http://chuweizhou-m:8123 for jupyter, we should execute the statement in the Power Shell or Google Cloud SDK Shell shown as below.                                    
```python
gcloud compute ssh chuweizhou-m --project=curious-ocean-228920 --zone=europe-west3-a -- -D 1080 -N
```
Other options like (but the zone should be consistent with that you use for cluster creation)                   
```python     
gcloud compute ssh chuweizhou-m --project=curious-ocean-228920 --zone=us-east1-b -- -D 1080 -N
```             
To configure our browser using the cmd operations:                     
```python
cd C:\Program Files (x86)\Google\Chrome\Application
chrome.exe --proxy-server="socks5://localhost:1080" --user-data-dir="%Temp%\chuweizhou-m" http://chuweizhou-m:8088
```
![hadoop](https://github.com/zhouchw5/Course_study_uk.github.io/blob/First-Dance-with-PySpark/hadoop.png)             
The port for the jupyter:              
>http://chuweizhou-m:8123                      
![jupyter](https://github.com/zhouchw5/Course_study_uk.github.io/blob/First-Dance-with-PySpark/google%20jupyter.png)               
           
## 'Local repository' constructed in Hadoop, upload/download files to/from the bucket                  
This part we should utilize the VM SSH terminal.                                
![SSH Terminal](https://github.com/zhouchw5/Course_study_uk.github.io/blob/First-Dance-with-PySpark/VM%20SSH%20Terminal.png)                                        
                     
For example, we need to create a directory dblp in Hadoop and download two files dblp.xml.gz and author-large.txt, both of which would be got attaced to the bucket.                                       
```python
mkdir dblp
cd dblp
wget http://dblp.uni-trier.de/xml/dblp.xml.gz
wget http://webdam.inria.fr/Jorge/files/author-large.txt
gunzip -k dblp.xml.gz
cd ..          
# Copy the dblp directory from your local file system to HDFS: 
hadoop fs -put dblp/ /dblp
```
To list files:                 
```python
hadoop fs -ls /
```
To check the content of dblp directory in my local file system:             
```python
ls -al dblp
```
To get the selected file from Hadoop to our bucket in the Google Cloud Platform:                   
```python
# in the VM SSH Terminal
cd dblp
gsutil cp author-large.txt gs://chuwei/
```
                          
## Creating RDDs               
There are two ways to create an RDD in PySpark, one is to parallelize a list,                  
```python
data = sc.parallelize([('a', 1), ('b', 4), ('c',10)])
data.collect()
```
the other is to read from a data source (a file or database)                    
```python
# edit location
data_from_file = sc.\
    textFile(
        "gs://chuwei/author-large.txt", 
        4)
data_from_file.take(5)
```                 
![RDD construction](https://github.com/zhouchw5/Course_study_uk.github.io/blob/First-Dance-with-PySpark/RDD%20construction.png)                                  
RDD is a scheme-less data structure. We can access the object that stored in an RDD element as we would normally do in Python.            
```python
data_heterogenous = sc.parallelize([('Ferrari', 'fast'), {'Porsche': 100000}, ['Spain','visited', 4504]]).collect()
data_heterogenous
data_heterogenous[1]['Porsche']
```

## Transformations                 
### (a) .map(...)                
.map applies (...) to each element of the RDD. Here we transform each row of the **data_from_file** from a string to a list of strings.        
```python
def extractInformation(row):
    import re
    import numpy as np
    
    row = row.strip() # remove leading and trailing whitespaces
    words = np.array(row.split("\t")) # split the line into words by tab
    return words

data_from_file_conv = data_from_file.map(extractInformation)
data_from_file_conv.map(lambda row: row).take(5)
```
Or we can use a lambda expression to split and transform our dataset. We can get the same result given by the coding above.            
```python
import numpy as np
data_from_file_conv = data_from_file.map(lambda row: np.array(row.strip().split("\t")))
data_from_file_conv.take(5)
```
We can filter and transform only one part of an RDD element (firstly you should figure out what a RDD element looks like):            
```python
publish_year = data_from_file_conv.map(lambda row: int(row[3]))
publish_year.take(10)
```
or we can combine multiple part of an RDD element:            
```python
author_book = data_from_file_conv.map(lambda row: (row[0], row[2]))
author_book.take(5)
```
### .flatMap(...)
The .flatMap(...) method works similarly to .map(...) but returns a flattened result instead of a list.
```python
publish_year_2_flat = data_from_file_conv.flatMap(lambda row: (row[0], row[2]))
publish_year_2_flat.take(10)
```
### (b).filter(...)              
The .filter(...) method allows us to select elements of an RDD that satisfy specific criteria. Here we filter all the elements with author name 'Hans-Peter Seidel'.            
```python
data_filtered = data_from_file_conv.filter(lambda row: row[0] == 'Hans-Peter Seidel') 
data_filtered.take(5)
```
### (c).distinct()              
This method returns a list of distinct values of transformed RDD elements.                
```python
distinct_author = data_from_file_conv.map(lambda row: row[0]).distinct()
distinct_author.count()
```
### (d) .sample(...)             
The .sample() method returns a random subset of an RDD.                 
```python
fraction = 0.1
data_sample = data_from_file_conv.sample(False, fraction, 666)

data_sample.take(1)
```
We need to confirm that we really got 10% of all the elements.            
```python
length_original = data_from_file_conv.count()
length_sample = data_sample.count()
print('Original dataset: ', length_original) 
print('Sample', length_sample)
print('Ratio', length_sample/length_original)
```
### (e) Join        
Here we demonstrate the join operation for two pairs of RDDs:           


                  
Yours,                  
Chuwei Zhou        
2019.2.21                 
