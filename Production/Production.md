# CloudLabs Validations Using AWS Lambda  

### Steps to Use CloudLabs Validations Using AWS Lambda  

**Prerequisites**

Before performing the validations using the AWS Lambda in Cloudlabs, ensure that the AWS Lambda Function is set up properly. To set them up, please follow the provided steps. 

1. Log in to your AWS Account and search for Lambda in the search bar. Then click on it. 

2. Then click on Functions and then click on Create Function.

3. Choose Author from scratch.

4. Function name: S3BucketChecker.

5. Runtime: Select Python 3.12 (or the latest version).

6. Under Permissions, click "Change default execution role" and select Use an existing role. Choose the LambdaS3CheckerRole you made in Step 1.

7. Click Create function.

8. In the "Code" tab, delete everything and paste this in:  

```
import boto3
from botocore.exceptions import ClientError

def lambda_handler(event, context):
    # REPLACE THIS with the name of the bucket you want to check
    bucket_name = 'your-bucket-name-here'
    
    s3 = boto3.client('s3')
    
    try:
        # This checks if the bucket exists and if you have permission to see it
        s3.head_bucket(Bucket=bucket_name)
        return {
            'statusCode': 200,
            'body': f"Success! S3 bucket '{bucket_name}' is there in the account."
        }
    except ClientError as e:
        # If it returns a 404, it means the bucket is not there
        return {
            'statusCode': 404,
            'body': f"S3 bucket '{bucket_name}' is not there in the account."
        }
```

9. Click Deploy at the top of the code editor.  

10. Click the Test button (blue button).

11. Give the test a name like MyTest. You don't need to change the JSON data.

12. Click Save, then click Invoke/test again. 

13. Navigate to the ODL (1) section in the left menu and go to your respective ODL. Click the Users (2) button and deploy the user.
