# IAM

# IAM POLICY STRUCTURE
```json
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

# Ensure developers cannot turn off cloudTrail, create IAM users, or set up AWS Directory Service
### This is a Service control POLICY
```json
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
