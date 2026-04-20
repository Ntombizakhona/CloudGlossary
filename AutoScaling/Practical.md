### 🏗️ Let’s Build

Demonstrating AutoScaling by Provisioning an Auto Scaling Group
---------------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll…

**Provision an Auto Scaling Group and Terminate an Instance**

_This will demonstrate_ **_Autoscaling._**

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

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

**AmazonEC2FullAccess**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner:** 1 policy added

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

### Configure AutoScaling

**Step 09:** Navigate to the EC2 Console.

On the far right of the page, at the bottom, below **▼ Autoscaling**

Select **Auto Scaling Groups.**

**Step 10: Amazon EC2 Auto Scaling**

Click **Create Auto Scaling Group.**

You should be redirected to the Choose launch template or configuration page.

**Step 11: Choose launch template or configuration**

**Auto Scaling group name:** AutoScalingGroup

**Launch template:** Click **Create a launch template**

You should be redirected to the **Create launch template** page

### Create A Launch Template

_A launch template is like a reusable blueprint for EC2: it saves your instance settings so you can launch the same setup again later, share it with others, and maintain multiple versions as your configuration evolves_

**Step 12: Create launch template**

**Launch template name and description.**

**Launch template name _— required_:** AutoScalingTemplate

**Template version description:** My Auto Scaling Template

**Auto Scaling guidance:** ✔

**Step 13: Launch template contents**

**▼ Application and OS Images (Amazon Machine Image)**

Click **Quick Start**

**Select Amazon Linux**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name:** CloudGlossary

**Step 14: Network Settings**

**Subnet**: Don’t include in launch template.

**Firewall (Security groups)**: Select existing security group_._

**Common security groups**: CloudGlossarySG

▶ **Storage (volumes)**: Leave default

▶ **Resource tags**: Leave default

▶ **Advanced details**: Leave default

**Step 15:** ▶ **Summary**

Click **Create launch template**

✅**Green banner: Success**

Click **View launch templates**

**Step 16:** Navigate back to the **Choose launch template or configuration** page**.**

Click the refresh button next to **Select a launch template.**

Select **AutoScalingTemplate.**

**Version**: 1 ▼

Click **Next**

**Step 17: Choose instance launch options**

**Network**

**VPC:** defaultVPC

**Availability Zones and subnets**: Select all.

**Availability Zone distribution — _new_**: Select **Balanced best effort.**

Click **Next**

**Step 18: Integrate with other services — _optional_**

Click **Next**

**Step 19: Configure group size and scaling — _optional_**

**Desired capacity:** 2

**Min desired capacity:** 2

**Max desired capacity:** 4

Click **Next**

**Step 20: Add notifications — _optional_**

Click **Next**

**Step 21: Add tags — _optional_**

Click **Next**

**Step 20: Review**

Click **Create Auto Scaling group**

**Step 21: Auto Scaling groups**

Click on **AutoScalingGroup**

**Step 22: AutoScalingGroup**

Select **Instance management**

**Lifecycle:** InService

Click on 1 **instance id**

You should be redirected to the instance summary page.

**Step 23: Instance summary for**

**Instant state:** ✅Running

**Instance state** ▼**:** Terminate (delete) instance

Click **Terminate (delete)**

Go back to Instance management

You should notice that your Auto Scaling group launched a new instance.

Alternatively go to **Instances** ▼ and you will see the newer instances getting launched, and the Terminated ones getting deleted.

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _Launch Template_ and **Delete** The Launch Template
2.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                         +---------------------------+
                         |    IAM User Account       |
                         |  AmazonEC2FullAccess      |
                         +-------------+-------------+
                                       |
                         +-------------+-------------+
                         |      Launch Template      |
                         |   (AutoScalingTemplate)   |
                         | Amazon Linux 2023 t3.micro|
                         +-------------+-------------+
                                       |
                         +-------------+-------------+
                         |   Auto Scaling Group      |
                         |   (AutoScalingGroup)      |
                         | Desired: 2  | Min:2 Max: 4|
                         +-------------+-------------+
                                       |
              ------------------------------------------------
              |                        |                     |
   +----------+-------+    +-----------+------+    +---------+---------+
   |   EC2 Instance   |    |   EC2 Instance   |    |   EC2 Instance    |
   |    (t3.micro)    |    |    (t3.micro)    |    |    (t3.micro)     |
   |    InService     |    |    InService     |    |  Auto-Launched    |
   |   AZ: us-east-1a |    |   AZ: us-east-1b |    |  AZ: us-east-1c   |
   +------------------+    +------------------+    +-------------------+
              |                        |                     |
              ------------------------------------------------
                                       |
                         +-------------+-------------+
                         |        Default VPC        |
                         |  Multiple Availability    |
                         |         Zones             |
                         +---------------------------+
  Self-Healing Flow:
  -----------------------------------------------------------------------
  Instance Terminated --> ASG Detects Drop Below Desired --> New Instance
       (Manual)               (Health Check)                  Launched
  -----------------------------------------------------------------------
```

This walkthrough demonstrates one of AWS’s most important reliability patterns: the self-healing Auto Scaling Group (ASG).

**What was built:** An ASG backed by a reusable launch template (Amazon Linux 2023, t3.micro) spread across all availability zones in the default VPC, with a desired capacity of 2 instances, a minimum of 2, and a maximum of 4.

**The key demonstration:** When you manually terminate one of the running EC2 instances, the ASG detects that the actual count has dropped below the desired count and automatically launches a replacement. You never dip below 2 healthy instances becuase the group is self-healing.

1.  **High availability:** instances are distributed across multiple availability zones, so a single zone outage doesn’t take down your whole application.
2.  **Fault tolerance:** the ASG continuously monitors instance health and replaces unhealthy or terminated instances without manual intervention.
3.  **Scalability:** the max capacity of 4 gives the group headroom to scale out automatically under load (once scaling policies are added).

**Security note:** The tutorial correctly uses an IAM user with only `AmazonEC2FullAccess` (least privilege) rather than the root account — a best practice that limits blast radius if credentials are ever compromised.

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Auto Scaling](https://medium.com/p/ad945ba63939?postPublishedType=initial)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**14 April 2026**
