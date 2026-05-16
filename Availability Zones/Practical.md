### 🏗️ Let’s Explore

Observing Availability Zones In The AWS Console
-----------------------------------------------

You don’t need to build anything to understand availability zones. AWS exposes AZ information throughout the console. You just need to know where to look.

I know _(and hope)_ you’re eager to get started, so in this walkthrough we’ll:

**Explore your region’s AZs, see how subnets map to them, and understand how AWS uses AZ IDs behind the scenes.**

_This will demonstrate high_ **_Availability Zones_** _in the Cloud._

⚠️ **Note:** This walkthrough is observation only. You will not create or modify any resources, so there is nothing to clean up.

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Amazon Web Services**](https://medium.com/amazon-web-services-a8e57a9c6084)

### See Your Region’s Availability Zones

**Step 01:** Sign in to the **AWS Management Console**.

**Step 02:** Look at the region selector in the top-right corner of the console **United States** (**N. Virginia)** ▼.

This is the region you're currently viewing.

Every region contains multiple Availability Zones.

**💡 Tip: If you want to follow along exactly, select** (**N. Virginia)** ▼ .I**t’s the oldest AWS region.**

**Step 03:** Navigate to the **EC2 Console**

**Step 04:** On the left side of the screen, scroll down to ▼ **Network & Security** Click **Network Interfaces**.

**💡**This page may be empty if you haven’t launched anything. That’s fine. What we’re after is on the next screen.

**Step 05:** On the left side of the screen, scroll back up and click **Dashboard** (the top link).

**Step 06:** In the **Service health** section on the you’ll see a list of **Availability Zones** for your current region with their status:

```
**Region**
United States (N. Virginia)
**Status**
✅ This service is operating normally.
Zones
ZONE NAME    | ZONE ID    | STATUS
-------------|------------|---------------------------
us-east-1a   | use1-az6   | Operating normally
us-east-1b   | use1-az1   | Operating normally
us-east-1c   | use1-az2   | Operating normally
us-east-1d   | use1-az4   | Operating normally
us-east-1e   | use1-az3   | Operating normally
us-east-1f   | use1-az5   | Operating normally
```

**💡 What you’re seeing:** Each of these (a to f) is a **physically separate data center** (or cluster of data centers) in the Northern Virginia area.

They each have independent power, cooling, and networking. This is the foundation of high availability on AWS.

### Explore How Subnets Map to Availability Zones

Every subnet in AWS lives in exactly **one** Availability Zone. This is how you control _where_ your resources physically run.

**Step 07:** Navigate to the **VPC Console**

**Step 08:** On the left side of the screen under ▼ **Virtual private cloud**

Click **Subnets**.

**Step 09:** You’ll see a list of subnets.

Look at the **Availability Zone** column:

```
SUBNET ID      | AVAILABILITY ZONE | VPC
---------------|-------------------|-------------
subnet-abc123  | us-east-1a        | Default VPC
subnet-def456  | us-east-1b        | Default VPC
subnet-ghi789  | us-east-1c        | Default VPC
subnet-jkl012  | us-east-1d        | Default VPC
subnet-mno345  | us-east-1e        | Default VPC
subnet-pqr678  | us-east-1f        | Default VPC
```

**💡What you’re seeing:** AWS automatically created one subnet per Availability Zone in your **default VPC**.

Each subnet is tied to a specific AZ.

When you launch an EC2 instance into `subnet-abc123`, that instance physically runs in the `us-east-1a` data center.

If you launch another into `subnet-def456`, it runs in a completely separate building (`us-east-1b`).

**Step 10:** Click on any subnet to see its details.

Note the **Availability Zone** and **Availability Zone ID** fields.

### Understand AZ Names vs. AZ IDs

This is a detail that surprises many beginners.

**Step 11:** In the subnet detail view, notice two fields:

*   **Availability Zone:** `us-east-1a` (the _name_)
*   **Availability Zone ID:** `use1-az1` (the _ID_)

**💡Why are there two?**

AWS **randomizes AZ names per account**.

Your `us-east-1a` might be a different physical data center than someone else's `us-east-1a`.

This prevents everyone from piling into the same zone. The **AZ ID** (`use1-az1`) is the consistent, physical identifier that maps to the same data center for every account.

_This matters when you're coordinating across AWS accounts (e.g., sharing data or peering networks)._

**Step 12:** To see all AZ IDs for your region, navigate back to the **Service Health** on the EC2 **Dashboard.**

**💡If you’re working with a colleague and you both want resources in the same physical data center, compare _AZ IDs_, not AZ names.**

### See AZs in the Global Infrastructure Map

**Step 13:** Open a new browser tab and go to:

```
https://aws.amazon.com/about-aws/global-infrastructure/regions_az/
```

**Step 14:** Scroll down to the interactive map.

Click on any **region** to see how many Availability Zones it contains.

**💡What you’re seeing:** Regions with more AZs give you more options for spreading workloads across independent failure domains. Most regions have at least 3 AZs which is enough to survive the loss of any single zone.

### Observe AZ Assignment When Launching an Instance (Without Actually Launching)

You can see how AZ selection works without creating anything.

**Step 15:** Navigate back to the **EC2 Console**

Click **Launch instances** ▼.

**Step 16:** Scroll down to ▼ **Network settings**

Click **Edit**.

**Step 17:** Look at the **Subnet** dropdown.

You’ll see your subnets listed with their AZ:

*   `subnet-abc123 (us-east-1a)`
*   `subnet-def456 (us-east-1b)`
*   `subnet-ghi789 (us-east-1c)`
*   `No preference` (AWS picks for you)

**💡What you’re seeing:** This is where you decide which Availability Zone your instance runs in.

Selecting a specific subnet pins your instance to that AZ’s physical data center.

Selecting “No preference” lets AWS choose,which is fine for single instances but not ideal when you’re designing for high availability (you’d want to deliberately spread across multiple AZs).

**Step 18:** Click **Cancel.** We’re just observing, not launching.

**💡What’s next?**

Now that you’ve seen where Availability Zones live in the console, try the [**Availability Tutorial**](https://medium.com/availability-300d472ddece) to build a real multi-AZ architecture with a load balancer and auto scaling group. And watch traffic shift between AZs in real time!

### 🏁 The End🏁

---
# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Availability Zones](https://ntombizakhona.medium.com/availability-zones-8364186c666e)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**16 May 2026**
