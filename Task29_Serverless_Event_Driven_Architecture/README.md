TASK 5 — Serverless + Event-Driven Architecture (AWS + Azure)
📌 Objective

Implement an event-driven serverless architecture using:

Storage Triggers

Serverless Compute

Managed NoSQL Databases

Monitoring & Logging

This project demonstrates cloud-native architecture using AWS and Azure.

🌍 Architecture Overview
🔹 AWS Flow
User Upload → Amazon S3 → AWS Lambda → DynamoDB → CloudWatch Logs
🔹 Azure Flow
User Upload → Azure Blob Storage → Azure Function → Cosmos DB

Both architectures are fully serverless and event-driven.

☁️ PART 1 — AWS IMPLEMENTATION
🔹 Step 1: Create S3 Bucket

Navigate to AWS Console → S3

Click Create bucket

Name: serverless-task5-bucket

Region: Same for all resources

Keep default settings

Create bucket

Purpose: Stores uploaded files and triggers Lambda.

🔹 Step 2: Create DynamoDB Table

Go to DynamoDB → Create table

Table name: Task5Table

Partition key: id (String)

Capacity mode: On-demand

Create table

Purpose: Stores metadata of uploaded files.

🔹 Step 3: Create IAM Role for Lambda

Go to IAM → Roles → Create role

Trusted entity: Lambda

Attach policies:

AWSLambdaBasicExecutionRole

AmazonDynamoDBFullAccess

Role name: LambdaTask5Role

Purpose: Grants Lambda permission to write logs and access DynamoDB.

🔹 Step 4: Create Lambda Function

Go to Lambda → Create function

Name: Task5Lambda

Runtime: Python 3.x

Execution role: Use LambdaTask5Role

Replace default code with:

import json
import boto3
import uuid

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Task5Table')

def lambda_handler(event, context):
    for record in event['Records']:
        file_name = record['s3']['object']['key']
        
        table.put_item(
            Item={
                'id': str(uuid.uuid4()),
                'file_name': file_name
            }
        )

    return {
        'statusCode': 200,
        'body': json.dumps('Data stored successfully!')
    }

Click Deploy.

🔹 Step 5: Configure S3 Trigger

Open Lambda → Add Trigger

Select S3

Choose your bucket

Event type: All object create events

Add trigger

Now Lambda runs automatically when a file is uploaded.

🔹 Step 6: Verify Logs (CloudWatch)

Go to CloudWatch → Log Groups

Open:

/aws/lambda/Task5Lambda

Logs are created automatically after first execution.

🔹 Step 7: Test AWS Architecture

Upload file to S3

Check:

Lambda Monitoring tab

CloudWatch Logs

DynamoDB table items

Expected Result:
A new item with file name is inserted into DynamoDB.

☁️ PART 2 — AZURE IMPLEMENTATION
🔹 Step 1: Create Resource Group

Azure Portal → Resource Groups

Name: rg-task5

Region: Same for all services

🔹 Step 2: Create Storage Account (Blob)

Azure Portal → Storage Accounts → Create

Name: task5storage

Region: Same

Performance: Standard

Redundancy: LRS

After creation:

Go to Containers

Create container named:

uploads

Purpose: Uploading files triggers Azure Function.

🔹 Step 3: Create Cosmos DB

Azure Portal → Azure Cosmos DB → Create

API: Core (SQL)

Account name: task5cosmos

After deployment:

Data Explorer → Create Database:

Task5DB

Create Container:

Task5Container

Partition key: /id

Purpose: Stores file metadata.

🔹 Step 4: Create Azure Function App

Azure Portal → Function App → Create

Runtime: Python

Plan: Consumption (Serverless)

Region: Same

🔹 Step 5: Create Blob Trigger Function

Inside Function App → Functions → Create

Template: Blob Trigger

Storage account: Select created storage

Container: uploads

🔹 Step 6: Connect Function to Cosmos DB

Replace code with:

import logging
import uuid
import azure.functions as func
from azure.cosmos import CosmosClient

def main(myblob: func.InputStream):

    url = "YOUR_COSMOS_URL"
    key = "YOUR_COSMOS_KEY"

    client = CosmosClient(url, credential=key)
    database = client.get_database_client("Task5DB")
    container = database.get_container_client("Task5Container")

    item = {
        "id": str(uuid.uuid4()),
        "file_name": myblob.name
    }

    container.create_item(body=item)

    logging.info(f"Stored {myblob.name} in Cosmos DB")

Get URI and Key from:
Cosmos DB → Keys

Save and deploy.

🔹 Step 7: Test Azure Architecture

Upload file to Blob container uploads

Check:

Function Monitor logs

Cosmos DB Data Explorer

Expected Result:
A new document with file name appears in Cosmos DB.

📊 Monitoring & Logging
Platform	Monitoring Tool
AWS	CloudWatch Logs
Azure	Function Monitor + Application Insights
🏗️ Key Concepts Demonstrated

Event-driven architecture

Serverless computing

Object storage triggers

Managed NoSQL databases

Cloud monitoring

Cross-cloud implementation

💰 Cost Considerations

Both implementations use:

Serverless compute (pay per execution)

On-demand NoSQL database

Standard storage

Costs remain very low for testing purposes.


✅ Final Outcome

Successfully implemented:

✔ Event-driven architecture
✔ Fully serverless infrastructure
✔ Managed database integration
✔ Monitoring and logging enabled
✔ Cross-cloud deployment (AWS + Azure)

🎉 Task Completed Successfully

This project demonstrates practical implementation of modern cloud-native serverless architecture across two major cloud providers.
