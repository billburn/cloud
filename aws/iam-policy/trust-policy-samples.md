# Trust Policies

## Simple Trust Policy

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## Multi-Service Trust Policy

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
    "Service": [
        "ec2.amazonaws.com",
        "s3.amazonaws.com"
   ]
},
      "Action": "sts:AssumeRole"
    }
  ]
}
```

[URL](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)