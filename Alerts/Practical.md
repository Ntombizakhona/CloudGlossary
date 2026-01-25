### 🏗️ Let’s Build

Setting Up Alerts with Amazon SNS
---------------------------------

I know _(hope)_ you’re eager to set something up. I

n this practical, hands-on-tutorial, we will:

**Demonstrate Alerts with Amazon Simple Notification Service.**

### Prerequisites

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

**AmazonSNSFullAccess**

Click **Next.**

Click **Add permissions.**

✅**Green banner:** 1 policy added

### Build Using Your IAM Account

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 08:** Sign in with your IAM Account.

### Create Topic

**Step 09:** Navigate to Amazon SNS by typing **SNS** on the search bar.

Click **Simple Notification Service**

**Step 10: Topics**

Click **Create topic**

**Step 11**: **Create topic**

**Type:** Standard.

**Name:** CloudGlossaryAlert

**Display name — _optional_**: My Cloud Glossary Alert

Click **Create topic.**

✅**Green banner: Topic CloudGlossaryAlert created successfully.**

You can create subscriptions and send messages to them from this topic.

### Create Subscription

**Step 12: Subscriptions**

Click **Create subscription**

**Step 13: Create subscription**

**Protocol**: Email

**Endpoint:** _Your Email Address_

Click **Create subscription.**

✅**Green banner: Subscription to CloudGlossaryAlert created successfully.**

**Step 14:** Check _your email_ and confirm the subscription by clicking the link in the message you receive.

**💡Verification:**

**Subscription confirmed!**

You have successfully subscribed.

**Step 15:** Navigate to your Amazon SNS page, and click on **Topics.**

Select **CloudGlossaryAlert.**

Click **Publish Message.**

**Subject — _optional_:** My Cloud Glossary Alert

**Step 16: Message body**

**Message structure:** Identical payload for all delivery protocols.

**Message body to send to the endpoint:** Amazon Simple Notification Service (SNS) is a flexible and powerful tool for managing alerts.

Click **Publish message**

✅**Green banner: Message published to topic CloudGlossaryAlert successfully.**

**Step 17:** Check your email, you should see the alert.

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _SNS_ and **Delete** The Topic & Subscription.
2.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

In this hands-on tutorial, we successfully implemented a complete alert system using Amazon SNS by:

### Setup Phase

Configured IAM permissions following the principle of least privilege.

Granted AmazonSNSFullAccess to our IAM user account.

Used IAM account instead of root for enhanced security.

### Implementation Phase

Created a Standard SNS topic named “CloudGlossaryAlert”.

Set up an email subscription to receive notifications.

Confirmed the subscription through email verification.

### Testing Phase

Published a test message to verify the alert system functionality.

Successfully received the alert notification via email.

### Key Learning

We demonstrated how cloud alerts work in practice by building a functional notification system that can instantly deliver messages across multiple channels.

This foundation can be extended to monitor real infrastructure events, integrate with monitoring tools, and trigger automated responses.

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Alerts](https://ntombizakhona.medium.com/alerts-b0ecabc83b72?postPublishedType=repub)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**12 December 2024**
