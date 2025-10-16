### Let’s Build
# Set Up Your Personal AWS Account

I know *(hope)* you’re eager to set something up, so in this practical, hands-on-tutorial, we will observe the ease of entry by setting up an AWS Root Account for Administration and Billing, an IAM Account for Development purposes and Multifactor Authentication for securing your accounts.

## Prerequisites
1. An Email Address
2. Debit or Credit Card
3. Authenticator App (you can choose from the list of compatible applications) for Multifactor Authentication (MFA)


## Set Up Your Personal AWS Account
Your personal AWS account is your own space where you can explore, create, and innovate freely. It’s perfect for learning and experimenting with new skills, working on personal projects, developing and testing applications, hosting your website or blog, and storing and managing your personal data. With your personal AWS account, you have the freedom to try new things, showcase your talents, and bring your ideas to life.


**Step 1:** Open your favourite web browser and type in: *aws.amazon.com*
There are so many links (you think).

But, don’t worry, just focus on the top right corner, there should be an orange button, waiting for you to click on it.


**Step 2:** Click on the Create AWS Account button on the top right corner of your screen.

After you click on the Create AWS Account button, you should be redirected to the portal, where you will create your AWS account.


**Step 3:** Enter your Root user email address & your preferred AWS Account Name, and click Verify Email Address.


**Step 4:** Confirm your email address with the Verification Code in order to proceed.

The code is valid for 10 minutes, so ensure you provide it timeously, or request a new one.

Once you have verified your email address, you will move on and create your password.


**Step 5:** Create Your Password.

Create Your Password and click continue, and you will find the Contact Information page.


**Step 6:** Select Personal — for your own projects under “How do you plan to use AWS?”

Then fill out the rest of the form accordingly with your personal details.

Read and agree to the AWS Customer Agreement.

Click **Continue.**



**Step 7:** Enter your Billing Information

Make sure you have a valid payment method.

Click **Continue.**


**Step 8**: Confirm your identity via text message or call.

Click **Continue.**


**Step 9:** Select a Support Plan: Select Basic support — Free.

Click **Complete Sign Up.**


**Step 10:** Congratulations! That’s what you should see next, as AWS starts activating your account, it won’t take long at all, if you followed the steps properly.


You will receive an email when your account has been activated.


**Step 11:** Click Go to the AWS Management Console button, while you wait for your activation email.


**Step 12:** Welcome to Amazon Web Services, says the activation email. Now head back to the AWS Management Console and log in with the Root User Email Account and Password that you configured in Step 3 and Step 5.


**Step 13:** Click Sign In.


**Step 14:** There it is, in all it’s glory, the AWS Management Console!


## The AWS Management Console
The AWS Management Console is your one-stop shop for managing your AWS services and resources! From this central hub, you can easily monitor, manage and modify your resources, applications and services, all in one place. It’s designed to be easy to use, even if you’re new to AWS, so you can get started right away!



**Step 15:** Quickly familiarize yourself with the console.

Categorical List of Services Offered By AWS:
<br>
On the left side of the menu, click on ‘Services’ to see a list of all the amazing services AWS offers, organized by category.


**Step 16:** Click on the circled question mark button (?) to see some of the official support resources offered by AWS.



**Step 17:** On the right, click on N. Virginia, and marvel at the numerous regions that contribute to AWS’s global infrastructure.

Oh, by the way, a new region in Taiwan is reportedly coming soon.


**Step 18:** On the farthest right, click on your Account Name, and this is where you’ll find the more advanced administrative controls for your account, such as Billing and Account creation.


**Step 19:** Navigate back to the top left corner. Click on Services.


**Step 20:** Select Security, Identity & Compliance on the left side of the drop down menu.

## Create an IAM (Identity And Access Management) User
Your IAM account is your gateway to secure and controlled access to yourS resources. With an IAM account, you can share access with others while maintaining granular control over permissions, ensuring that each user has only the access they need.



**Step 21:** Select IAM.
You should be redirected to the IAM Dashboard.


**Step 22:** Navigate to the left side, under Access Management, select Users.


**Step 23:** Click the Create Users button.


**Step 24:** Specify User Details.

***Step 24.1:*** Create a relevant user name.
Check: Provide user access to the AWS Management Console — optional

***Step 24.2:*** “Are you providing console access to a person?”
Click I want to create an IAM User.

***Step 24.3:*** Console Password.
Select a Custom Password, that follows the password principles, that you can see below the text-area.

***Step 24.4:*** Users must create a new password at next sign-in — Recommended: make sure that this is checked, and click Next.


**Step 25:** You are now in the Set Permissions screen.

It is best practice to attach policies to a group, but since you’re creating your first user, and have no groups yet, select Attach Policies directly.


**Step 26:** Search for and select IAMFullAccess.
It is considered a best practice (important and necessary) to select the most restrictive policy as this ensures that users and applications only have the permissions they need, reducing the risk of data breaches and unauthorized access. You will incrementally add the relevant permissions as time goes on.

Click **Next.**


**Step 27:** Review and Create your User Details and Permissions summary, and click Create User.


**Step 28:** Congratulations. You have created an IAM User.


**Step 29:** Copy the Console Sign-In URL, Username and Password.


**Step 30:** Enter the Console Sign-In URL in your browser, so that you can sign in as the IAM user you just created.

*Note:* If you are using one browser, you will be signed out of your previous session as a root user.


**Step 31:** Sign in as IAM User.

Enter the Account Alias or AccountID.

Enter the IAM Username.

Enter the Password.

Click Sign In


**Step 32:** Since you selected : “Users must create a new password at next sign-in’’ in Step 24.4 You must change you password to continue.


Enter the Old Password.


Create Your New Password.


Confirm Password and Sign-in.


**Step 33:** Welcome to the AWS Management Console as an IAM user.


How do you know that you’re logged in as an IAM User?
Check the top right corner, it should say username @ accountname, if you click on it, you will see the Account ID, and your IAM Username.



## Enable Multifactor Authentication
Multifactor authentication (MFA) boosts account security by demanding more than just a password to log in, much like accessing a safe requires both the combination and a physical key. Just as a password is like the combination, MFA adds a second form of verification — like a code, biometric scan, or app-generated code — to ensure only authorized individuals can unlock and access their accounts.


This way, even if someone knows your password, they won’t be able to get into your account without that second form of verification. It adds an extra layer of security to keep your account safe, providing an additional barrier against unauthorized access and giving you peace of mind that your personal information is protected


**Step 34:** On the top left corner, click on the Services button.


**Step 35:** Select Security, Identity & Compliance on the left side of the drop down menu.


**Step 36:** Select IAM.


**Step 37:** Navigate to the left side, under Access Management, select Users


**Step 38:** Click on the User you just created.


**Step 39:** Navigate to the Security Credentials Tab.


**Step 40:** Click Assign MFA device.


**Step 41:** Give your device a name in Device Name.


**Step 42:** Under MFA Device, select Authenticator App.

Click Next.



**Step 43:** Set Up Device: Download an authentication application.
Personally, I recommend Authy because you can seamlessly access it from multiple devices and it’s an authenticator app that hasn’t given me problems; however, you can choose from the list of compatible applications presented to you, or use your existing authenticator app.


**Step 44:** Scan the QR code.


**Step 45:** Enter two Consecutive Codes from your MFA device to validate it.


**Step 46:** Click Add MFA.


**Step 47:** Congratulations: MFA Device Assigned.


### End of Tutorial


## Building Tutorial Overview
We covered the basics of account creation and security on AWS. 

The root user account serves as the master administrator with unlimited access, while the IAM user is created to perform specific roles and tasks with limited permissions.

To add an extra layer of security, Multi-Factor Authentication (MFA) is used, requiring a second form of verification beyond just a password. By understanding and utilizing these components, you can effectively manage access to your cloud resources and ensure the security of your account.
