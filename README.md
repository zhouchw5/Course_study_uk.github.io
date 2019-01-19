# Development Environment Constructed in the Distributed Computing for Big Data                                                                                             
With my original github account taken as private, I decided to register a new github account used for the course Distributed Computing for Big Data. Because one SSH key generated from the Git GUI has been used for the old account, I have to generate a new SSH key, by using [Git Bash](https://help.github.com/articles/connecting-to-github-with-ssh/), associated with my new account, to rebuild the connection between my online github and my local repositories.                              

```python
$ ssh-keygen -t rsa -b 4096 -C "(this should be my email address)"
# Generating public/private rsa key pair.
# Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
# Enter passphrase (empty for no passphrase): [Type a passphrase]
# Enter same passphrase again: [Type passphrase again]
```
               
After adding the SSH key to the ssh-agent and copying the SSH key from the defaulted file to the clipboard, we can add this new SSH key to a Github account.                
                   
And the next step is to get access to Google Cloud Platform (GCP) by using a gmail account and install the Google Cloud SDK.              
![the interface of GCP](https://github.com/zhouchw5/Course_study_uk.github.io/blob/master/GCP.png)              
                     
Some basic operations in Google Cloud SDK(Software Development Kit):
- Creating/Deleting Storage Buckets                 
![buckets](https://github.com/zhouchw5/Course_study_uk.github.io/blob/development-environment-constructing-in-Big-Data-course/buckets.png)          
- Uploading/Downloading Files from Storage Buckets              
![file](https://github.com/zhouchw5/Course_study_uk.github.io/blob/development-environment-constructing-in-Big-Data-course/file.png)        
- Creating/Deleting a Google Cloud Dataproc Cluster                  
![cluster](https://github.com/zhouchw5/Course_study_uk.github.io/blob/development-environment-constructing-in-Big-Data-course/cluster.png)                    
                   
The corresponding Google Cloud SDK approaches can be shown as:                
```python
# see what buckets we have:
gsutil ls
# Create a bucket, for example creating a bucket named chuwei (if a bucket with the same name has been already created in your project, an error would come up with the exceptions):                  
gsutil mb gs://chuwei/
# Upload a file, for example helloworld.py
gsutil cp helloworld.py gs://chuwei
# Check the file lists inside the bucket:            
gsutil ls gs://chuwei


# Download a file (we can also do it by Google Cloud Console approach):           
gsutil cp gs://my-bucket/helloworld.py Desktop
# Remove a file: 
gsutil rm gs://chuwei/helloworld.py
# Remove the whole bucket:
gsutil rm -r gs://chuwei


# Before running jobs on a Google Cloud dataproc cluster, firstly to create a cluster: 
# like a new cluster name chuweizhou, within a project with the id 01234
gcloud dataproc clusters create chuweizhou --project 01234 --bucket chuwei
# submit a job: 
gcloud dataproc jobs submit pyspark --cluster chuweizhou helloworld.py
# Delete a cluster:
gcloud dataproc clusters delete chuweizhou
# Delete the bucket:
gsutil rm -r gs://chuwei                             
```
                  
Now we can try to run the Jupyter notebooks on Google Cloud Dataproc clusters.                 

                  
                    
                    

                      
**Yours,**                
**Chuwei Zhou**                    
**2019.01.18**                                 
