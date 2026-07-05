### 🏗️ Let’s Build

Demonstrating Bandwidth By Using A Cloud Delivery Network
---------------------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

Use a **Content Delivery Network (CDN)** to optimize _bandwidth_ and deliver content fast to a global audience.

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/authentication-fb0d207899a1)
2.  [**Multisession Support Enabled**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)

### Add Additional Permissions to Your IAM Account

> **_💡 Principle of Least Privilege:_** _It is considered a best practice to grant users only the necessary permissions to perform their tasks, it is a fundamental security concept that will help keep your systems secure in the long run._

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

**Step 02:** Select **⁝⁝⁝ Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen under ▼ **Access management**

Select **IAM users**

**Step 05:** I**AM users**

Select the **Cloud Glossary** IAM User.

**Step 06: CloudGlossary**

Select **Permissions.**

Click **Add permissions** ▼

Select **Add permissions.**

You should be redirected to the **Add permissions** page.

**Step 07: Add permissions**

**Permission options:** Attach policies directly

On the Search bar type and check:

`**AmazonS3FullAccess**`

`**CloudFrontFullAccess**`

`**CloudWatchReadOnlyAccess**`

Click **Next**

**Step 08: Review**

Click **Add permissions**

✅**Green banner: 3** policies added to CloudGlossary

Build With Your IAM User Account
--------------------------------

> **_💡_**_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 09:** Sign in with your IAM Account.

### Create an S3 Bucket and Upload Content

> **_💡_**_You need something to serve before you can optimize its delivery._
> 
> _Start by creating a bucket and adding a simple web page._

**Step 01:** Open the **S3** console and choose **Create bucket**.

**Step 02: Create bucket**

*   **Bucket type:** `**General purpose**`
*   **Bucket namespace:** `**Account Regional namespace (Recommended)**`
*   **Bucket name prefix:** `**bandwidth**`

> **_💡Leave Block all public access enabled. CloudFront will reach the content securely, so the bucket itself stays private_**.

Click **Create bucket**.

✅**Green banner: Successfully created bucket “bandwidth-XXXXXX-us-east-1-an”**

**Step 03:** Click **↑Upload**

Click **Add files**

**Step 04: Create and upload a small** `**index.html**` **file.**

> **_💡Any simple HTML file works. Even one line like_** `**_<h1>Cloud Glossary Bandwidth!</h1>_**`**_._**

Click **Upload**.

> **_💡Keep the file small while learning. You can add images or larger media later to see compression and caching in action._**

✅**Green banner: Upload succeeded**

### Create a CloudFront Distribution

> **_💡The CloudFront distribution is your CDN. It caches your content at edge locations worldwide._**

**Step 05:** Open the **CloudFront** console

**Step 06:** Click **Create distribution**.

**Step 07: Choose a plan:** `**Free**`

Click **Next**

**Step 08: Get started**

*   **Distribution name:** `**bandwidth**`
*   **Distribution type:** `**Single website or app**`

Click **Next**

**Step 09: Specify origin**

*   O**rigin type:** `**Amazon S3**`
*   **S3 origin:** `**Browse S3**` **→** `**bandwidth-xxxxx**` **→ Choose**
*   ✔ **Allow private S3 bucket access to CloudFront — _Recommended_**
*   **Origin settings:** `**Use recommended origin settings**`
*   **Cache settings:** `**Use recommended cache settings tailored to serving S3 content**`

Click **Next**

**Step 10: Enable Security**

Click **Next**

**Step 11: Review and create**

Click **Create distribution**

✅**Green banner: Successfully created new distribution.**

### Enable Compression

> **_💡Compression shrinks text-based files before they travel to viewers, saving bandwidth._**

**Step 12:** In your distribution, open the **Behaviors** tab.

**Step 13:** Select the default behavior and choose **Edit**.

**Step 14: Edit behavior**

Set **Compress objects automatically** to **Yes**.

Click **Save changes**.

✅**Green banner:** The default cache behavior was updated.

### Test Delivery Through CloudFront

> **_💡Confirm your content is being served from the CDN._**

**Step 15:** In the distribution’s **General** tab, copy the **Distribution domain name** (it looks like `d1234abcd.cloudfront.net`).

> **_💡Wait until the distribution Status shows Enabled (deployment takes a few minutes)._**

**Step 16:** Open `https://<your-distribution-domain>/index.html` in a browser

> **_💡Wyou should see your page, now served from the nearest edge location._**
> 
> **_Reload the page. The first load fetches from S3._**
> 
> **_Later loads are served from the edge cache, which is faster and uses less origin bandwidth._**

### Monitor Bandwidth Usage

> **_💡Keep an eye on how much data you’re transferring._**

**Step 17:** In the CloudFront console, open the ▼ **Reports & analytics** section to view **Cache statistics**

**Step 18:** Under ▼ **Telemetry,** Open the **Monitoring** tab to see **CloudWatch** metrics like **Data Transfer** (outbound bandwidth to viewers) and **Requests**.

> **_💡Watch how cache hits reduce the load and the outbound bandwidth on your S3 origin._**

**You now have a working CDN that delivers content quickly worldwide while minimizing outbound bandwidth from your origin.**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  Navigate to _CloudFront_ and **Disable & Delete** The Distribution
2.  Navigate to _S3_ and **Empty & Delete** The Bucket
3.  Confirm in **CloudWatch** that no further data transfer is being recorded.
4.  Login with your _Administrative Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

```
                          +---------------------------+
                          |     IAM User Account      |
                          |    AmazonS3FullAccess     |
                          |    CloudFrontFullAccess   |
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |      Amazon S3 Bucket     |
                          |   (bandwidth-demo-site)   |
                          |   Origin: index.html      |
                          +-------------+-------------+
                                        |
                          +-------------+-------------+
                          |  CloudFront Distribution  |
                          |   Compression: Enabled    |
                          |   Origin Access Control   |
                          +-------------+-------------+
                                        |
               ------------------------------------------------
               |                        |                     |
    +----------+-------+    +-----------+------+    +---------+---------+
    |   Edge Location  |    |   Edge Location  |    |   Edge Location   |
    |    (Americas)    |    |     (Europe)     |    |   (Asia Pacific)  |
    |   Cached Copy    |    |   Cached Copy    |    |    Cached Copy    |
    +------------------+    +------------------+    +-------------------+
               |                        |                     |
               ------------------------------------------------
                                        |
                          +-------------+-------------+
                          |       Global Viewers      |
                          |   Low latency, less       |
                          |   outbound from origin    |
                          +---------------------------+
    Delivery Flow:
   -----------------------------------------------------------------------
   Viewer Request --> Nearest Edge --> Cache Hit? --> Serve Fast (no origin)
                                          |  miss
                                          --> Fetch from S3 origin once
   -----------------------------------------------------------------------
```

This walkthrough demonstrates one of AWS’s most important performance patterns: using a **Content Delivery Network (CDN)** to optimize bandwidth and deliver content fast to a global audience.

### **What Was Built**

An Amazon S3 bucket (`bandwidth`) holds a simple web page, and an Amazon CloudFront distribution sits in front of it with compression enabled. CloudFront caches the content at edge locations around the world.

### **The Key Demonstration**

When a viewer requests the page, CloudFront serves it from the nearest edge location instead of the origin bucket. The first request fetches from S3 once, then every cached request after that is served from the edge which is faster for users and using far less outbound bandwidth from your origin.

### **Application Speed**

Content served from a nearby edge location dramatically reduces latency compared to a single distant origin.

### **Cost Efficiency**

Caching at the edge means fewer requests reach S3, lowering outbound data transfer costs (which is where cloud bandwidth charges usually come from).

### **Scalability**

The CDN absorbs traffic spikes across its global network, so a surge in viewers doesn’t overwhelm your origin.

### Least Privilege

This tutorial uses an IAM user with scoped, least-privilege managed policies (`AmazonS3FullAccess` and `CloudFrontFullAccess`) rather than the root account. A best practice that limits blast radius if credentials are ever compromised.

---
# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Bandwidth](https://medium.com/p/a9ac97111a87?postPublishedType=initial)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**05 July 2026**
