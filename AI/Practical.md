### 🏗️ Let’s Build

A Complete Agentic AI Development Setup
---------------------------------------

I know _(hope)_ you’re eager to set something up.

In this practical, hands-on-tutorial, we will:

1.  **Set up a complete development environment using modern agentic AI tools**
2.  **Create a beautiful application through vibe coding**
3.  **Learn web development and cloud engineering concepts through natural language interaction with AI**

### Prerequisites for Pro Tier (Start At Step 01)

1.  **💸 $20per mo for Kiro Pro (R330 per month) 💸**
2.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
3.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
4.  [**AWS Organization**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html)
5.  [**VS Code**](https://code.visualstudio.com/)

### Prerequisites for Free Tier (Start At Step 37)

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**AWS BuilderID**](https://builder.aws.com/content/2zcHXEQEQkxFslPN4dT0Qm2CSJA/your-guide-to-builder-center)
4.  [**VS Code**](https://code.visualstudio.com/)

### **💸** Pro Tier Guide

**Setting Up AWS Identity Center**
----------------------------------

_AWS Identity Center provides centralized access management for your AWS resources and applications._

**Step 01**: Sign in with your Administrative Root User Account

Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

Click **IAM Identity Center**

**Click Enable**

**Step 02: IAM Identity Center Dashboard**

**IAM Identity Center setup:** Click **Confirm identity store**

**Step 03: Settings**

**Instance name:** Developers

**Enable identity-enhanced sessions:** Click Enable

**Enable identity-enhanced sessions:** Click **Enable**

✅**Green banner:** Identity-enhanced sessions successfully enabled.

**Step 04: ▼ Multi-account permissions**

Click **Permission sets**

**Step 05: Permission sets**

Click **Create permission set**

**Step 06: Select permission set type**

**Permission set type**

**Types:** Predefined permission set

**Policy for predefined permission set**

**Select an AWS managed policy:** PowerUserAccess

Click **Next**

**Step 07: Specify permission set details**

**Permission set details**

**Permission set name:** DeveloperAccess

**Description — _optional:_** Developer Access

**Session Duration:** 8 hours

Click **Next**

**Step 08: Review and create**

Click **Create**

✅**Green banner: The permission set “DeveloperAccess” was successfully created**

**Step 09: Click Users**

Click **Add user**

**Step 10: Specify user details**

**Username:** Enter username

**Password:** Send an email to this user with password setup instructions.

**Email Address:** Enter _your_ email Address

**Confirm email address:** Confirm _your_ email address

First name: _Your_ First name

Last name: _Your_ Last name

Display name: _Your_ Display name

Click **Next.**

**Step 11: Add user to groups — _optional_**

Click **Next**

**Step 12: Review and add user**

Click **Add user**

✅**Green banner: The user “cloudglossary” was successfully added.**

The user will receive an email with a link to set up a password and instructions to connect to the AWS access portal.

The link will be valid for up to 7 days. You can grant this user permissions to accounts or applications so that they can access their assigned AWS accounts and cloud applications when they sign in to the AWS access portal.

**Step 13: Open your Mailbox or Check your Emails**

**💡Verification:** You should see an email with, **Invitation to join AWS Identity Center**

Click **Accept invitation**

**Step 14: New user sign up**

**Username:** Your username

**New Password:** Set _your_ password

**Confirm Password:** Confirm _your_ password

Click **Set new password**

✅**Successfully created cloudglossary**

Your user account was successfully created.

**Step 15: Sign in**

**Username:** Enter _your_ username

Click **Next**

**Password:** Enter _your_ password

Click **Sign in**

**Step 16: Access portal**

**💡Verification: You have navigated to the AWS access portal**

After your administrator gives you access to applications and AWS accounts, you can find them here.

**Step 17: Navigate to your IAM Identity Center User**

Select **AWS Accounts**

Click **Assign accounts**

**Step 18: Assign AWS accounts to user**

**Permission sets:** DeveloperAccess

Select **AWS Organization**

Click **Assign**

✅**Green banner:** Successfully configured all assignments

**Setting Up Amazon Q Developer & Kiro**
----------------------------------------

### Amazon Q Developer

_Amazon Q Developer is an AI-powered coding assistant that understands your codebase and helps with development tasks._

**Step 19:** Select **⁝⁝⁝ Machine Learning** on the left side of the drop down menu.

Click **Amazon Q**

**Step 20: Amazon Q**

Click **Get started** ▼

Select **Amazon Q Developer**

**Step 21: Choose your AWS Session**

**ℹ️ Blue Banner:** **Amazon Q Developer and Kiro now share the same administration console.**

You can access your existing Amazon Q Developer Pro subscriptions or provision new ones from the left navigation or directly go to **Amazon Q Developer subscriptions page**.

Click **Settings**

**Step 22: Settings**

Click **Sign up for Kiro**

**Step 23: Welcome to Kiro!**

Click **Enable**

✅**Green banner: Successfully created Kiro profile**

You can now add users and groups in your team to Kiro.

**Step 24: Add your team to Kiro**

Click **Add user**

**Step 25: Select a Kiro plan**

Select **Kiro Pro**

Click **Continue**

**Step 26: Assign users**

Select the User you created in **14.**

Click **Assign**

✅**Green banner: Successfully created Kiro subscription for 1 user**

If you created subscriptions using groups, there may be a delay of up to 24 hours before your users can successfully access the subscription.

### **VS Code Setup**

**Step 27: Install Q Developer IDE Extension**

In VS Code search **Amazon Q** in extensions marketplace

Click **Install**

**Do you trust the publisher “Amazon Web Services”?:** Click Trust Publisher & Install

**Do you trust the authors of the files in this workspace?:** Trust Workspace & Install

**Step 28: Start Using Amazon Q**

**Click Sign In**

**Step 29: Choose sign in option:** Company account

Click **Continue**

**Step 30: Sign in with AWS IAM Identity Center**

**Start Url**: Enter your url

**Region:** us-east-1

**Step 31: Authenticating in browser**

Do you want

Click Yes.

**Step 32: Allow AWS IDE Extensions for VSCode to access your data?**

Click **Allow access.**

✅ **Request approved**

**💡Verification:** You should see the following message displayed on your browser:

**AWS IDE Extensions for VS Code have been given requested permissions**

**You can close this window and start using AWS IDE Extensions for VS Code**

**ℹ️ AmazonQ:** Successfully connected to AWS IAM Identity Center

**Step 33: Meet Amazon Q**

Click **Try example**

### Setting Up Kiro

_Kiro is an AI-powered development environment that provides agentic capabilities for coding_.

**Step 34:** [**Download Kiro**](https://kiro.dev/)

**Step 35: Sign in with your organization identity**

**Step 36: Sign in with AWS IAM Identity Center**

**Start Url**: Enter your url

**Region:** us-east-1

Click **Continue**

**Step 37: Allow Kiro IDE to access your data?**

Click **Allow access**

**Step 38: Kiro Pro**

**Credits: 0 used / 1000 covered in plan**

> **_⚠️Skip to Step 45 for Vibe Coding with Kiro or Q_**

### ⛔ End of Pro Tier Set Up Guide⛔

### Free Tier Guide

Setting Up Amazon Q Developer & Kiro
------------------------------------

### VS Code Setup

**Step 39: Install Q Developer IDE Extension**

In VS Code search **Amazon Q** in extensions marketplace

Click **Install**

**Do you trust the publisher “Amazon Web Services”?:** Click Trust Publisher & Install

**Do you trust the authors of the files in this workspace?:** Trust Workspace & Install

**Step 40: Start Using Amazon Q**

**Click Sign In**

**Step 41: Choose sign in option:** Personal account

### Setting Up Kiro

**Step 42:** [**Download Kiro**](https://kiro.dev/)

**Step 43: Sign in with your BuilderID**

**Step 44: Kiro Free**

**Credits: 0 used / 50 covered in plan**

### ⛔ End of Free Tier Set Up Guide⛔

### 🏗️ Let’s _Finally_ Build

Vibe Coding With Kiro
---------------------

**Building Our Application with Vibe Coding**

_Now let’s build something simple but impressive using “vibe coding”, where we describe what we want in Natural Language and let the AI agents help us build it._

**Project Idea:** A Beautiful, Interactive _Hello World_ Page

_Perfect for beginners in Artificial Intelligence, Cloud Computing & Web Development!_

_This project demonstrates the power of AI-assisted development without overwhelming complexity._

**Step 45:** **Project Initialization**

**Create a new project folder:** cloud-glossary

**Create a single HTML file:** index.html

**Step 46:** **Vibe Coding Session with Q Developer or Kiro or try Both**

**Simply describe what you want in natural language:**

_Create a beautiful, modern Hello World page with:_

1.  _A gradient background that animates_
2.  _Large, centered text that says ‘Hello, AI World!’_
3.  _A subtitle explaining this was built with AI assistance_
4.  _Smooth fade-in animation when the page loads_
5.  _A button that changes the greeting to different languages when clicked_
6.  _Modern, clean design with good typography_

**Step 47: What Happens Next**

**The AI generates a complete HTML file with embedded CSS and JavaScript**

You review the code and see how it works

You can ask for modifications:

_“Make the gradient more vibrant”_

_or_

_“Add more languages”_

**The AI explains any code you don’t understand**

**Step 48:** **Learning Through Vibe Coding**

**No need to remember CSS syntax**: just describe the look you want

**Don’t know JavaScript?** Describe the behavior and learn from the generated code

**Iterate quickly:** _“Make it more playful” or “Add a dark mode toggle”_

**Build confidence** by seeing immediate results

**Step 49:** **Example Interaction**

```
You: "Add floating particles in the background"
Kiro: [Generates canvas animation code with particles]
You: "Make the button pulse gently to draw attention"
Kiro: [Adds CSS animation with keyframes]
You: "Explain how the language switching works"
Kiro: [Provides clear explanation of the JavaScript array and event listener]
```

**Step 50:** **Kiro As A Coding Assistant & Mentor**

Vibe sessions aren’t just for building, you can also use them to learn as you go.

If you run into code you don’t understand, ask Kiro to explain what it does in plain language and walk you through it step by step.

Kiro can also help you get your project running on your own computer (so you can test it locally), and show you how to put your site online when you’re ready, whether that’s with GitHub (like GitHub Pages) or a simple hosting option like Amazon S3.

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Ask _Kiro_ if you need to **Terminate or Delete** anything based on your session.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

We demonstrated:

1.  Setting up AWS Identity Center for secure access management (Pro Tier)
2.  Configuring Amazon Q Developer for AI-assisted coding (Pro & Free Tier)
3.  Installing and configuring Kiro for agentic development (Pro & Free Tier)
4.  Building a beautiful, interactive “Hello World” page using vibe coding techniques
5.  Using AI as both a coding assistant and mentor

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [AI](https://medium.com/@ntombizakhona/artificial-intelligence-5028f826c856)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**02 December 2024**
