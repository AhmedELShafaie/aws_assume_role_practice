# aws_assume_role_practice


## This repo aim to test Github action with AWS AssumeRole 

    1. Create identity provider
        . Choose OpenID Connect
            Provider URL:   https://token.actions.githubusercontent.com
            Audience:   sts.amazonaws.com
        . Create IAM Role 
            * Choose Web identity 
            * Choose Identity provider: "https://token.actions.githubusercontent.com"
            * Choose Audience: sts.amazonaws.com
            * Add permissions(Policies) 
            * Set Role name,Description
            * In the Select trusted entities it will show 
````json
{
"Version": "2012-10-17",
"Statement": [
    {
        "Effect": "Allow",
        "Action": "sts:AssumeRoleWithWebIdentity",
        "Principal": {
            "Federated": "arn:aws:iam::xxxxxxxxxxxx:oidc-provider/token.actions.githubusercontent.com"
        },
        "Condition": {
            "StringEquals": {
                "token.actions.githubusercontent.com:aud": [
                    "sts.amazonaws.com"
                ]
            }
        }
    }
]
}
````