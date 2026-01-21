### 🏗️ Let’s Build

Demonstrating Abstraction in the Cloud with Amazon Beanstalk
------------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Deploy a Basic Static Site.**

_This will demonstrate abstraction by contrasting Amazon Elastic Compute Cloud (EC2) and Amazon Beanstalk, which is considered an_ **_abstraction_** _of EC2._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

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

**AdministratorAccess-AWSElasticBeanstalk**

**AmazonS3FullAccess**

**AWSCloudFormationFullAccess**

**AmazonRDSFullAccess**

**CloudWatchFullAccess**

**CloudWatchFullAccessV2**

**IAMFullAccess**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 8** policies added to CloudGlossary

### Create an IAM EC2 Instance Profile for Elastic Beanstalk

_An EC2 instance profile is a container for an IAM role that you attach to an EC2 instance so the instance can automatically get temporary AWS credentials and access AWS services without storing access keys on the server._

**Step 09:** On the left side of the screen under ▼ **Access management**

Select **Roles**

**Step 10: Roles**

Click **Create role**

**Step 11: Select trusted entity**

Select **AWS service**

**Use Case:** EC2

**Use Case:** EC2

Click **Next**

**Step 12: Add permissions**

Select **AdministratorAccess-AWSElasticBeanstalk**

Click **Next**

**Step 13: Name, review, and create**

Role name: **AbstractionRole**

Click **Create role**

✅**Green banner: Role AbstractionRole created.**

Click **View role**

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 14:** Sign in with your IAM Account.

Depending on how long ago you last logged in and your password policy, you might have to reset your password using your Administrative Account. Ignore Steps **14.1–14.8** if you don’t have to reset your password.

**Step 14.1**: Sign in with your Administrative Root User Account in order to reset your password.

**Step 14.2:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 14.3:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 14.4:** On the left side of the screen expand **Access management.**

**Step 14.5:** Select **Users.**

**Step 14.6:** Select the CloudGlossary IAM User.

**Step 14.7:** Select **Security credentials.**

Click **Manage console access.**

Select **Reset password.**

Under **Console password,** Select **Custom password.**

Click **Reset password.**

✅**Green banner: You have successfully enabled the user’s new password.**

This is the only time you can view this password. After you close this window, if the password is lost, you must create a new one.

**Step 14.8:** Click **Close.**

Elastic Compute Cloud Tutorial
------------------------------

_Amazon Elastic Compute Cloud (EC2) is AWS’s service for renting virtual servers (“_**_instances_**_”) in the cloud._

_You choose the instance size and operating system, run your applications on it, and can scale up/down or start/stop instances as needed, paying for the compute you use._

**Step 15:** Before you proceed, make sure that you’re signed in with your IAM User Account, and that you’re in the **N. Virginia** ▼ region (us-east-1).

### Launch EC2 Instances

**Step 16:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Step 17: Dashboard**

Click **Launch instance.**

**Step 18: Launch an instance**

Under **Name and Tags.**

**Name:** NoAbstraction

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

select **Create new key pair.**

You should be redirected to the **Create key pair** pop up.

**Step 19: Create key pair**

**Key pair name:** CloudGlossary

**Key pair type:** RSA

**Private key file format**: .pem

Click **Create key pair.**

Save it on your local device.

> **_⚠️ Keep this Key pair safe because we will be using this Key pair throughout the Cloud Glossary Tutorials._**

**Step 20:** ▼ **Network settings.**

Click **Edit**

Scroll to **Firewall (security groups)**

Select **Create security group.**

**Security group name — _required_:** CloudGlossarySG

**Description — _required_:** Security Group for My Cloud Glossary Tutorials

Under **Inbound Security Group Rules.**

Click **Add Security group rule.**

**Type:** Select **HTTP.**

**Source Type**: Select **Anywhere.**

▼ **Configure storage:** leave as default.

**Step 21:** ▶ **Advanced details**

Scroll to the bottom, but, don’t scroll too fast, make a note of all the features you can manually configure until you reach **User data — _optional._**

Paste this

```
#!/bin/bash
# 📦 Update system packages (works on both AL2 and AL2023)
sudo yum update -y
# 🐍 Install Python3 and pip (AL2023 compatible)
sudo yum install -y python3 python3-pip
# 🔧 Install Flask using pip3
sudo pip3 install flask
# 📁 Create a directory for the app
mkdir -p /home/ec2-user/hello-world
# 🐍 Create the Flask application
cat > /home/ec2-user/hello-world/app.py <<EOF
from flask import Flask
app = Flask(__name__)
@app.route('/')
def hello():
    return "Hello World from EC2! This is NO ABSTRACTION"
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
EOF
# ▶️ Run the Flask app in background
cd /home/ec2-user/hello-world
nohup sudo python3 app.py > app.log 2>&1 &
```

**Step 22:** At the right of the page ▼ **Summary**

**Number of instances:** 2

Click **Launch instance.**

✅**Green banner: Success**

Successfully initiated launch of instances (i-0ee3d369d7bb6x401, i-0d20b6b0e771e85xb)

Click **View all instances**

You should be redirected to the instances dashboard.

**Step 23:** Make sure your **NoAbstraction** instances are in the **Running** state.

**Name:** NoAbstraction

**Instance State:** ✅Running

Click on the **Instance ID** of the first instance.

Copy the **Public IPv4 address,** and paste it into your browser.

> **_⚠️_**_Make sure it begins with_ **_http:// (_**_Port 80) and not_ **_https://_** _(Port 443). You will received_ **_ERR_CONNECTION_TIMED_OUT_** _if it begins with_ **_https://_** _because the Security group and the app associated with your instance is open on Port_ **_80 (HTTP)_** _and not_ **_Port 443 (HTTPS)._**

**💡Verification:** You should see the following message displayed on your browser:

**Hello World from EC2! This is NO ABSTRACTION**

### Configure AutoScaling

**_Autoscaling_** _is like having extra help ready to step in when needed._

_In simple terms,_ **_autoscaling_** _is a feature that automatically adjusts the number of servers (instances) your application uses based on how much traffic or work it’s handling._

_If your app gets busy (like during a sale or a viral moment),_ **_autoscaling adds more servers_** _to handle the load._

_If things get quiet,_ **_autoscaling removes extra servers_** _to save money._

_This way, your application always has just the right amount of resources — never too many (wasting money) or too few (causing slowdowns or crashes)._

**Step 24:** Navigate back to the EC2 Console.

On the far right of the page, at the bottom, below **▼ Autoscaling**

Select **Auto Scaling Groups.**

**Step 25: Amazon EC2 Auto Scaling**

Click **Create Auto Scaling Group.**

You should be redirected to the Choose launch template or configuration page.

**Step 26: Choose launch template or configuration**

**Auto Scaling group name:** CloudGlossaryASG

**Launch template:** Click **Create a launch template**

You should be redirected to the **Create launch template** page

### Create A Launch Template

_A launch template is like a reusable blueprint for EC2: it saves your instance settings so you can launch the same setup again later, share it with others, and maintain multiple versions as your configuration evolves_

**Step 27: Create launch template**

**Launch template name and description.**

**Launch template name _— required_:** CloudGlossaryLaunchTemplate_._

**Template version description:** Version One

**Auto Scaling guidance:** ✔

**Step 28: Launch template contents**

**▼ Application and OS Images (Amazon Machine Image)**

Click **Quick Start**

**Select Amazon Linux**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name:** CloudGlossary

**Step 29: Network Settings**

**Subnet**: Don’t include in launch template.

**Firewall (Security groups)**: Select existing security group_._

**Common security groups**: CloudGlossarySG

▶ **Storage (volumes)**: Leave default

▶ **Resource tags**: Leave default

**▼ Advanced details**: Scroll to the bottom and paste the code below.

```
#!/bin/bash
# 📦 Update system packages (works on both AL2 and AL2023)
sudo yum update -y
# 🐍 Install Python3 and pip (AL2023 compatible)
sudo yum install -y python3 python3-pip
# 🔧 Install Flask using pip3
sudo pip3 install flask
# 📁 Create a directory for the app
mkdir -p /home/ec2-user/hello-world
# 🐍 Create the Flask application
cat > /home/ec2-user/hello-world/app.py <<EOF
from flask import Flask
app = Flask(__name__)
@app.route('/')
def hello():
    return "Autoscaling! This is NO ABSTRACTION"
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
EOF
# ▶️ Run the Flask app in background
cd /home/ec2-user/hello-world
nohup sudo python3 app.py > app.log 2>&1 &
```

**Step 30:** ▶ **Summary**

Click **Create launch template**

✅**Green banner: Success**

Successfully created CloudGlossaryLaunchTemplate(lt-06c6e3d2e4be2314x).

Click **View launch templates**

**Step 31:** Navigate back to the **Choose launch template or configuration** page**.**

Click the refresh button next to **Select a launch template.**

Select **CloudGlossaryLaunchTemplate.**

**Version**: 1 ▼

Click **Next**

**Step 32: Choose instance launch options**

**Network**

**VPC:** defaultVPC

**Availability Zones and subnets**: Select all.

**Availability Zone distribution — new**: Select **Balanced best effort.**

Click **Next**

**Step 33: Integrate with other services — optional**

### Load Balancing

**_Load balancing_** _is like having a traffic cop for your application._

_When lots of users try to access your app at the same time, a_ **_load balancer_** _makes sure the traffic is spread out evenly across all your servers. This prevents any single server from being overwhelmed while others sit idle._

_It ensures:_

_Your app runs smoothly, even under heavy traffic._

_If one server fails, the load balancer sends traffic to the healthy servers so users don’t notice any issues._

_Think of it as distributing the workload to keep everything running efficiently!_

**Step 34:** **Load balancing**

**Select Load balancing options:** **A**ttach to a new load balancer.

**Load balancer type:** Application Load Balancer (HTTP, HTTPS)

**Load balancer name**: CloudGlossaryLB

**Load balancer scheme**: Internet-facing.

**Network mapping**: Leave default.

**Listeners and routing**

**Protocol**: HTTP

**Port**: 80

**Default routing (forward to)**: Create a target group.

**New target group name**: CloudGlossaryTargetGroup

**VPC Lattice integration options**

**Select VPC Lattice service to attach:** No VPC Lattice service

Leave everything as default.

Click **Next.**

**Step 35: Configure group size and scaling — optional.**

**Desired capacity: 2.**

**Scaling.**

**Min desired capacity: 1**

**Max desired capacity: 2**

**Automatic scaling — _optional_**: No scaling policies

**Instance maintenance policy:** No policy

**Additional capacity settings:** Default

**Additional settings:** Leave all unchecked

Click **Next**

**Step 36:** **Add notifications — _optional_**

Click **Next**_._

**Step 37**: **Add tags — _optional_**

Click **Next**_._

**Step 38: Review**

Click **Create Auto Scaling Group.**

If you performed the steps successfully, you should be looking at the **Auto Scaling groups page.**

**Step 39:** Navigate back to your **Instances page.**

You should have four **Running** instances.

**Step 40:** ✔ **Check** the instances we just created from the Auto Scaling Group.

**Instance state**: Terminate (delete) instance

**Terminate (delete) instance?** : Terminate (delete)

✅**Green banner:** Successfully initiated termination (deletion) of i-0f95564236cf29x76,i-0978c29d74cc4x761

💡**Verification:** As soon as the instances are **Terminated**, your Auto Scaling group will automatically launch new instances.

**Step 41: Instance State: Running**

When this instance is in **Running** state, click on the **Instance ID** of the newly launched instance.

Copy the **Public IPv4 address,** and paste it into your browser.

> **_⚠️_**_Make sure it begins with_ **_http:// (_**_Port 80) and not_ **_https://_** _(Port 443). You will received_ **_ERR_CONNECTION_TIMED_OUT_** _if it begins with_ **_https://_** _because the Security group and the app associated with your instance is open on Port_ **_80 (HTTP)_** _and not_ **_Port 443 (HTTPS)._**

**💡Verification:** You should see the following message displayed on your browser:

**Autoscaling! This is NO ABSTRACTION**

**Step 42:** Navigate to ▼ **Load Balancing.**

Select **Target Groups.**

Click **CloudGlossaryTargetGroup.**

**Step 43: CloudGlossaryTargetGroup**

Select **Targets**

**Registered targets**

Click **Register targets**

**Step 44: Register Targets**

✔ Select all Available Instances.

Ports for the selected instances: **80**

Click **Include as pending below.**

Click **Register pending targets.**

✅**Green banner:** 2 targets registered successfully to CloudGlossaryTargetGroup

Wait for all of them to reach **Healthy** status.

**Step 45:** Navigate to ▼ **Load Balancing.**

Click **Load Balancers.**

Click **CloudGlossaryLB**

Copy the **DNS name** and paste it into your browser

**💡Verification:** You should see the following message displayed on your browser:

**Hello World from EC2! This is NO ABSTRACTION**

Reload the Web Page.

**💡Verification:** You should see the following message displayed on your browser:

**AutoScaling! This is NO ABSTRACTION**

Reload the Web Page.

**💡Verification:** You should see the following message displayed on your browser:

**Hello World from EC2! This is NO ABSTRACTION**

Reload the Web Page.

> **_⚠️ You might not see it in this particular order, but your Load Balancer will attempt to distribute traffic equally from all the instances you registered as targets._**

Elastic Beanstalk Tutorial
--------------------------

_Elastic Beanstalk is a service that makes it easy to run your application in the cloud without worrying about the servers._

_You just upload your code, and Beanstalk automatically sets up everything you need, like servers (EC2), load balancers, scaling, and updates. It handles the heavy lifting so you can focus on your app, not the infrastructure._

**Step 46:** Navigate back to the **Management Console**

Click On **⁝⁝⁝ Services**

Select **Compute**

Click on **Elastic Beanstalk.**

**Step 47: Amazon Elastic Beanstalk**

Click **Create application**

**Step 48:** **Configure environment**

**Environment Tier:** Web server environment

**Step 49: Application information**

**Application name:** type **AbstractionApp**

**Step 50: Environment information**

**Environment name**: Leave default.

**Domain**: Leave blank for autogenerated value.

▼ **Environment description**: type _This is Abstraction._

**Step 51: Platform**

**Platform:** Python ▼

**Platform branch**: Python 3.14 running on 64bit Amazon Linux 2023.

**Platform version**: 4.9.1 (Recommended)

**Application Code**: Sample application

**Presets**: Single instance (free tier eligible)

Click **Next**

**Step 52: Configure server access**

**Service access**

**Service role:** Click **Create role**

**Step 53: Service Role:** _Create and use new service role_

**Step 54: Select trusted entity**

Select **AWS service**

**Use Case:** Elastic Beanstalk ▼

**Use Case:** Elastic Beanstalk — Environment

Click **Next**

**Step 55: Add permissions**

Click **Next**

**Step 56: Name, review, and create**

**Role name:** aws-elasticbeanstalk-service-role

Click **Create role**

✅**Green banner: Role aws-elasticbeanstalk-service-role created**

**Step 57:** Navigate back to **Configure server access**

**Service role**: aws-elasticbeanstalk-service-role

**EC2 instance profile:** AbstractionRole.

**EC2 key pair — optional:** CloudGlossary

Click **Next**

**Step 58: Set up networking, database, and tags — _optional_**

**VPC:** defaultVPC

**Public IP address:** ✔ Enable

**Instance Subnets:** ✔ Check all.

**Enable Database**

**Choose database subnets:** ✔ Select all.

**Database settings:** Leave default except for Username and Password

**Username:** admin

**Password:** AdminPassword#2026

**Availability:** High (Multi-AZ)

**Database deletion policy:** Delete.

Click **Next.**

**Step 59: Configure instance traffic and scaling — _optional_**

**▼ Instances**

**Root volume (boot device).**

**Root volume type**: General Purpose 3 (SSD) ▼

Scroll to **EC2 Security Groups**

Check **CloudGlossarySG**

**▼ Capacity**

**Auto scaling group**

**Environment type:** Load balanced.

**Min Instances: 2**

**Max Instances: 4**

**Fleet composition**: On-Demand instances

**Architecture:** x86_64

**Instance types**. Select **t2.small**

Leave the rest as default.

**Load balancer network settings**

**Load balancer subnets:** select All.

**Load Balancer Type:**

Select **Application Load Balancer.**

Select **Dedicated.**

**Listeners:** 80

**Processes**: default.

Leave the rest as default.

Click **Next**

**Step 60: Configure updates, monitoring, and logging — _optional_**

**▼ Monitoring**

**Health reporting:** Basic.

**▼ Managed platform updates**

**Managed updates:** _Uncheck._

Leave the rest as default.

Click **Next.**

**Step 61: Review**

Click **Create.**

🔁**Blue Banner:** Elastic Beanstalk is launching your environment. This will take a few minutes_._

> **_⚠️ Observe Elastic Beanstalk in action as it spins up your resources in the Events Section._**

✅**Green banner:** Environment successfully launched.**.**

**Step 62: Health:** ✅**Green**

Click on the **Domain** link

**💡Verification:** You should see the following message displayed on your browser:

### Welcome to Your Elastic Beanstalk Application

Congratulations! Your Python application is now running on your own dedicated environment in the AWS Cloud.

> **_⚠️ Scroll Further and analyze the page to familiarize yourself with Elastic Beanstalk capabilities and features_**

_If you want to see the Instances launched by Beanstalk, you can head over to your Instances page._

**Step 63:** Click on the **AbstractionApp** instance.

Copy the **Public IPv4 address,** and paste it into your browser.

> **_⚠️_**_Make sure it begins with_ **_http:// (_**_Port 80) and not_ **_https://_** _(Port 443). You will received_ **_ERR_CONNECTION_TIMED_OUT_** _if it begins with_ **_https://_** _because the Security group and the app associated with your instance is open on Port_ **_80 (HTTP)_** _and not_ **_Port 443 (HTTPS)._**

**💡Verification:** You should see the following message displayed on your browser:

### Welcome to Your Elastic Beanstalk Application

Congratulations! Your Python application is now running on your own dedicated environment in the AWS Cloud.

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _Elastic Beanstalk_ and **Terminate** your Application.
2.  Navigate to _EC2_ and **Terminate** your Instances.
3.  Navigate to _Security Groups_ and **Delete** your Security Groups.
4.  Navigate to _Auto Scaling Groups_ and **Delete** your Launch Template.
5.  Navigate to _Load balancers_ and **Delete** your Load Balancer.
6.  Navigate _Target Groups_ and **Delete** your Target Group.
7.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

**Building Tutorial Overview**
------------------------------

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KkXL28fLtfHiZef0mjn2NQ@2x.jpeg)

### EC2 Approach

_Low Abstraction_

1.  Manually configured security groups
2.  Manually set up auto scaling groups
3.  Manually configured load balancers
4.  Manually managed target groups
5.  Required deep understanding of AWS networking
6.  Multiple steps and configuration screens
7.  Direct control over every component

### Elastic Beanstalk Approach

_High Abstraction_

1.  Uploaded code and selected platform
2.  Beanstalk automatically created EC2 instances
3.  Beanstalk automatically configured load balancing
4.  Beanstalk automatically set up auto scaling
5.  Beanstalk automatically managed security groups
6.  Single deployment process
7.  Focus on application, not infrastructure

### **Key Observations**

1. **Time Investment**: EC2 required significantly more time and steps

2. **Complexity**: EC2 demanded understanding of multiple AWS services

3. **Error Potential**: More manual steps mean more opportunities for mistakes

4. **Maintenance:** EC2 requires ongoing manual maintenance and updates

5. **Speed to Market**: Beanstalk gets you running faster

We observed how Elastic Beanstalk is an _abstraction_ of EC2. With EC2, you are responsible for setting up everything yourself: launching servers, installing software like Python, and managing scaling, load balancing, and updates.

In contrast, Elastic Beanstalk simplified this process by letting you upload your code, and it automatically handled the underlying tasks for you.

Behind the scenes, Beanstalk still uses EC2 instances, but it abstracts away the complexity, so you can focus on building and running your application instead of managing infrastructure.

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Abstraction](https://ntombizakhona.medium.com/abstraction-d1335bec022e)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**27 November 2024**

