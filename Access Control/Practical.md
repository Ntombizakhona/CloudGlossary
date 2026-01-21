### 🏗️ Let’s Build

Creating an IAM Group and Assigning Granular Limited Permissions
----------------------------------------------------------------

I know _(hope)_ you’re eager to set something up…

In the [**previous post**](https://medium.com/@ntombizakhona/abstraction-d1335bec022e), we assigned _permissions_ and _instance roles_, but they were not granular because we were just demonstrating Abstraction.

In this practical, hands-on-tutorial, we will:

**Create an IAM group and assign granular limited permissions.**

_This will demonstrate_ **_access control_** _by using Identity and Access Management (IAM) and adhering to the Principle of Least Privilege._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

### Identity-Based Access Control

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **User groups**

**Step 05: User groups**

Click **Create group**

**Step 06: Create user group**

**User group name:** CloudGlossary

**Add users to the group — Optional:** Add your IAM User.

**Attach permissions policies — Optional:** AmazonEC2ReadOnlyAccess

Click **Create user group**

✅**Green banner: CloudGlossary user group created.**

**Step 07: Add session** and sign in with your IAM Account

### Launch EC2 Instances

**Step 08:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

**Step 09:** Select **EC2.**

**Step 10:** Click **Launch instance.**

**Step 11: Launch an instance**

**Name: AccessControl**

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name _— required:_** CloudGlossary

Click **Launch instance.**

**❌ Red Banner**: **Instance launch failed**

You failed to launch the instance because neither your user nor your group has the permissions to launch instances, only to **view them.**

_Throughout the Cloud Glossary, we will continuously witness and explore Access Control concepts and the Principle of Least Privilege as we provision resources._

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Login with your _Root User Account_, and **Remove All Permissions** Associated with your IAM Account.


### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

The tutorial’s “failure” to launch an instance is actually a success: it proves your **access control** is working correctly. This real-world demonstration shows how proper access control prevents unauthorized actions, even when users have legitimate accounts.

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Access Control](https://ntombizakhona.medium.com/access-control-306607c6385a?postPublishedType=repub)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**28 November 2024**
