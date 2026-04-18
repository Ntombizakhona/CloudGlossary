### 🏗️ Let’s Build

Authorisation in Action
-----------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll…

**Create an IAM group and assign granular limited permissions.**

_This will demonstrate_ **_Authorisation_**

### Prerequisites

1.  [**Access Control**](https://medium.com/access-control-306607c6385a)
2.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
3.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

### Identity-Based Access Control

**Step 01**: Sign in with your **Administrative Account** in order to grant permissions to your active _Development IAM Account._

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **User groups**

**Step 05: User groups**

Click **Create group**

**Step 06: Create user group**

**User group name:** Authorisation

**Add users to the group — Optional:** Add your CloudGlossary IAM User.

**Attach permissions policies — Optional:** AmazonEC2ReadOnlyAccess

Click **Create user group**

✅**Green banner: Authorisation user group created.**

**Step 07: Add session** and sign in with your IAM Account

### Launch EC2 Instances

**Step 08:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

**Step 09:** Select **EC2.**

**Step 10:** Click **Launch instance.**

**Step 11: Launch an instance**

**Name: Authorisation**

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name _— required:_** CloudGlossary

Click **Launch instance.**

**❌ Red Banner**: **Instance launch failed**

You failed to launch the instance because neither your user nor your group has the permissions to launch instances, only to **view them.**

_Basically, you’re not authorised to launch EC2 instances._

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

If you launched any instances or services, don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Login with your _Administrative Account_, and **Delete The Group.**

### ⛔ End of Cleaning Up Protocol ⛔

```
                ┌──────────────────────────────┐
                │   Admin (Root / IAM Admin)   │
                │  (Full Permissions)          │
                └────────────┬─────────────────┘
                             │
                             │ Creates & Configures
                             ▼
                ┌──────────────────────────────┐
                │  IAM Group: "Authorisation"  │
                │  Policy: EC2 ReadOnly        │
                └────────────┬─────────────────┘
                             │
                             │ Assigns User
                             ▼
                ┌──────────────────────────────┐
                │     IAM User (Developer)     │
                │   Limited Permissions        │
                └────────────┬─────────────────┘
                             │
                             │ Attempts Action
                             ▼
                ┌──────────────────────────────┐
                │        Amazon EC2            │
                │  Launch Instance Attempt     │
                └────────────┬─────────────────┘
                             │
                             ▼
                    ❌ Access Denied
          (Not Authorised to Launch Instance)
```

Building Tutorial Overview
--------------------------

The tutorial demonstrates identity-based access control on AWS using two accounts in parallel sessions: an admin and a development IAM user.

The admin signs into IAM, creates a user group called “Authorisation”, adds the development user to it, and attaches the `AmazonEC2ReadOnlyAccess` managed policy.

The development user then switches sessions and attempts to launch an EC2 instance (Amazon Linux 2023, t3.micro).

The launch fails with a red banner, the expected and intentional outcome because the policy only grants read access, not the ability to create instances.

The failure is the proof of concept: authorisation is working exactly as intended.

Additional Resources

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Authorisation](https://ntombizakhona.medium.com/authorisation-ce5e449e621a)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**09 April 2026**
