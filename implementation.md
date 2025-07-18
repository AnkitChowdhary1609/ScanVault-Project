## 🛠️ Step-by-Step Setup: AWS-Based Receipt Automation Pipeline

This walkthrough will help you build a serverless receipt processing system using AWS tools from start to finish.

---

## Set Up Amazon S3 Bucket (for receipt uploads)

### ✅ Instructions:

1.	Go to S3 Console → Click "Create Bucket"
2.	Give it a name (e.g., scanvault-storage-ankit1609)
3.	Choose your region (e.g., ap-south-1)
4.	Click "Create bucket"
5.	Inside the bucket, create a folder (e.g., scanvault-incoming/) for organized uploads

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 04 55 PM" src="https://github.com/user-attachments/assets/e9fbb5ae-435c-4c41-bcc2-6038eb20a0d1" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 06 47 PM" src="https://github.com/user-attachments/assets/e44a4832-eda0-426a-9f70-354dde7871d0" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 05 46 PM" src="https://github.com/user-attachments/assets/f675c309-a99e-4729-8c64-bbe75b51537b" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 07 22 PM" src="https://github.com/user-attachments/assets/2db7365a-3baa-4bec-8d1f-814cfb521dc0" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 08 35 PM" src="https://github.com/user-attachments/assets/ed45f1b8-d438-45d4-ae9d-39003a077381" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 08 59 PM" src="https://github.com/user-attachments/assets/80035b91-38f1-41d8-94d1-4f7141c64458" />

## Configure DynamoDB Table (for storing extracted data)

### ✅ Instructions:

1.	Navigate to DynamoDB Console → Click "Create Table"
2.	Table Name: ScanVault-Receipts-Table
3.	Set Partition Key as receipt_id (Type: String)
4.	Set Sort Key as date (Type: String) 
5.	Click "Create"

## Setup Amazon SES (for email alerts)

### ✅ Instructions:

1.	Open Amazon SES Console
2.	Under Verified Identities, verify your sender email
3.	If your account is in sandbox mode, also verify recipient email
4.	Note the selected region (e.g., ap-south-1) for Lambda usage

## Create IAM Role for Lambda (permissions handler)

### ✅ Instructions:

1.	Go to IAM Console → Click Roles → Create Role
2.	Choose Lambda as the use case
3.	Attach the following policies:
    *	AmazonS3ReadOnlyAccess
    *	AmazonTextractFullAccess
    *	AmazonDynamoDBFullAccess
    *	AmazonSESFullAccess
    *	AWSLambdaBasicExecutionRole
4.	Name the role: ScanVault-lambdrole

## Deploy the Lambda Function (core processor)

### ✅ Instructions:

1.	Visit AWS Lambda Console → Click "Create Function"
2.	Function Name: processingLambda
3.	Runtime: Choose Python 3.9 or Node.js
4.	Use existing role → Select ScanVault-lambdrole
5.	In Configuration → Environment variables, add required key-values
6.	Go to Code section → Paste the code from your python.py → Click Deploy
7.	In Configuration → General settings, click Edit
8.	Increase the timeout to 2 minutes (default is too low for large files)

## Set Up S3 Trigger for Lambda

### ✅ Instructions:

1.	Open the S3 Bucket
2.	Go to the Properties tab
3.	Scroll to Event Notifications → Click "Create event notification"
4.	Prefix: incoming/
5.	Event type: All object create events

## Upload a Sample Receipt (to test the pipeline)

### ✅ Instructions:

1.	Open the S3 Bucket you created
2.	Navigate into the scanvault-incoming/ folder
3.	Click "Upload"
4.	Select a sample receipt image or PDF
5.	Click "Upload"
6.	The Lambda function will automatically process it, extract the data using Textract, store it in DynamoDB, and send an email via SES

## Repeat step number 3 again to verify the another mail account aswell

✍️ **Author**: *Ankit Chowdhary*  
📬 *Feel free to connect on [LinkedIn](https://www.linkedin.com/in/ankit-chowdhary-1609ac/)*  




