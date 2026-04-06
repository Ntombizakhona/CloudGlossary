### 🏗️ Let’s Build

Exploring Attributes on AWS
---------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Launching An EC2 Instance.**

_This will demonstrate how_ **_attributes_** _shape every decision you make when creating a cloud resource._

### Prerequisites

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**Elastic Compute Cloud Tutorial**](https://medium.com/@ntombizakhona/abstraction-d1335bec022e)

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

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner:** 1 policy added

Build Using Your IAM Account
----------------------------

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your IAM Account.

**Step 10: Navigate to the EC2 Dashboard**

_The EC2 Dashboard is the central hub for managing your virtual machine instances._

Select **⁝⁝⁝ Compute** on the left side of the drop down menu.

Select **EC2.**

**Dashboard**

💡 **Attribute Spotlight:** Notice the Region selector in the top-right corner of the console United States (**N. Virginia)** ▼

This is your **_first attribute_**: the geographical location where your resource will be created. Choosing a region close to your users reduces latency and can impact compliance requirements.

**Step 11: Launch A New Instance**

Click **Launch instance**

You will be presented with a configuration form where nearly every field represents a cloud attribute.

**Launch An Instance**

**Name:** Attributes-Instance

Click **Add additional tags**

**Key:** Name → **Value:** Attributes-Instance

**Key:** Environment → **Value:** Testing

**Key:** Owner → **Value:** CloudGlossary

💡 **Attribute Spotlight:** Tags are user-defined attributes that don’t affect how the instance runs, but they are invaluable for organizing, filtering, and managing resources especially as your cloud environment grows. Many organizations enforce tagging policies to track costs by team or project.

**Step 12: Select an Amazon Machine Image (AMI)**

▼ **Application and OS Images (Amazon Machine Image)**

Select **Amazon Linux 2023 kernel 6.1 AMI (Free Tier eligible)**

💡 **Attribute Spotlight:** The AMI is an attribute that defines the operating system, pre-installed software, and base configuration of your instance. Think of it as choosing the foundation and blueprint of your house before construction begins.

**Step 13: Choose the Instance Type**

▼ **Instance type**

Select **t3.micro (Free tier eligible).**

_Notice that each instance type displays its vCPUs, Memory (GiB), and Network Performance._

💡 **Attribute Spotlight:** The instance type is one of the most critical attributes. It determines the computational power of your virtual machine such as how much CPU, RAM, and network bandwidth your resource will have. Selecting the right instance type is like choosing the engine size for a car: too small and performance suffers, too large and you waste money.

**Step 14:** [**Configure the Key Pair (Access Attribute)**](https://medium.com/@ntombizakhona/abstraction-d1335bec022e)

▼ **Key pair (login)**

**Key pair name _— required:_** CloudGlossary

💡 **Attribute Spotlight:** The key pair is a security attribute that controls who can access your instance. Without it, remote login is impossible. This directly ties to the Access Permissions attribute discussed earlier, forming a foundational layer of cloud security.

**Step 15: Configure Network Settings**

▼ **Network settings.**

Click **Edit**

Scroll to **Firewall (security groups)**

Select **Create security group.**

**Security group name — _required_:** CloudGlossarySG

**Description — _required_:** Security Group for My Cloud Glossary Tutorials

Under **Inbound Security Group Rules.**

Click **Add Security group rule.**

**Type:** Select **HTTP.**

**Source Type**: Select **Anywhere.**

Review the following attributes:

*   **VPC:** Leave the default VPC selected.
*   **Subnet:** Choose a subnet or leave it as _No preference_ to let AWS assign one automatically.
*   **Auto-assign public IP:** Ensure this is set to Enable so you can connect to your instance from the internet.
*   **Security group:** Select Create security group and ensure a rule exists to Allow SSH traffic from My IP.

💡 **Attribute Spotlight:** Every field here is a network attribute. The VPC defines your isolated virtual network, the subnet determines the availability zone, the public IP makes the instance reachable, and the security group acts as a virtual firewall controlling inbound and outbound traffic. Together, these attributes dictate how your resource communicates with the outside world.

**Step 16: Configure Storage Attributes**

▼ **Configure storage:** leave as default.

Under Configure storage, you will see a default volume (typically 8 GiB, gp3).

You can modify:

*   **Size (GiB):** The total storage capacity.
*   **Volume type:** Options include gp3 (general purpose SSD), io1 (provisioned IOPS SSD), st1 (throughput-optimized HDD), and others.

💡 **Attribute Spotlight:** Storage size and volume type are attributes that directly impact performance and cost. A general-purpose SSD is suitable for most workloads, while provisioned IOPS is designed for I/O-intensive databases. Choosing the wrong storage attribute can lead to bottlenecks or unnecessary expenses.

**Step 17: Review and Launch**

Review all the attributes you have configured in the Summary panel on the right side of the screen.

▼ **Summary**

**Number of instances:** 1

**Software Image (AMI):** Amazon Linux 2023 AMI 2023.10.20260330.0 x86_64 HVM kernel-6.1

**Virtual server type (instance type):** t3.micro

**Firewall (security group):** CloudGlossarySG

Click **Launch instance**

✅**Green banner: Success**

**Step 18:View Your Instance Attributes in Action**

Click **View all instances** to return to the **EC2 Instances dashboard.**

Select your newly launched instance and explore the Details, Security, Networking, Storage, and Tags tabs at the bottom of the screen.

Notice how every attribute you configured is now visible and active:

*   **The Details tab** shows the instance ID, instance type, AMI, public IP, and availability zone.
*   **The Security tab** displays the security group rules and key pair name.
*   **The Networking tab** lists the VPC, subnet, public and private IP addresses.
*   **The Storage tab** shows the attached volume, its size, and type.
*   **The Tags tab** lists your custom metadata.

💡 **Attribute Spotlight:** Every piece of information you see on this screen is an attribute. Together, these attributes fully define your cloud resource: what it is, where it lives, who can access it, how it connects, and how it’s organized. Mastering attributes means mastering your cloud environment.

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Select your instance, click Instance state → Terminate instance.
2.  Login with your _Root User Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

```
┌─────────────────────────────────────────────────────────────────────┐
│                         AWS CLOUD                                   │
│                     Region: us-east-1                               │
│                  (Geographic Location Attribute)                    │
│                                                                     │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │                    VPC (Virtual Private Cloud)                │  │
│  │                  (Network Configuration Attribute)            │  │
│  │                                                               │  │
│  │  ┌─────────────────────────────────────────────────────────┐  │  │
│  │  │              Subnet (Availability Zone: us-east-1a)     │  │  │
│  │  │              (Region & Availability Zone Attribute)     │  │  │
│  │  │                                                         │  │  │
│  │  │  ┌────────────────────────────────────────────────────┐ │  │  │
│  │  │  │              Security Group                        │ │  │  │
│  │  │  │         (Access Permissions Attribute)             │ │  │  │
│  │  │  │         Inbound Rule: Allow SSH (Port 22)          │ │  │  │
│  │  │  │                                                    │ │  │  │
│  │  │  │  ┌──────────────────────────────────────────────┐  │ │  │  │
│  │  │  │  │           EC2 Instance                       │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   Name: my-first-cloud-instance              │  │ │  │  │
│  │  │  │  │   (Tag Attribute)                            │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   AMI: Amazon Linux 2023                     │  │ │  │  │
│  │  │  │  │   (Machine Image Attribute)                  │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   Instance Type: t2.micro                    │  │ │  │  │
│  │  │  │  │   (Instance Type Attribute)                  │  │ │  │  │
│  │  │  │  │   - 1 vCPU                                   │  │ │  │  │
│  │  │  │  │   - 1 GiB Memory                             │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   Key Pair: my-key-pair                      │  │ │  │  │
│  │  │  │  │   (Access Permission Attribute)              │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   Tags:                                      │  │ │  │  │
│  │  │  │  │   - Environment: Testing                     │  │ │  │  │
│  │  │  │  │   - Owner: YourName                          │  │ │  │  │
│  │  │  │  │   (Tag Attributes)                           │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  │   ┌───────────────────────────────────────┐  │  │ │  │  │
│  │  │  │  │   │       EBS Volume                      │  │  │ │  │
│  │  │  │  │   │    (Storage Attribute)                │  │  │ │  │  │
│  │  │  │  │   │                                       │  │  │ │  │  │
│  │  │  │  │   │    Size: 8 GiB                        │  │  │ │  │  │
│  │  │  │  │   │    Type: gp3 (General Purpose SSD)    │  │  │ │  │  │
│  │  │  │  │   └───────────────────────────────────────┘  │  │ │  │  │
│  │  │  │  │                                              │  │ │  │  │
│  │  │  │  └──────────────────────────────────────────────┘  │ │  │  │
│  │  │  │                                                    │ │  │  │
│  │  │  └────────────────────────────────────────────────────┘ │  │  │
│  │  │                                                         │  │  │
│  │  │                  Public IP: Auto-assigned               │  │  │
│  │  │                  (Network Configuration Attribute)      │  │  │
│  │  │                                                         │  │  │
│  │  └─────────────────────────────────────────────────────────┘  │  │
│  │                                                               │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                     │
└──────────────────────────────────┬──────────────────────────────────┘
                                   │
                                   │ SSH (Port 22)
                                   │ Secured by Key Pair
                                   │
                            ┌──────┴──────┐
                            │             │
                            │    USER     │
                            │  (Your PC)  │
                            │             │
                            └─────────────┘
```

Building Tutorial Overview
--------------------------

The step-by-step guide bridges theory and practice by walking you through the process of launching an Amazon EC2 instance on AWS. Each step is designed to spotlight a specific cloud attribute in a real-world context, starting with foundational choices like selecting a region and naming your resource with tags, then progressing through more complex configurations such as instance type, networking, and storage.

Along the way, “Attribute Spotlight” callouts connect each console action back to the concepts covered in the article, reinforcing your understanding through hands-on repetition.

The tutorial stays within the AWS Free Tier so you can follow along without incurring costs, and it wraps up with a cleanup step to build responsible cloud management habits from the start.

By the end, you’ll have not only launched your first cloud resource but also seen firsthand how attributes work together to fully define, secure, and organize that resource within your cloud environment.

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Attributes](https://ntombizakhona.medium.com/attributes-de42fc2b93b2?postPublishedType=repub)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**02 April 2026**
