### Let’s Build
# Demonstrating Abstraction in the Cloud with Amazon Beanstalk

I know *(hope)* you’re eager to set something up, so in this practical, hands-on-tutorial, we will deploy a basic static site. 
This will demonstrate abstraction by contrasting Amazon Elastic Compute Cloud (EC2) and Amazon Beanstalk, which is considered an abstraction of EC2.

## Prerequisites
An AWS Administrative Account that has an Alias Account Configured (IAM)

## Add Additional Permissions to Your IAM Account
**Principle of Least Privilege:** It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run.


**Step 1:** Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.


**Step 2:** Select Security, Identity & Compliance on the left side of the drop down menu.


**Step 3:** Select IAM.
You should be redirected to the IAM Dashboard.


**Step 4:** On the left side of the screen expand Access management.


**Step 5:** Select Users.


**Step 6:** Select the IAM User.


**Step 7:** Select Permissions.

Click Add permissions.

Select Add Permissions.

You should be redirected to the Add permissions page.


**Step 8:** Select Add policies directly.


**Step 9:** On the Search bar type and check: AmazonEC2FullAccess.

On the Search bar type and check: AdministratorAccess-AWSElasticBeanstalk.

On the Search bar type and check: AmazonS3FullAccess

On the Search bar type and check: AWSCloudFormationFullAccess

On the Search bar type and check: AmazonRDSFullAccess.

On the Search bar type and check: CloudWatchFullAccess


**Step 10:** Click Next.

You should be redirected to the Review page.


**Step 11:** Click Add permissions.


**Step 12:** If you performed the steps successfully, you should see a green banner: 6 policies added.

Create an IAM EC2 Instance Profile for Elastic Beanstalk


**Step 13:** Below Users. Select Roles.


**Step 14:** Click Create role.


**Step 15:** You should be redirected to the Select trusted entity page.

Select AWS service.

Use Case: EC2.

Click Next.


**Step 16:** Add permissions. Select AdministratorAccessAWSElasticBeanstalk

Click Next.

You should be redirected to the Name, review, and create page.


**Step 17:** Role name: AbstractionRole

Click Create role.


**Step 18:** If you performed the steps successfully, you should see a green banner.

Click View role.

Build Using Your IAM Account


**Step 19:** Log out of your Administrative Account, and Sign in with your IAM Account.

Depending on how long ago you last logged in and your password policy, you might have to reset your password using your Administrative Account. Ignore 

***Steps 20.1 —20.8*** if you don’t have to reset your password.

***Step 20.1:*** Sign in with your Administrative Root User Account in order to reset your password.

***Step 20.2:*** Select Security, Identity & Compliance on the left side of the drop down menu.

***Step 20.3:*** Select IAM.
You should be redirected to the IAM Dashboard.

***Step 20.4:*** On the left side of the screen expand Access management.

***Step 20.5:*** Select Users.

***Step 20.6:*** Select the IAM User.

***Step 20.7:*** Select Security credentials.

Click Manage console access.

Select Reset password.

Under Console password, Select Custom password.

Click Reset password.

If you performed the steps successfully, you should see a green banner:

You have successfully enabled the user’s new password.

This is the only time you can view this password. After you close this window, if the password is lost, you must create a new one.

***Step 20.8:*** Click Close.


## Elastic Compute Cloud Tutorial
Before you proceed, make sure that you’re signed in with your IAM User Account, and that you’re in the N.Virginia region (us-east-1).

### Launch EC2 Instances


**Step 21:** Select Compute on the left side of the drop down menu.


**Step 22:** Select EC2.


**Step 23:** Click Launch instance.


**Step 24:** Under Name and Tags, Name your instance NoAbstraction.


**Step 25:** Under Application and OS Images (Amazon Machine Image).

Click Quick Start.

Select Amazon Linux.

Under Amazon Machine Image (AMI), select Amazon Linux 2 AMI (HVM) (Free Tier eligible).

Under Architecture, select 64-bit (x86).


**Step 26:** Under Instance type, select t2.micro (Free tier eligible).

**Step 27** Under Key pair (login), select Create new key pair.

You should be redirected to the Create key pair pop up.

Key pair name: AbstractionKey.

Key pair type: RSA

Private key file format: .pem

Click Create key pair.

Save it on your local device.


**Step 28:** Under Network settings.

Click Edit.

Navigate to Firewall (security groups).

Select Create security group.

Security group name — required: type in MySecurityGroup.

Description — required: type in Security Group for My Web Servers.

Under Inbound Security Group Rules.

Click Add Security group rule.

Type: Select HTTP.

Source Type: Select Anywhere.


**Step 29:** Configure storage: leave as default.


**Step 30:** Advanced details: leave as default, scroll to the bottom, but, don’t scroll too fast, make a note of all the features you can manually configure until you reach User data — optional.

Paste this
```
#!/bin/bash
# Update and install dependencies
sudo yum update -y
sudo yum install -y python3
sudo pip3 install flask

# Create a directory for the app
mkdir /home/ec2-user/hello-world

# Create the Flask application
cat > /home/ec2-user/hello-world/app.py <<EOF
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello World from EC2! This is NO ABSTRACTION"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
EOF

# Run the Flask app
nohup python3 /home/ec2-user/hello-world/app.py
```

**Step 31:** At the right of the page Summary.

Number of instances: 2.

Click Launch instance.

If you performed the steps successfully, you should see a green banner:
Success.

Successfully initiated launch of instances.


**Step 32:** At the bottom of the page, click View all instances.
You should be redirected to the instances dashboard. Make sure your instances are in the Running state.


**Step 33:** Click on the Instance ID of the first instance.


**Step 34:** Copy the Public IPv4 address, and paste it into your browser.
Note: Make sure it begins with http:// (Port 80) and not https:// (Port 443). You will received ERR_CONNECTION_TIMED_OUT if it begins with https:// because the Security group associated with your instance is open on Port 80 (HTTP) and not Port 443 (HTTPS).


**Step 35:** Congratulations! If you performed the steps successfully, you should see the following message:

Hello World from EC2! This is NO ABSTRACTION

### Configure AutoScaling
Autoscaling is like having extra help ready to step in when needed.
In simple terms, autoscaling is a feature that automatically adjusts the number of servers (instances) your application uses based on how much traffic or work it’s handling.

If your app gets busy (like during a sale or a viral moment), autoscaling adds more servers to handle the load.

If things get quiet, autoscaling removes extra servers to save money.
This way, your application always has just the right amount of resources — never too many (wasting money) or too few (causing slowdowns or crashes).


**Step 36:** Navigate back to the Console. On the far right of the page, at the bottom, below Autoscaling, select Auto Scaling Groups.


**Step 37:** Click Create Auto Scaling Group.

You should be redirected to the Choose launch template or configuration page.
Name. 

Auto Scaling group name: AutoScalingGroup.

Launch template: Launch template: Click Create a launch template

You should be redirected to the Create launch template page.

Create launch template

Launch template name and description.

Launch template name — required: MyLaunchTemplate.

Template version description: Version 1

Auto Scaling guidance: Unchecked.

Launch template contents

Application and OS Images (Amazon Machine Image)

Select Currently in use.

Instance Type: t3.micro.

Key pair (login): AbstractionKey.

Network Settings

Subnet: Don’t include in launch template.

Firewall (Security groups): Select existing security group.

Common security groups: MySecurityGroup.

Storage (volumes): leave default.

Resource tags: leave default.

Advanced details: Scroll to the bottom and paste the code below.
```
#!/bin/bash

# Update and install dependencies
sudo yum update -y
sudo yum install -y python3
sudo pip3 install flask

# Create a directory for the app
mkdir /home/ec2-user/hello-world

# Create the Flask application
cat > /home/ec2-user/hello-world/app.py <<EOF
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Autoscaling: This is NO ABSTRACTION"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
EOF

# Run the Flask app
nohup python3 /home/ec2-user/hello-world/app.py &
```
*Summary*: click Create launch template.

If you performed the steps successfully, you should see a green banner:
Success.

Successfully created MyLaunchTemplate.

Click View launch templates.

Navigate back to the Choose launch template or configuration page.

Click the refresh button next to Select a launch template.

Select MyLaunchTemplate.

Click Next.


**Step 38:** Network: ensure defaultVPC is selected.

Availability Zones and subnets: select all.

Availability Zone distribution — new: select Balanced best effort.

Click Next.


### Load balancing
Load balancing is like having a traffic cop for your application.
When lots of users try to access your app at the same time, a load balancer makes sure the traffic is spread out evenly across all your servers. This prevents any single server from being overwhelmed while others sit idle.

It ensures:
Your app runs smoothly, even under heavy traffic.
If one server fails, the load balancer sends traffic to the healthy servers so users don’t notice any issues.

Think of it as distributing the workload to keep everything running efficiently!

### Attach to a new load balancer
**Step 39:** Load balancing: select Attach to a new loadbalancer.

Load balancer type: select Application Load Balancer (HTTP, HTTPS)

Load balancer name: MyLoadBalancer.

Load balancer scheme: Internet-facing.

Network mapping: Leave default.

Listeners and routing:

Protocol: HTTP

Port: 80

Default routing (forward to): Create a target group.

New target group name: MyTargetGroup.

VPC Lattice integration options: No VPC Lattic service.

Leave everything as default.

Click Next.


**Step 40:** Configure group size and scaling — optional.

Desired capacity: 2.

Scaling.

Min desired capacity: 1

Max desired capacity: 2

Automatic scaling — optional: No scaling policies.

Instance maintenance policy: No policy.

Additional capacity settings: Default.

Additional settings: Leave all unchecked.

Click Next.


**Step 41:** Add notifications — optional: click Next.


**Step 42:** Add tags — optional: click Next.


**Step 43:** Review: Click Create Auto Scaling Group.

If you performed the steps successfully, you should be looking at the Auto Scaling groups page.

Navigate back to your instances page.

You should have three running instances.


**Step 44:** Check the instance we just created from the Auto Scaling Group.

Instance state: Terminate (delete) instance.

Terminate (delete) instance? : click Terminate (delete)

As soon as the instance is Terminated, your Auto Scaling group will automatically launch a new instance.

When this instance is in running state, click on the Instance ID of the newly launched instance.

Copy the Public IPv4 address, and paste it into your browser.

Note: Make sure it begins with http:// (Port 80) and not https:// (Port 443). You will received ERR_CONNECTION_TIMED_OUT if it begins with https:// because the Security group associated with your instance is open on Port 80 (HTTP) and not Port 443 (HTTPS).

If you performed the steps successfully, you should see the following message:

Autoscaling: This is NO ABSTRACTION


**Step 45:** Navigate to Load Balancing.

Select Target Groups.

Click MyTargetGroup.

Targets.

Registered Targets.

Click Register Targets.

Select all Available Instances.

Click Include as pending below.

Click Register pending targets.

Wait for all of them to reach Healthy status.


**Step 46:** Navigate to Load Balancing.

Click Load Balancers.

Click MyLoadBalancer.

Copy the DNS name and paste it into your browse, you should see (Instance One):

Hello World from EC2: This is NO ABSTRACTION

Reload the Web Page, you should see (Instance Two):
Hello World from EC2: This is NO ABSTRACTION

Reload the Web Page, you should see (Instance Three):
Autoscaling: This is NO ABSTRACTION

You might not see it in this particular order, but your Load Balancer will attempt to distribute traffic equally from all the instances you registered as targets.


## Elastic Beanstalk Tutorial
Elastic Beanstalk is a service that makes it easy to run your application in the cloud without worrying about the servers.

You just upload your code, and Beanstalk automatically sets up everything you need, like servers (EC2), load balancers, scaling, and updates. It handles the heavy lifting so you can focus on your app, not the infrastructure.


**Step 47:** Navigate back to the Amazon Management Console.


**Step 48:** Click On Services.


**Step 49:** Select Compute.


**Step 50:** Click on Elastic Beanstalk.


**Step 51:** Under Get Started, click Create Application.
You should be redirected to the Configure environment page.


**Step 52:** Environment Tier: select Web server environment.
Application information. 

Application name: type Abstraction.

Environment name: leave default.

Domain: choose available domain name.

Environment description: type This is Abstraction.

Platform. Platform type. Select Managed platform.

Platform. Choose a platform: Python

Platform branch: Python 3.12 running on 64bit Amazon Linux 2023.

Platform version: 4.3.1

Application Code: Sample application

Presets: Single instance (free tier eligible)

Click Next.

You should be redirected to the Configure server access page.


**Step 53:** Service Role: Create and use new service role

Service role name: aws-elasticbeanstalk-service-role

EC2 key pair: AbstractionKey

EC2 instance profile: AbstractionRole.

Click Next.

You should be redirected to the Set up networking, database, and tags — optional page.


**Step 54:**
Virtual Private Cloud

Select defaultVPC.

Instance settings

Public IP address. Check Activated.

Instance Subnets: Check all.

Database
Choose database subnets: Select all.

Enable database,

Restore a snapshot — optional

Snapshot: None.

Database settings: Leave default excpet for Username and Password

Username: admin
Password: AdminPassword#2024

Database deletion policy: Delete.

Click Next.

You should be redirected to the Configure instance traffic and scaling — optional page.


**Step 55:**
Instances
Root volume (boot device). Root volume type: General Purpose 3 (SSD)

Scroll to EC2 Security Groups. Check MySecurityGroup.

Capacity
Auto scaling group.

Environment type: Load balanced.

Instances
2 Min
4 Max

Fleet composition: On-Demand Instances.

Architecture: x86_64

Instance types. Select t2.micro

Leave the rest as default.


**Step 56:**
Load balancer network settings
Load balancer subnets: select All.

Load Balancer Type:
Select Application Load Balancer.
Select Dedicated.

Listeners: 80

Processes: default.

Leave the rest as default.

Click Next.

You should be redirected to the Configure updates, monitoring, and logging — optional page.


**Step 57:**
Monitoring

Health reporting: Basic.

Managed platform updates

Activated: Uncheck.

Leave the rest as default.

Click Next.


**Step 58:** Click Submit.

Blue Banner: Elastic Beanstalk is launching your environment. This will take a few minutes.

Observe Elastic Beanstalk in action as it spins up your resources.

If you performed the steps successfully, you should eventually see a green banner:

Environment successfully launched.

And your Health status should move from Grey to Green.


**Step 59:** Click on the Domain.

Congratulations
Your first AWS Elastic Beanstalk Python Application is now running on your own dedicated environment in the AWS Cloud

This environment is launched with Elastic Beanstalk Python Platform
If you want to see the Instances launched by Beanstalk, you can head over to your Instances page.


**Step 60:** Click on the Abstraction instance.
Copy the Public IPv4 address, and paste it into your browser.

Note: Make sure it begins with http:// (Port 80) and not https:// (Port 443). You will received ERR_CONNECTION_TIMED_OUT if it begins with https:// because the Security group associated with your instance is open on Port 80 (HTTP) and not Port 443 (HTTPS).

You should see the same:

Congratulations
Your first AWS Elastic Beanstalk Python Application is now running on your own dedicated environment in the AWS Cloud

This environment is launched with Elastic Beanstalk Python Platform
Important


### Clean Up Resources
*Don’t get a Bill Shock by leaving unnecessary resources running.*

Navigate to Elastic Beanstalk and Delete your Application.

Navigate to EC2 and Terminate your Instances.

Navigate to Security Groups and Delete your Security Groups.

Navigate to Auto Scaling Groups and Delete your Launch Template.

Navigate to Load balancers and Delete your Load Balancer.

Navigate Target Groups and Delete your Target Group.

Login with your Root User Account, and Remove All Permissions Associated with your IAM Account.

### End of Tutorial.


# Building Tutorial Overview
We observed how Elastic Beanstalk is an abstraction of EC2. With EC2, you are responsible for setting up everything yourself: launching servers, installing software like Python, and managing scaling, load balancing, and updates.

In contrast, Elastic Beanstalk simplified this process by letting you upload your code, and it automatically handled the underlying tasks for you.
Behind the scenes, Beanstalk still uses EC2 instances, but it abstracts away the complexity, so you can focus on building and running your application instead of managing infrastructure.
