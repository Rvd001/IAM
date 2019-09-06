# IAM

# IAM POLICY STRUCTURE
``` json
 {
"Statement":[{
"Effect":"effect",
"Principal":"principal",
"Action":"action",
"Resource":"arn",
"Condition":{
    "condition":{"Key":"Value"}
        }
    }
  ]
}

```


# Ensure developers cannot turn off cloudTrail, create IAM users, or set up AWS Directory Service
### This is a Service control POLICY

``` json
{
    "Version": "2012-10-17",
    "Statement":[
        {

            "sid": "DenyUnapprovedAction",
            "Effect": "Deny",
            "Action": [

                "ds:*",
                "iam:CreateUser",
                "Cloudtrail:stoplogging"

            ],

            "Resource": [
                "*"
            ]

        }

    ]

}

```
# Ensure your Developers can create resources, but only in approved regions

``` json

{
    "Effect": "Allow",
    "Action": [
        "secretsmanager:*",
        "lambda:*",
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject"

    ],

    "Resources": "*",
    "Condition": {

        "StringEquals": {

            "aws:RequestedRegion": [
                "us-west-1",
                "us-west-2"


            ]



        }

    }

}

```
