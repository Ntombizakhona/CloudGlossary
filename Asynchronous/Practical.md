### 🏗️ Let’s Build

Building an Asynchronous Image Processing Pipeline on AWS
---------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Build a real asynchronous pipeline where a user uploads an image to Amazon S3, which triggers an AWS Lambda function via Amazon SQS to generate a thumbnail.**

```
User uploads image → S3 Bucket → S3 Event Notification → SQS Queue → Lambda Function(s) → Thumbnail saved to S3
                                                                        ↑
                                                              Auto-scales to parallel
                                                              instances under load
```

_This will demonstrate asynchronous systems in the cloud._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  **A .jpg Image On Your Device To Test With**

### Add Additional Permissions to Your IAM Account

_Principle of Least Privilege: It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **Users**

**Step 05: Users**

Select the **Cloud Glossary** IAM User.

**Step 06: CloudGlossary**

Select **Permissions.**

Select **Add permissions.**

You should be redirected to the **Add permissions** page.

**Step 07: Add permissions**

**Permission options:** Attach policies directly

On the Search bar type and check:

**AmazonS3FullAccess**

**AmazonSQSFullAccess**

**AWSLambda_FullAccess**

**IAMFullAccess**

**CloudWatchLogsReadOnlyAccess**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 5** policies added to CloudGlossary

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your IAM Account.

### Create the S3 Buckets

**You need two buckets:** _one for original uploads and one for generated thumbnails._

**Step 10:** Open the **Amazon S3 Console**

Click Create bucket

**Step 11: Create bucket**

**AWS Region:** US East (N. Virginia) us-east-1

**Bucket type:** General purpose

**Bucket namespace:** Account Regional namespace (recommended)

**Bucket name:** async-uploads

Leave all other settings as default

Click **Create bucket**

**Step 12: Create bucket**

**AWS Region:** US East (N. Virginia) us-east-1

**Bucket type:** General purpose

**Bucket namespace:** Account Regional namespace (recommended)

**Bucket name:** async-thumbnails

Leave all other settings as default

Click **Create bucket**

💡 **Write down both bucket names. You’ll reference them throughout this tutorial.**

### Create the SQS Queue

_This queue sits between S3 and Lambda. When an image is uploaded, S3 sends a message to this queue instead of calling Lambda directly, giving you the decoupling and resilience that async is all about._

**Step 13:** Open the **Amazon SQS Console**

Make sure you’re in the same region as your S3 buckets.

**⚠️ This is critical.** S3 event notifications can only send to an SQS queue in the same region as the bucket. If the regions don’t match, no error will appear. Messages simply won’t be delivered, and your pipeline will silently fail.

**Step 14:** Click **Create queue**

**Step 15: Create queue**

**Type:** Standard

**Name:** async-image-queue

Click **Create queue**

✅**Green banner: Queue async-image-queue created successfully**

💡After creation, you’ll land on the queue’s detail page. Copy the **ARN** (it looks like arn:aws:sqs:us-east-1:123456789012:async-image-queue). You’ll need it next.

### Allow S3 to Send Messages to SQS

_S3 needs permission to push event notifications into your queue. We’ll set this up with a least-privilege access policy: only your specific uploads bucket can send messages to this specific queue._

**Step 16:** On your queue’s detail page in the SQS Console, click the **Queue policies** tab

**Step 17: Access policy**

Click **Edit**

Replace the existing policy with the following (update the placeholder values with your actual ARN and bucket name):

```
{
  "Version": "2012-10-17",
  "Statement": [    {
      "Sid": "AllowS3ToSendMessage",
      "Effect": "Allow",
      "Principal": {
        "Service": "s3.amazonaws.com"
      },
      "Action": "sqs:SendMessage",
      "Resource": "arn:aws:sqs:<your-region>:<your-account-id>:async-image-queue",
      "Condition": {
        "ArnEquals": {
          "aws:SourceArn": "arn:aws:s3:::async-uploads-<your-unique-id>"
        }
      }
    }
  ]
}
```

💡 _This policy follows the principle of least privilege. It only allows the S3 service to perform sqs:SendMessage, and only when the request comes from your specific uploads bucket. No other service or bucket can write to this queue._

Click **Save**

✅**Green banner: Saved configurations for queue async-image-queue successfully.**

**You can now send and receive messages.**

### Configure S3 Event Notifications

_Now tell your uploads bucket to send a message to SQS whenever a new .jpg file is uploaded._

**Step 17:** Go back to the **S3 Console** and click on your _async-uploads_-<your-unique-id> bucket

Click the **Properties** tab

Scroll down to **Event notifications** and click **Create event notification**

**Step 18: Create event notification**

**Event name:** image-upload-notification

**Suffix:** .jpg (this filters so only JPG uploads trigger the event)

**Event types:** check All object create events (**s3:ObjectCreated:***)

**Destination:** SQS queue

**Specify SQS queue:** Choose from your SQS queues

**SQS queue:** async-image-queue

Click **Save changes**

✅**Green banner: Successfully created event notification “image-upload-notification”.**

**Operation successfully completed.**

💡 _Now every .jpg upload to your bucket will drop a message into the SQS queue. The upload is done. The user isn’t waiting. This is the async handoff in action._

### Create the IAM Role for Lambda (Least Privilege)

_Before creating the Lambda function, it needs an IAM role that defines exactly what it’s allowed to do. We’ll scope this tightly to only the resources it needs._

**Step 19:** Open the **IAM Console**

On the left side of the screen under ▼ **Access management**

Select **Roles**

Click **Create role**

**Step 20: Select trusted entity**

**Trusted entity type:** AWS service

**Use case:** Lambda

Click **Next**

**Step 21: Add permissions**

Click **Next**

**Step 22: Name, review, create**

**Role name:** async-thumbnail-lambda-role

Click **Create role**

✅**Green banner: Role async-thumbnail-lambda-role created.**

**Step 23:** Attach a custom least-privilege policy

Click **View role.**

Under the **Permissions** tab: click **▼ Add permissions** → **Create inline policy**

**Step 24: Specify permissions**

**Policy editor:** JSON

Paste this with your information.

```
{
  "Version": "2012-10-17",
  "Statement": [    {
      "Sid": "ReadFromUploadsBucket",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::async-uploads-<your-unique-id>/*"
    },
    {
      "Sid": "WriteToThumbnailsBucket",
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::async-thumbnails-<your-unique-id>/*"
    },
    {
      "Sid": "ReadFromSQSQueue",
      "Effect": "Allow",
      "Action": [        "sqs:ReceiveMessage",
        "sqs:DeleteMessage",
        "sqs:GetQueueAttributes"
      ],
      "Resource": "arn:aws:sqs:<your-region>:<your-account-id>:async-image-queue"
    },
    {
      "Sid": "WriteLogs",
      "Effect": "Allow",
      "Action": [        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:<your-region>:<your-account-id>:log-group:/aws/lambda/async-thumbnail-generator:*"
    }
  ]
}
```

Click **Next**

**Step 25: Review and create**

**Policy name:** async-thumbnail-policy

Click **Create policy**

✅**Green banner: Policy async-thumbnail-policy created.**

**🔒 Least Privilege Breakdown:**

*   **s3:GetObject** means that Lambda can only _read_ from the uploads bucket, nothing else
*   **s3:PutObject** means that Lambda can only _write_ to the thumbnails bucket, nothing else
*   **sqs:ReceiveMessage, sqs:DeleteMessage, sqs:GetQueueAttributes** means that Lambda can only read and remove messages from this one queue (it needs all three to poll SQS)
*   **logs:*** mean that scoped to only this function’s log group, so Lambda can write its execution logs

### Create the Lambda Function

_Now let’s create the function that does the actual work: reading images and generating thumbnails._

**Step 26:** Open the **Lambda Console**

Click **Create function**

Select **Author from scratch**

**Function name:** async-thumbnail-generator

**Runtime:** Python 3.12

**Architecture:** x86_64

**Under Permissions:** expand **▶ Change default execution role**

**Execution role:** Use another role

**Choose an existing role:** async-thumbnail-lambda-role

Click **Create function**

✅**Green banner:** Successfully created the function **async-thumbnail-generator**

### Add the Pillow Layer

_Lambda doesn’t include the Pillow image library by default. We’ll add it as a layer so our function can resize images._

**Step 27: Dismiss** pop up

**Step 28:** On your function page, scroll down to Layers

Click **Edit**

**Step 29:** Edit layers

Click **Add a layer**

**Step 30: Choose a layer**

**Layer source:** Specify an ARN

**Enter the following ARN** (this is a community-maintained Pillow layer for Python 3.12):

```
arn:aws:lambda:us-east-1:770693421928:layer:Klayers-p312-Pillow:10
```

**⚠️ Note:** _This layer is maintained by the open-source_ [_Klayers project_](https://github.com/keithrozario/Klayers)_, not by AWS directly. If you’re using a different region than us-east-1, or if this version is outdated by the time you read this, check the_ [_Klayers GitHub repository_](https://github.com/keithrozario/Klayers) _for the correct ARN — look for the Pillow layer matching Python 3.12 in your region._

Click **Add**

Click **Save**

✅**Green banner:** Successfully updated the function **async-thumbnail-generator**.

### Add the Function Code

**Step 31:** Scroll to the Code section on your function page

In the code editor, replace the default contents of lambda_function.py with:

```
import boto3
import json
from PIL import Image
import io
import os
import urllib.parse
s3 = boto3.client("s3")
# Read the thumbnail bucket name from an environment variable
THUMBNAIL_BUCKET = os.environ["THUMBNAIL_BUCKET"]
THUMBNAIL_SIZE = (200, 200)
def lambda_handler(event, context):
    """
    Processes SQS messages triggered by S3 upload events.
    Each message contains info about an uploaded image.
    Lambda may receive multiple messages in a single invocation
    (based on the batch size configured on the SQS trigger).
    Under load, AWS runs many instances of this function in parallel.
    """
    for record in event["Records"]:
        # Each record is one SQS message
        # The SQS message body contains the S3 event notification as JSON
        try:
            body = json.loads(record["body"])
            # Validate that this is an S3 event with the expected structure
            if "Records" not in body or len(body["Records"]) == 0:
                print(f"Skipping non-S3 event message: {record['body'][:200]}")
                continue
            s3_event = body["Records"][0]
            source_bucket = s3_event["s3"]["bucket"]["name"]
            # URL-decode the key in case the filename has spaces or special characters
            source_key = urllib.parse.unquote_plus(
                s3_event["s3"]["object"]["key"]
            )
            print(f"Processing: s3://{source_bucket}/{source_key}")
            # Download the original image from the uploads bucket
            response = s3.get_object(Bucket=source_bucket, Key=source_key)
            image_content = response["Body"].read()
            # Create a 200x200 thumbnail
            image = Image.open(io.BytesIO(image_content))
            image.thumbnail(THUMBNAIL_SIZE)
            # Save the thumbnail to a bytes buffer
            buffer = io.BytesIO()
            image.save(buffer, "JPEG")
            buffer.seek(0)
            # Upload the thumbnail to the thumbnails bucket
            thumbnail_key = f"thumb-{source_key}"
            s3.put_object(
                Bucket=THUMBNAIL_BUCKET,
                Key=thumbnail_key,
                Body=buffer,
                ContentType="image/jpeg",
            )
            print(f"Thumbnail saved: s3://{THUMBNAIL_BUCKET}/{thumbnail_key}")
        except Exception as e:
            print(f"Error processing record: {str(e)}")
            print(f"Record body: {record.get('body', 'N/A')[:500]}")
            # Re-raise so SQS knows this message wasn't processed successfully.
            # The message will return to the queue (or go to the dead-letter queue
            # if one is configured) for retry.
            raise
    return {"statusCode": 200, "body": "Thumbnails generated"}
```

Click **Deploy** to save the code.

✅**Green banner:** Successfully updated the function **async-thumbnail-generator**.

💡**Why the try/except matters:** In asynchronous systems, failures happen in the background where no one is watching. Without error handling and logging, a corrupted image or unexpected message format would cause a silent failure. The try/except block logs the error for debugging, then re-raises the exception so SQS knows the message wasn’t processed, allowing it to be retried or sent to a dead-letter queue.

### Set the Environment Variable

_The function needs to know which bucket to write thumbnails to._

**Step 32:** Click the **Configuration** tab

Click **Environment variables** in the left sidebar

Click **Edit**

**Step 33: Edit environment variables**

Click **Add environment variable**

**Key:** THUMBNAIL_BUCKET

**Value:** async-thumbnails-<your-unique-id>

Click **Save**

✅**Green banner:** Successfully updated the function **async-thumbnail-generator**.

### Adjust the Timeout

_Image processing can take a few seconds. The default 3-second timeout is too short._

**Step 34:** Still in the **Configuration** tab

Click **General configuration**

Click **Edit**

**Step 35: Edit basic settings**

**Memory:** 256 MB

**Timeout:** 0 min 30 sec

Click **Save**

✅**Green banner:** Successfully updated the function **async-thumbnail-generator**.

### Connect SQS to Lambda

_This is the final wiring. We tell Lambda to automatically poll the SQS queue for new messages._

**Step 36:** On your Lambda function page, click **Add trigger**

**Step 37: Add trigger**

**Trigger configuration:** Select a source **▼**

Select **SQS**

**SQS Queue:** async-image-queue

**Activate trigger:** ✔ Checked

**Batch size:** 5

Click **Add**

✅**Green banner: The trigger async-image-queue was successfully added to function async-thumbnail-generator.**

💡 **What batch size means:** _A batch size of 5 means Lambda can receive up to 5 SQS messages in a single invocation. That’s why the function code loops through event[“Records”]. There could be 1 to 5 messages per call. If one message in a batch fails (and the exception is raised), all messages in that batch become visible in the queue again for retry. Under heavy load, AWS runs many Lambda instances in parallel, each handling its own batch. This is where async and parallel combine._

**Lambda will now automatically pick up messages from the queue and run your function. No servers to manage, no polling code to write.**

### Test It

_Time to see your async pipeline in action._

**Step 38:** Go to the **S3 Console** and open your **async-uploads**-<your-unique-id> bucket

Click **Upload**

Click **Add files** and select a **.jpg** image from your device

Click **Upload**

✅**Green banner: Upload succeeded**

_The upload completes immediately. Behind the scenes, here’s what’s happening asynchronously:_

1.  S3 sends an event notification to SQS _(event-driven)_
2.  The message sits in the queue _(message queue)_
3.  Lambda picks up the message, downloads the image, creates a thumbnail, and saves it _(serverless worker)_

**Step 39: Wait about 10–15 seconds, then:**

1.  Open your async-thumbnails-<your-unique-id> bucket
2.  You should see a file called thumb-<your-original-filename>.jpg
3.  Click on it and open it — that’s your auto-generated thumbnail

**Want to see parallel in action?** Try uploading 10 or 20 .jpg images at once. Check CloudWatch logs afterward, you may see multiple log streams, each representing a different Lambda instance that ran in parallel.

### If Something Went Wrong

_Check the Lambda logs:_

**Step 40:** Go to the **CloudWatch Console**

Click **▶ Logs** in the left sidebar

Click **Log management**

Under **Log Groups,** Click on **/aws/lambda/async-thumbnail-generator**

Click the most recent log stream

Look for error messages, common issues include:

**Access Denied:** double-check the bucket names in your IAM policy

**No module named ‘PIL’:** make sure the Pillow layer was added correctly

**Timeout:** increase the timeout in Lambda configuration

**No log streams at all:** check that the SQS queue and S3 bucket are in the same region

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _Lambda_ and **Delete** The Function.
2.  Navigate to S_QS_ and **Delete** The Queue
3.  Navigate to _S3_ and **Delete** The Buckets
4.  Navigate to _CloudWatch_ And **Delete** The Log group
5.  Navigate to _IAM_ and **Remove All Permissions, Roles and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
┌──────────┐       Event         ┌──────────┐      Trigger      ┌──────────────────┐
│          │   Notification      │          │                   │ AWS Lambda       │
│  Amazon  │ ──────────────────► │  Amazon  │ ─────────────────►│ Instance 1 ─────►│─┐
│    S3    │   "new .jpg file"   │   SQS    │   "process this"  │ Instance 2 ─────►│ │
│ (uploads)│                     │  (queue) │                   │ Instance N ─────►│ │
│          │                     │          │                   │ (auto-scales)    │ │
└──────────┘                     └──────────┘                   └──────────────────┘ │
     ▲                                                                               │
     │                                                              Reads original,  │
     │  User uploads                                                writes thumbnail │
     │  image here                                                        │          │
     │                                                                    ▼          │
     │                                                             ┌──────────┐      │
     │                                                             │  Amazon  │      │
     │                                                             │    S3    │ ◄────┘
     └───────────────── User continues ───────────────────────────│(thumbnails)│
                          browsing                                 └──────────┘
              (async — didn't wait)                            (parallel — multiple
                                                                instances at once)
```

Every concept from the theory section maps directly to something you just built.

Amazon SQS served as your message queue, receiving event notifications each time an image landed in S3.

AWS Lambda was your serverless function, spinning up on demand to process those images without any server management.

Together, they formed an event-driven architecture: an S3 upload triggered a message to SQS, which triggered Lambda automatically.

The processing was fully decoupled and asynchronous: the user’s upload and the image processing happened independently, so the user never had to wait.

Under load, Lambda demonstrated auto-scaling and parallel execution, with multiple instances processing different images simultaneously.

And when you combine both patterns, async plus parallel, you get a system where SQS absorbs upload spikes while Lambda scales out to process them concurrently.

_You’ve just built the coffee shop. S3 is the counter where orders come in, SQS is the cup queue, Lambda functions are the baristas making drinks in the background, and AWS automatically adds more baristas when the morning rush hits._

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Asynchronous](https://ntombizakhona.medium.com/asynchronous-4acaa0158820)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**18 March 2026**
