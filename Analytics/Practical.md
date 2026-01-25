### Let’s Build

Creating a Word Cloud With OpenSearch Serverless
------------------------------------------------

I know (hope) you’re eager to set something up. In this practical, hands-on-tutorial, we will demonstrate **Analytics** with Amazon OpenSearch Service

_Amazon OpenSearch Service (formerly Amazon Elasticsearch Service) is a managed service that makes it easy to deploy, secure, and operate OpenSearch and Elasticsearch clusters in the AWS Cloud. OpenSearch is a search and analytics engine that enables users to search, analyze, and visualize large volumes of data in real time. It is often used for log analytics, full-text search, security monitoring, and operational intelligence._

### Prerequisites

1.  [An AWS Administrative Account](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [An AWS IAM User Account](https://medium.com/amazon-web-services-a8e57a9c6084)

### Add Permissions

**Step 01:** Log in to AWS Management Console with Your Root User / Administrator Account.

_In keeping up with the Spirit of the_ [_Principle of Least Privilege_](https://medium.com/@ntombizakhona/access-control-306607c6385a)_, we will only assign permissions relevant to the task at hand._

**Step 02:** Select **Security, Identity & Compliance** on the left side of the drop down menu.

**Step 03:** Select **IAM.**

You should be redirected to the IAM Dashboard.

**Step 04:** On the left side of the screen expand **Access management.**

Select **Users.**

Select your **IAM User.**

**Step 05:** Select Add permissions. Create inline policy

**Policy editor:** `**JSON**`

Replace the code with the code below:

```
{
 "Version": "2012-10-17",
 "Statement": [  {
   "Action": [    "aoss:*",
    "aoss:DashboardsAccessAll",
    "aoss:ListSecurityConfigs",
    "aoss:GetAccessPolicy",
    "aoss:CreateCollection",
    "aoss:ListCollections",
    "aoss:BatchGetCollection",
    "aoss:DeleteCollection",
    "aoss:CreateAccessPolicy",
    "aoss:ListAccessPolicies",
    "aoss:UpdateAccessPolicy",
    "aoss:CreateSecurityPolicy",
    "aoss:GetSecurityPolicy",
    "aoss:UpdateSecurityPolicy",
    "iam:ListUsers",
    "iam:ListRoles"
   ],
   "Effect": "Allow",
   "Resource": "*"
  }
 ]
}
```

Click **Next.**

**Policy Name: myOpenSearchPolicy.**

Click **Create policy.**

**Green Banner:** _Policy myOpenSearchPolicy created._

And then attach the following policies directly:

**AmazonOpenSearchServiceFullAccess**

**Step 06:** Log in to the AWS Management Console with your IAM User.

### Create OpenSearch Collection

**Step 07:** On the top left corner, click on the **Services** button.

Select **Analytics** on the left side of the drop down menu.

Select **Amazon OpenSearch Service.**

Under **Serverless,** Click **Dashboard.**

Get started: Click **Get Started.**

**Step 08:** Collection name: **word-cloud**

**Description — optional:** My Word Cloud Collection.

**Collection type:** Search

**Deployment type:** Uncheck **Enable redundancy (active replicas)**

**Security:** Standard Create

**Encryption:** Use an AWS owned key.

**Network Access Settings.** Access Type: **Public.**

Check: **Enable access to OpenSearch Endpoint** and **Enable access to OpenSearch Dashboards**

Click **Next.**

**Step 09: Data access policy options:** Uncheck Automatically match access policy settings

**Select policy definition method:** Visual editor.

Click **Rule 1.**

**Rule name:** word-cloud-rule.

Click **Add principals.** Select **IAM Users and roles**.

**Properties:** Users.

Select **_yourUser._**

Click **Save.**

**Step 10: Grant permissions.**

**Alias and template permissions:** Select all.

Index Permissions: **Select all.**

Click **Next.**

**Step 11: Data access policy settings:** Create as a new data access policy.

**Access policy name:** word-cloud-data-ace

**Description — optional:** My OpenSearch Access Policy.

Click **Next.**

**Step 12:** Review and create collection.

Click **Submit.**

**Green Banner:** _Successfully created word-cloud_

Overview. Status: **Active.**

### Create an Index

**Step 13**: **Under Overview, click the OpenSearch Dashboards URL**

**Step 14:** Welcome to OpenSearch Dashboards.

Click **Add data.**

**Step 15**: Click the menu button.

**Step 16**: Under **Management,** select **Dev Tools.**

**Step 17:** Replace the code with

```
PUT my-index
```

**Step 18:** Click the play button to send request.

You should receive a success **200-OK** status with the following output:

```
{
  "acknowledged": true,
  "shards_acknowledged": true,
  "index": "my-index"
}
```

### Create an Index Pattern

**Step 19**: Under **Overviews,** click the **OpenSearch Dashboards URL.**

Welcome to OpenSearch Dashboards.

**Step 20:** Click **Add data.**

Click the menu button.

Under **Management,** select **Stack Management.**

**Step 21:** Click **Index Patterns.**

**Step 22:** Click **Create Index pattern.**

Index Pattern name: **my-index.**

**Step 23:** Click **Next step.**

**Step 24:** Click **Create index pattern.**

### View Dashboard

**Step 25:** Navigate back to your menu. Under **OpenSearch Dashboard**, click **Dashboard.**

**Step 26:** Click **Create dashboard.**

**Step 27:** Click **Create new.**

**Step 28:** New Visualization, select **Tag Cloud.**

**Step 29:** Navigate back to your menu. Under OpenSearch Dashboard, click Visualisations, and view your “Word Cloud.”

### Explore OpenSearch Capabilities With Sample Data

> OpenSearch is a powerful and versatile tool that goes far beyond creating basic – though fun – word clouds. To truly appreciate its capabilities, start by installing sample data and explore the wide range of features it offers for searching, analyzing, and visualizing data.

**Step 30:** Navigate back to your menu. Under **OpenSearch Dashboard**, click **Dashboard.**

**Step 31:** Click **Install some sample data.**

**Step 32:** Sample web logs. Click **Add data.**

**Step 33:** Click **View data.**

**Step 34:** View the different types of visualizations from the Web logs sample data, or whichever one you selected.

### Important

Clean Up Resources
------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running, because as from the [1st of February 2024, AWS has started charging for IP addresses](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights/#:~:text=Effective%20February%201%2C%202024%20there,attach%20to%20an%20EC2%20instance).).

1.  Navigate back to OpenSearch Service.
2.  Under **Serverless,** Click **Collections.**
3.  Check **word-cloud.**
4.  Click **Delete.**
5.  Confirm **Delete.**
6.  Login with your _Root User Account_, and **Remove All Permissions** Associated with your IAM Account.

### End of Tutorial

Building Tutorial Overview
--------------------------

We quickly created a word cloud to showcase just how easy it is to get started with OpenSearch Serverless. By exploring sample data, we were able to highlight the various ways this powerful tool allows you to visualize and gain insights from your data.

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Analytics](https://ntombizakhona.medium.com/analytics-dd6e58eea952)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**22 June 2025**
