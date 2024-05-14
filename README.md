{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lambda:*",
                "states:*"
            ],
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "lambda:FunctionName": "abc-*",
                    "states:StateMachineArn": "arn:aws:states:*:*:stateMachine:abc-*"
                }
            }
        },
        {
            "Effect": "Deny",
            "Action": [
                "lambda:DeleteFunction",
                "states:DeleteStateMachine"
            ],
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "lambda:FunctionName": "abc-*",
                    "states:StateMachineArn": "arn:aws:states:*:*:stateMachine:abc-*"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams",
                "logs:GetLogEvents"
            ],
            "Resource": "arn:aws:logs:*:*:log-group:/aws/lambda/abc-*:*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/Project": "abc"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::abc-*",
                "arn:aws:s3:::abc-*/*"
            ],
            "Condition": {
                "StringEquals": {
                    "s3:prefix": "abc",
                    "s3:delimiter": "/"
                }
            }
        }
    ]
}
