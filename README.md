# AWS Review Session 1

**Index**

**1. AWS Global Infrastructure**

1.1. AWS Regions

1.2. AWS Availability Zones

1.3. Points of Presence

1.3.1. Edge Locations

1.3.2. Regional Edge Caches

1.4.  Local Zones

1.5. Wavelength Zones

1.6. Outposts

**2. Amazon CloudFront**

**3. Regional Edge Caches**

**4. Identity and Access Management IAM**

4.1. AWS IAM

4.2. What is Least Privilege?

4.3. IAM Users and Groups

4.4. AWS Organizations

**5. IAM Policies**

**6. Amazon Resource Names (ARNs)**

**7. IAM Roles**

**8.  AWS IAM federation**

**9. Security Token Service (STS)**

**10. Revoking Temporary Credentials**

**11. Amazon S3 (Amazon Simple Storage Service)**

11.1. S3 storage classes

11.2. S3 Bucket Policies

11.3. S3 Transfer Acceleration (S3TA)

## 1. AWS Global Infrastructure:

AWS (Amazon Web Services) Global Infrastructure is designed to deliver secure, highly available, low-latency cloud services globally

It's made up of several key components that work together to ensure resilience, scalability, and performance.
  
### 1.1. AWS Regions : A physical location around the world where AWS clusters data centers.

Each AWS Region consists of multiple, isolated, and physically separate Availability Zones.

AWS Regions are totally isolated from each other, creating the greatest possible fault tolerance and stability

### 1.2. AWS Availability Zones (AZs): One or more discrete data centers with redundant power, networking, and connectivity in an AWS Region.

AZs give customers the ability to operate production applications and databases that are more highly available, fault tolerant, and scalable than would be possible from a single data center

easily AZs are connected to each other with fast, private fiber-optic networking, enabling you to architect applications that automatically fail-over between AZs without interruption.
 
### 1.3. Points of Presence (PoP): Smaller endpoints used for hosting cached data.

600+ Edge Locations and 13 regional mid-tier regional cache servers

Points of Presence enable Amazon CloudFront to securely deliver data, videos, applications, and APIs to customers globally with low latency and high transfer speeds, all within a developer-friendly environment.

### 1.4. Summary (AWS Global Infrastructure)

AWS (Amazon Web Services) Global Infrastructure is designed to deliver secure, highly available, low-latency cloud services globally

It's made up of several key components that work together to ensure resilience, scalability, and performance
________________________________________

🗺️ 1. Regions

•	A Region is a geographic area that contains multiple isolated locations called Availability Zones.

•	AWS has 30+ Regions worldwide (e.g., US East (N. Virginia), EU (Frankfurt), Asia Pacific (Tokyo)).

•	Each Region is completely isolated from the others for fault tolerance and stability.

•	You choose a Region to deploy your resources closer to your users.
________________________________________

🏢 2. Availability Zones (AZs)

•	An AZ is one or more data centers with independent power, cooling, and networking.

•	A Region typically has 2 to 6 AZs.

•	They're close enough for low latency but far enough apart to prevent failures from affecting multiple zones.

•	You can design fault-tolerant applications by deploying across multiple AZs.
________________________________________

📦 3. Edge Locations

•	Edge locations are part of the AWS Global Content Delivery Network (CDN), used by services like Amazon CloudFront.

•	They’re closer to end users and help cache and deliver content with low latency.

•	There are hundreds of edge locations worldwide.
________________________________________

💼 4. Local Zones

•	These extend AWS infrastructure to large metro areas.

•	They bring compute, storage, and other services closer to users for ultra-low latency applications (e.g., video games, AR/VR).

•	Example: Los Angeles Local Zone.
________________________________________

🛰️ 5. Wavelength Zones

•	Designed for 5G applications, hosted at telecom providers' data centers.

•	Let you build applications with millisecond latencies to mobile and connected devices.

•	Used with telecom carriers like Verizon, Vodafone.
________________________________________

🏭 6. Outposts

•	AWS Outposts are racks of AWS-managed hardware installed in your on-premises data center.

•	You can run AWS services locally but manage them with the same tools/APIs as in the cloud.
________________________________________

🌐 Summary Diagram 

  [ Global Infrastructure ]
           |
  ┌────────┴────────┐
[ Regions ]     [ Edge Network ]
     |                |
[ AZs ]         [ Edge Locations, Local Zones, Wavelength, Outposts ]
________________________________________

📌 Why It Matters:

•	High availability: Multi-AZ and multi-region designs help with disaster recovery.

•	Performance: Local Zones and Edge Locations reduce latency.

•	Compliance & data residency: Some organizations choose regions for legal/data sovereignty reasons.

## 2. Amazon CloudFront: Security deliver content with low latency and high transfer speeds

CloudFront is a Content Delivery Network CDN. It reduces latency for end users by leveraging the 450+ Points of Presence in the AWS network to deliver content to a global audience.

Any exam question that addresses the distribution of content to a global audience (especially static content) typically points to the use of Amazon CloundFront.

Content Delivery Network CDN with low latency, high transfer speeds.

Use cases: deliver fast and secure websites, accelerate dynamic content delivery APIs, stream live and on-demand video, distribute patches and updates.

### 2.1. Summary

🌐 What is Amazon CloudFront?

Amazon CloudFront is a Content Delivery Network (CDN) service from AWS.

It delivers your web content (HTML, CSS, JavaScript, images, videos, APIs) quickly and securely to users around the world using AWS’s global network of edge locations (Points of Presence).
________________________________________

🚀 Key Purpose

✅ Speed up content delivery

✅ Reduce latency

✅ Offload traffic from origin servers

✅ Secure content with encryption and access control
________________________________________

📦 How it Works (Step-by-Step)

1.	User Requests Content

o	A user visits your website or app and requests content (e.g., an image or video).

2.	CloudFront Checks Cache at Edge Location

o	CloudFront routes the request to the nearest Edge Location (PoP).

o	If the content is cached there (called a “cache hit”), it’s served immediately.

3.	No Cache? CloudFront Fetches from Origin

o	If the content is not cached (a “cache miss”), CloudFront retrieves it from the origin server (e.g., S3, EC2, or external server).

4.	Content Delivered and Cached

o	The content is sent to the user and stored (cached) in the Edge Location for future requests.

## 3. Regional Edge Caches: Regional edge caches for less popular content

Content not popular enough to store in a POPs (Point Of Presence) will be stored in a regional cache to get more content closer to users

Useful for content with an over-time decay in popularity.

CloudFront locations between origin server and POPs, with larger cache than individual POPs. Serves as intermediary hop for content

Requests go from viewer, to edge location, to regional edge caches, checking for content availability at each site before requesting directly from origin server.

### 3.1. Summary

🌐 What are AWS Regional Edge Caches?

Regional Edge Caches are an intermediate caching layer between:

1.	CloudFront Edge Locations (PoPs), and

2.	Your origin servers (e.g., S3, EC2, API Gateway, or any custom origin)

They sit closer to the origin than the edge locations but farther from the users — like a “middle tier.”
________________________________________

📦 Why do they exist?

•	To reduce the load on origin servers

•	To optimize cache-hit ratio

•	To help CloudFront scale better for large global content delivery

When CloudFront edge locations don't have the requested content, they try the regional edge cache first before going all the way to the origin
 
## 4. Identity and Access Management IAM: policies and technologies used to ensure the appropriate access to technology resources

### 4.1. AWS IAM provides fine-grained access control across all of AWS. With IAM, you can specify who can access which service and resources, under which conditions

IAM Policies allow you to manage permissions for your workforce and systems to ensure least-privileged access

### 4.2. What is Least Privilege?: A core component in AWS Security Best Practices AND in understanding Access

The principle of Least Privilege is that a user/resource should be granted the least amount of permissions or privileges needed to complete their job role

If a user does not need an access right, they should not have that access right

The exam will sometimes ask you to evaluate permissions/policies documents in response to providing access to a user

These questions assume that you understand the principle of least privilege

### 4.3. IAM Users and Groups: the building blocks of AWS Identity and Access Management

**IAM Users**: an IAM User is an entity that is created in AWS to represent the person, or application, that uses it to interact with AWS

**IAM Groups**: an IAM Group is a collection of IAM users. User groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users

Example: you could have a user group called Admins and give that user group typical administrator permissions
 
### 4.4. AWS Organizations: an account management service that enables account consolidation and organization

A way to consolidate accounts, assign permissions to OUs, and automate the onboarding of new team members based on job function

**Organizations**: an entity created to consolidate your AWS accounts

**Root**: parent container for all the accounts for your organization

**Organizational Unit (OU)**: a container for accounts within a root. An OU can also contain other OUs

An account management service that enables account consolidation and organization.

**Account**: an account in an organization is a standard AWS account that contains AWS resources and identities. 

**Service Control Policy (SCP)**: a policy that specifies the services and actions that users and roles can use in the accounts that the SCP affects.

**Tagging**: a best practices for your OUs to keep track of your AWS accounts and resources. This assists with more granular monitoring and logging of your AWS environment.

## 5. IAM Policies

IAM Policies are the bedrock of strong IAM security. Understanding how the policies work and being able to interpret them is critical for success as an Architect and on the exam.

Identity Policies are IAM policies that are applied to identities. This can include both users as well as roles that users can assume. These are different than resource policies.

Implicit versus Explicit Allow/Deny: The default response to all requests is an Implicit Deny. This stance can be overridden by allowing the user access with a permissions policy – this grants the user access because it has been Explicitly Allowed. The same process can be done with an Explicit Deny policy. This will deny access regardless of the permissions the user might have.


 
Resource Policies: unlike an identity-based policy, a resource-based policy specifies WHO (which principal) can access that resource. The principals identified within a resource-based policy include accounts, IAM users, federated users, IAM roles, assumed-role sessions, or AWS services.

Resource-based policies are attached to a resource.
 

A policy samples: AWS Identity and Access Management (IAM) policy
 
Enable/Disable Region (Specific to Hong Kong): So this allows enabling or disabling the Hong Kong (ap-east-1) region, and only that region.

View Console Permissions: So this allows read-only access to view account info and available regions.

This IAM policy:
1.	Grants permission to enable/disable only the ap-east-1 (Hong Kong) region.
2.	Grants permission to view AWS account details and list available regions.

Policy interpretation: This flow chart provides details about how the decision is made as AWS authenticates the principal that makes the request. AWS evaluates the policy types in this order.

Flowchart representing how AWS evaluates permissions to determine whether a user or role is allowed or denied access to perform an action.

 










Go to Index

6. Amazon Resource Names (ARN): A way to uniquely identify AWS resources.

We require an ARN when you need to specify a resource unambiguously across all of AWS, such as in IAM policies, AWS RDS tags, and API calls.

ARN Format: The specific formats depend on the resource. To use an ARN, replace the italicized text with the resource-specific information.

Be aware that the ARNs for some resources omit the Region, the account ID, or both the Region and the account ID. 

 

Go to Index

 

7. IAM Roles: Roles are a way for users to temporarily gain permissions.

AWS Roles have the same makeup as an IAM user with the following differences: 

-	An IAM role does not have long term credentials associated with it. A principal (user, machine, or authenticated identity) assumes the role and inherits permissions assigned to the user.  

-	Temporary access is granted using Security Token Service (STS). Token expiration reduces the risks associated with credentials leaking or being reused. 

-	An IAM role has a trust policy that defines which conditions must be met to allow other principals to assume it. 

In general, there are four scenarios where IAM roles might be used:

-	One AWS service accesses another AWS Service.
-	One AWS account accesses another AWS account.
-	A third-party web identity needs access (for example: Google, Facebook, Cognito) 
-	Authentication using SAML2.0 federation (enables SSO)


Go to Index

8. AWS IAM federation: In AWS IAM, the term federate (or federation) refers to the process of allowing users from an external identity system (like your corporate directory or a third-party provider) to access AWS without creating IAM users in your AWS account.

 

 

 


 

 

 

 





 

 

Go to Index

 

9. Security Token Service (STS): Request temporary, limited-privilege credentials for AWS IAM

STS allows you to provide temporary, limited-privilege credentials for your IAM users, or users that you federate as a part of access authentication. STS is a service that is available globally.

Temporary credentials can be assumed by authorized identities through the generate credentials (sts:AssumeRole) command.








 
Go to Index

10. Revoking Temporary Credentials: Roles can be assumed by MANY identities who will all get the same permissions. What happens if those credentials are compromised?

Changing Trust policies only effect identities that have not already assumed the role. These policies changes NO impact on existing credentials. 

Changing the Permissions policy will impact all credentials. Updating the policy with AWSRevokeOlderSessions inline deny for any sessions older than now. This signs out all identities that have currently assumed the role and applies the new policies.

















Go to Index

 

11. Amazon S3 (Amazon Simple Storage Service): Provides infinitely scalable, highly durable object storage in the AWS
Cloud.

 

Stores objects in resources called Buckets, which can be up to 5TB in size, but there are no to total limits to the number of objects stored.

Designed to provide 99.99999% durability and 99.99% availability.

Offered at multiple tiers of pricing based on the frequency the objects are needed, and the speed at which they are required to be retrieved. 














11.1. S3 storage classes: Amazon S3 currently provides a range of storage classes offerings to fit our customers needs. 

Each storage class is purpose-built for varying access patterns at corresponding costs.

Amazon S3 is an important service to understand trade-offs and use cases for each storage class. Read these carefully for giveaways that might be included in the questions stem that highlight a storage class as an option.



 




 

11.2. S3 Bucket Policies: A bucket policy that allows a principal (AWS Account ID 11111111111) to read and write to the bucket “sample-bucket-reinvent”

 

Who / what can be a principal in an S3 bucket policy?

Valid principals for your bucket policies include
• AWS account and root user
• IAM users
• Federated users (using web identity or SAML federation)
• IAM roles
• Assumed-role sessions
• AWS services
• Anonymous users (public) – not recommended



11.3. S3 Transfer Acceleration (S3TA): Provides faster, long-distance S3 uploads & downloads

S3 Transfer Acceleration (S3TA) reduces the variability in Internet routing, congestion and speeds that can affect transfers, and logically shortens the distance to S3 for remote applications. S3TA improves transfer performance by routing traffic through Amazon CloudFront’s globally distributed Edge Locations and over AWS backbone networks, and by using network protocol optimizations.

Amazon S3 Transfer Acceleration is a feature that speeds up file transfers between clients and Amazon S3 buckets, especially over long distances. It achieves this by routing data through Amazon CloudFront's globally distributed Edge Locations, utilizing the AWS backbone network for optimized performance.

 
S3TA helps reduce network variability by physically shortening the distance between your apps and AWS. Any question that speaks to long-distance uploads, or finding ways to increase data transfer with S3 – consider S3TA.

