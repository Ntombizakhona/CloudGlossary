### 🏗️ Let’s Build

Deploying An Apache HTTP Server on AWS
-------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Deploy an Apache HTTP Server.**

Prerequisites
-------------

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**A Key Pair**](https://medium.com/abstraction-d1335bec022e)
4.  [**Familiarity with HTML**](https://medium.com/html-in-the-cloud-dc23a04bfe51)
5.  [**Familiarity with Linux or the Command Line**](https://medium.com/linux-in-the-cloud-1274f654f972)

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

**AmazonEC2FullAccess**

✅**Green banner:** 1 policy added

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 08:** Sign in with your IAM Account.

**Step 09:** Before you proceed, make sure that you’re signed in with your IAM User Account, and that you’re in the **N. Virginia** ▼ region (us-east-1).

### Launch EC2 Instances

**Step 10:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Step 11: Dashboard**

Click **Launch instance.**

**Step 12: Launch an instance**

Under **Name and Tags.**

**Name:** ApacheWebServer

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

select **CloudGlossary**

**Step 13:** ▼ **Network settings.**

Click **Edit**

Scroll to **Firewall (security groups)**

Select **Create security group.**

**Security group name — _required_:** CloudGlossarySG

**Description — _required_:** Security Group for My Cloud Glossary Tutorials

Under **Inbound Security Group Rules.**

**Type:** Select **SSH**

**Source Type**: Select **Anywhere.**

Click **Add Security group rule.**

**Type:** Select **HTTP.**

**Source Type**: Select **Anywhere.**

Click **Add security group rule**

**Type:** Select **HTTP.**

**Source Type**: Select **AnywShere.**

▼ **Configure storage:** leave as default

▼ **Advanced details:** leave as default

Click **Launch instance**

✅**Green banner: Success**

Click **View all instances**

### Create an IAM Policy for EC2 Instance Connect

**Step 14: Navigate to IAM**

On the left side of the screen under ▼ **Access management**

Select **Users**

**Step 15: Users**

Select the **Cloud Glossary** IAM User.

**Step 16: CloudGlossary**

Select **Permissions**

Click **Add permissions** ▼

Select **Create inline policy**

**Step 17: Specify permissions**

**Policy editor:** JSON

```
{
    "Version": "2012-10-17",
    "Statement": [        {
            "Sid": "EC2InstanceConnect",
            "Effect": "Allow",
            "Action": [                "ec2-instance-connect:SendSSHPublicKey"
            ],
            "Resource": [                "arn:aws:ec2:*:*:instance/*"
            ],
            "Condition": {
                "StringEquals": {
                    "ec2:osuser": "ec2-user"
                }
            }
        },
        {
            "Sid": "DescribeInstances",
            "Effect": "Allow",
            "Action": [                "ec2:DescribeInstances",
                "ec2:DescribeInstanceConnectEndpoints"
            ],
            "Resource": "*"
        }
    ]
}
```

Click **Next**

**Step 18: Review and create**

**Policy name:** EC2InstanceConnectPolicy

Click **Create policy**

✅**Green banner: Policy EC2InstanceConnectPolicy created.**

### EC2 Instance Connect

**Step 19:** ✔ **Select Your Instance**

Click **Connect**

**Step 20: Connect**

Select **EC2 Instance Connect**

Click **Connect**

### Install Apache

**Step 21: Run these commands**

```
# Update package lists
sudo dnf update -y
# Install Apache (called 'httpd' on Amazon Linux)
sudo dnf install httpd -y
# Start Apache and enable it to start on boot
sudo systemctl start httpd
sudo systemctl enable httpd
# Verify Apache is running
sudo systemctl status httpd
```

You should see output indicating **Apache is active (running):**

```
● httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled)
     Active: active (running) since ...
```

### Verify Security Group Settings

**Step 22: Go to EC2 Dashboard**

▼ **Network & Security**

**Security Groups**

Select **CloudGlossarySG**

Click **Inbound rules** tab

Verify you have:

*   **HTTP** (Port 80) from 0.0.0.0/0
*   **HTTPS** (Port 443) from 0.0.0.0/0

### Deploy a Sample Website

**Step 23:** Let’s replace the default Apache page with a custom website:

```
# Navigate to the web root directory
cd /var/www/html
# Create a custom homepage (this will override the default Apache welcome page)
sudo nano index.html
```

**Step 24:** Paste this:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Apache Server on AWS</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
        }
        .container {
            text-align: center;
            padding: 40px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            max-width: 600px;
        }
        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
            background: linear-gradient(90deg, #e94560, #ff6b6b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        p {
            font-size: 1.2em;
            line-height: 1.6;
            margin-bottom: 15px;
            color: #b8b8d1;
        }
        .success-badge {
            display: inline-block;
            padding: 10px 25px;
            background: linear-gradient(90deg, #00b894, #00cec9);
            border-radius: 25px;
            font-weight: bold;
            margin: 20px 0;
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        .info {
            margin-top: 30px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }
        .info h3 {
            color: #e94560;
            margin-bottom: 10px;
        }
        code {
            background: rgba(255, 255, 255, 0.1);
            padding: 2px 8px;
            border-radius: 4px;
            font-family: 'Courier New', monospace;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚀 Apache HTTP Server</h1>
        <p>Welcome to your cloud-deployed web server!</p>
        <div class="success-badge">✓ Successfully Running on AWS EC2</div>
        <p>You've successfully deployed Apache HTTP Server on Amazon Web Services.</p>
        
        <div class="info">
            <h3>Server Information</h3>
            <p>Web Server: <code>Apache/2.4</code></p>
            <p>Operating System: <code>Amazon Linux 2023</code></p>
            <p>Cloud Provider: <code>Amazon Web Services</code></p>
        </div>
    </div>
</body>
</html>
```

**Step 25: Save the file:**

Press _Ctrl + O_, then _Enter_ to **save**

Press _Ctrl + X_ to **exit**

### Test Your Deployment

**Step 26: Open a new tab**

Enter your EC2 instance’s public IP address:

```
http://<YOUR-PUBLIC-IP>
```

💡**You should see your custom Apache landing page!**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _EC2_ and **Delete** The Instance.
2.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.
3.  🚫 **Don’t Delete The Security Group.**

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*A2yU5GzYRkjUKZAz-1qAzQ.png)

Throughout this tutorial, we developed several essential cloud computing skills.

We mastered EC2 instance launching, which involved creating and configuring a virtual server within AWS.

We practiced SSH access techniques to securely connect to our cloud server via the terminal, ensuring encrypted communication between our local machine and the remote instance.

We also covered Apache installation, learning how to install and configure the httpd web server on a Linux-based operating system.

Understanding security groups was crucial, we configured AWS firewall rules to control exactly which network traffic could reach our instance.

Finally, we performed web deployment by placing a custom HTML website on our server and making it accessible to the internet.

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Apache HTTP](https://ntombizakhona.medium.com/apache-http-8404a1b11d26)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**07 February 2026**
