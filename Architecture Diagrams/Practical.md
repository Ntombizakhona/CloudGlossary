### 🏗️ Let’s Build

Architecture Diagram of Serverless Architecture
-----------------------------------------------

I know _(and hope)_ you’re eager to get started, so in this practical, hands-on tutorial we’ll:

**Build An Architecture Diagram of Serverless Architecture.**

### Prerequisites

[**CloudPulse: Capstone Project & Architecture Review**](https://medium.com/capstone-project-architecture-review-38db82027d5f)

### Open Draw.io and Create a New File

**Step 01:** Open your **browser**

**Step 02:** Go to [**https://app.diagrams.net**](https://app.diagrams.net/)

**Step 03: Set the filename**

CloudPulse-Architecture-Diagram

**Type:** XML file (.draw.io)

Click **Rename**

💡**Verification:** You now have an empty white canvas.

**Step 04:** Configure Your Canvas

**Set Up the Grid**

Go to **View** in the top menu

💡**Verification:** Make sure **✔ Grid** is checked

💡**Verification:** Make sure **✔ Ruler** is checked (this helps align shapes perfectly)

**Step 05:** Set Page Size

On the right side of the page

Change the page size to A3 Landscape

Select **Landscape**

**A3 (297 mm x 420mm) ▼**

_This gives you plenty of room for all CloudPulse components_

**Step 06:** Set Background Colour

**Set Background to white (#FFFFFF)**

**Step 07:** Load the AWS Icon Library

Look at the **left sidebar** where shapes are listed

**Scroll to the very bottom** of the sidebar

Click **+ More Shapes**

**Step 08:** In the dialog that opens, scroll to the **Networking** section

**Networking**

**✔ AWS 17**

**✔ AWS 18**

**✔ AWS 2026**

**✔ AWS 3D**

Select **Labels.**

Click **Apply**

💡**Verification:** You should now see AWS shape categories in your left sidebar:

```
▼ AWS X
  ├── AWS General
  ├── AWS Compute
  ├── AWS Database
  ├── AWS Storage
  ├── AWS Networking
  ├── AWS Security
  ├── AWS App Integration
  ├── AWS Management
  └── ... and more
```

**_You can also search for any AWS service by typing its name in the Search box at the top of the left panel (e.g., type “Lambda” to find the Lambda icon instantly)._**

**Step 09:** Draw the Title Block

**Let’s start with the title at the top of the diagram**

**Double-click** on an empty area near the top of the canvas

A **text box** will appear

Type:

```
CloudPulse
Serverless Task Management Application
Architecture Diagram
```

**Step 10: Select the text and format it:**

Font size 10, Center aligned, Bold for “Users / Browser”

**Step 11:** Arrange All Components on the Canvas

Before drawing connections, organize the layout. Here’s the recommended spatial arrangement:

```
LEFT SIDE                    CENTER                          RIGHT SIDE
(Outside AWS)               (Inside Region)                  (Outside AWS)
                    ┌─────────────────────────────────┐
                    │                                 │
                    │   [S3 Bucket]                   │
                    │   (top-left)                    │
                    │                                 │
[Users/Browser] ──► │   [API Gateway] ──► [Lambda] ──► [DynamoDB]    │
                    │   (center-left)   (center)    (center-right)│
                    │                                 │
                    │   [IAM]        [CloudWatch] ──► [SNS] ──── ► [Admin Email]
                    │   (bottom-left) (bottom-center) (bottom-right)│
                    │                                 │
                    │   [Budgets]                     │
                    │   (bottom-far-left)             │
                    │                                 │
                    └─────────────────────────────────┘
```

**Step 12:** Final Layout Review and Alignment

**Check Your Layout Against This Map**

```
┌──────────────────────────────────────────────────────────────────────┐
│                        TITLE BLOCK                                   │
│               CloudPulse Architecture Diagram v1.0                   │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│                 ┌── AWS Cloud ────────────────────────────────┐      │
│                 │  ┌── Region: us-east-1 ──────────────────┐  │      │
│                 │  │                                       │  │      │
│                 │  │     TOP ROW (Data Layer):             │  │      │
│  [Users/        │  │     [S3]                              │  │      │
│   Browser]      │  │                                       │  │Admin │
│                 │  │     MIDDLE ROW (API & Compute):       │  │Email]│
│      ──────►    │  │     [API GW] ──► [Lambda] ──► [DDB]   │  │      │
│                 │  │                                       │  │      │
│                 │  │     BOTTOM ROW (Operations):          │  │      │
│                 │  │     [IAM]  [CloudWatch] ──► [SNS] ────┼──┼──►   │
│                 │  │     [Budgets]                         │  │      │
│                 │  │                                       │  │      │
│                 │  │     CALLOUTS (Well-Architected):      │  │      │
│                 │  │     [Security] [Reliability] [Cost]   │  │      │
│                 │  │                                       │  │      │
│                 │  └───────────────────────────────────────┘  │      │
│                 └─────────────────────────────────────────────┘      │
│                                                                      │
│  [Legend]                    [Data Flow Description]                 │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Step 13:** Export Your Diagram

**Export as PNG (High Resolution)**

Go to File → Export as → PNG

Configure:

**Zoom:** 200% (for crisp, high-resolution output)

**Border width:** 15px

**Selection only:** Unchecked

**Include a copy of my diagram:** ✅

Click **Export** → Download

**Step 14:** Export as SVG (Scalable Vector)

Go to File → Export as → SVG

Click **Export** → Download

**Step 15:** Export as PDF (Documentation)

Go to File → Export as → PDF

Click **Export** → Download

**Step 16:** Save the Editable File

Go to **File** → Save As

Save as **CloudPulse-Architecture-Diagram.drawio**

Store this in your project repository alongside your code

**_🎉_ You now have a complete, professional architecture diagram for the CloudPulse Serverless Task Management Application that maps directly to the 12-Week AWS Workshop Challenge capstone project.**

### 🏁End of Building Tutorial 🏁

### Clean Up Procedure

⚠️Terminate Resources⚠️
-----------------------

Don’t get a [**Bill Shock**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html) by leaving unnecessary resources running.

**If you decided to follow the CloudPulse Tutorial and build anything on AWS, make sure you delete all of it.**

### ⛔ End of Cleaning Up Protocol ⛔

Building Tutorial Overview
--------------------------

You created an Architecture Diagram

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Architecture Diagrams](https://medium.com/@ntombizakhona/architecture-diagrams-9de5a563d608)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**15 February 2026**
