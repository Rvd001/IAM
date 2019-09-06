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
# Enable your developers to create IAM roles to pass to EC2 and Lambda, but ensure they cannot exceed their own permission
### (Allow create role but only with a specifiv permission boundary allow attach managed policies but only to roles with a specific boundary)


``` json

    {

        "Effect": "Allow",
        "Action": [

            "iam:DetachRolePolicy",
            "iam:CreateRole",
            "iam:AttachRolePolicy"

        ],

        "Resource": "arn:aws:iam::123456789:role/unicorns-*",
        "Condition":{
            "StringEquals": {
                "iam:PermissionsBoundary":
                "arn:aws:iam::123456789:policy/region-restriction"

            }

        }

    }

```

# Enable developers working on the Dorky Project and the Sneaky Project to manage their own resources without also managing the other project's

``` json




```