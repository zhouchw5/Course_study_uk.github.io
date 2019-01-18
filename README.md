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
!(the interface of GCP)[https://github.com/zhouchw5/Course_study_uk.github.io/blob/master/GCP.png]

                  
                    
                    

                      
**Yours,**                
**Chuwei Zhou**                    
**2019.01.18**                                 
