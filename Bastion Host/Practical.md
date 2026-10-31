### 🏗️ Let’s Build

Launching A Bastion Host On AWS
-------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Launch A Bastion Host On AWS Using**

_This will demonstrate The Concept of Bastion Hosts._

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**Abstraction**](https://medium.com/abstraction-d1335bec022e)

### Add Additional Permissions to Your IAM Account

_Principle of Least Privilege: It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access Management**

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

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 1** policy added

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

### Launch the Bastion Host

**Step 09:** Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Step 10: Dashboard**

Click **Launch instance.**

**Step 11: Launch an instance**

Under **Name and Tags.**

**Name:** `**bastion-host**`

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.18 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name:** CloudGlossary

**Step 12:** ▼ **Network settings**

Click **Edit**

Select a **subnet**

> **_⚠️_** _Make sure_ **_Auto-assign public IP_** _is_ `**_Enable_**`

**Firewall (security groups)**: `**Create security group**`

**Name:** `**bastionSG**`

✔ **Allow SSH traffic from:** ▼ `**My IP**`

> **_💡My IP_** _restricts SSH to your current connection only. Never set the source to_ `_0.0.0.0/0_` _(anywhere), which would open the gate to the whole internet._

▶ **Storage (volumes)**: Leave default

▶ **Resource tags**: Leave default

▶ **Advanced details**: Leave default

**Step 13:** ▶ **Summary**

Click **Launch instance**

✅**Green banner: Success**

**Step 14:** Click **View all instances**

### Launch the Private Server

**Step 15: EC2 Dashboard**

Click **Launch instances**

**Step 16: Launch an instance**

Under **Name and Tags.**

**Name:** `**private-server**`

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.18 AMI (Free Tier eligible)**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

▼ **Key pair (login)**

**Key pair name:** CloudGlossary

**Step 17:** ▼ **Network settings**

Click **Edit**

> **_⚠️_** _Make sure_ **_Auto-assign public IP_** _is_ `**_Disable_**`

**Firewall (security groups)**: `**Create security group**`

**Name:** `**privateSG**`

**Inbound Security Group Rules:** Click **Remove**

▶ **Storage (volumes)**: Leave default

▶ **Resource tags**: Leave default

▶ **Advanced details**: Leave default

**Step 18:** ▶ **Summary**

Click **Launch instance**

✅**Green banner: Success**

**Step 19:** Click **View all instances**

### ⚠️ Confirm The Bastion’s Subnet Has A Route To The Internet

**Step 20:** Select `**bastion-host**`, open the **Networking** tab, and click the **Subnet ID**.

On the subnet page, open the **Route table** tab and look for a route with **Destination** `0.0.0.0/0` and **Target** `igw-...`.

The target is an **internet gateway** (the VPC component that connects it to the internet). The default VPC comes with this route, so it's usually already there. Without it, nothing on the internet can reach the bastion, and SSH times out.

**Step 21: If the route is missing**

Open the **VPC** console and choose **Internet gateways**. If no gateway shows **State = Attached** for the default VPC, choose **Create internet gateway**, name it `bastion-igw`, and choose **Create internet gateway**.

Then choose **Actions → Attach to VPC**, select the default VPC, and choose **Attach internet gateway**.

Choose **Route tables** and select the route table shown on the subnet’s **Route table** tab. On the **Routes** tab, choose **Edit routes → Add route**. Set **Destination** to `0.0.0.0/0`, set **Target** to **Internet Gateway**, select your gateway (`igw-...`), and choose **Save changes**.

> **_💡This_** `**_0.0.0.0/0_**` **_is a route, not a firewall rule. It lets traffic travel between the subnet and the internet, but_** `**_bastion-sg_**` **_still decides who is allowed to connect._**

### Allow SSH Only From the Bastion

**Step 22: EC2 Dashboard**

▼ **Network & Security**

Click **Security Groups**

**Step 23: Security Groups**

Select `**privateSG**`

Select **Inbound rules**

Click `**Edit** **inbound rules**`

**Step 24: Edit inbound rules**

Click **Add rule**

Type: `**SSH**`

Source: `**bastionSG**`

Click **Save rules**

✅**Green banner: Inbound security group rules successfully modified on security group**

> **_💡Referencing the bastion’s security group as the source is more robust than a fixed IP. It keeps working even if the bastion’s private IP changes._**

### Connect Through the Bastion (the “Jump”)

**Step 25: EC2 Dashboard**

Select `**bastion-host**`

Click **Connect**

**Step 26: Connect to Linux instance**

Select **In SSH Client**

**Step 27: How to connect**

Open a terminal on your laptop and connect to the bastion using your key.

> _1. Open an SSH client_
> 
> _2. Locate or download your private key file_
> 
> _3. Ensure your key is not publicly viewable_
> 
> `**_chmod 400 "CloudGlossary.pem"_**`
> 
> _4. Connect to your instance using its Public DNS_
> 
> `**_ssh -A -i "CloudGlossary.pem" ec2-user@_<YOUR_BASTION_PUBLIC_IP>_.compute-1.amazonaws.com_**`

**💡The** `**-A**` **flag forwards your key securely so you can jump onward without copying the key onto the bastion**

**Step 28:** Once you’re on the bastion, jump to the private server using its **private IP**:

```
ssh ec2-user@<PRIVATE_SERVER_PRIVATE_IP>
```

**Congratulations.** You’re now on the private server. Reached entirely through the guarded gate.

### Verify The Server Is Sealed Off

> **_💡Confirm the private server can’t be reached directly._**

**Step 29: EC2 Dashboard**

Check that `**private-server**` has **no Public IPv4 address**.

**Step 30: On Your Laptop**

From your laptop (not the bastion), try to SSH directly to the private server’s private IP.

It should fail or time out, proving the only way in is through the bastion.

**_You now have a working bastion host: one guarded, logged, IP-restricted entry point protecting a private server._**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _EC2_ and **Terminate The Instances.**
2.  Navigate to _EC2_ and **Delete The Security Groups**
3.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                          +---------------------------+
                          |     IAM User Account      |
                          |    AmazonEC2FullAccess    |
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |     Your Admin Laptop     |
                          |   SSH from My IP only     |
                          +-------------+-------------+
                                        |  SSH (port 22)
                                        v
   ================================ Default VPC ==============================
   |                                                                         |
   |   +---------------------------+                                         |
   |   |   PUBLIC SUBNET           |                                         |
   |   |  +---------------------+  |                                         |
   |   |  |    Bastion Host     |  |                                         |
   |   |  |   (bastion-host)    |  |                                         |
   |   |  |  Public IP + SSH    |  |                                         |
   |   |  |  SG: bastion-sg     |  |                                         |
   |   |  +----------+----------+  |                                         |
   |   +-------------|-------------+                                         |
   |                 |  SSH (only from bastion-sg)                           |
   |                 v                                                       |
   |   +---------------------------+                                         |
   |   |   PRIVATE SUBNET          |                                         |
   |   |  +---------------------+  |                                         |
   |   |  |   Private Server    |  |                                         |
   |   |  |  (private-server)   |  |                                         |
   |   |  |  NO public IP       |  |                                         |
   |   |  |  SG: private-sg     |  |                                         |
   |   |  +---------------------+  |                                         |
   |   +---------------------------+                                         |
   ==========================================================================
    Access Flow:
   -----------------------------------------------------------------------
   Admin  -->  SSH to Bastion (public)  -->  Jump/SSH to Private Server
   (My IP)      guarded front gate            reachable only via bastion
   -----------------------------------------------------------------------
```

This walkthrough demonstrates one of AWS’s most important security patterns: a **single, guarded entry point** into an otherwise-private network.

### **What Was Built**

A bastion host (`bastion-host`) running in a public subnet with SSH open only to your own IP, and a private server (`private-server`) in a private subnet with no public IP. Security groups ensure the private server accepts SSH _only_ from the bastion.

### **The Key Demonstration:**

You connect to the bastion from your laptop, then “jump” from the bastion to the private server. The private server is never exposed to the internet, yet you can still administer it.

Every path in goes through the guarded gate.

### **Reduced Attack Surface**

Only one instance is reachable from the internet, and only from your IP, instead of exposing every server.

### **Traceability**

All administrative access funnels through one host, making it easy to log and audit who connected and when.

### **Defense in Depth**

Layered security groups mean that even if someone reached the public subnet, the private server still won’t accept their connection.

### **Security Note**

This tutorial uses an IAM user with a scoped, least-privilege managed policy (`AmazonEC2FullAccess`) rather than the root account. A best practice that limits blast radius if credentials are ever compromised. Inbound SSH is restricted to your IP, never left open to the world.

Version Control
---------------

### Originally Published

**28 October 2026**

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Bastion Host](https://ntombizakhona.medium.com/bastion-host-be2e1b881ebe)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**28 October 2026**
