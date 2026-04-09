Authorisation
=============

Controlling Who Can Do What
---------------------------

In the world of cloud computing, **authorisation** plays a crucial role in maintaining the security and integrity of systems, applications, and data. While authentication answers the question, _Who are you?_, authorisation goes a step further and asks, **_What are you allowed to do?_**

Let’s consider a real-world scenario: Your company stores customer records in a cloud database. A customer support agent needs access to view customer profiles but should never be able to delete or modify them.

Through cloud authorisation, you can create a policy or assign a role that grants read-only access, ensuring data security, accountability, and compliance without slowing the agent down.

Authorisation in the Cloud
--------------------------

Authorisation in the cloud is the process of determining which resources an authenticated user, application, or system is permitted to access and what actions they can perform on those resources. This spans a wide range of operations, including but not limited to:

*   Reading data from databases or storage buckets
*   Modifying files, configurations, or records
*   Deploying applications or services
*   Managing infrastructure such as virtual machines, networks, or security groups
*   Deleting resources or revoking other users’ access

Without authorisation, every authenticated user would have unrestricted access to everything. A scenario that would be both chaotic and dangerous.

Why Authorisation Matters
-------------------------

The cloud offers unparalleled flexibility and scalability, but without strict access controls, it can also open the door to significant risk. Data breaches, accidental deletions, compliance violations, and insider threats are all consequences of poorly managed access. Proper authorisation mechanisms ensure:

### Least Privilege Access

Users only receive the permissions they need to do their jobs. Mo more, no less. This dramatically reduces the blast radius if an account is compromised.

### Resource Protection

Sensitive data and critical services are only accessible to approved individuals or systems. This keeps proprietary information, customer data, and infrastructure configurations safe.

### Regulatory Compliance

Many industries (healthcare, finance, government) are subject to strict regulations such as HIPAA, GDPR, SOC 2, and PCI-DSS, all of which require documented and enforceable access controls.

### Auditability

Cloud platforms like AWS, keep detailed logs of who accessed what and when. Services such as AWS CloudTrail are critical for compliance reporting, forensic investigation, and troubleshooting.

### Separation of Duties

Authorisation enables organisations to ensure that no single individual has unchecked control over critical processes. For example, the person who writes code should not be the same person who approves its deployment to production.

Common Cloud Authorisation Models
---------------------------------

### 1. Role-Based Access Control (RBAC)

Users are assigned roles, and each role carries a predefined set of permissions. For example, a _Developer_ role may allow code deployment, while an _Admin_ role grants broader access to system settings and user management.

**Best for:** Organisations with clearly defined job functions and predictable access needs.

**Example:** _In AWS, you might create an IAM role called S3ReadOnlyAccess and attach it to all data analysts in your team._

### 2. Attribute-Based Access Control (ABAC)

Permissions are granted based on attributes such as department, geographic location, project tag, security clearance, or even time of access. This model is more flexible and dynamic than RBAC.

**Best for:** Large, complex environments where access needs to adapt to changing contexts.

**Example:** _A policy that allows access to a resource only if the user’s department tag matches the resource’s department tag and the request is made during business hours._

### 3. Policy-Based Access Control

Cloud-native services like AWS IAM allow the creation of fine-grained policies written in JSON or YAML that define access at the user, group, service, and resource level.

**Best for:** Granular, custom access control scenarios across cloud services.

**Example:** _An AWS IAM policy that explicitly allows an EC2 instance to read from a specific S3 bucket but denies access to all other buckets._

### 4. Rule-Based Access Control

Access is determined by a set of predefined rules set by a system administrator. Unlike RBAC (which is based on roles), rule-based control applies universally regardless of who the user is.

**Best for:** Enforcing blanket security rules such as blocking access from certain IP ranges or outside business hours.

Best Practices for Authorisation in the Cloud
---------------------------------------------

### 1. Apply the Principle of Least Privilege

Start with zero permissions and grant only what is necessary. Regularly prune unused permissions.

### 2. Use Roles and Policies Instead of Direct Permissions

Assigning permissions directly to individual users leads to sprawl and management headaches. Group-based and role-based approaches scale far more effectively.

### 3. Regularly Review and Audit Permissions

Access needs change as people switch teams, projects, or leave the organisation. Schedule periodic access reviews (at least quarterly).

### 4. Use Multi-Factor Authentication (MFA) Alongside Authorisation

MFA strengthens the authentication layer, ensuring that even if credentials are compromised, unauthorized access is far less likely.

### 5. Implement Deny-by-Default Policies

Unless explicitly permitted, access should be denied. This prevents accidental exposure of sensitive resources.

### 6. Tag and Organise Resources

Consistent resource tagging (by environment, project, team) makes it far easier to write and manage authorisation policies.

### 7. Automate Where Possible

Use Infrastructure as Code (IaC) tools like Terraform or AWS CloudFormation to define and version-control your access policies, reducing human error.

### Putting It All Together With An Analogy

A High-Security Office Building
-------------------------------

_Authentication_ is like checking in at the front desk. You show your ID badge, and the security guard confirms who you are.

**Authorisation,** on the other hand, is what determines which doors your access card can open once you’re inside. Maybe you can get into the marketing department, but not the server room or the executive suite. Your level of access is based on your role, your clearance level, and your responsibilities.

Now imagine you’re a contractor brought in for a specific project. You’d get a temporary badge that only opens the doors relevant to your work and it expires when the project ends. That’s the principle of least privilege and time-bound access in action.

In the cloud, it works the same way: after verifying your identity (authentication), authorisation controls what you’re allowed to do and see based on policies, roles, or attributes.

Additional Resources
--------------------

### [Access Control](https://medium.com/access-control-306607c6385a)

Imagine a world where anyone, regardless of authority or qualifications, could do whatever they wanted.

Think about someone unqualified performing medical procedures on you or an unlicensed, inexperienced driver transporting your loved ones.

That kind of chaos is something I’d never want to face.

### [Authentication](https://medium.com/authentication-fb0d207899a1?postPublishedType=repub)

Authentication is rooted in a straightforward principle: _before you let someone in, make sure they are who they claim to be._

In a physical world, this might mean checking a driver’s license or a passport.

In the digital world, and especially in the cloud, authentication translates this concept into technical mechanisms that verify user identity across networks, devices, and applications.

### [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

> AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources.
> 
> With IAM, you can manage permissions that control which AWS resources users can access.
> 
> You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.
> 
> IAM provides the infrastructure necessary to control authentication and authorization for your AWS accounts.



Summary
-------

### Prerequisites

1.  [Access Control](https://medium.com/access-control-306607c6385a)
2.  [Authentication](https://medium.com/authentication-fb0d207899a1?postPublishedType=repub)

### Theory

1.  Introduction
2.  Authorisation in the Cloud
3.  Why Authorisation Matters
4.  Common Cloud Authorisation Models
5.  Best Practices
6.  Putting It All Together With An Analogy: A High Security Office Building
7.  Concluding Remarks: The Impact of Artificial Intelligence on Glossary Term

### Cloud Glossary Terms Mentioned in this Article

1.  Access Control
2.  Attribute
3.  Authentication
4.  Automate
5.  Buckets
6.  Cloud Native
7.  Data
8.  Database
9.  IP
10.  Least Privilege
11.  Logs
12.  Multifactor Authentication
13.  Networks
14.  Scalability
15.  Security
16.  Security Groups
17.  Storage
18.  Tag
19.  Virtual Machines

Alternatives to Reading
-----------------------

### [Listen on Spotify](https://open.spotify.com/episode/1q3If5gPgyF366A2jKRcvy?si=Xjtlfk8zRjO_gG38iDHG_g&nd=1&dlsi=be51df148e42456d)

> [_Cloud Computing Simplified: A Cloud Glossary for Beginners_](https://open.spotify.com/show/2cjYlSlpvIRxLNFpT4jflP)
> 
> **_Episode Name_**_: Authorisation_
> 
> **_By:_** _Ntombizakhona Mabaso_

### Concluding Remarks

Authorisation in the cloud is about control making sure the right people have the right access at the right time. Combined with strong authentication, it forms one of the foundational pillars of a secure cloud strategy.

As organisations continue to scale and migrate workloads to the cloud, understanding and implementing robust authorisation frameworks becomes more important than ever.

The Impact of AI on Authorisation
---------------------------------

Artificial intelligence is beginning to reshape how authorisation is designed, managed, and enforced in cloud environments. Here are the key ways AI is influencing this space:

### 1. Intelligent Permission Recommendations

AI-powered tools can analyse usage patterns and recommend right-sized permissions. For example, AWS IAM Access Analyzer uses automated reasoning to identify overly permissive policies and suggest tighter alternatives, helping teams enforce least privilege without the guesswork.

### 2. Anomaly Detection and Adaptive Access

Machine learning models can establish baselines of normal user behaviour and flag deviations in real time. If a developer who typically accesses resources during business hours suddenly makes API calls in the AMs from an unfamiliar location, AI-driven systems can automatically trigger additional verification or temporarily restrict access.

### 3. Automated Policy Generation and Management

Rather than manually crafting JSON policies, AI tools can generate authorisation policies based on observed behaviour, job function descriptions, or natural language prompts. This lowers the barrier to entry for teams without deep security expertise.

### 4. Dynamic and Context-Aware Authorisation

AI enables a shift from static role assignments to dynamic, context-aware access decisions. Instead of granting blanket permissions, AI can evaluate real-time signals like device posture, network environment, risk score, and ‘recent activity to determine whether a request should be approved, denied, or escalated. This is a core component of Zero Trust Architecture.

### 5. Continuous Compliance Monitoring

AI can continuously audit authorisation configurations against regulatory frameworks (POPIA, HIPAA, GDPR, SOC 2) and automatically flag or even remediate non-compliant policies before they become vulnerabilities.

### 6. Predictive Risk Scoring

Advanced AI systems can assign risk scores to users, sessions, or access requests based on historical data and contextual signals. High-risk requests can be routed through additional approval workflows or blocked entirely, adding an intelligent layer of defence.

**_AI is not replacing authorisation. It is making it smarter, faster, and more adaptive. As cloud environments grow more complex, AI-driven authorisation will become essential for maintaining security at scale without sacrificing agility or user experience_**

Version Control
---------------

### Originally Published

**09 April 2026**


---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Authorisation](https://ntombizakhona.medium.com/authorisation-ce5e449e621a)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**09 April 2026**
