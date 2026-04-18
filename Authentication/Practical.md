### 🏗️ Let’s Build

Authentication in Action
------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll…

1.  Create an **Administrative IAM User** for _Assigning Permissions to Other IAM Users_
2.  And enable **Multi-Factor Authentication** (MFA) to _secure your account._

_This will demonstrate_ **_Authentication_**

### Prerequisites

1.  [**Amazon Web Services**](https://medium.com/amazon-web-services-a8e57a9c6084)
2.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
3.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

### Setup Your Admin IAM User Account

**Step 01:** Sign in With Your **Root** User Account

**Step 02:** Click on **⋮⋮⋮** **Services.**

Select **Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** Navigate to the left side, under ▼ **Access Management**, select **Users.**

**Step 05:** Click the **Create User** button.

**Step 06:** **Specify User Details.**

**Step 06.1: User name:** TheAdmin

**Check**: Provide user access to the AWS Management Console — _optional_

**Step 06.2: “Are you providing console access to a person?”**

Click **I want to create an IAM User.**

**Step 06.3:** **Console Password.**

Select a **Custom Password,** that follows the password principles, that you can see below the text-area.

**Custom Password:** @CloudGlossaryAdmin#2026!

**Step 06.4:** **Users must create a new password at next sign-in — Recommended:** uncheck.

Click **Next.**

**Step 07:** You are now in the **Set Permissions** screen.

It is best practice to attach policies to a group, but since you’re creating your first user, and have no groups yet, select **Attach Policies directly.**

**Step 08:** Search for and select **AdministratorAccess**

Click **Next.**

**Step 09:** **Review and Create** your User Details and Permissions summary, and click **Create User.**

✅**Green banner:** User created successfully.

You can view and download the user’s password and email instructions for signing in to the AWS Management Console.

**Step 10:** **Congratulations.** You have created an IAM User.

**Step 11:** Copy the **Console Sign-In URL, Username and Password.**

Click **View user**

**Step 12: Continue without viewing or downloading console password?**

Click **Continue**

**Step 13: Summary**

Click **Security Credentials**

Scroll to **Multi-factor authentication (MFA)**

### Enable Multifactor Authentication

**Step 14:** Click **Assign MFA device**

**Step 15: Select MFA Device**

**MFA Device name:** TheAdminMFA

**MFA Device:** Authenticator app

Click **Next.**

**Step 16: Set Up Device**

**Scan the QR code.**

**Enter two Consecutive Codes from your MFA device** to validate it.

Click **Add MFA.**

✅**Green banner:** MFA device assigned

💡 **Verification:** You should see **MFA device assigned**

**Step 17: Add session**

Sign in as the Admin IAM user you just created.

_Now you have an Admin IAM User for Administrative Tasks, an IAM User For Building & a Root User Account for Billing & Cost Management._

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

If you launched any instances or services, don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                ┌──────────────────────────┐
                │      Root User Account   │
                │ (Billing & Ownership)    │
                └────────────┬─────────────┘
                             │
                             │ Creates & Manages
                             ▼
                ┌──────────────────────────┐
                │     IAM Service (AWS)    │
                │  Identity Management     │
                └────────────┬─────────────┘
                             │
                             │ Creates
                             ▼
                ┌──────────────────────────┐
                │     Admin IAM User       │
                │        (TheAdmin)        │
                └────────────┬─────────────┘
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
 ┌───────────────┐   ┌───────────────┐   ┌───────────────┐
 │ Username      │   │ Password      │   │ MFA Device     │
 │ (Identity)    │   │ (Auth Factor) │   │ (2nd Factor)   │
 └───────────────┘   └───────────────┘   └───────────────┘
                             │
                             ▼
                ┌──────────────────────────┐
                │   Authenticated Access   │
                │   to AWS Resources       │
                └──────────────────────────┘
```

This tutorial walks through creating an admin IAM user on AWS with MFA enabled.

You start by signing into your root account, then navigate to IAM → Users to create a new user called “TheAdmin” with console access, a custom password, and the AdministratorAccess policy attached directly.

After confirming the user is created, you copy the sign-in URL and credentials, then navigate to the user’s Security Credentials tab to assign an MFA device (an authenticator app) by scanning a QR code and entering two consecutive codes.

Finally, you sign in as the new admin user, giving you three distinct accounts: root (for billing), an admin IAM user (for administrative tasks), and the ability to create further IAM users for building.


---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Authentication](https://ntombizakhona.medium.com/authentication-fb0d207899a1?postPublishedType=repub)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**08 April 2026**
