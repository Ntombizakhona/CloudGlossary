### 🏗️ Let’s Build

Demonstrating Anti-Patterns on AWS
----------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Walk through the AWS Console to demonstrate common Anti-patterns and their proper solutions.**

_You’ll learn by seeing what not to do, and then how to fix it._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**Setup Cost Alerts With AWS Budgets**](https://medium.com/amazon-web-services-a8e57a9c6084)

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

**AmazonEC2FullAccess**

**AmazonS3FullAccess**

**SecretsManagerReadWrite**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner:** 3 policies added to CloudGlossary

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your **IAM Account**

**Step 10:** Before you proceed, make sure that you’re signed in with your IAM User Account, and that you’re in the **N. Virginia** ▼ region (us-east-1).

Launch EC2 Instances
--------------------

**Step 11:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Step 12: Dashboard**

Click **Launch instance.**

**Step 13: Launch an instance**

Under **Name and Tags.**

**Name:** AntiPattern-OverProvisioned

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **m5.4xlarge**

⚠️**Anti Pattern Alert:**

Notice the m5.4xlarge instance has:

*   16 vCPUs
*   64 GB Memory
*   Cost: ~**0.768/hour∗∗( 0.768/_hour_∗∗( 552/month)

**For a simple “Hello World” app, we’re wasting ~95% of resources!**

💸 **DON’T** actually launch this instance! This is just to show you what **NOT** to do.

**Step 14:** **Launch a Right-Sized EC2 Instance**

Still on the EC2 Launch Instance page

**Name:** BestPractice-Rightsized

Click **Add additional tags.**

*   Add: **Key** = Environment, **Value** = Development
*   Add: **Key** = Project, **Value** = AntiPattern

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible)**

✅**Best Practice:**

The t3.micro instance has:

*   2 vCPUs
*   1 GB Memory
*   Cost: ~**0.0104/hour∗∗( 0.0104/_hour_∗∗( 7.50/month)

💸 **Savings:** 98.6% compared to the anti-pattern!

▼ **Key pair (login)**

Select **CloudGlossary**

**Step 15:** ▼ **Network settings.**

Scroll to **Firewall (security groups)**

Select **Create security group.**

Check **Allow SSH traffic from My IP**

Check **Allow HTTPS traffic from the internet**

▼ **Configure storage:** leave as default.

▼ **Advanced details:** leave as default

Click **Launch instance**

**🎉 Congratulations!** You’ve launched a properly-sized, tagged instance!

### Review Your Security Group (Firewall Rules)

**Step 16:** Go back to EC2 in the Console

In the left sidebar, click **Security Groups** under **▼ Network & Security**

Find the security group attached to your instance (click on your **instance first to see which one**)

Click on the **Security Group ID** to view its rules

**Step 17:** Check the Inbound Rules:

❌ **Anti-Pattern:** SSH open to 0.0.0.0/0 _(the whole internet)_

✅ **Best Practice:** SSH open only to Your-IP/32 _(just you!)_

❌ **Anti-Pattern:** All ports open

✅ **Best Practice:** Only necessary ports _(22, 443)_

Create an Encrypted S3 Bucket
-----------------------------

Let’s create a secure storage bucket:

**Step 18:** Navigate to S3.

Click **Create bucket**

**Bucket type:** General purpose

**Bucket name:** CloudGlossary[Account-ID]

Object ownership: **ACLs disabled**

**Step 19: Block Public Access settings for this bucket**

✔ Ensure **Block all public access”**is checked (this is the default,keep it!)

**Bucket versioning:** Enable

**Default encryption:**
Server-side encryption with Amazon S3 managed keys (SSE-S3)

💡This encrypts all your data automatically!

Click **Create bucket**

**✅ Security Best Practices Applied:**

🔒 All public access blocked

🔐 Encryption enabled by default

📝 Versioning protects your data

Store Secrets Securely with AWS Secrets Manager
-----------------------------------------------

### Understanding Hardcoded Credentials (The Wrong Way)

Another common anti-pattern is hardcoding database passwords directly in your application code:

```
# ❌ ANTI-PATTERN: Hardcoded credentials - NEVER DO THIS!
DB_PASSWORD = "SuperSecret123!"  # 😱 Anyone with code access sees this!
```

**🚨 Why This Is Dangerous:**

1.  Credentials visible if code is shared or leaked
2.  Can’t change passwords without updating code
3.  No way to track who accessed the credentials

### Store Secrets Securely (AWS Secrets Manager)

Instead of hardcoding passwords, use AWS Secrets Manager!

**Step 20:** Navigate to **Secrets Manager**

Click **Store a new secret**

**Step 21: Choose secret type**

**Secret type:** Other type of secret

**Step 22:** Key/value pairs

**Key:** username **Value:** admin

Click **+ Add row**

**Key:** password Value: **MyCloudGlossary123!**

Click **+ Add row**

**Key:** database **Value:** myapp

Click **Next**

**Step 23: Configure secret**

**Secret name:** myapp/database/credentials

**Description:** Enter Database credentials for my demo app

Click **Next**

**Step 24**: **Configure rotation — _optional_**

Click **Next**

**Step 25: Review**

Click **Store**

✅**Green banner:** **You successfully stored the secret myapp/database/credentials. To show it in the list, choose Refresh.**

Use the sample code to update your applications to retrieve this secret.

Click **See sample code.**

💡**Why This Is Better:**

1.  Secrets are encrypted at rest
2.  Access is logged in CloudTrail
3.  You can rotate passwords without changing code
4.  IAM controls who can access secrets

Set Up Cost Monitoring (Avoid Surprise Bills)
---------------------------------------------

One of the biggest anti-patterns is not monitoring your costs. Let’s fix that!

### [Create a Budget Alert](https://medium.com/amazon-web-services-a8e57a9c6084)

> If you don’t have a Budget Configured already, refer to Cloud Glossary Article: [**Amazon Web Services**](https://medium.com/amazon-web-services-a8e57a9c6084)
> 
> Activity 01
> 
> Setup Cost Alerts With AWS Budgets
> 
> _AWS Budgets is an AWS tool that helps you set spending (or usage) limits and get alerts so your AWS costs don’t surprise you._

💡 **Why Budgets Matter:**

1.  You’ll get an email if spending approaches your limit
2.  No more surprise bills at month-end!
3.  Free tier usage is protected

### View Cost Explorer

**Step 26: Navigate to Cost Explorer**

1.  See spending by service
2.  Filter by your tags (Environment, Project)
3.  Spot unused resources

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _EC2_ and **Terminate** the instance.
2.  Navigate to _S3_ and **Delete** the bucket.
3.  Navigate to _Secrets Manager_ and **Delete** the secret. (Schedule Minimum Deletion)
4.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

**Phase 1: The Wrong Way (Anti-Patterns Demonstrated)**

*   Launched an over-provisioned EC2 instance (m5.4xlarge) costing ~$552/month
*   Hardcoded database credentials directly in Python code
*   Left security groups open to the entire internet

**Phase 2: The Right Way (Best Practices Applied)**

*   Right-sized and tagged our EC2 instance (t3.micro) reducing costs by 98.6%
*   Implemented AWS Secrets Manager for secure credential storage
*   Set up budget alerts to prevent surprise bills
*   Applied restrictive security groups and encryption on a bucket


# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Anti-Patterns](https://ntombizakhona.medium.com/anti-patterns-b2ee6eac8a7f?postPublishedType=repub)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**05 February 2026**
