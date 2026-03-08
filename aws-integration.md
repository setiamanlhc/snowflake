# Configure a Snowflake storage integration to access Amazon S3


# Allow Snowflaket to Read S3 bucket

https://docs.snowflake.com/en/user-guide/data-load-s3-allow

1. Execute  USE ROLE to switch to AccountAdmin
```
USE ROLE ACCOUNTADMIN;
```

2. Query  SYSTEM$GET_SNOWFLAKE_PLATFORM_INFO() info.

```
SELECT SYSTEM$GET_SNOWFLAKE_PLATFORM_INFO();
```

3. Allow Snowflake VPC to access S3 bucket

```
{
   "Version":"2012-10-17",		 	 	 
   "Id": "Policy1415115909153",
   "Statement": [
     {
       "Sid": "Access-to-specific-VPC-only",
       "Principal": "*",
       "Action": "s3:*",
       "Effect": "Deny",
       "Resource": ["arn:aws:s3:::amzn-s3-demo-bucket",
                    "arn:aws:s3:::amzn-s3-demo-bucket/*"],
       "Condition": {
         "StringNotEquals": {
           "aws:SourceVpc": "vpc-1a2b3c4d"
         }
       }
     }
   ]
}

```
