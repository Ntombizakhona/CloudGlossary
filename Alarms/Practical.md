### 🏗️ Let’s Build

Setting Up a Billing Alarm on AWS
---------------------------------

I know _(hope)_ you’re eager to set something up.

In this practical, hands-on-tutorial, we will:

**Set up a billing alarm that will alert you when usage or spending surpasses your budgeted limit.**

### Prerequisites

1.  [**An AWS Administrative Account**](https://medium.com/@ntombizakhona/amazon-web-services-a8e57a9c6084)

### Setting Up A Billing Alarm on AWS

_A billing alarm is an AWS feature that automatically notifies you when your spending crosses a predefined threshold. It provides real-time visibility into your AWS costs, enabling you to take proactive action before expenses exceed your budget._

**Which Account Should You Use?**

Since billing is an administrative task and this tutorial doesn’t involve building infrastructure, you _could_ technically use your root account. However, best practice is to always use your IAM user whenever possible, even for following tutorials.

Here’s the recommended approach:

**IAM User:** Use for daily tasks, building resources, and following tutorials

**Root User:** Reserve exclusively for critical billing and administrative tasks that require root access

By consistently working with your IAM user, you’ll develop secure habits that protect your AWS environment in the long run.

**Step 01: Access Billing Console**

Select **Billing and Cost Management**

**Step 02:** **Navigate to Budgets**

Under **Budgets and Planning,** click **Budgets**

Click **Create budget**

**Step 03: Choose budget type**

**Budget setup:** Use a template (simplified)

**Templates — new:** Zero spend budget

**Budget name:** My Zero-Spend Budget

**Email Recipients:** Your Email Address

Click **Create budget**

✅**Green banner:** Your budget My Zero-Spend Budget has been created successfully.

### 🏁End of Building Tutorial 🏁

Building Tutorial Overview
--------------------------

In this hands-on tutorial, we created a zero-spend budget alarm in AWS that monitors your account for any charges beyond the free tier.

This budget automatically sends email notifications when your AWS spending exceeds $0.01, helping you catch unexpected costs early and avoid bill shock.

The setup uses AWS’s simplified budget template, making it quick to configure essential cost monitoring for your cloud resources.

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Alarms]([https://ntombizakhona.medium.com/amazon-web-services-a8e57a9c6084](https://ntombizakhona.medium.com/alarms-656943304f1b?postPublishedType=repub))
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**08 December 2024**
