### Let’s Build
# Setting Up Alerts with Amazon SNS

I know *(hope)* you’re eager to set something up. In this practical, hands-on-tutorial, we will demonstrate Alerts with *Amazon Simple Notification Service.*

Amazon Simple Notification Service (SNS) is a flexible and powerful tool for managing alerts.

## Prerequisites
1. An AWS Administrative Account
2. An AWS IAM User Account

## Add Permissions
**Step 01:** Log in to AWS Management Console with Your Root User / Administrator Account.

In keeping up with the Spirit of the Principle of Least Privilege, we will only assign permissions relevant to the task at hand.


**Step 02:** Select Security, Identity & Compliance on the left side of the drop down menu.


**Step 03:** Select IAM.

You should be redirected to the IAM Dashboard.


**Step 04:** On the left side of the screen expand Access management.

Select Users.

Select your IAM User.


**Step 05:** Select Add permissions. Add permissions.

Permissions options: Attach policies directly

Select: AmazonSNSFullAccess

Click Next.

Click Add permissions.


**Step 06:** Log in to the AWS Management Console with your IAM User.

Create Topic


**Step 07:** Navigate to Amazon SNS by typing it on the search bar.


**Step 08:** Topic Name: MyAlertTopic

Click Next Step.

**Step 09:** Type: Standard.

Display name — optional: My Cloud Glossary Alert

Click Create topic.

Green Banner: Topic MyAlertTopic created successfully.

You can create subscriptions and send messages to them from this topic.

## Create Subscription

**Step 10:** Click Create subscription

Protocol: Email.

Endpoint: Your Email Address

Click Create subscription.

Green Banner: Subscription to MyAlertTopic created successfully.

The ARN of the subscription is arn:aws:sns:us-east-1:your-acount-id:MyAlertTopic:14d1b200-fce6–4bf7-bc9d-06c8736e4809.


**Step 11:** Check your email and confirm the subscription by clicking the link in the message you receive.
Subscription confirmed!

You have successfully subscribed.

Test Your Alert


**Step 12:** Navigate to your Amazon SNS page, and click on Topics.

Select MyAlertTopic.

Click Publish Message.

Subject: My Alert

Message body

Message structure: Identical payload for all delivery protocols.

Message body to send to the endpoint: Amazon Simple Notification Service (SNS) is a flexible and powerful tool for managing alerts.

Click Publish message

Green Banner: Message published to topic MyAlertTopic successfully.


**Step 13:** Check your email, you should see the alert.


**Step 14:** Login with your Root User Account, and Remove All Permissions Associated with your IAM Account.

### End of Tutorial.


# Building Tutorial Overview
We observed Alerts in the Cloud, by publishing a message on Amazon SNS.
