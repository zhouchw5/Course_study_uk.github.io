# First Dance with PySpark                   
- Buckets and clusters conctruction in Google Cloud Platform                       
- VM SSH connection and browser configuration                    
- 'Local repository' constructed in Hadoop, upload/download files to/from the bucket                   
- Coding performance in PySpark using jupyter                                        
                              
## Buckets and clusters construction in Google Cloud Platform                    
This part can be finished in PowerShell (Windows System) or Google Cloud SDK Shell.                  
```python
# Create a bucket, for example creating a bucket named chuwei:                    
gsutil mb gs://chuwei/          
# cluster construction and SSH configuration
gcloud dataproc clusters create chuweizhou --bucket chuwei --subnet default --zone europe-west3-a --master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 2 --worker-machine-type n1-standard-4 --worker-boot-disk-size 500 --image-version 1.3-deb9 --project curious-ocean-228920 --initialization-actions gs://dataproc-initialization-actions/jupyter/jupyter.sh
```




Yours,                  
Chuwei Zhou        
2019.2.21                 
