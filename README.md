
## Route 53
use load balance to divert the service to active datacentre.
use route 53 DNS services to connect an application that is deployed in a different location.



## scale out - scaling the same size of server in multiple locations - cost effective
## scale up - increase the size of the server

- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
- `sudo apt-get install python`
- `sudo apt-get install python-pip`
- `sudo apt-get install awscli`
- `aws configure`
- enter your AWS access key
- enter your AWS secret key
- when prompted for the region enter `eu-west-1`
- when prompted for output format enter `json`
- `aws s3 ls` (will list all the s3 buckets) example-trello uses s3 bucket to store images
- `aws s3 mb` (make buckets) - aws s3 mb s3://devops-bootcamp-barath-bucket (naming convention use - not _ & uppercase)
- create a any type of file in local `sudo nano devops_bootcamp_test.text`
- copy the file to the bucket `aws s3 cp (copy) devops_bootcamp_test.text s3://devops-bootcamp-barath-bucket/`

**BY DEFAULT THE FILE WILL BE RESTRICTED TO VIEW BY ANY OTHERS UNLESS IS THE PERMISSION IS AUTHORIZED**
to make it globally accessible follow the steps shown below
- go the S3 bucket
- edit bucket policy to grant public read access to your bucket
- add the following code and update the Resource to your bucket name
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}

- save changes


delete the file from the local vm
aws s3 sync s3://devops-bootcamp-barath-bucket/ devops_bootcamp_test.text (download from the bucket as a directory)
aws s3 rm s3://devops-bootcamp-barath-bucket/devops_bootcamp_test.text (delete the file from the bucket)
aws s3 rb s3://devops-bootcamp-barath-bucket (remove the bucket)
 