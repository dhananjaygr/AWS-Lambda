# CloudLabs Validations Using AWS Lambda

### Steps to Use CloudLabs Validations Using AWS Lambda

### **Prerequisites**

Before performing validations using AWS Lambda in CloudLabs, please make sure that the AWS Lambda function is set up properly. To set it up, please follow the steps below.

1. Log in to your AWS account and search for **Lambda** in the search bar. Then click on it.

   ![](./Img/01.png)

2. Click on **Functions**, and then click on **Create function**.

   ![](./Img/02.png)

3. Choose **Author from scratch** and provide the following:

   **Function name**: `S3BucketChecker`

   **Runtime**: Select **Python 3.12** (or the latest version).

   ![](./Img/03.png)

5. Under **Permissions**, click **Change default execution role** and select **Use an existing role**. Choose the **LambdaS3CheckerRole** you created in Step 1. Then click **Create function**.

   ![](./Img/04.png)

6. In the **Code** tab, delete the existing code and paste the following:

   ```python
   import boto3
   from botocore.exceptions import ClientError

   def lambda_handler(event, context):
       # REPLACE THIS with the name of the bucket you want to check
       bucket_name = 'your-bucket-name-here'
       
       s3 = boto3.client('s3')
       
       try:
           # This checks if the bucket exists and if you have permission to access it
           s3.head_bucket(Bucket=bucket_name)
           return {
               'statusCode': 200,
               'body': f"Success! S3 bucket '{bucket_name}' exists in the account."
           }
       except ClientError:
           return {
               'statusCode': 404,
               'body': f"S3 bucket '{bucket_name}' does not exist in the account."
           }
   ```

7. Click **Deploy**.

   ![](./Img/05.png)

8. Click the **Test** button (blue button).

   ![](./Img/06.png)

9. Provide a test name such as **MyTest**. You do not need to modify the JSON data.

10. Click **Save**, and then click **Invoke/Test** again.

   ![](./Img/08.png)

11. Log in to the CloudLabs portal and navigate to the required tenant (WIZ). On the left-hand side of the page, you will see the **Template** section.

12. Navigate to **Template (1)** from the left menu and go to your respective template. Click the **Edit (2)** button.

13. Navigate to the **ODL (1)** section in the left menu, go to your respective ODL, click the **Users (2)** button, and deploy the user.

* Convert this into a **formal SOP**
* Add a **“Validation Result”** section
* Add **error-handling explanations**
* Make it **CloudLabs documentation–ready** (internal format)
