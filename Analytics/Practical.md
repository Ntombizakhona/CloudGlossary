### 🏗️ Let’s Build

Creating a Word Cloud With AWS SageMaker
----------------------------------------

I know _(hope)_ you’re eager to set something up. In this practical, hands-on tutorial, we will:

**Create a word cloud using AWS SageMaker.**

AWS Sagemaker is Amazon’s fully managed achine learning service. SageMaker provides a powerful Python-based notebook environment perfect for data science workflows, including text analysis and visualization.

_AWS SageMaker is a comprehensive machine learning platform that enables developers and data scientists to build, train, and deploy ML models at scale. For our purposes, we’ll use SageMaker Studio’s notebook environment to programmatically generate a word cloud from text data._

### Prerequisites

Prerequisites
-------------

1.  [**An AWS Administrative Account that has an Alias Account Configured (IAM)**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)
2.  [**Multisession Support Enabled.**](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/multisession.html)
3.  [**Basic familiarity with Python (helpful but not required)**](https://medium.com/python-in-the-cloud-1462f61e3293)

### Add Permissions

**Step 01**: Sign in with your Administrative Root User Account in order to grant permissions to your active Alias or IAM Account.

_In keeping up with the Spirit of the_ [_Principle of Least Privilege_](https://medium.com/@ntombizakhona/access-control-306607c6385a)_, we will only assign permissions relevant to the task at hand._

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

Select **Create inline policy**

**Step 07: Specify Permissions**

**Policy editor:** JSON

Replace the code with this:

```
{
    "Version": "2012-10-17",
    "Statement": [        {
            "Effect": "Allow",
            "Action": [                "sagemaker:*",
                "datazone:*",
                "s3:*",
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents",
                "iam:PassRole",
                "iam:GetRole",
                "iam:CreateRole",
                "iam:CreateServiceLinkedRole",
                "iam:AttachRolePolicy",
                "iam:PutRolePolicy",
                "servicecatalog:*",
                "ram:*",
                "kms:CreateGrant",
                "kms:Decrypt",
                "kms:DescribeKey",
                "kms:Encrypt",
                "kms:GenerateDataKey",
                "kms:ReEncrypt*"
            ],
            "Resource": "*"
        }
    ]
}
```

Click **Next**

**Step 08: Review and create**

**Policy name:** mySageMakerUnifiedStudioPolicy

Click **Create policy**

✅**Green banner: Policy mySageMakerUnifiedStudioPolicy created.**

Click **Add permissions** ▼

Select **Add permissions.**

You should be redirected to the **Add permissions** page.

**Step 09: Add permissions**

**Permission options:** Attach policies directly

On the Search bar type and check:

**AmazonSageMakerFullAccess**

**SageMakerStudioUserIAMConsolePolicy**

**AmazonDataZoneFullAccess**

**AWSServiceCatalogAdminFullAccess**

**IAMFullAccess**

Click **Next**

Click **Add permissions.**

✅**Green banner:** 5 policies added to CloudGlossary

### Build Using Your IAM Account

_Build using your IAM account (not the root account) because it’s safer and more controllable: you can enforce least privilege, require MFA, track actions per user in CloudTrail, and quickly remove or rotate access if something goes wrong, while keeping the powerful root account locked down for rare account-level tasks._

**Step 10:** Sign in with your IAM Account.

### Create a SageMaker Domain

**Step 11:** On the top left corner, click on the **⁝⁝⁝ Services** button.

Select **Analytics**

Select **Amazon Sagemaker**

Click **Get started**

**Step 12:** **Set up Amazon SageMaker Unified Studio**

_Leave default_

Click **Set up**

**💡Verification:**

**Setting up Amazon SageMaker Unified Studio…**

**Setting up Amazon SageMaker Unified Studio…**

**Hang tight, your domain administration experience will open once this one-time setup is complete.**

**Step 13:** **Amazon Sagemaker**

Click **Open**

Click **Accept**

**Step 14: Under IDE, Click JupyterLab**

_Note: The first launch may take several minutes as SageMaker provisions your environment._

**Step 15: Create a New Notebook**

Under Notebook, click on **Python 3 (ipykernel)** to create a new notebook.

Your notebook is now ready. You should see an empty cell waiting for input.

**Step 16: Install Required Libraries**

In the first cell of your notebook, enter the following code to install the word cloud library:

```
!pip install wordcloud
```

Click the ▶ Run button in the toolbar, or press Shift+Enter to execute the cell.

**💡Verification**

Wait for the installation to complete. You should see output indicating successful installation.

```
Installing collected packages: wordcloud
Successfully installed wordcloud-1.9.6
```

**Step 17: Import Libraries**

In a new cell, import the necessary libraries:

```
from wordcloud import WordCloud
import matplotlib.pyplot as plt
```

▶ Run the cell (Shift+Enter).

**Step 18: Prepare Sample Text Data**

In a new cell, create sample text data for your word cloud:

```
# Sample text about cloud analytics
text = """
Analytics data cloud AWS SageMaker machine learning artificial intelligence
visualization insights business intelligence dashboard metrics performance
scalability serverless computing storage database processing real-time
streaming batch ETL transform load extract warehouse lake data science
predictive modeling algorithm training deployment inference neural network
deep learning natural language processing computer vision automation
optimization cost-effective innovation digital transformation enterprise
solution infrastructure platform service cloud-native microservices
containers orchestration monitoring logging security compliance governance
big data hadoop spark distributed computing cluster node storage object
relational NoSQL graph time-series analytics reporting BI dashboards
KPIs metrics trends patterns anomaly detection forecasting regression
classification clustering segmentation recommendation personalization
customer insights user behavior engagement retention conversion
analytics cloud AWS machine learning data science visualization
"""
```

▶ Run the cell.

**Step 19: Generate the Word Cloud**

In a new cell, create and configure your word cloud:

```
# Create the word cloud
wordcloud = WordCloud(
    width=800,
    height=400,
    background_color='white',
    colormap='viridis',
    max_words=100,
    min_font_size=10,
    max_font_size=100
).generate(text)
```

▶ Run the cell.

**Step 20: Display the Word Cloud**

```
# Display the word cloud
plt.figure(figsize=(15, 8))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.title('Cloud Analytics Word Cloud', fontsize=20, fontweight='bold')
plt.tight_layout(pad=0)
plt.show()
```

▶ Run the cell.

🎉 **_Congratulations! You should now see a colourful word cloud visualization with words sized according to their frequency in the text!_**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

1.  In _JupyterLab,_ **Delete** your Notebook.
2.  **Stop** the J_upyterLab_ space.
3.  Click _Domain Management,_ select your project and **Delete** it.
4.  Login with your _Root User / Admin Account_, and **Remove All Permissions and Policies** associated with your IAM Account.

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

We created a word cloud programmatically using Python in AWS SageMaker Unified Studio, demonstrating the flexibility and power of this new integrated analytics environment.

This approach gives you complete control over your visualization, allowing for extensive customization and the ability to process data from various sources.

SageMaker Unified Studio is ideal for teams who want to:

1.  Collaborate on data science projects in a unified environment
2.  Access data, analytics, and ML capabilities from a single interface
3.  Write custom analysis code with JupyterLab
4.  Integrate with other AWS data services seamlessly
5.  Build reproducible data pipelines
6.  Extend visualizations into machine learning workflows

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Analytics](https://ntombizakhona.medium.com/analytics-dd6e58eea952)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**22 June 2025**
