### 🏗️ Let’s Build

Demonstrating Backups With AWS Backup
-------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

Create an automated backup of an Amazon EC2 instance using **AWS Backup.**

_This will demonstrate the importance of a repeatable, scheduled backup workflow that follows best practices._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

### Add Additional Permissions to Your IAM Account

> **_💡 Principle of Least Privilege:_** _It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **IAM users**

**Step 05:** I**AM users**

Select the **Cloud Glossary** IAM User.

**Step 06: CloudGlossary**

Select **Permissions.**

Click **Add permissions** ▼

Select **Add permissions.**

You should be redirected to the **Add permissions** page.

**Step 07: Add permissions**

**Permission options:** Attach policies directly

On the Search bar type and check:

`**AmazonEC2FullAccess**`

`**AWSBackupFullAccess**`

`**IAMFullAccess**`

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 3** policies added to CloudGlossary

Build With Your IAM User Account
--------------------------------

> **_💡_**_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your IAM Account.

### Launch An EC2 Instance

**Step 10:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Step 11: Dashboard**

Click **Launch instance** ▼

**Step 12: Launch an instance**

Under **Name and Tags.**

**Name:** `**backup-server**`

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

select **Proceed without a key pair (Not recommended)**

At the right of the page ▼ **Summary**

Click **Launch instance.**

✅**Green banner: Success**

**Step 13:** Click **View all instances**

You should be redirected to the instances dashboard.

⚠️ Wait until the instance shows **Running** in the EC2 console.

### Create A Backup Vault

> **_💡_**_A backup vault is the container that stores your recovery points and lets you organize and encrypt them._

**Step 14:** Search for and open the **AWS Backup** console.

**Step 15:** In the left navigation, choose **Vaults.**

**Step 16: Vaults**

Click **Create backup vault**.

**Step 17:** **Create vault**

*   **Vault name:** `**backup-vault**`
*   **Vault type:** `**Backup vault**`
*   **Encryption key:** `**default (aws/backup)**`

Click **Create vault**

✅**Green banner: Backup vault backup-vault has been created successfully.**

### Create A Backup Plan

> **_💡_**_The backup plan defines when backups run and how long they are kept._

**Step 18:** Click **Create backup plan**.

**Step 19: Create backup plan**

*   **Backup plan options:** `**Build a new plan**`
*   **Backup plan name:** `**backup-plan**`

**Backup rule configuration**

*   **Backup rule name:** `**backup-rule**`
*   **Backup vault ▼:** `**backup-vault**`
*   **Backup frequency:** `**Daily**`
*   **Backup window:** `**Use default**`
*   ✔ **Move backups from warm to cold storage**
*   **Time in warm storage:** `**7 days**`
*   **Total retention period:** `**100 days**`

Click **Create plan**

✅**Green banner: Backup plan “backup-plan” creation successful.**

### Assign Resources To The Plan

**Step 20: Assign resources**

*   **Resource assignment name:** `**backup-resources**`
*   **IAM Role:** `**Default role**`

**Resource selection**

1.  **Define resource selection:** `**Include specific resources types**`
2.  **Select specific resource types:** `**EC2: backup-server**`
3.  **Exclude specific resource IDs from the selected resource types — _optional:_** `**Leave default**`
4.  **Refine selection using tags — _optional:_** `**Leave default**`

Click **Assign resources**.

> **_💡_**_Assigning by tag is the scalable approach. Any future instance tagged_ `_Backup = true_` _is automatically protected._

### Run An On-Demand Backup

> **_💡_**_Don’t wait for the schedule. Verify the setup immediately._

**Step 22: Under ▼ My account**

Select **Protected resources**

**Step 23: Protected Resources**

Click **Create on-demand backup**.

**Step 24: Create on-demand backup**

*   **Resource type:** `**EC2: backup-server**`
*   **Backup window:** `**Create backup now**`
*   **Total retention period:** `**7 Days**`
*   **Backup vault:** `**backup-vault**`
*   **IAM Role:** `**Default role**`

Click **Create on-demand backup**.

> _⚠️ Watch the job move to_ **_Completed_** _under_ **_Jobs_**_._

### Restore And _Verify_

> **_💡_**_A backup is only useful if you can restore it._

**Step 25:** Click **Vaults**

Select **backup-vault**

**Step 26: backup-vault**

✔ **Recovery point**

**Actions ▼:** `**Restore**`

**Step 27: Restore backup**

Confirm the restore settings (instance type, subnet, security group)

Click **Restore backup**

_When the restore job completes, confirm the new instance launches and your data is intact._

> _💡You now have an automated, scheduled, and verified backup workflow that follows the 3–2–1 rule with offsite cloud storage._

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _SNS_ and **Delete** The Topic & Subscription.
2.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                          +---------------------------+
                          |     IAM User Account      |
                          |    AWSBackupFullAccess    |
                          |    AmazonEC2FullAccess    |
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |        EC2 Instance       |
                          |       (backup-server)     |
                          | Amazon Linux 2023 t3.micro|
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |       AWS Backup Plan     |
                          |      (backup-plan)     |
                          |  Daily | Retain 365 days  |
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |   Encrypted Backup Vault  |
                          |  (beginners-backup-vault) |
                          +-------------+-------------+
                                        |
               ------------------------------------------------
               |                        |                     |
    +----------+-------+    +-----------+------+    +---------+---------+
    |  Recovery Point  |    |  Recovery Point  |    |  Recovery Point   |
    |     (Day 1)      |    |     (Day 2)      |    |    (On-Demand)    |
    |   Warm Storage   |    |   Warm Storage   |    |   Warm Storage    |
    +------------------+    +------------------+    +-------------------+
               |                        |                     |
               ------------------------------------------------
                                        |
                          +-------------+-------------+
                          |    Cold Storage (>30d)    |
                          |    then Expire (>365d)    |
                          +---------------------------+
    Recovery Flow:
   -----------------------------------------------------------------------
   Instance Lost  -->  Open Vault  -->  Select Recovery  -->  New Instance
     (Manual)        (Recovery Pts)      Point & Restore       Launched
   -----------------------------------------------------------------------
```

This walkthrough demonstrates one of AWS’s most important reliability patterns: a **centrally managed, automated backup and recovery workflow** using AWS Backup.

**What was built:** An AWS Backup plan (`backup-plan`) that automatically protects an Amazon Linux 2023 `t3.micro` EC2 instance on a daily schedule, storing each recovery point in an encrypted vault (`backup-vault`) with a lifecycle policy that moves backups to cold storage after 7 days and expires them after 100.

**The key demonstration:** When an instance is lost through accidental deletion, hardware failure, or a ransomware event you open the vault, pick a recovery point, and restore a fully working replacement. Your data is never gone because a clean, offsite copy is always available.

**Protection against data loss:** every scheduled and on-demand backup creates an independent recovery point, so you can roll back to a known-good state at any time.

**Durability and security:** recovery points are stored in an encrypted vault separate from the source instance, keeping your backups safe even if the original resource is compromised.

**Cost efficiency:** the lifecycle policy automatically tiers older backups to cheaper cold storage and deletes expired ones, so you retain what you need without paying for stale data.

**Security note:** The tutorial correctly uses an IAM user with scoped managed policies (`AWSBackupFullAccess` and `AmazonEC2FullAccess`) rather than the root account . A least-privilege best practice that limits blast radius if credentials are ever compromised.

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Backups](https://ntombizakhona.medium.com/backups-1589601afdb5)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**26 June 2026**
