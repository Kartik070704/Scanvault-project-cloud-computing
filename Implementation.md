🛠️ Step-by-Step Setup: AWS-Based Receipt Automation Pipeline
This walkthrough will help you build a serverless receipt processing system using AWS tools from start to finish.
________________________________________
1️⃣ Set Up Amazon S3 Bucket (for receipt uploads)
✅ Instructions:
1.	Go to S3 Console → Click "Create Bucket"
2.	Choose your region (e.g., ap-south-1)
3.	Give it a name (e.g., scanvault-storage-kartik07)
4.	Click "Create bucket"
5.	Inside the bucket, create a folder (e.g., scanvault-incoming/) for organized uploads
 

2️⃣ Configure DynamoDB Table (for storing extracted data)
✅ Instructions:
1.	Navigate to DynamoDB Console → Click "Create Table"
2.	Table Name: ScanVault-Receipts-Table
3.	Set Partition Key as receipt_id (Type: String)
4.	Set Sort Key as date (Type: String)
5.	Click "Create"
 
 
3️⃣ Setup Amazon SES (for email alerts)
✅ Instructions:
1.	Open Amazon SES Console
2.	Under Verified Identities, verify your sender email
3.	If your account is in sandbox mode, also verify recipient email
4.	Note the selected region (e.g., ap-south-1) for Lambda usage	 
 
 
4️⃣ Create IAM Role for Lambda (permissions handler)
✅ Instructions:
1.	Go to IAM Console → Click Roles → Create Role
2.	Choose Lambda as the use case
3.	Attach the following policies:
o	AmazonS3ReadOnlyAccess
o	AmazonTextractFullAccess
o	AmazonDynamoDBFullAccess
o	AmazonSESFullAccess
o	AWSLambdaBasicExecutionRole
4.	Name the role: ScanVault-lambdrole
 
 
5️⃣ Deploy the Lambda Function (core processor)
✅ Instructions:
1.	Visit AWS Lambda Console → Click "Create Function"
2.	Function Name: processingLambda
3.	Runtime: Choose Python 3.9 or Node.js
4.	Use existing role → Select ScanVault-lambdrole
5.	In Configuration → Environment variables, add required key-values
6.	Go to Code section → Paste the code from your python.py → Click Deploy
7.	In Configuration → General settings, click Edit
8.	Increase the timeout to 2 minutes (default is too low for large files)

 
6️⃣ Set Up S3 Trigger for Lambda
✅ Instructions:
1.	Open the S3 Bucket
2.	Go to the Properties tab
3.	Scroll to Event Notifications → Click "Create event notification"
4.	Prefix: incoming/
5.	Event type: All object create events
 
Thank You…………
