Availability
============

Accessibility Despite Downtime
------------------------------

In the world of cloud computing, **availability** refers to the ability of a system, application, or service to remain accessible and operational over time.

_High_ **availability** ensures that users and businesses can rely on their cloud-hosted resources without worrying about unexpected outages, slowdowns, or disruptions.

What Is Cloud Availability?
---------------------------

Cloud availability is commonly measured as a percentage of uptime. For example, a cloud provider offering “_five nines_” availability (99.999%) is committing to no more than about 5 minutes of downtime per year.

```
| Availability Level| Common Name | Max Downtime / Year |
|-------------------|-------------|---------------------|
| 99%               | Two nines   | ~3.65 days          |
| 99.9%             | Three nines | ~8.7 hours          |
| 99.99%            | Four nines  | ~52.6 minutes       |
| 99.999%           | Five nines  | ~5.26 minutes       |
```

These levels are made possible through advanced infrastructure, redundancy, and failover mechanisms that are built into the cloud provider’s architecture.

Why Is Availability Important?
------------------------------

Availability is essential for both small startups and large enterprises. Here’s why:

### Business Continuity

Downtime can result in lost revenue, productivity, and customer trust.

### Global Access

Users expect 24/7 access, regardless of time zones.

### Compliance & SLAs

Many industries require a guaranteed level of service availability to meet regulatory standards.

How Cloud Providers Ensure High Availability
--------------------------------------------

### Redundancy

Cloud providers deploy data and services across multiple servers, zones, or even geographic regions. If one fails, others take over seamlessly.

### Load Balancing

Distributes traffic across multiple instances to prevent overload and improve response times.

### Auto Recovery

Services automatically restart or shift to healthy resources in the event of failure.

### Backup & Replication

Regular data backups and real-time replication protect against data loss and ensure fast recovery.

### Putting It All Together With An Analogy

Power Grid
----------

Think of cloud availability like a power grid. Just as we expect our lights to turn on whenever we flip a switch, users expect cloud-based apps and services to be available when they need them.

Behind the scenes, engineers work to maintain backup power sources, detect failures early, and reroute supply

Just as cloud providers do for digital systems.

Additional Resources
--------------------

### [AWS Well-Architected Framework — Reliability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html)

> The focus of this paper is the reliability pillar of the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/). It provides guidance to help customers apply best practices in the design, delivery, and maintenance of Amazon Web Services (AWS) environments.

### [Advanced Multi AZ Resilience Patterns](https://docs.aws.amazon.com/whitepapers/latest/advanced-multi-az-resilience-patterns/advanced-multi-az-resilience-patterns.html)

> Many customers run their workloads in highly available, multi-Availability Zone (AZ) configurations.
> 
> These architectures perform well during binary failure events, but often encounter problems with _gray_ failures.
> 
> The manifestations of this type of failure can be subtle, and defy quick and definitive detection.
> 
> This paper provides guidance on how to instrument workloads to detect impact from gray failures that are isolated to a single Availability Zone, and then take action to mitigate that impact in the Availability Zone.

### [What Is Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)?

> Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.
> 
> You create collections of EC2 instances, called _Auto Scaling groups_.
> 
> You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size.
> 
> You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size.
> 
> If you specify the desired capacity, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances.
> 
> If you specify scaling policies, then Amazon EC2 Auto Scaling can launch or terminate instances as demand on your application increases or decreases.

### [What Is An Application Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)

> Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones.
> 
> It monitors the health of its registered targets, and routes traffic only to the healthy targets.
> 
> Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

### [AWS Service Level Agreements](https://aws.amazon.com/legal/service-level-agreements/)

> AWS commits to offer Service Level Agreements (SLAs) for all paid, generally available services.

Summary
-------

### Prerequisites

1.  [**Abstraction**](https://medium.com/@ntombizakhona/abstraction-d1335bec022e)
2.  [**Apache HTTP**](https://medium.com/apache-http-8404a1b11d26)
3.  [**Auto Scaling**](https://medium.com/auto-scaling-ad945ba63939)

### Theory

1.  Introduction
2.  What Is Cloud Availability?
3.  Why Is Availability Important?
4.  How Cloud Providers Ensure High Availability
5.  Putting It All Together With An Analogy: Power Grid
6.  Concluding Remarks: The Impact of Artificial Intelligence on Availability

### Hands On

1.  Add Additional Permissios To Your IAM Account
2.  Build Using Your IAM Account
3.  Create a VPC With Two Public Subnets
4.  Enable Auto-Assign Public IP on Both Subnets
5.  Create a Launch Template
6.  Create an Application Load Balancer (ALB)
7.  Create an Auto Scaling Group
8.  Test High Availability
9.  Simulate a Failure
10.  Clean Up Procedure

### Cloud Glossary Terms Mentioned in this Article

1.  Backup
2.  Failover
3.  Load Balancing
4.  Redundancy
5.  Replication
6.  SLAs
7.  Traffic

Alternatives to Reading
-----------------------

### [Listen on Spotify](https://open.spotify.com/episode/1q3If5gPgyF366A2jKRcvy?si=Xjtlfk8zRjO_gG38iDHG_g&nd=1&dlsi=be51df148e42456d)

> [_Cloud Computing Simplified: A Cloud Glossary for Beginners_](https://open.spotify.com/show/2cjYlSlpvIRxLNFpT4jflP)
> 
> **_Episode Name_**_: Availability_
> 
> **_By:_** _Ntombizakhona Mabaso_

### Concluding Remarks

Cloud availability is not just a technical feature. It’s a **business priority**. By leveraging the cloud’s built-in fault tolerance, geographic redundancy, and intelligent automation, organizations can ensure their critical systems stay online and accessible even in the face of unexpected disruptions.

When evaluating a cloud provider, always review their **Service Level Agreement (SLA)** to understand the availability guarantees they offer.

The Impact of Artificial Intelligence on Availability
-----------------------------------------------------

Artificial intelligence is reshaping how we think about cloud availability in several important ways:

### **Predictive Failure Detection**

AI models can analyze telemetry data (CPU patterns, disk I/O anomalies, network latency spikes) to predict hardware and software failures _before_ they cause downtime. AWS services like Amazon DevOps Guru already use machine learning to surface operational insights and recommend remediation steps proactively.

### **Intelligent Auto-Scaling**

Traditional auto-scaling reacts to thresholds (e.g., “add an instance when CPU exceeds 70%”). AI-driven scaling anticipates demand by learning traffic patterns, therefore scaling up before a spike hits and scaling down gracefully afterward, reducing both cost and risk of overload.

### **Self-Healing Infrastructure**

AI-powered runbooks and automated remediation can diagnose root causes and execute fixes (restart services, reroute traffic, roll back deployments) faster than any human on-call engineer. This shrinks mean-time-to-recovery (MTTR) from minutes to seconds.

### **New Pressure on Infrastructure**

AI workloads themselves are placing unprecedented demands on cloud infrastructure. A 2026 report by Cockroach Labs found that 83% of technology leaders believe AI-driven demand will cause their data infrastructure to fail without major upgrades within 24 months ([source](https://www.prnewswire.com/news-releases/cockroach-labs-2026-ai-report-finds-ai-scale-is-pushing-enterprise-infrastructure-toward-failure-302673598.html)). GPU-intensive training and inference workloads require rethinking how availability is architected fom power and cooling to network fabric and storage tiering.

### **AI Observability**

As AI workloads multiply, traditional monitoring falls short. Organizations are investing in AI-specific observability tools that track model latency, GPU utilization, and inference queue depth alongside classic infrastructure metrics, ensuring availability standards extend to this new class of workload.

### The Bottom Line:

AI is both a **powerful tool for improving availability** and a **new source of complexity** that availability strategies must account for. The organizations that thrive will be those that use AI to strengthen their resilience while proactively upgrading infrastructure to handle AI’s growing demands.

Version Control
---------------

### Originally Published

**03 May 2025**

### Updates

---

# The Original

**Blog:** [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona)
<br>
**Article Link:** [Availability](https://medium.com/@ntombizakhona/availability-300d472ddece)
<br>
Originally Published by [Ntombizakhona Mabaso](https://medium.com/@ntombizakhona) 
<br>
**03 May 2026**

