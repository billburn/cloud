## S3 Sample CORS Policy

* This policy is applied on the destination bucket, where you want the resources to be pulled from
* We allow our source bucket to pull resources from the destination bucket
```
[
    {
        "AllowedHeaders": [
            "Authorization"
        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "http://mysourcebucket-devops-associate.s3-website-us-east-1.amazonaws.com"
        ],
        "MaxAgeSeconds": 3000
    }
]
```