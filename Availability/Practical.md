### 🏗️ Let’s Build

Demonstrating Availability By Building A Highly Available Application On AWS
----------------------------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll provision:

1.  Provision A Virtual Private Cloud (VPC) spanning **two Availability Zones**
2.  An **Application Load Balancer (ALB)** distributing traffic
3.  An **Auto Scaling Group** of EC2 instances that self-heals when an instance fails
4.  A basic web page served from each instance so you can see failover in action

_This will demonstrate high_ **_Availability_** _in the Cloud._

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**Abstraction**](https://medium.com/@ntombizakhona/abstraction-d1335bec022e)
4.  [**Apache HTTP**](https://medium.com/apache-http-8404a1b11d26)
5.  [**Auto Scaling**](https://medium.com/auto-scaling-ad945ba63939)

### Add Additional Permissions to Your IAM Account

_Principle of Least Privilege: It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your **Administrative Account** in order to grant permissions to your active _Development IAM Account._

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **IAM users**

**Step 05: IAM users**

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

**AmazonVPCFullAccess**

**ElasticLoadBalancingFullAccess**

**AutoScalingFullAccess**

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 4** policies added to CloudGlossary

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

### Create a VPC With Two Public Subnets

_A VPC is your isolated network in AWS. We need subnets in_ **_two different Availability Zones_** _so that if one data-center zone goes down, the other keeps serving traffic_

**_Why two AZs?_** _Each Availability Zone is a physically separate data center (or cluster of data centers). Spreading across two means a failure in one zone does not take your entire application offline._

**Step 09: Navigate to the VPC Console**

Click **Create VPC**

**Step 10: Create VPC
Resource to create:** VPC and more

*   **Name tag auto-generation:** `availability`
*   **IPv4 CIDR block:** `10.0.0.0/16`
*   **IPv6 CIDR block:** `No IPv6 CIDR block`
*   **Tenancy:** `default`
*   **Number of Availability Zones:** `2`
*   **Number of public subnets:** `2`
*   **Number of private subnets:** `0`
*   **NAT gateways ($) — _updated:_** `None`
*   **VPC endpoints:** `None`
*   **DNS Options:** `Both checked`

Click **Create VPC**

**Step 11:** Click **View VPC**

**Step 12:** On the left side of the screen under ▼ **Security**

Click **Security groups**

**Step 13: Security groups**

Click **Create security group**

*   **Security group name:** `availabilitySG`
*   **Description:** Allow HTTP traffic
*   **VPC:** Select `availability-vpc`

**Inbound rules**

Click **Add rule**

```
| Type | Protocol | Port Range | Source                    |
|------|----------|------------|---------------------------|
| HTTP | TCP      | 80         | 0.0.0.0/0 (Anywhere IPv4) |
```

Click **Add rule**

```
| Type | Protocol | Port Range | Source               |
|------|----------|------------|----------------------|
| HTTP | TCP      | 80         | ::/0 (Anywhere IPv6) |
```

Click **Create Security group**

✅**Green banner: Security group was created successfully**

### Enable Auto-Assign Public IP on Both Subnets

⚠️ **This step is critical.** Without public IPs, your EC2 instances cannot reach the internet to download Apache during boot. The User Data script will fail silently, Apache will never start, and the ALB health checks will time out,resulting in unhealthy targets and a 502 Bad Gateway error.

**Step 14:** On the left side of the screen under ▼ **Virtual private cloud**

Click **Subnets**

**Step 15:** Select `availability-subnet-public1-<az>`

Click **Actions** ▼ → **Edit subnet settings**.

**Step 16: Edit subnet settings**

Check ✔ **Enable auto-assign public IPv4 address**

Click **Save**.

✅**Green banner: You have successfully changed subnet settings:**

*   Enable auto-assign public IPv4 address

**Step 17:** Select `availability-subnet-public2-<az>`

Click **Actions** ▼ → **Edit subnet settings**.

**Step 18: Edit subnet settings**

Check ✔ **Enable auto-assign public IPv4 address**

Click **Save**.

✅**Green banner: You have successfully changed subnet settings:**

*   Enable auto-assign public IPv4 address

### Create A Launch Template

**Step 19: Navigate to the EC2 Dashboard**

On the left side of the screen under ▼ **Instances**

Click **Launch Template**

**Step 20:** Click **Create launch template**

**Step 21: Create launch template**

**Launch template name and description.**

**Launch template name _— required_:** AvailabilityTemplate

**Template version description:** Version One

**Auto Scaling guidance:** ✔

**Step 22: Launch template contents**

**▼ Application and OS Images (Amazon Machine Image)**

Click **Quick Start**

**Select Amazon Linux**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name:** CloudGlossary

**Step 23: Network Settings**

**Subnet**: Don’t include in launch template.

**Firewall (Security groups)**: Select existing security group_._

**Common security groups**: availabilitySG

▶ **Storage (volumes)**: Leave default

▶ **Resource tags**: Leave default

**▼ Advanced details**: Scroll to the bottom and paste the code below **User data _— optional:_**

```
#!/bin/bash
set -euo pipefail
dnf update -y
dnf install -y httpd
# IMDSv2-compatible metadata fetch
TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
INSTANCE_ID=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/instance-id)
AZ=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/placement/availability-zone)
cat <<EOF > /var/www/html/index.html
<!DOCTYPE html>
<html lang="en">
<head><meta charset="UTF-8"><title>HA Demo</title>
<style>
  body { font-family: Arial, sans-serif; text-align: center; padding: 50px;
         background: #f0f4f8; color: #1a202c; }
  .card { background: white; border-radius: 12px; padding: 40px;
          max-width: 500px; margin: auto; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
  h1 { color: #2b6cb0; }
  .info { font-size: 1.2em; margin: 10px 0; }
  .az { color: #38a169; font-weight: bold; }
</style>
</head>
<body>
  <div class="card">
    <h1>High Availability Demo</h1>
    <p class="info">Instance ID: <strong>${INSTANCE_ID}</strong></p>
    <p class="info">Availability Zone: <span class="az">${AZ}</span></p>
    <p>Refresh this page repeatedly to see the load balancer route you
       to different instances in different Availability Zones.</p>
  </div>
</body>
</html>
EOF
systemctl enable --now httpd
```

> **What does the User Data script do?** It installs the Apache web server and creates a simple HTML page that displays the instance’s ID and Availability Zone. This lets you _see_ the load balancer distributing traffic.

**Step 24:** ▶ **Summary**

Click **Create launch template**

✅**Green banner: Success**

Click **View launch templates**

### Create an Application Load Balancer (ALB)

_The ALB is the single entry point for users. It distributes requests across healthy instances._

**Step 25:** On the left side of the screen under ▼ **Load Balancing**

Click **Load Balancers**

**Step 26: Load balancers**

Click **Create Load balancer** ▼

Select **Create Application Load Balancer**

**Step 27: Create Application Load Balancer**

*   **Load balancer:** `availabilityALB`
*   **Scheme:** Internet-facing
*   **Load balancer IP address type:** IPv4
*   **VPC:** `availability-vpc`
*   **Availability Zones and subnets:** Check both Availability Zones and select the corresponding public subnets.
*   **Security group:** Select `CloudGlossarySG` _(remove the default SG)._

**Listeners and routing**

*   ▼ Listener **HTTP:80**
*   Routing action: **Forward to target groups**
*   Click **Create target group** (a new tab opens):

**Step 28: Create target group**

*   **Target type:** Instances
*   **Target group name:** `availabilityTG`
*   **Protocol:** HTTP
*   **Port:** 80
*   **IP address type:** IPv4
*   **VPC:** `availability-vpc`
*   **Protocol version:** HTTP1

**Health checks**

*   **Health check protocol:** `HTTP`▼
*   **Health check path:** `/`

Click **Next** → do **not** register targets manually (Auto Scaling will do this) → **Create target group**.

✅**Green banner:** Successfully created the target group: **availabilityTG**. Anomaly detection is automatically applied to all registered targets. Results can be viewed in the **Targets** tab.

**Step 29: Back on the ALB tab**

Refresh the target group dropdown and select `availabiltyTG`.

Click **Create load balancer**

✅**Green banner: Successfully created load balancer: availabilityALB**

⚠️Wait for the ALB state to become **Active** (1–2 minutes).

**Step 30:** Copy the **DNS name.** You will use it to test.

### Create an Auto Scaling Group

**Step 31:** On the left side of the screen under ▼ **Auto Scaling**

Click on **Auto Scaling Groups**

**Step 32:** Click **Create Auto Scaling group**

*   **Auto Scaling Group name:** `availabilityASG`
*   **Launch template:** `AvailabilityTemplate`
*   **Version**: 1 ▼

Click **Next**

**Step 33: Choose instance launch options**

*   **VPC:** `availability-vpc`
*   **Availability Zones and subnets:** `Select both`
*   **Availability Zone distribution — _new_**: Select **Balanced best effort.**

Click **Next**

**Step 34: Integrate with other services — _optional_**

*   **Select Load balancing options:** `Attach to an existing load balancer`
*   **Select the load balancers to attach:** `Choose from your load balancer target groups`
*   **Existing load balancer target groups:** `availabilityTG`
*   **Additional health check types— _optional_:** ✔`Turn on Elastic Load Balancing health checks`

Click **Next**

**Step 35: Configure group size and scaling — _optional_**

*   **Desired capacity:** `2`
*   **Min desired capacity:** `2`
*   **Max desired capacity:** `4`

Click **Next**

**Step 36: Add notifications — _optional_**

Click **Next**

**Step 37: Add tags — _optional_**

Click **Next**

**Step 38: Review**

Click **Create Auto Scaling group**

✅**Green banner:** availabilityASG created successfully

### Test High Availability

**Step 39: Verify Load Balancing**

Open a browser and navigate to the ALB DNS name:

```
http://ha-demo-alb-XXXXXXXXX.<region>.elb.amazonaws.com
```

You should see the **High Availability Demo** page showing an Instance ID and Availability Zone.

**💡Refresh the page several times.** You will see the Instance ID and AZ change as the load balancer routes you to different instances.

### Simulate a Failure

Now let’s prove that the system self-heals:

**Step 40:** Go to the **EC2 Console** → **Instances**.

*   Select one of the `availabilityASG` instances.
*   Click **Instance state** → **Terminate instance** → Confirm.
*   **Immediately refresh** the ALB URL in your browser. After a brief moment, all requests will be served by the **surviving instance** in the other AZ .

No downtime for the end user.

*   Within 1–2 minutes, check the **Auto Scaling Group** activity tab. You will see that a **new replacement instance** has been launched automatically.
*   Once the new instance passes its health check, refreshing the browser will again show **two different instances** across two AZs.

**Congratulations. You just witnessed high availability in action.**

_The load balancer detected the failed instance, stopped sending it traffic, and the Auto Scaling Group replaced it automatically._

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _AutoScaling_ and **Delete** The Auto Scaling Group
2.  Navigate to _Load Balancing_ and **Delete** The Load Balancer
3.  Navigate to _Load Balancing_ and **Delete** The Target Group
4.  Navigate to _Instances_ and **Delete** The Launch Template
5.  Navigate to _Network and Security_ and **Delete** The Security Group
6.  Navigate to _VPC Dashboard_ and **Delete** The VPC
7.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                              Internet
                                  │
                                  ▼
                    ┌───────────────────────────┐
                    │ Application Load Balancer │
                    │      (availabilityALB)    │
                    └─────────────┬─────────────┘
                                  │
               ┌──────────────────┴──────────────────┐
               │                                     │
               ▼                                     ▼
      ┌─────────────────┐                  ┌─────────────────┐
      │ Availability    │                  │ Availability    │
      │ Zone A          │                  │ Zone B          │
      │ Public Subnet A │                  │ Public Subnet B │
      └────────┬────────┘                  └────────┬────────┘
               │                                     │
               ▼                                     ▼
      ┌─────────────────┐                  ┌─────────────────┐
      │ EC2 Instance    │                  │ EC2 Instance    │
      │ Apache Installed│                  │ Apache Installed│
      │ Web Page Hosted │                  │ Web Page Hosted │
      └────────┬────────┘                  └────────┬────────┘
               │                                    │
               └──────────────┬─────────────────────┘
                              │
                              ▼
                    ┌────────────────────┐
                    │ Auto Scaling Group │
                    │   (availabilityASG)│
                    │ Min: 2 | Max: 4    │
                    └────────────────────┘
              Entire Infrastructure Inside:
        ┌─────────────────────────────────────────┐
        │ Virtual Private Cloud (availability-vpc)│
        │ CIDR: 10.0.0.0/16                       │
        └─────────────────────────────────────────┘
```

### **What Was Built**

A high-availability web application on AWS, spanning two physically separate Availability Zones so that a failure in one data center cannot take the application offline.

### **Key Components And Their Roles**

The VPC (`10.0.0.0/16`) is the isolated network container. Inside it, two public subnets live in two different Availability Zones, AZ 1 and AZ 2,each with its own EC2 instance running Apache HTTP.

The Application Load Balancer sits in front of everything. It’s the single public entry point, distributing incoming HTTP traffic across both instances. Because it spans both AZs, it can route around a failed instance automatically.

The Auto Scaling Group keeps two instances running at all times (min 2, max 4). If an instance is terminated whether manually or due to a real failure the ASG detects it and launches a replacement, automatically registering it with the target group.

The Target Group (`availabilityTG`) is the glue between the ALB and the EC2 instances. It runs HTTP health checks on each instance and tells the ALB which ones are healthy enough to receive traffic.

The Security Group allows inbound TCP port 80 from anywhere (IPv4 and IPv6), while blocking everything else.

The Launch Template defines exactly how new instances should be created: AMI, instance type, security group, and a user-data script that installs Apache and serves a page showing the instance ID and AZ.

### **How High Availability Actually Works Here**

When one instance fails, the ALB stops sending it traffic within seconds (as soon as health checks fail). The ASG then launches a fresh instance using the launch template, and once it passes its health check, the ALB adds it back into rotation.

_All without any manual intervention or user-facing downtime._


# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Availability](https://medium.com/@ntombizakhona/availability-300d472ddece)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**03 May 2026**


