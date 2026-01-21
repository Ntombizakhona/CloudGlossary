### 🏗️ Let’s Build

Set Up Your Personal AWS Account
--------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

1.  Set up an **AWS Root Account** for _Administration and Billing_
2.  Create an **IAM User** for _Development_
3.  And enable **Multi-Factor Authentication** (MFA) to _secure your accounts_

### Prerequisites

1.  An Email Address
2.  Debit or Credit Card
3.  Authenticator App (_you can choose from the_ [_list of compatible applications_](https://aws.amazon.com/iam/features/mfa/?audit=2019q1)) for Multifactor Authentication (MFA)

### Set Up Your Personal AWS Account

_Your personal AWS account is your own space where you can explore, create, and innovate freely. It’s perfect for learning and experimenting with new skills, working on personal projects, developing and testing applications, hosting your website or blog, and storing and managing your personal data. With your personal AWS account, you have the freedom to try new things, showcase your talents, and bring your ideas to life._

**Step 01:** Open your favourite web browser and type in: [**aws.amazon.com**](https://aws.amazon.com/)

There are so many links (you think).

But, don’t worry, just focus on the top right corner, there should be an **Black Button**, waiting for you to click on it.

**Step 02:** Click on the **Create account** button on the top right corner of your screen.

After you click on the **Create AWS Account** button**,** you should be redirected to the portal, where you will create your AWS account.

New accounts get to start with $100 (R1500+)in AWS credits now, isn’t that cool?

> _Try AWS at no cost for up to 6 months_
> 
> _Start with USD $100 in AWS credits, plus earn up to USD $100 by completing various activities._

**Step 03:** Enter your **Root user email address** & your preferred **AWS Account Name**, and click **Verify Email Address.**

**Step 04:** Confirm your email address with the **Verification Code** in order to proceed.

The code can take up to 5 minutes to arrive and is valid for 60 seconds, so ensure you provide it timeously, or request a new one.

Once you have verified your email address, you will move on and create your password.

**Step 05:** **Create Your Password.**

**Create Your Password** and click continue, and you will find the **Contact Information page.**

**Step 06:** **Choose your account plan**

Select **Choose free plan.**

**Step 07:** **Contact Information**

**How do you Plan to use AWS?**

**Select:** Personal — for your own projects

Then fill out the rest of the form accordingly with **your personal details.**

**Nearby AWS Region selection _— optional_**

**Enabling nearby AWS Regions can provide benefits including improved performance. Uncheck the Region to prevent its usage.**

**Check:** Enable Africa (Cape Town) Region

_You can enable the region near you, but we will be using the United States North Virginia region when we build._

Read and agree to the AWS Customer Agreement.

**Check:** I have read and agree to the terms of the [AWS Customer Agreement](https://aws.amazon.com/agreement/) .

Click Agree and Continue.

**Step 08:** Enter your **Billing Information**

Make sure you have a valid payment method.

> _Our verification process holds USD $1 (or equivalent) for 3–5 days to verify your account and prevent fraud._

Click **Continue.**

**Step 09:** **Confirm your identity via text message or call.**

Click **Continue.**

**Step 10:** **Select a Support Plan:** Select **Basic support — Free.**

Click **Complete Sign Up.**

**Step 11: Congratulations!** That’s what you should see next, as AWS starts activating your account, it won’t take long at all, if you followed the steps properly.

You will receive an email when your account has been activated.

**Step 12:** Click **Go to the AWS Management Console** button, while you wait for your activation email.

**Step 13:** **Welcome to Amazon Web Services,** says the activation email. Now head back to the AWS Management Console and log in with the Root User Email Account and Password that you configured in **Step 03** and **Step 05.**

**Step 14:** Click **Sign In.**

**Step 15:** There it is, in all it’s glory, the **AWS Management Console!**

### The AWS Management Console

_The AWS Management Console is your one-stop shop for managing your AWS services and resources!_

_From this central hub, you can easily monitor, manage and modify your resources, applications and services, all in one place._

_It’s designed to be easy to use, even if you’re new to AWS, so you can get started right away!_

**Step 16:** Quickly familiarize yourself with the console.

**Categorical List of Services Offered By AWS:** On the left side of the menu, click on **‘Services’** to see a list of all the amazing services AWS offers, organized by category.

**Step 17:** Click on the circled question mark button **(?)** to see some of the official **support resources** offered by AWS.

**Step 18:** On the right, click on **N. Virginia** ▼, and marvel at the numerous regions that contribute to AWS’s global infrastructure.

**Step 19:** On the farthest right, click on your **Account Name**, and this is where you’ll find the more advanced administrative controls for your account, such as Billing and Account creation.

**Step 20:** Navigate back to the top left corner. Click on **⋮⋮⋮** **Services.**

**Step 21:** Select **Security, Identity & Compliance** on the left side of the drop down menu.

### Setup Your IAM User Account

Create an IAM (Identity And Access Management) User
---------------------------------------------------

_Your IAM account is your gateway to secure and controlled access to your AWS resources. With an IAM account, you can share access with others while maintaining granular control over permissions, ensuring that each user has only the access they need._

**Step 22:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 23:** Navigate to the left side, under ▼ **Access Management**, select **Users.**

**Step 24:** Click the **Create Users** button.

**Step 25:** **Specify User Details.**

**Step 25.1: User name:** CloudGlossary

**Check**: Provide user access to the AWS Management Console — _optional_

**Step 25.2: “Are you providing console access to a person?”**

Click **I want to create an IAM User.**

**Step 25.3:** **Console Password.**

Select a **Custom Password,** that follows the password principles, that you can see below the text-area.

**Custom Password:** @CloudGlossaryAdmin#2026!

**Step 25.4:** **Users must create a new password at next sign-in — Recommended:** uncheck.

Click **Next.**

**Step 26:** You are now in the **Set Permissions** screen.

It is best practice to attach policies to a group, but since you’re creating your first user, and have no groups yet, select **Attach Policies directly.**

**Step 27:** Search for and select **AdministratorAccess**

_We are using the AdministratorAccess policy for brevity and for quickly activating the additional $100… But it is considered a best practice (important and necessary) to select the most restrictive policy as this ensures that users and applications only have the permissions they need, reducing the risk of data breaches and unauthorized access._

_You should always incrementally add the relevant permissions as time goes on._

Click **Next.**

**Step 28:** **Review and Create** your User Details and Permissions summary, and click **Create User.**

✅**Green banner:** User created successfully.

You can view and download the user’s password and email instructions for signing in to the AWS Management Console.

**Step 29:** **Congratulations.** You have created an IAM User.

**Step 30:** Copy the **Console Sign-In URL, Username and Password.**

Click **View user.**

**Step 31: Summary**

Click **Create access key**

**Use case:** Command Line Interface (CLI)

**Confirmation**: check _I understand the above recommendation and want to proceed to create an access key._

Click **Next**

**Step 32:** Click **Create access key**

**Step 33:** Click **Download .csv file**

Click **Done.**

**Step 34:** Click **Security Credentials**

Scroll to **Multi-factor authentication (MFA)**

💡**Verification:** You should see the user created successfully with access keys displayed

Enable Multifactor Authentication
---------------------------------

_Multifactor authentication (MFA) boosts account security by demanding more than just a password to log in, much like accessing a safe requires both the combination and a physical key._

_Just as a password is like the combination, MFA adds a second form of verification like a code, biometric scan, or app-generated code to ensure only authorized individuals can unlock and access their accounts._

_This way, even if someone knows your password, they won’t be able to get into your account without that second form of verification. It adds an extra layer of security to keep your account safe, providing an additional barrier against unauthorized access and giving you peace of mind that your personal information is protected_

**Step 35:** Click **Assign MFA device**

**Step 36: Select MFA Device**

**MFA Device name:** CloudGlossary

**MFA Device:** Authenticator app

Click **Next.**

**Step 37: Set Up Device**

Download an Authenticator app

Personally, I recommend **Authy** because you can seamlessly access it from multiple devices and it’s an authenticator app that hasn’t given me problems; however, you can choose from the [list of compatible applications](https://aws.amazon.com/iam/features/mfa/?audit=2019q1) presented to you, or use your existing authenticator app.

**Scan the QR code.**

**Enter two Consecutive Codes from your MFA device** to validate it.

Click **Add MFA.**

✅**Green banner:** MFA device assigned

You can register up to 8 MFA devices of any combination of the currently supported MFA types with your AWS account root and IAM user. With multiple MFA devices, you only need one MFA device to sign in to the AWS console or create a session through the AWS CLI with that user.

💡 **Verification:** You should see **MFA device assigned**

**Step 38:** Copy the **Console sign in link**

Enter the Console Sign-In URL in your browser, so that you can sign in as the IAM user you just created.

How do you know that you’re logged in as an IAM User?

Check the top right corner.

Click **account name (account-id)** ▼

You should see your IAM Username there.

### **Let’s Build**

**Earning Your Extra $100**
---------------------------

_Now here’s where it gets interesting. AWS wants you to actually try their services, so they’ll give you $20 for each of these 5 activities. Think of it as a guided tour of Cloud Computing, except you get paid to take it._

**Activity 01:** Cloud Finance **→** Budgets

**Activity 02:** Compute **→** EC2

**Activity 03:** Databases **→** RDS

**Activity 04:** Serverless **→** Lambda

**Activity 05:** AI **→** Bedrock

_Make sure you are in the North Virginia Region_ (**N. Virginia** ▼)

### Activity 01

Setup Cost Alerts With AWS Budgets
----------------------------------

_AWS Budgets is an AWS tool that helps you set spending (or usage) limits and get alerts so your AWS costs don’t surprise you._

_You can create budgets for things like monthly cost, forecasted cost, or service usage (e.g., EC2 hours), and AWS will email (or send notifications to SNS) when you hit thresholds like 50%, 80%, or 100% of your budget._

_It’s commonly used to track costs by account, service, region, or tags and to help teams stay within a planned cloud budget._

**Step 39: Access Billing Console**

Click your **Root account name** (top right)

Select **Billing and Cost Management**

**Step 40:** **Navigate to Budgets**

Under **Budgets and Planning,** click **Budgets**

Click **Create budget**

**Step 41: Choose budget type**

**Budget setup:** Use a template (simplified)

**Templates — new:** Zero spend budget

**Budget name:** My Zero-Spend Budget

**Email Recipients:** Your Email Address

Click **Create budget**

✅**Green banner:** Your budget My Zero-Spend Budget has been created successfully.

_You will be notified when you spending exceeds Zero Dollars._

**Step 42: Navigate to Billing and Payments**

💸 **Credit** **Verification: $20 Credited**

**Credit Name:** _Explore AWS: Set up a cost budget using AWS Budgets_

### Activity 02

Launch A Server With Amazon EC2
-------------------------------

_Amazon EC2 (Elastic Compute Cloud) is a service from AWS that lets you rent a virtual computer in the cloud._

_Instead of buying a physical server, you can create an “instance” (a virtual machine), choose its size (CPU and memory), and run your website or application on it._

_You can start and stop it anytime, scale to more instances if you need more power, and you generally pay only for the time and resources you use._

**Step 43:** Access EC2 Console

In AWS Console, search for **EC2**

Click on **EC2**

Click **Launch Instance**

**Step 44: Name and tags**

**Name:** MyServer

▼ **Application and OS Images (Amazon Machine Image):** Amazon Linux 2023

**Instance type:** t3.micro

**Key pair (login):** Proceed without a key pair (Not recommended)

Click **Launch instance**

✅**Green banner:** **Success**

Successfully initiated launch of instance (i-0e58295647f2183bd)

Click on the Instance ID.

**Instance State:** Running

💡 **Verification:** Instance is running.

**Step 45: Navigate to Billing and Payments**

💸 **Credit** **Verification: $20 Credited**

**Credit Name:** _Explore AWS: Launch an instance using EC2_

### Activity 03

Create A Database with Amazon RDS
---------------------------------

_Amazon RDS (Relational Database Service) is an AWS service that makes it easier to run a relational database in the cloud without managing most of the setup and maintenance yourself._

_You choose a database engine like MySQL, PostgreSQL, MariaDB, Oracle, or SQL Server (and AWS also offers Amazon Aurora, a high-performance option), and RDS handles things like backups, patching, monitoring, and scaling._

_You connect to it like a normal database, but AWS takes care of much of the operational work behind the scenes._

**Step 46: Access RDS Console**

Search for **RDS** in AWS Console

Click on **Aurora and RDS** service

Click **Create a database**

**Step 47: Create database**

**Choose a database creation method:** Easy create

**Step 48: Configuration**

**Engine type:** MySQL

**Edition:** MySQL Community

**DB instance size:** Dev/Test

**DB instance identifier:** my-database

**Master username:** admin

**Credentials management:** Self managed

**Master password:** MasterPassword

**Confirm master password:** MasterPassword

Click **Create database**

**Step 49: Wait for status “Available**” _(takes 5–10 minutes)_

✅**Green banner: Successfully created database my-database**

You can use settings from my-database to simplify configuration of **suggested database add-ons** while we finish creating your DB for you.

**Step 50: Navigate to Billing and Payments**

💸 **Credit** **Verification: $20 Credited**

**Credit name:** _Explore AWS: Create an Aurora or RDS database_

### Activity 04

Build A Serverless App With Lambda
----------------------------------

_AWS Lambda is a_ **_serverless compute_** _service that lets you run code without managing servers._

_You upload your function (in languages like Python, Node.js, Java, etc.), and Lambda automatically runs it when it’s triggered, such as by an API call (API Gateway), an S3 file upload, a database change, or a scheduled event._

_It scales automatically and you generally pay only for the number of requests and the time your code runs._

**Step 51: Access Lambda Console**

Search for **Lambda**

Click on **Lambda**

Click **Create a function**

**Step 52: Create function:** Author from scratch

**Function name:** myFunction

Click **Create function**

**Step 53: Dismiss Pop Up**

✅ **Green banner:** Successfully created the function **myFunction**. You can now change its code and configuration. To invoke your function with a test event, choose “Test”.

**Step 54: Click Test**

Click Create new test event

**Event name:** test-event

**Template-optional:** Hello World

Click **Save**

**Green banner:** The test event “test-event” was successfully saved.

Click Test

**Executing function: succeeded**

```
{
 "statusCode": 200,
 "body": "\"Hello from Lambda!\""
}
```

**Step 55: Navigate to Billing and Payments**

💸 **Credit** **Verification: $20 Credited**

**Credit name:** _E_xplore AWS: Create a web app using AWS Lambda

### Activity 05

**Prompt an AI Model with Amazon Bedrock**
------------------------------------------

_Amazon Bedrock is an AWS service that lets you build generative AI apps using foundation models (LLMs and image models) without having to host or manage the models yourself._

_You can access models from providers like Anthropic, Meta, Mistral, and Amazon (Titan) through an API, and use features like Agents (to take actions), Knowledge Bases / RAG (to answer using your documents), and built-in security and access controls._

_You pay based on usage, such as the number of input/output tokens or inference calls._

**Step 56: Access Bedrock Console**

Search for **Bedrock** in AWS Console

Click on **Amazon Bedrock**

**Step 57: Test**

**Chat / Text playground**

Click **Open playground**

**Step 58: Chat Mode**

Click **Select model**

1.  **Categories:** Amazon
2.  **Models:** Nova Pro
3.  **Inference:** On demand

Click **Apply**

**Step 59: _Write a prompt and choose Run to generate a response._**

> Pretend you’re a helpful wizard, explain my question in one simple sentence, then give one fun example. What is Cloud Computing?

Enter your prompt and click ▶ **Run**

**Step 60:** My Response:

**Simple Explanation:** Cloud Computing is using a network of remote servers on the internet to store, manage, and process data, rather than a local server or a personal computer.

**Fun Example:** Imagine you have a magical chest (the cloud) where you can store all your treasure (data). Whenever you need some treasure, you just ask the wizard (server) guarding the chest, and he brings it to you instantly, no matter where you are in the kingdom (anywhere with internet access).

_And that is how you can take advantage of LLMs to be your Study Buddy or Tutor as you master the Cloud!_

**Step 61: Navigate to Billing and Payments**

💸 **Credit** **Verification: $20 Credited**

**Credit name:** _Explore AWS: Use a foundation model in the Amazon Bedrock playground_

### Congratulations

**Check Your Credit Balance**
-----------------------------

1. Go to **Billing and Cost Management**

2. Click **Credits** in left sidebar

3. You should see:

**$100** from account creation

$20 × 5 activities = **$100** additional

💸 **Total: $200 in credits**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

1.  Terminate instance to avoid charges

Select instance → Actions → Instance State → **Terminate**

2. Select your database

Actions → **Delete**

3. Select your function

Actions → **Delete**

4. Select your IAM User and Remove the AdministratorAccess permisson.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*nIdmVRCvjMAa1Kar5Q4bzw@2x.jpeg)

We covered the complete journey from AWS account creation to hands-on cloud computing experience, earning $200 in free credits along the way.

The foundation began with account security fundamentals: the root user account serves as the master administrator with unlimited access (reserved for emergency use only), while the IAM user is created to perform specific roles and tasks with limited permissions for daily operations. To add an extra layer of security, Multi-Factor Authentication (MFA) was implemented, requiring a second form of verification beyond just a password.

Building on this secure foundation, we then gained practical experience with five core AWS services through hands-on activities. We set up cost monitoring and financial governance using AWS Budgets to track spending and receive alerts. We launched our first virtual server with Amazon EC2, learning the fundamentals of cloud computing infrastructure. We created a managed MySQL database with Amazon RDS, exploring database-as-a-service concepts. We built a serverless function using AWS Lambda, discovering the power of event-driven, serverless computing. Finally, we interacted with AI foundation models through Amazon Bedrock, experiencing how modern AI services integrate into cloud applications.

Each activity not only earned us $20 in AWS credits but also provided hands-on experience with essential cloud computing concepts. From the initial $100 signup bonus to the $100 earned through practical learning, we achieved the full $200 in free tier credits while building a comprehensive understanding of AWS services.

By understanding and utilizing these security components alongside practical service implementation, you can effectively manage access to your cloud resources, ensure the security of your account, and gain real-world experience with the core services that power modern cloud applications. This combination of security best practices and hands-on learning creates a solid foundation for your cloud computing journey.


# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Amazon Web Services](https://ntombizakhona.medium.com/amazon-web-services-a8e57a9c6084)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**21 June 2024**
