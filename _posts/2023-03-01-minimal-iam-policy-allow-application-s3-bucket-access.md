---
title: 'The minimal AWS IAM policy for using a bucket with an application'
type: post
date: 2023-03-01 13:30
tags: amazon aws iam policy bucket s3
category: devops
image: https://source.unsplash.com/BrunIOLQMfQ
---

This is the minimal policy for an application to access only an AWS S3 bucket in which it would upload / download files and generate signed urls for public access.

![Sad eggs](https://source.unsplash.com/BrunIOLQMfQ)

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetObjectAcl",
                "s3:PutObjectAcl",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket-name",
                "arn:aws:s3:::bucket-name/*"
            ]
        }
    ]
}
```

Create a IAM user. Attach the above policy with `bucket-name` replaced.

Enjoy and remember to ignore all people that suggest you attach a give all permissions policy. You don't give your house keys to strangers, right?
