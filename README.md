# AWS-Cost-Optimization

![image](https://github.com/user-attachments/assets/7872ce47-88ba-4205-b009-8d81006c3f91)

 Top 5 Cost Optimization Tip for AWS Cloud
 1. Right-Sizing Resources
What it is: Ensure the instances and resources match your workload requirements.
Actions:
Use AWS Cost Explorer and Compute Optimizer to identify underutilized or overprovisioned instances.
Downsize or switch to more appropriate instance families (e.g., from m5.large to t4g.medium if applicable).
Schedule instances to shut down during non-peak hours using AWS Instance Scheduler.

  2. Use Savings Plans and Reserved Instances (RIs)
What it is: Commit to a usage plan for predictable workloads to get lower rates.
Actions:
Leverage Savings Plans for compute usage (flexible across EC2, Fargate, and Lambda).
Purchase Reserved Instances for long-term workloads (1 or 3 years).
Regularly analyze unused RIs and adjust accordingly.

  3. Optimize Storage Costs
What it is: Ensure storage is appropriately tiered and unnecessary data is removed.
Actions:
Move infrequently accessed data to Amazon S3 Intelligent-Tiering or Glacier.
Use EBS Volume Manager to delete unattached EBS volumes.
Transition RDS snapshots and logs to lower-cost storage classes when feasible.

  4. Leverage Spot Instances
What it is: Use spot instances for workloads that are flexible in timing.
Actions:
Replace on-demand instances with Spot Instances for non-critical workloads like batch processing or CI/CD pipelines.
Use Spot Fleets or EC2 Auto Scaling to handle interruptions effectively.
Combine Spot with Savings Plans for hybrid cost management.

 5. Monitor and Automate Cost Management
What it is: Continuously monitor usage and costs with AWS tools and automation.
Actions:
Set up AWS Budgets and CloudWatch Alarms for cost thresholds.
Automate cost tagging and cleanup of unused resources (e.g., idle EC2 instances, unutilized Load Balancers).
Enable Cost Anomaly Detection to spot unusual spikes early.

Bonus Tips
Use AWS Trusted Advisor for tailored recommendations.
Consolidate billing under AWS Organizations for volume discounts.


![image](https://github.com/user-attachments/assets/ad754f17-698b-4ef5-b864-a339ca525190)

Why People Move to the Cloud
1. Cost Efficiency
Why: The cloud eliminates the need for upfront capital expenditures on hardware and reduces ongoing costs for maintenance, power, and cooling.
How:
Pay-as-you-go pricing models allow businesses to only pay for the resources they use.
Scalability ensures that resources can be increased or decreased based on demand, avoiding over-provisioning.

2. Scalability and Flexibility
Why: The cloud provides the ability to scale resources up or down quickly in response to changing business needs.
How:
Autoscaling features dynamically adjust resources during peak or idle times.
Wide range of services (compute, storage, databases) ensures businesses can adapt to market demands without delays.

3. Improved Performance and Reliability
Why: Cloud providers offer high-performance infrastructure and global networks to ensure low latency and high availability.
How:
Data replication across multiple regions and availability zones minimizes downtime.
Services like Content Delivery Networks (CDNs) ensure faster delivery of content worldwide.

4. Enhanced Security and Compliance
Why: Cloud providers invest heavily in robust security measures, helping organizations meet stringent compliance requirements.
How:
Features like data encryption, identity and access management (IAM), and built-in firewalls.
Compliance with standards like GDPR, HIPAA, and ISO ensures businesses remain secure and regulated.

5. Innovation and Agility
Why: Cloud environments foster innovation by providing access to cutting-edge technologies and tools.
How:
Services like AI/ML, IoT, and serverless computing enable rapid development and testing.
Developers can focus on building solutions without worrying about managing infrastructure.

AWS Cloud Cost Optimization: Identifying and Removing Stale EBS Snapshots
Objective: Optimize AWS storage costs by identifying and deleting unused EBS snapshots that are no longer associated with any active EC2 instance.

Overview:
This process involves creating a Lambda function that automatically scans for EBS snapshots in your account, checks their association with active EC2 instances, and deletes snapshots deemed stale. This approach helps reduce unnecessary storage costs.

![image](https://github.com/user-attachments/assets/964e8c18-1771-46ab-a228-a82d358fc533)

AWS Cloud Cost Optimization: Identifying and Removing Stale EBS Snapshots
Objective: Optimize AWS storage costs by identifying and deleting unused EBS snapshots that are no longer associated with any active EC2 instance.

Overview:
This process involves creating a Lambda function that automatically scans for EBS snapshots in your account, checks their association with active EC2 instances, and deletes snapshots deemed stale. This approach helps reduce unnecessary storage costs.

How It Works:

The Lambda function retrieves a list of all EBS snapshots owned by the account.

It fetches information about active EC2 instances (both running and stopped).

For each snapshot, the function determines whether the associated volume is linked to any active EC2 instance.

If the snapshot is no longer in use (stale), the function deletes it, ensuring efficient storage usage.

![image](https://github.com/user-attachments/assets/faa1ed5e-72ed-4290-a73c-6603b74cce38)

The Cost of Forgotten Snapshots: A Real-World Example
Imagine this: a developer takes a daily snapshot of an Amazon Elastic Block Store (EBS) volume to back up their work. This practice continues over a year, resulting in a growing collection of snapshots. Each snapshot incurs storage costs, but it's a small price to pay for the assurance of having backups.

What Went Wrong?
Over time, the developer decides the EC2 instance and its volume are no longer needed and deletes them. However, they overlook one critical detail: snapshots aren’t automatically deleted when the instance or volume is removed. The snapshots continue to sit in storage, silently racking up costs.

Here’s a breakdown of the situation:

Daily snapshots: 1 snapshot/day

Total snapshots in a year: 365 snapshots

Snapshot size: ~50 GB each

Storage cost per GB (standard EBS pricing): $0.05/GB/month

Monthly cost of snapshots:

365×50
 GB
×
0.05
 USD/GB
=

912.50
 
USD
365×50GB×0.05USD/GB=912.50USD
Annual cost of forgotten snapshots:
912.50
×
12
=
10
,
$950
 
USD
$912.50×12= $10,950USD

That’s $10,950 annually for unused snapshots—a significant expense caused by a small oversight.

Example
1. Create and EC2 Instance
   ![image](https://github.com/user-attachments/assets/133c0f39-70a3-4114-886c-20c2bcffe7f7)
   ![image](https://github.com/user-attachments/assets/0b53362a-b016-4a8d-b422-a68d305aa954)

Next we create a Lambda function
![image](https://github.com/user-attachments/assets/b360f631-0ffd-4fb1-993f-f633afcbc12c)

![image](https://github.com/user-attachments/assets/4d739914-5249-49c5-9903-292dbed6872e)
When you run the test your function will Fail the reason is permission
You will need to Give it 
Describle snapshot
Delete snapshot 
![image](https://github.com/user-attachments/assets/58e9da40-0ee9-4f5b-99dc-a135ac4c1d0e)


![image](https://github.com/user-attachments/assets/62ade1ff-52ca-451d-9dc1-b0577a13bafc)

![image](https://github.com/user-attachments/assets/5ee93d59-a29b-42b6-8405-b4a67546f44a)

