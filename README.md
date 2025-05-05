# 📦 S3 Upload Monitor & Daily Email Notification System

This project is an automated S3 upload monitoring and reporting system built using AWS services and written in Go (Golang). It logs every file upload to a monitored S3 bucket and sends a daily summary email to selected users with details about the uploaded files.

---

## 🛠️ Technologies Used

- **AWS Lambda** – For serverless event processing
- **Amazon S3** – Storage of uploaded objects
- **Amazon DynamoDB** – To log and store object metadata
- **Amazon SES** – To send daily summary emails
- **Amazon EventBridge** – To trigger daily scheduled tasks
- **Go (Golang)** – Programming language for all Lambda functions

---

## 📌 Features

- Realtime capture of S3 object uploads
- Metadata extraction (S3 URI, object name, size, type)
- Logs data in DynamoDB
- Daily email summary sent via Amazon SES
- Fully serverless, scalable, and low-cost architecture

---

## 🧭 Architecture Overview

```plaintext
  [User Uploads to S3]
           ↓
   [S3 Event Notification]
           ↓
  [Lambda Function #1]
   ↳ Extract Metadata
   ↳ Store in DynamoDB

    [Daily Schedule - EventBridge]
                    ↓
           [Lambda Function #2]
           ↳ Query DynamoDB
           ↳ Send Email via SES
````

---

## 🧩 Data Stored in DynamoDB

| Field         | Description                        |
| ------------- | ---------------------------------- |
| `date`        | Partition key (upload date)        |
| `object_name` | Sort key (name of uploaded object) |
| `uri`         | Full S3 URI of the object          |
| `size`        | File size in bytes                 |
| `type`        | File type (MIME or extension)      |

---

## 📧 Daily Email Format

At the end of each day, the system sends an email with the following table:

| S3 URI                     | Object Name | Object Size | Type      |
| -------------------------- | ----------- | ----------- | --------- |
| s3://bucket-name/file1.png | file1.png   | 1.2 MB      | image/png |
| s3://bucket-name/data.csv  | data.csv    | 32 KB       | text/csv  |

---


---

## 🚀 Deployment Steps

1. Create and configure:

   * S3 bucket
   * DynamoDB table
   * Verified SES emails
2. Deploy Lambda #1 for S3 trigger
3. Deploy Lambda #2 and set up EventBridge schedule
4. Ensure IAM roles have correct permissions
5. Upload files to S3 and verify emails

---

## 🧪 Testing

* Upload files via AWS Console or SDK to the S3 bucket.
* Check DynamoDB entries for object metadata.
* Review SES inbox after scheduled run.
* Use CloudWatch Logs for debugging.

---
