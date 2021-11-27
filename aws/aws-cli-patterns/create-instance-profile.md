# Something

## Create IAM Role and attach Trust Policy

```
aws iam create-role --role-name DEV_ROLE --assume-role-policy-document file://trust_policy_ec2.json
```

## Create the Policy (s3_read_access.json)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
          "Sid": "AllowUserToSeeBucketListInTheConsole",
          "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
          "Effect": "Allow",
          "Resource": ["arn:aws:s3:::*"]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::cfst-3035-730dfae8c7f86d612403a8af99b-s3bucketdev-azae8573faiw/*",
                "arn:aws:s3:::cfst-3035-730dfae8c7f86d612403a8af99b-s3bucketdev-azae8573faiw"
            ]
        }
    ]
}
```

## Attach the policy document to the policy

```
aws iam create-policy --policy-name DevS3ReadAccess --policy-document file://dev_s3_read_access.json
```

## Create Instance Profile and attach the IAM Policy

```
aws iam attach-role-policy --role-name DEV_ROLE --policy-arn "arn:aws:iam::172347799282:policy/DevS3ReadAccess"

aws iam create-instance-profile --instance-profile-name DEV_PROFILE

aws iam add-role-to-instance-profile --instance-profile-name DEV_PROFILE --role-name DEV_ROLE
```

## List the attached role policies (instance profile)

```
aws iam list-attached-role-policies --role-name DEV_ROLE
```

## Validate instance profile

```
aws iam get-instance-profile --instance-profile-name DEV_PROFILE
```

## Associate the instance profile with EC2 instance

```
aws ec2 associate-iam-instance-profile --instance-id i-0d995a89f159095ce --iam-instance-profile Name="DEV_PROFILE"
```

## Validate EC2 has instance profile attached

```
aws ec2 describe-instances --instance-ids i-0d995a89f159095ce
```

## Validate EC2 has assumed the correct instance profile

```
aws sts get-caller-identity
```