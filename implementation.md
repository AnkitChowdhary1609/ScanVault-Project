## 🛠️ Step-by-Step Setup: AWS-Based Receipt Automation Pipeline

This walkthrough will help you build a serverless receipt processing system using AWS tools from start to finish.

---

## 1️⃣ Set Up Amazon S3 Bucket (for receipt uploads)

### ✅ Instructions:

1.	Go to S3 Console → Click "Create Bucket"
2.	Choose your region (e.g., ap-south-1)
3.	Give it a name (e.g., scanvault-storage-ankit1609)
5.	Click "Create bucket"
6.	Inside the bucket, create a folder (e.g., scanvault-incoming/) for organized uploads

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 04 55 PM" src="https://github.com/user-attachments/assets/e9fbb5ae-435c-4c41-bcc2-6038eb20a0d1" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 05 46 PM" src="https://github.com/user-attachments/assets/f675c309-a99e-4729-8c64-bbe75b51537b" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 06 47 PM" src="https://github.com/user-attachments/assets/e44a4832-eda0-426a-9f70-354dde7871d0" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 07 22 PM" src="https://github.com/user-attachments/assets/2db7365a-3baa-4bec-8d1f-814cfb521dc0" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 08 35 PM" src="https://github.com/user-attachments/assets/ed45f1b8-d438-45d4-ae9d-39003a077381" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 08 59 PM" src="https://github.com/user-attachments/assets/80035b91-38f1-41d8-94d1-4f7141c64458" />

## 2️⃣ Configure DynamoDB Table (for storing extracted data)

### ✅ Instructions:

1.	Navigate to DynamoDB Console → Click "Create Table"
2.	Table Name: ScanVault-Receipts-Table
3.	Set Partition Key as receipt_id (Type: String)
4.	Set Sort Key as date (Type: String) 
5.	Click "Create"

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 09 31 PM" src="https://github.com/user-attachments/assets/2d113e67-4b77-46a4-b9cd-5a319c371912" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 11 31 PM" src="https://github.com/user-attachments/assets/41cf98f2-1d18-4282-a15c-cf26222a314f" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 11 59 PM" src="https://github.com/user-attachments/assets/10cb0917-1575-4994-8d35-dd9317227192" />


## 3️⃣ Setup Amazon SES (for email alerts)

### ✅ Instructions:

1.	Open Amazon SES Console
2.	Under Verified Identities, verify your sender email
3.	If your account is in sandbox mode, also verify recipient email
4.	Note the selected region (e.g., ap-south-1) for Lambda usage

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 12 45 PM" src="https://github.com/user-attachments/assets/b4a861ca-e3b9-4f64-9181-6f47d1720de0" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 13 37 PM" src="https://github.com/user-attachments/assets/68a322b2-5fb4-4771-b500-849a9056ac14" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 13 54 PM" src="https://github.com/user-attachments/assets/bfdb52f8-8457-4838-b986-bcdc934268da" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 14 38 PM" src="https://github.com/user-attachments/assets/753cb89e-bb52-494c-82dd-35218f64cf88" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 5 57 41 PM" src="https://github.com/user-attachments/assets/4e4cb0b0-9c28-45dc-ad71-06cde15b193c" />

## 4️⃣ Create IAM Role for Lambda (permissions handler)

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

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 17 10 PM" src="https://github.com/user-attachments/assets/4b320672-6ef5-4439-bfa7-462e68e0707c" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 17 55 PM" src="https://github.com/user-attachments/assets/d606731e-57f3-40e7-94bd-85570f570c7b" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 18 33 PM" src="https://github.com/user-attachments/assets/233b4e0b-9144-4983-a41b-036f2a4f4fd3" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 19 19 PM" src="https://github.com/user-attachments/assets/568abf38-dc65-494b-81d8-139bd28c5d45" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 19 32 PM" src="https://github.com/user-attachments/assets/94ee1e82-fecb-4cc3-9782-c31fb3bcf3c7" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 19 56 PM" src="https://github.com/user-attachments/assets/b7bbdc16-38ad-4fc6-a084-dc274f22153c" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 20 09 PM" src="https://github.com/user-attachments/assets/6d699f1a-4a89-4edc-bb3b-ecd5c31030c3" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 20 35 PM" src="https://github.com/user-attachments/assets/f395efe1-1660-44f0-9ca2-ad5d62f9f25d" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 21 33 PM" src="https://github.com/user-attachments/assets/d7b870b7-6fbf-4598-9cb8-7e7b29631314" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 21 39 PM" src="https://github.com/user-attachments/assets/f8ef529e-f941-4e84-a84a-df4af9b551d3" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 21 48 PM" src="https://github.com/user-attachments/assets/4f7d412a-c8a5-4dcd-a30b-5dec135bcbf4" />

## 5️⃣ Deploy the Lambda Function (core processor)

### ✅ Instructions:

1.	Visit AWS Lambda Console → Click "Create Function"
2.	Function Name: processingLambda
3.	Runtime: Choose Python 3.9 or Node.js
4.	Use existing role → Select ScanVault-lambdrole
5.	In Configuration → Environment variables, add required key-values
6.	Go to Code section → Paste the code from your python.py → Click Deploy
7.	In Configuration → General settings, click Edit
8.	Increase the timeout to 2 minutes (default is too low for large files)

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 15 21 PM" src="https://github.com/user-attachments/assets/658e61ab-44a8-40f6-bcde-61b5d10c8dc9" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 16 38 PM" src="https://github.com/user-attachments/assets/fb58be25-4cc1-466b-9064-23ccc387d135" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 22 24 PM" src="https://github.com/user-attachments/assets/1ee7149e-64eb-4210-a08f-a810c75d30d9" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 8 09 06 PM" src="https://github.com/user-attachments/assets/cff7de4d-cb6c-4846-9270-cf72f0bb41b8" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 26 10 PM" src="https://github.com/user-attachments/assets/27256de8-bd01-4b5e-9fbb-3a36dd28b1e5" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 26 21 PM" src="https://github.com/user-attachments/assets/9de06203-b52a-43d5-aa1b-1412f12d694d" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 23 32 PM" src="https://github.com/user-attachments/assets/6311672e-03a9-488d-b519-35bb7a6d390b" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 23 44 PM" src="https://github.com/user-attachments/assets/b1776523-b6ff-4b8d-9a25-34e8abf6b4c6" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 23 50 PM" src="https://github.com/user-attachments/assets/5eed89b1-5a17-442f-a061-cfb4a267bebd" />

## 6️⃣ Set Up S3 Trigger for Lambda

### ✅ Instructions:

1.	Open the S3 Bucket
2.	Go to the Properties tab
3.	Scroll to Event Notifications → Click "Create event notification"
4.	Prefix: incoming/
5.	Event type: All object create events

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 27 40 PM" src="https://github.com/user-attachments/assets/1f4c810e-fbe6-4c01-b0bf-ed24768235ad" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 29 19 PM" src="https://github.com/user-attachments/assets/a1317cc1-c253-4bab-8daa-e3e756106855" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 29 25 PM" src="https://github.com/user-attachments/assets/bd11d84f-d7c0-49b6-ab58-23f9596405f7" />

## 7️⃣ Upload a Sample Receipt (to test the pipeline)

### ✅ Instructions:

1.	Open the S3 Bucket you created
2.	Navigate into the scanvault-incoming/ folder
3.	Click "Upload"
4.	Select a sample receipt image or PDF
5.	Click "Upload"
6.	The Lambda function will automatically process it, extract the data using Textract, store it in DynamoDB, and send an email via SES

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 33 56 PM" src="https://github.com/user-attachments/assets/e919839d-a0c4-4485-9a40-589c1e962c59" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 36 29 PM" src="https://github.com/user-attachments/assets/48872aab-2e74-4675-a885-acd274e39a5c" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 36 37 PM" src="https://github.com/user-attachments/assets/5a96d016-7c94-4ae8-bcab-858a60b56551" />

## 8️⃣ Repeat step number 3 again to verify the another mail account aswell

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 38 25 PM" src="https://github.com/user-attachments/assets/506bda39-2a3d-42e3-98ec-109dabc98832" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 38 36 PM" src="https://github.com/user-attachments/assets/9e935cdb-7831-434f-9426-7b5af12cd1fc" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 39 06 PM" src="https://github.com/user-attachments/assets/24e22207-cb10-4150-8d03-b16634487f2f" />

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 42 43 PM" src="https://github.com/user-attachments/assets/09f016c4-804b-4d4d-95a9-5aed7f72d013" />

## ⌨️ Code

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 8 09 19 PM" src="https://github.com/user-attachments/assets/7ede30ca-7ff0-4acb-88f6-b430974028ca" />

## 📨 Result

<img width="1470" height="956" alt="Screenshot 2025-07-18 at 4 42 01 PM" src="https://github.com/user-attachments/assets/17bd87ec-a707-403f-b4dc-c22f6ed37277" />


✍️ **Author**: *Ankit Chowdhary*  
📬 *Feel free to connect on [LinkedIn](https://www.linkedin.com/in/ankit-chowdhary-1609ac/)*  




