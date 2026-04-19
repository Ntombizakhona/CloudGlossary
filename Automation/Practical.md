### 🏗️ Let’s Build

Demonstrating Automation With CloudFormation And The AWS CLI
------------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**AWS CloudFormation to automatically provision a simple cloud resource using Infrastructure as Code (IaC).**

_This will demonstrate Automation by provisioning an S3 Bucket without using the console._

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  **A Basic Text Editor**

### Add Additional Permissions to Your IAM Account

_Principle of Least Privilege: It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your **Administrative Account** in order to grant permissions to your active _Development IAM Account._

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

**AmazonS3FullAccess**

**AWSCloudFormationFullAccess**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 2** policies added to CloudGlossary

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

### Create Your CloudFormation Template

_A CloudFormation template is a JSON or YAML file that describes the resources you want AWS to create._

**Step 09:** Open your text editor on your local machine.

**Step 10:** Create a new file and name it **s3-bucket-template.yaml**

**Paste** this and **Save** the file:

```
AWSTemplateFormatVersion: '2010-09-09'
Description: >
  A simple CloudFormation template that creates an S3 bucket
  with server-side encryption enabled automatically.
Resources:
  MyAutomatedS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub 'my-automated-bucket-${AWS::AccountId}'
      VersioningConfiguration:
        Status: Enabled
      BucketEncryption:
        ServerSideEncryptionConfiguration:
          - ServerSideEncryptionByDefault:
              SSEAlgorithm: AES256
Outputs:
  BucketName:
    Description: The name of the S3 bucket created by this template
    Value: !Ref MyAutomatedS3Bucket
  BucketARN:
    Description: The ARN of the S3 bucket
    Value: !GetAtt MyAutomatedS3Bucket.Arn
```

What’s happening here?

**AWSTemplateFormatVersion:** Tells AWS which template version to use

**Description:** A human-readable summary of what the template does

**Resources:** The core section. Resources define the AWS resources to create

**MyAutomatedS3Bucket:** A logical name for the S3 bucket resource

**BucketName:** Uses _!Sub_ to dynamically insert your AWS Account ID, ensuring uniqueness

**VersioningConfiguration:** Enables versioning so you can recover previous versions of objects

**BucketEncryption:** Automatically enables AES-256 server-side encryption

**Outputs:** Returns useful information (bucket name, ARN) after creation

**💡 If you were to create this bucket manually, you might forget to enable versioning or encryption. With the template, these security best practices are baked in every single time.**

### Deploy the Stack via the CloudFormation Console

**Step 11:** In the **AWS Management Console.** Type **CloudFormation** in the search bar at the top and click on the result.

**Step 12: CloudFormation Dashboard**

Click **Create stack ▼**

Select **With new resources (standard)**

**Step 13: Create stack**

Prepare template: **Choose an existing template**

Specify template: **Upload a template file**

Upload a template file: **Choose file**

💡**CloudFormation automatically validated the syntax of your template when you uploaded it. If there were any YAML formatting errors, you’d see an error message here instead of being able to proceed.**

Click **Next.**

**Step 14: Specify stack details**

Stack name: **my-first-automation-stack**

There are no parameters to configure for this template, so click **Next.**

**Step 15: Configure stack options**

On the Configure stack options page, you’ll see several optional settings:

**Tags:**You can add tags to the stack itself (not the resources inside it). For now, skip this.

**Permissions**: You can specify an IAM role for CloudFormation to assume. Since our user already has the necessary permissions, leave this blank.

**Stack failure options:** Leave the default: Roll back all stack resources.

**Advanced options:** Leave all defaults.

Click **Next.**

**Step 16: Review and create**

On the Review page, verify all the details:

**Stack name:** my-first-automation-stack

**Template:** The file you uploaded

Review the template’s description and resources listed

Scroll to the bottom and click **Submit.**

💡**You’ll be taken to the stack’s detail page, where you can watch the creation in real time.**

**Step 16: Monitor the Deployment**

```
Timestamp       Logical ID                   Status                Status Reason
-----------     --------------------------   --------------------  ---------------
2026-XX-XX      my-first-automation-stack    CREATE_IN_PROGRESS    User initiated
2026-XX-XX      MyAutomatedS3Bucket          CREATE_IN_PROGRESS    —
2026-XX-XX      MyAutomatedS3Bucket          CREATE_COMPLETE       —
2026-XX-XX      my-first-automation-stack    CREATE_COMPLETE       —
```

✅ **Once the stack status shows CREATE_COMPLETE in green, your automation has succeeded!**

### Verify the Resources

Let’s confirm that our S3 bucket was created exactly as specified.

**Step 17:** Check the **Outputs** tab.

```
Key           Value                                          Description
-----------   --------------------------------------------   ------------------------------------------------
BucketName    my-automated-bucket-123456789012               The name of the S3 bucket created by this template
BucketARN     arn:aws:s3:::my-automated-bucket-123456789012  The ARN of the S3 bucket
```

**Step 18:** Check the **Resources** tab.

✅ You’ll see your MyAutomatedS3Bucket with its Physical ID (the actual bucket name) and a status of **CREATE_COMPLETE.**

Click the **Physical ID link** to open the S3 bucket in a new tab.

### **Verify The Bucket Configuration**

**Step 19:** In the S3 bucket view, click the **Properties** tab.

Scroll down to **Bucket Versioning**: confirm it shows **Enabled.**

Scroll down to **Default encryption**: confirm it shows **Server-side encryption with Amazon S3 managed keys (SSE-S3).**

**💡 Everything is exactly as defined in our template. No manual checkbox clicking, no chance of forgetting a setting. The template enforced our desired configuration automatically.**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _CloudFormation_ and **Delete** The Stack.
2.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```

┌─────────────────────────────────────────────────────────────────────────────┐
│                        AUTOMATION TUTORIAL ARCHITECTURE                     │
└─────────────────────────────────────────────────────────────────────────────┘
  ┌──────────────┐         ┌──────────────────┐         ┌──────────────────┐
  │              │         │                  │         │                  │
  │  ADMIN USER  │ ───────▶│   IAM CONSOLE    │───────▶│  CREATE USER     │
  │              │         │                  │         │  automation-     │
  └──────────────┘         └──────────────────┘         │  tutorial-user   │
                                                        └────────┬─────────┘
                                                                 │
                                                        Attach Policies
                                                                 │
                                                                 ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         PRINCIPLE OF LEAST PRIVILEGE                        │
│                                                                             │
│  ┌─────────────────────────────┐     ┌────────────────────────────────┐     │
│  │  AWSCloudFormation          │     │     AmazonS3FullAccess         │     │
│  │  FullAccess                 │     │                                │     │
│  │                             │     │  Full access to all S3         │     │
│  │  Full access to all         │     │  actions and resources         │     │
│  │  CloudFormation actions     │     │                                │     │
│  │  and resources              │     │                                │     │
│  │                             │     │                                │     │
│  │  (AWS Managed Policy)       │     │  (AWS Managed Policy)          │     │
│  └─────────────────────────────┘     └────────────────────────────────┘     │
│                                                                             │
│  ⚠️  NOTE: In production, scope these down to specific resources and        │
│     actions using custom policies for true least privilege.                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
                        ┌──────────────────────┐
                        │  LOG IN AS RESTRICTED│
                        │  automation-tutorial-│
                        │  user                │
                        └──────────┬───────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           BUILD & DEPLOY                                    │
│                                                                             │
│                                                                             │
│   ┌─────────────────┐        ┌──────────────────────────────────────┐       │
│   │                 │        │      s3-bucket-template.yaml         │       │
│   │   LOCAL TEXT    │        │                                      │       │
│   │   EDITOR       │───────▶│  AWSTemplateFormatVersion: '2010'     │       │
│   │                 │ Create │  Resources:                          │       │
│   └─────────────────┘  File  │    MyAutomatedS3Bucket:              │       │
│                              │      Type: AWS::S3::Bucket           │       │
│                              │      Properties:                     │       │
│                              │        - Versioning: Enabled         │       │
│                              │        - Encryption: AES256          │       │
│                              └──────────────────┬───────────────────┘       │
│                                                 │                           │
│                                              Upload                         │
│                                                 │                           │
│                                                 ▼                           │
│                              ┌──────────────────────────────────────┐       │
│                              │                                      │       │
│                              │    AWS CLOUDFORMATION CONSOLE        │       │
│                              │                                      │       │
│                              │    1. Create Stack                   │       │
│                              │    2. Upload Template                │       │
│                              │    3. Stack Name:                    │       │
│                              │       my-first-automation-stack      │       │
│                              │    4. Configure Options (defaults)   │       │
│                              │    5. Review & Submit                │       │
│                              │                                      │       │
│                              └──────────────────┬───────────────────┘       │
│                                                 │                           │
│                                         Provisions                          │
│                                                 │                           │
│                                                 ▼                           │
│                              ┌──────────────────────────────────────┐       │
│                              │                                      │       │
│                              │          AMAZON S3 BUCKET            │       │
│                              │                                      │       │
│                              │  Name: my-automated-bucket-          │       │
│                              │        [AccountId]                   │       │
│                              │                                      │       │
│                              │  ┌────────────┐  ┌───────────────┐   │       │
│                              │  │ Versioning │  │  Encryption   │   │       │
│                              │  │  ENABLED   │  │   AES-256     │   │       │
│                              │  └────────────┘  └───────────────┘   │       │
│                              │                                      │       │
│                              └──────────────────────────────────────┘       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                              VERIFY                                         │
│                                                                             │
│   ┌──────────────────┐  ┌──────────────────┐  ┌────────────────────────┐    │
│   │                  │  │                  │  │                        │    │
│   │   Events Tab     │  │   Outputs Tab    │  │   S3 Console           │    │
│   │                  │  │                  │  │                        │    │
│   │ CREATE_COMPLETE  │  │ BucketName:      │  │ ✓ Versioning Enabled   │    │
│   │                  │  │ BucketARN:       │  │ ✓ Encryption AES-256   │    │
│   │                  │  │                  │  │                        │    │
│   └──────────────────┘  └──────────────────┘  └────────────────────────┘    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                             CLEAN UP                                        │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                                                                     │   │
│   │                    DELETE STACK                                     │   │
│   │             (CloudFormation Console)                                │   │
│   │                                                                     │   │
│   │    Automatically removes ──▶  S3 Bucket                             │   │
│   │                               Stack Resources                       │   │
│   │                                                                     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                                                                     │   │
│   │              DELETE IAM RESOURCES (Admin Account)                   │   │
│   │                                                                     │   │
│   │    Delete ──▶  automation-tutorial-user                             │   │
│   │                (Detaches AWSCloudFormationFullAccess                │   │
│   │                 and AmazonS3FullAccess automatically)               │   │
│   │                                                                     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

```

The step-by-step exercise above demonstrated Automation in action: with a single template file and a few clicks in the CloudFormation console, you provisioned a fully configured, encrypted, versioned S3 bucket and tore it all down cleanly.

Critically, we did all of this using only the minimum permissions required, reinforcing that good automation and good security go hand in hand.

Imagine doing that for hundreds of resources across multiple environments.

_That_ is the true power of automation.



---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Automation](https://medium.com/p/e1affd1c3265?postPublishedType=initial)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**12 April 2026**
