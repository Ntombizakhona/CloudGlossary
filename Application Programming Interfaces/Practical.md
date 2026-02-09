### 🏗️ Let’s Build

APIs in the Cloud
-----------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Use Amazon API Gateway and AWS Lambda to build a serverless API.**

Prerequisites
-------------

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

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

Click **Add permissions** ▼

Select **Add permissions.**

You should be redirected to the **Add permissions** page.

**Step 07: Add permissions**

**Permission options:** Attach policies directly

On the Search bar type and check:

**AWSLambda_FullAccess**

**AmazonAPIGatewayAdministrator**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 2** policies added to CloudGlossary

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your IAM Account.

### Create a Lambda Function

**Step 10:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **Lambda**

**Step 11:** Click **Create function**

**Step 12:** Select **Author from scratch**

**Function name:** myFirstAPI

**Runtime:** Python 3.14

**Architecture:** x86_64

Click **Create function**

✅**Green banner: Successfully created the function myFirstAPI. You can now change its code and configuration. To invoke your function with a test event, choose “Test”.**

**Step 13:** In the code editor, replace the default code with:

```
import json
def lambda_handler(event, context):
    # Get the HTTP method and path
    http_method = event.get('httpMethod', 'GET')
    
    # Sample response data
    response_body = {
        'message': 'Hello from your first AWS API!',
        'method': http_method,
        'timestamp': '2024-01-15T10:30:00Z'
    }
    
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*'
        },
        'body': json.dumps(response_body)
    }
```

**Step 14:** Click **Deploy** to save your function

✅**Green banner:** Successfully updated the function **myFirstAPI**.

### Create an API Gateway

**Step 15:** Navigate to Amazon API Gateway in the AWS Console

Click **Create API**

**Step 16: REST API**

Click **Build**

**Step 17: Create REST API**

**API Details:** New API

**API name:** MyFirstRestAPI

**_Description — optional:_** A beginner-friendly REST API

**Endpoint Type**: Regional

**Security policy — new:** TLS_1_0

Click **Create API**

✅**Green banner:** Successfully created REST API ‘MyFirstRestAPI (1xhxjod5xl)’.

### Create a Resource and Method

**Step 18:** In your new API, click **Create Resource**

**Step 19: Create resource**

**Resource path:** /

**Resource name:** greeting

Click **Create Resource**

✅**Green banner:** Successfully created resource ‘/greeting’

**Step 20:** With **/greeting** selected, click **Create Method**

**Step 21: Create method**

Method type: **GET** ▼

**Integration type:** Lambda Function

**Lambda function:** Select myFirstAPI

**us-east-1 ▼:** myFirstAPI

Click **Create method**

✅**Green banner: Successfully created** method ‘GET’ in ‘greeting’. Redeploy your API for the update to take effect.

### Deploy Your API

**Step 22:** Click Deploy API

**Step 23: Create a new stage**

**Stage name:** dev

**Description:** Development stage

Click **Deploy**

✅**Green banner:** **Successfully created** deployment for MyFirstRestAPI. This deployment is active for dev.

Copy the **Invoke URL** displayed (it will look like: [https://abc123.execute-api.us-east-1.amazonaws.com/dev)](https://abc123.execute-api.us-east-1.amazonaws.com/dev))

### Test Your API

**Step 24: Using a web browser**

Paste your invoke URL with the resource path:

```
https://abc123.execute-api.us-east-1.amazonaws.com/dev/greeting
```

Expected response:

```
{"statusCode": 200, "headers": {"Content-Type": "application/json", "Access-Control-Allow-Origin": "*"}, "body": "{\"message\": \"Hello from your first AWS API!\", \"method\": \"GET\", \"timestamp\": \"2024-01-15T10:30:00Z\"}"}
```

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _Lambda_ and **Delete** The Function.
2.  Navigate to _API_ Gateway and **Delete** The API.
3.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔


Building Tutorial Overview
--------------------------

By completing this tutorial, you have:

1.  Built a real serverless API
2.  Used IAM securely
3.  Written backend logic in Python
4.  Exposed an API endpoint on the internet
5.  Understood how cloud services work together

This is **exactly how production APIs are born,** just at a beginner-friendly scale.
