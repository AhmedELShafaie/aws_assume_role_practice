# aws_assume_role_practice


## This repo aim to test Github action with AWS AssumeRole :joy:

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
                "token.actions.githubusercontent.com:sub" [
                    "repo:ahmedelshafaie/aws_assume_role_practice:ref:refs/heads/main"
                ],  
                "token.actions.githubusercontent.com:aud": [
                    "sts.amazonaws.com"
                ]
            }
        }
    }
]
}
````

We need to add to which Github actions we need to authorize this role.
This is made by adding provider_identity in this case "token.actions.githubusercontent.com" with ":sub"
token.actions.githubusercontent.com:sub [
    repo:GITHUB_USER||GITHUB_ORG/REPOSITORY_NAME:pull_request" ,
    repo:GITHUB_USER||GITHUB_ORG/REPOSITORY_NAME:ref:refs/head/branch_name     ###This is for push request to branch
]


