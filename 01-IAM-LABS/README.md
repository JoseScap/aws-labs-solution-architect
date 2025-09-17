# 📝 Practice Exercises

## 🎯 Learning Approach

**Progressive Learning Path**: These exercises are designed to be completed progressively, not all at once. Each section builds upon the previous one, requiring specific knowledge and skills that are developed through the exercises.

**How to use this lab:**
- **Start with Easy exercises** to build a solid foundation
- **Complete at least 6-8 Easy exercises** before moving to Intermediate
- **Master Intermediate concepts** before attempting Hard exercises
- **Focus on understanding** rather than rushing through exercises
- **Take breaks** between sections to consolidate learning

**Remember**: Each section has minimum requirements. Don't skip ahead - the knowledge you gain in earlier exercises is essential for success in more advanced scenarios.

## 🟢 Easy - Foundation Level

**Perfect for beginners** who are new to AWS IAM or need to solidify their understanding of basic concepts. These exercises focus on fundamental IAM principles and simple permission patterns.

**What you'll learn:**
- Basic IAM policy structure and syntax
- Simple allow/deny permission patterns
- Single-service access controls
- Fundamental S3 and VPC permissions
- Basic role-based access control

**Prerequisites:** Basic understanding of AWS services (S3, VPC, EC2)
**Estimated time:** 2-3 hours per exercise
**Key skills developed:** Policy writing, resource ARN construction, basic security principles

### 1. **Full S3 Access Within Account Only**

Create a policy that allows a **specific user** complete access to all S3 buckets within the account, but not to buckets from other accounts.

#### ✅ Checklist:
- [ ] Research IAM policy structure for S3 access
- [ ] Identify correct resource ARN pattern for account-level access
- [ ] Implement policy that restricts access to current account only
- [ ] Test the policy implementation
- [ ] Verify cross-account access is properly denied

---

### 2. **S3 Read-Only Access Restricted by Prefix**

Grant a **group** read-only access to objects within a bucket, but only if they start with `reports/2025/`.

#### ✅ Checklist:
- [ ] Research IAM groups and their use cases
- [ ] Identify required S3 permissions for read-only access
- [ ] Research S3 prefix-based access control conditions
- [ ] Implement the policy with proper conditions
- [ ] Test both allowed and denied access scenarios

---

### 3. **VPC Creation Access but No Deletion**

Allow a **user** to create new VPCs and subnets, but explicitly deny the action to delete them.

#### ✅ Checklist:
- [ ] Research EC2 VPC and subnet permissions
- [ ] Understand the difference between allow and deny effects
- [ ] Research how to implement explicit deny statements
- [ ] Implement policy with creation permissions and deletion denials
- [ ] Test both creation and deletion scenarios

---

### 4. **NACLs Read-Only Control**

Grant a **security group** read-only access to Network Access Control Lists (NACLs) across all VPCs.

#### ✅ Checklist:
- [ ] Research NACL permissions and read-only access patterns
- [ ] Understand the difference between describe and modify permissions
- [ ] Research resource patterns for cross-VPC access
- [ ] Implement read-only policy for NACLs
- [ ] Test access across multiple VPCs

---

### 5. **Restricted Security Groups Access**

A **junior user** can modify rules in security groups, but cannot delete them or create new ones.

#### ✅ Checklist:
- [ ] Research security group management permissions
- [ ] Understand the difference between rule modification and group management
- [ ] Research how to implement granular permission restrictions
- [ ] Implement policy allowing rule changes but preventing group management
- [ ] Test both allowed and denied operations

---

### 6. **S3 Bucket Accessible Only via Role**

Create a policy so that **only a specific role** (e.g., `FinanceRole`) can upload files to the `finance-reports` bucket.

#### ✅ Checklist:
- [ ] Research S3 bucket policies vs IAM policies
- [ ] Understand role-based access control in S3
- [ ] Research how to specify role principals in bucket policies
- [ ] Implement bucket policy with role-specific access
- [ ] Test access with the specified role and verify others are denied

---

### 7. **Internet Gateways Management**

A **network role** should be able to attach and detach internet gateways to a VPC, but not create or delete them.

#### ✅ Checklist:
- [ ] Research internet gateway management permissions
- [ ] Understand the difference between gateway lifecycle and attachment operations
- [ ] Research how to implement selective permission grants
- [ ] Implement policy allowing attachment but preventing lifecycle management
- [ ] Test both allowed and denied operations

---

### 8. **Multiple Access Combination**

An **auditor role** can:

* Read objects in all S3 buckets.
* View VPC, subnets, and route table configurations.
* Cannot modify anything.

#### ✅ Checklist:
- [ ] Research read-only access patterns across multiple AWS services
- [ ] Understand the scope of describe vs modify permissions
- [ ] Research how to implement comprehensive read-only access
- [ ] Implement policy combining multiple service read permissions
- [ ] Test read access across all specified services and verify write operations are denied

---

## 🟡 Intermediate - Advanced Concepts

**Ideal for practitioners** with some IAM experience who want to master conditional access controls and complex permission scenarios. These exercises introduce advanced IAM features and multi-service interactions.

**What you'll learn:**
- Conditional access controls (IP, time, MFA, tags)
- Policy precedence and explicit deny patterns
- Cross-service permission management
- Advanced S3 and VPC features
- Complex role and group management

**Prerequisites:** Completion of Easy exercises or equivalent IAM experience
**Estimated time:** 3-4 hours per exercise
**Key skills developed:** Conditional logic, policy optimization, service integration, security best practices

### 9. **Conditional S3 Access by IP**

A **role** should be able to list and read objects from a bucket, but only if the connection comes from your office IP (e.g., `203.0.113.0/24`).

#### ✅ Checklist:
- [ ] Research IAM roles and their characteristics
- [ ] Identify required S3 permissions for listing and reading
- [ ] Research IP-based access control conditions in IAM
- [ ] Implement the policy with IP restrictions
- [ ] Test access from different IP ranges

---

### 10. **Route Tables Access Within Specific VPC**

Give a **role** permissions to manage route tables, but only within VPC `vpc-123456`.

#### ✅ Checklist:
- [ ] Research EC2 route table management permissions
- [ ] Understand VPC-specific access control conditions
- [ ] Research how to construct VPC ARNs for conditions
- [ ] Implement policy with VPC-specific restrictions
- [ ] Test operations in both allowed and denied VPCs

---

### 11. **Tag-Based Access in VPC**

Allow a **group** to manage subnets, but only if they have the tag `"Environment": "Dev"`.

#### ✅ Checklist:
- [ ] Research tag-based access control in AWS
- [ ] Understand EC2 subnet management permissions
- [ ] Research how to implement resource tag conditions
- [ ] Implement policy with tag-based restrictions
- [ ] Test operations on resources with and without required tags

---

### 12. **Deny Bucket Access Except for One User**

Create an **explicit denial policy** for all users in a group, except one (`JuanDev`), who should be able to access the bucket.

#### ✅ Checklist:
- [ ] Research explicit deny policies and their precedence
- [ ] Understand username-based access control conditions
- [ ] Research how to implement user exceptions in deny policies
- [ ] Implement deny policy with user exception
- [ ] Test access for both the exception user and group members

---

### 13. **S3 Access Only with MFA Enabled**

Allow a **user** to access S3 objects only if they logged in with MFA.

#### ✅ Checklist:
- [ ] Research MFA implementation in AWS IAM
- [ ] Understand MFA-based access control conditions
- [ ] Research how to configure MFA for users
- [ ] Implement policy requiring MFA authentication
- [ ] Test access with and without MFA enabled

---

### 14. **S3 Access with Time Condition**

A **temporary user** can access an S3 bucket only during business hours (e.g., 9 AM to 6 PM UTC).

#### ✅ Checklist:
- [ ] Research time-based access control in AWS IAM
- [ ] Understand date/time condition operators
- [ ] Research timezone handling in IAM policies
- [ ] Implement policy with time-based restrictions
- [ ] Test access during and outside allowed time periods

---

### 15. **S3 Bucket Versioning and Lifecycle Management**

A **data management role** can manage S3 bucket versioning and lifecycle policies, but cannot delete objects or modify bucket settings.

#### ✅ Checklist:
- [ ] Research S3 versioning and lifecycle management permissions
- [ ] Understand the difference between object-level and bucket-level permissions
- [ ] Research how to implement granular S3 management permissions
- [ ] Implement policy allowing versioning and lifecycle management
- [ ] Test versioning operations and verify deletion is denied

---

### 16. **VPC Flow Logs Management**

A **network monitoring group** can create, modify, and delete VPC Flow Logs, but cannot access the actual log data stored in S3.

#### ✅ Checklist:
- [ ] Research VPC Flow Logs permissions and requirements
- [ ] Understand the relationship between VPC Flow Logs and S3 storage
- [ ] Research how to separate Flow Logs management from data access
- [ ] Implement policy for Flow Logs management without S3 access
- [ ] Test Flow Logs operations and verify S3 access is denied

---

### 17. **VPC Endpoints for S3 Access**

A **network architect** can create and manage VPC endpoints for S3, but cannot modify the VPC's route tables or security groups.

#### ✅ Checklist:
- [ ] Research VPC endpoint permissions and requirements
- [ ] Understand the relationship between VPC endpoints and routing
- [ ] Research how to separate endpoint management from network configuration
- [ ] Implement policy for VPC endpoint management
- [ ] Test endpoint creation and verify network modification is denied

---

### 18. **VPC Peering Route Management**

A **network engineer** can manage routes in VPC peering connections, but cannot create or delete the peering connections themselves.

#### ✅ Checklist:
- [ ] Research VPC peering route management permissions
- [ ] Understand the difference between peering lifecycle and route management
- [ ] Research how to implement route-specific access controls
- [ ] Implement policy for route management without peering control
- [ ] Test route operations and verify peering lifecycle is denied

---

## 🔴 Hard - Expert Level

**Designed for experienced professionals** preparing for advanced AWS certifications or implementing complex enterprise security requirements. These exercises challenge you with real-world scenarios involving multiple services and sophisticated access control patterns.

**What you'll learn:**
- Multi-service integration and complex permission orchestration
- Advanced AWS service features (encryption, replication, compliance)
- Cross-account and cross-region access patterns
- Enterprise security and compliance requirements
- Troubleshooting complex IAM scenarios

**Prerequisites:** Completion of Intermediate exercises or 2+ years of AWS IAM experience
**Estimated time:** 4-6 hours per exercise
**Key skills developed:** Enterprise architecture, compliance design, advanced troubleshooting, security governance

### 19. **Peering Connections Management**

Grant permissions to an **architects group** to create and accept peering connections between VPCs.

#### ✅ Checklist:
- [ ] Research VPC peering connection permissions
- [ ] Understand the difference between creating and accepting peering connections
- [ ] Research cross-account peering considerations
- [ ] Implement policy for peering connection management
- [ ] Test peering operations and cross-account scenarios

---

### 20. **S3 Cross-Region Replication Control**

A **backup administrator** can configure S3 cross-region replication between specific buckets, but cannot modify the source bucket's replication settings.

#### ✅ Checklist:
- [ ] Research S3 cross-region replication permissions
- [ ] Understand the difference between source and destination bucket permissions
- [ ] Research how to implement replication-specific access controls
- [ ] Implement policy for replication configuration without source modification
- [ ] Test replication setup and verify source bucket protection

---

### 21. **S3 Bucket Encryption Management**

A **security officer** can manage S3 bucket encryption settings and KMS keys, but cannot access the encrypted objects or modify bucket policies.

#### ✅ Checklist:
- [ ] Research S3 encryption and KMS permissions
- [ ] Understand the difference between encryption management and data access
- [ ] Research how to implement encryption-specific access controls
- [ ] Implement policy for encryption management without data access
- [ ] Test encryption operations and verify data access is denied

---

### 22. **S3 Transfer Acceleration Control**

A **performance engineer** can enable and configure S3 Transfer Acceleration, but cannot modify bucket policies or access the accelerated endpoints.

#### ✅ Checklist:
- [ ] Research S3 Transfer Acceleration permissions
- [ ] Understand the relationship between acceleration and bucket policies
- [ ] Research how to implement acceleration-specific access controls
- [ ] Implement policy for acceleration management without policy access
- [ ] Test acceleration configuration and verify policy modification is denied

---

### 23. **VPC DNS Resolution Management**

A **DNS administrator** can manage VPC DNS resolution settings and Route 53 private hosted zones, but cannot modify VPC peering or transit gateway configurations.

#### ✅ Checklist:
- [ ] Research VPC DNS and Route 53 private hosted zone permissions
- [ ] Understand the relationship between DNS management and VPC networking
- [ ] Research how to separate DNS management from network configuration
- [ ] Implement policy for DNS management without network modification
- [ ] Test DNS operations and verify network configuration is denied

---

### 24. **S3 Object Lock and Retention**

A **compliance officer** can configure S3 Object Lock and retention policies, but cannot modify existing locked objects or change bucket versioning settings.

#### ✅ Checklist:
- [ ] Research S3 Object Lock and retention permissions
- [ ] Understand the relationship between Object Lock and versioning
- [ ] Research how to implement compliance-specific access controls
- [ ] Implement policy for Object Lock management without object modification
- [ ] Test Object Lock operations and verify object modification is denied

---

### 25. **VPC Transit Gateway Management**

A **network architect** can create and manage VPC Transit Gateway attachments, but cannot modify the attached VPCs or their route tables.

#### ✅ Checklist:
- [ ] Research VPC Transit Gateway permissions and requirements
- [ ] Understand the relationship between Transit Gateway and VPC management
- [ ] Research how to separate Transit Gateway management from VPC control
- [ ] Implement policy for Transit Gateway management without VPC modification
- [ ] Test Transit Gateway operations and verify VPC modification is denied
