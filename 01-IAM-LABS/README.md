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
- Resource-based policies (bucket policies)
- IAM permissions boundaries

**Prerequisites:** Basic understanding of AWS services (S3, VPC, EC2)
**Estimated time:** 2-3 hours per exercise
**Key skills developed:** Policy writing, resource ARN construction, basic security principles

### 1. **Full S3 Access Within Account Only** *(Identity-Based Policy)*

Create a policy that allows a **specific user** complete access to all S3 buckets.

#### 📋 **Solution Implementation:**

**Policy File:** [`01-FullS3AccessWithinAccountOnly.json`](01-FullS3AccessWithinAccountOnly.json)

This policy implements user-specific S3 access with the following key features:
- **Full S3 permissions** using `s3:*` action
- **User restriction** via `aws:username` condition targeting user "labs2"
- **Global resource access** with `"Resource": "*"` for all S3 buckets
- **Conditional access** ensuring only the specified user can perform S3 operations

#### ✅ Checklist:
- [x] Research IAM policy structure for S3 access
- [x] Implement policy that restricts access.
- [x] Test the policy implementation

---

### 2. **S3 Read-Only Access Restricted by Prefix** *(Identity-Based Policy)*

Grant a **group** read-only access to objects within a bucket, but only if they start with `2025/`.

#### 📋 **Solution Implementation:**

**Policy File:** [`02-S3ReadOnlyAccessRestrictedbyPrefix.json`](02-S3ReadOnlyAccessRestrictedbyPrefix.json)

This policy implements prefix-based S3 access control with three distinct statements:
- **Bucket listing** with `s3:ListAllMyBuckets` for general bucket discovery
- **Prefix-restricted listing** using `s3:ListBucket` with `StringLike` condition for `2025/*` prefix
- **Object access** limited to `2025/*` objects with comprehensive read permissions including `GetObject`, `GetObjectAcl`, `GetObjectAttributes`, and versioning support

#### ✅ Checklist:
- [x] Research IAM groups and their use cases
- [x] Identify required S3 permissions for read-only access
- [x] Research S3 prefix-based access control conditions
- [x] Implement the policy with proper conditions
- [x] Test both allowed and denied access scenarios

---

### 3. **VPC Creation Access but No Deletion** *(Identity-Based Policy)*

Allow a **user** to create new VPCs and subnets, but explicitly deny the action to delete them.

#### 📋 **Solution Implementation:**

**Policy File:** [`03-VpcCreationAccessbutNoDeletion.json`](03-VpcCreationAccessbutNoDeletion.json)

This policy implements selective VPC management with three key components:
- **Read permissions** with `ec2:Describe*` and `ec2:GetSubnetCidrReservations` for VPC discovery and information
- **Creation permissions** allowing `ec2:CreateVpc`, `ec2:CreateTags`, and `ec2:CreateSubnet` for infrastructure setup
- **Explicit denial** of deletion operations including `ec2:DeleteVpc`, `ec2:DeleteSubnet`, `ec2:DeleteInternetGateway`, `ec2:DeleteRouteTable`, and `ec2:DeleteSecurityGroup`

#### ✅ Checklist:
- [x] Research EC2 VPC and subnet permissions
- [x] Understand the difference between allow and deny effects
- [x] Research how to implement explicit deny statements
- [x] Implement policy with creation permissions and deletion denials
- [x] Test both creation and deletion scenarios

---

### 4. **NACLs Read-Only Control** *(Identity-Based Policy)*

Grant a **user, user group or role** read-only access to Network Access Control Lists (NACLs) across all VPCs.

#### 📋 **Solution Implementation:**

**Policy File:** [`04-NaclsReadOnlyControl.json`](04-NaclsReadOnlyControl.json)

This policy implements comprehensive read-only access to NACLs with the following features:
- **VPC discovery** with `ec2:DescribeVpcs` to list and identify VPCs
- **NACL information** using `ec2:DescribeNetworkAcls` for reading NACL configurations
- **Subnet context** with `ec2:DescribeSubnets` to understand NACL associations
- **Cross-VPC access** using `"Resource": "*"` to enable access across all VPCs in the account
- **Read-only design** ensuring no modification permissions are granted

#### ✅ Checklist:
- [x] Research NACL permissions and read-only access patterns
- [x] Understand the difference between describe and modify permissions
- [x] Research resource patterns for cross-VPC access
- [x] Implement read-only policy for NACLs
- [x] Test access across multiple VPCs

---

### 5. **S3 Bucket Accessible Only via Role** *(Resource-Based Policy)*

Create a policy so that **only a specific role** (e.g., `FinanceRole`) can upload files to the `finance-reports` bucket.

#### 📋 **Solution Implementation:**

This exercise requires a **multi-policy approach** to implement role-based S3 access:

1. **Identity Policy for Role Assumption** - [`05-S3BucketAccessibleOnlyViaRole-AssumeRoleIdentityPolicy.json`](05-S3BucketAccessibleOnlyViaRole-AssumeRoleIdentityPolicy.json)
   - Allows users to assume the `FinanceRole`
   - Uses `sts:AssumeRole` action with specific role ARN

2. **Role Trust Policy** - [`05-S3BucketAccessibleOnlyViaRole-FinanceRoleTrustPolicy.json`](05-S3BucketAccessibleOnlyViaRole-FinanceRoleTrustPolicy.json)
   - Defines who can assume the `FinanceRole`
   - Trusts the AWS account root to assume the role

3. **S3 Bucket Policy** - [`05-S3BucketAccessibleOnlyViaRole-BucketPolicy.json`](05-S3BucketAccessibleOnlyViaRole-BucketPolicy.json)
   - Resource-based policy attached to the S3 bucket
   - Allows only the `FinanceRole` to perform S3 operations
   - Grants `ListBucket`, `ListBucketMultipartUploads`, `ListBucketVersions`, and `PutObject` permissions

4. **Role Identity Policy** - [`05-S3BucketAccessibleOnlyViaRole-S3Read&WriteIdentityPolicy.json`](05-S3BucketAccessibleOnlyViaRole-S3Read&WriteIdentityPolicy.json)
   - Attached to the `FinanceRole` for S3 permissions
   - Provides `PutObject` and bucket listing capabilities
   - Ensures the role has necessary permissions when assumed

#### ✅ Checklist:
- [x] Research S3 bucket policies vs IAM policies
- [x] Understand role-based access control in S3
- [x] Research how to specify role principals in bucket policies
- [x] Implement bucket policy with role-specific access
- [x] Test access with the specified role and verify others are denied

---

### 6. **Internet Gateways Management** *(Identity-Based Policy)*

A **network role** should be able to attach and detach internet gateways to a VPC, but not create or delete them.

#### 📋 **Solution Implementation:**

**Policy File:** [`06-InternetGatewaysManagement.json`](06-InternetGatewaysManagement.json)

This policy implements selective Internet Gateway management with three key components:
- **Discovery permissions** with `ec2:Describe*` for listing and identifying existing Internet Gateways and VPCs
- **Attachment operations** allowing `ec2:AttachInternetGateway` and `ec2:DetachInternetGateway` for connecting/disconnecting gateways to VPCs
- **Explicit denial** of lifecycle operations including `ec2:CreateInternetGateway` and `ec2:DeleteInternetGateway` to prevent gateway creation and deletion
- **Selective access control** that separates operational management from resource lifecycle management

#### ✅ Checklist:
- [x] Research internet gateway management permissions
- [x] Understand the difference between gateway lifecycle and attachment operations
- [x] Research how to implement selective permission grants
- [x] Implement policy allowing attachment but preventing lifecycle management
- [x] Test both allowed and denied operations

---

### 7. **Multiple Access Combination to Audit** *(Identity-Based Policy)*

An **auditor role** can:

* Read objects in all S3 buckets.
* View VPC, subnets, and route table configurations.
* Cannot modify anything.

#### 📋 **Solution Implementation:**

This exercise implements a **multi-policy audit solution** for comprehensive read-only access:

1. **Identity Policy for Role Assumption** - [`07-MultipleAccessCombinationToAudit-AssumeRoleIdentityPolicy.json`](07-MultipleAccessCombinationToAudit-AssumeRoleIdentityPolicy.json)
   - Allows users to assume the `AuditorRole`
   - Uses `sts:AssumeRole` action with specific role ARN

2. **Role Trust Policy** - [`07-MultipleAccessCombinationToAudit-AuditorRoleTrustPolicy.json`](07-MultipleAccessCombinationToAudit-AuditorRoleTrustPolicy.json)
   - Defines who can assume the `AuditorRole`
   - Trusts the AWS account root to assume the role

3. **Auditor Role Identity Policy** - [`07-MultipleAccessCombinationToAudit-AuditorIdentityPolicy.json`](07-MultipleAccessCombinationToAudit-AuditorIdentityPolicy.json)
   - **VPC Discovery**: `ec2:Describe*` for comprehensive VPC, subnet, and route table information
   - **S3 Discovery**: `s3:List*` for listing all buckets and their contents
   - **Read-only design**: Only describe and list permissions, no modification capabilities
   - **Multi-service access**: Combines EC2 and S3 permissions for comprehensive auditing

#### ✅ Checklist:
- [x] Research read-only access patterns across multiple AWS services
- [x] Understand the scope of describe vs modify permissions
- [x] Research how to implement comprehensive read-only access
- [x] Implement policy combining multiple service read permissions
- [x] Test read access across all specified services and verify write operations are denied

---

### 8. **S3 Bucket Policy for Cross-Account Access** *(Resource-Based Policy)*

Create a **resource-based policy** (bucket policy) that allows a specific external account (`123456789012`) to read objects from your bucket, but only from objects with the prefix `shared/`.

#### ✅ Checklist:
- [ ] Research S3 bucket policies vs IAM policies
- [ ] Understand cross-account access patterns in bucket policies
- [ ] Research how to specify external account principals
- [ ] Implement bucket policy with cross-account access and prefix restrictions
- [ ] Test access from the external account and verify other accounts are denied

---

### 9. **IAM Permissions Boundary for Delegated Access** *(Permissions Boundary)*

Create a **permissions boundary** that limits a delegated administrator to only manage IAM users and groups, but cannot create or delete roles or policies.

#### 📋 **Solution Implementation:**

This exercise implements a **two-policy approach** for delegated IAM administration:

1. **Identity Policy for Full IAM Access** - [`09-IamFullManagement-IdentityPolicy.json`](09-IamFullManagement-IdentityPolicy.json)
   - Grants comprehensive IAM permissions with `iam:*` action
   - Provides the base permissions needed for IAM management
   - Uses `"Resource": "*"` for account-wide IAM access

2. **Permissions Boundary Policy** - [`09-IamFullManagementBoundary-IdentityPolicy.json`](09-IamFullManagementBoundary-IdentityPolicy.json)
   - **Restricts scope** to only user and group management with `iam:*User*` and `iam:*Group*` actions
   - **Prevents role/policy management** by excluding `iam:*Role*` and `iam:*Policy*` actions
   - **Enforces delegation limits** ensuring the administrator cannot create or delete roles or policies
   - **Maintains user/group control** while preventing privilege escalation

#### ✅ Checklist:
- [x] Research IAM permissions boundaries and their purpose
- [x] Understand the difference between permissions boundaries and policies
- [x] Research how to implement granular IAM management restrictions
- [x] Implement permissions boundary for delegated IAM administration
- [x] Test boundary enforcement and verify role/policy management is denied

---

## 🟡 Intermediate - Advanced Concepts

**Ideal for practitioners** with some IAM experience who want to master conditional access controls and complex permission scenarios. These exercises introduce advanced IAM features and multi-service interactions.

**What you'll learn:**
- Conditional access controls (IP, time, MFA, tags)
- Policy precedence and explicit deny patterns
- Cross-service permission management
- Advanced S3 and VPC features
- Complex role and group management
- Session policies for temporary access
- Organization Service Control Policies (SCPs)
- Advanced resource-based policies

**Prerequisites:** Completion of Easy exercises or equivalent IAM experience
**Estimated time:** 3-4 hours per exercise
**Key skills developed:** Conditional logic, policy optimization, service integration, security best practices

### 10. **Conditional S3 Access by IP** *(Identity-Based Policy & Resource-Based Policy)*

A **role** should be able to list and read objects from a bucket, but only if the connection comes from your office IP (e.g., `203.0.113.0/24`).

**Variant A (Identity-Based Policy):** Apply the IP condition inside the IAM role's identity policy. This means the role can only list and read objects if the request comes from the allowed IP range(s).

**Variant B (Bucket Policy):** Apply the IP condition inside the S3 bucket policy itself. This ensures the bucket enforces the restriction regardless of which IAM role or user tries to access it.

#### ✅ Checklist:
- [ ] Research IAM roles and their characteristics
- [ ] Identify required S3 permissions for listing and reading
- [ ] Research IP-based access control conditions in IAM
- [ ] Research the difference between identity-based and resource-based IP restrictions
- [ ] Implement Variant A: Identity-based policy with IP restrictions
- [ ] Implement Variant B: Bucket policy with IP restrictions
- [ ] Test access from different IP ranges for both variants
- [ ] Compare the security implications of each approach

---

### 11. **Route Tables Access Within Specific VPC** *(Identity-Based Policy)*

Give a **role** permissions to manage route tables, but only within VPC `vpc-123456`.

#### ✅ Checklist:
- [ ] Research EC2 route table management permissions
- [ ] Understand VPC-specific access control conditions
- [ ] Research how to construct VPC ARNs for conditions
- [ ] Implement policy with VPC-specific restrictions
- [ ] Test operations in both allowed and denied VPCs

---

### 12. **Tag-Based Access in VPC** *(Identity-Based Policy)*

Allow a **group** to manage subnets, but only if they have the tag `"Environment": "Dev"`.

#### ✅ Checklist:
- [ ] Research tag-based access control in AWS
- [ ] Understand EC2 subnet management permissions
- [ ] Research how to implement resource tag conditions
- [ ] Implement policy with tag-based restrictions
- [ ] Test operations on resources with and without required tags

---

### 13. **Deny Bucket Access Except for One User** *(Identity-Based Policy)*

Create an **explicit denial policy** for all users in a group, except one (`JuanDev`), who should be able to access the bucket.

#### ✅ Checklist:
- [ ] Research explicit deny policies and their precedence
- [ ] Understand username-based access control conditions
- [ ] Research how to implement user exceptions in deny policies
- [ ] Implement deny policy with user exception
- [ ] Test access for both the exception user and group members

---

### 14. **S3 Access Only with MFA Enabled** *(Identity-Based Policy)*

Allow a **user** to access S3 objects only if they logged in with MFA.

#### ✅ Checklist:
- [ ] Research MFA implementation in AWS IAM
- [ ] Understand MFA-based access control conditions
- [ ] Research how to configure MFA for users
- [ ] Implement policy requiring MFA authentication
- [ ] Test access with and without MFA enabled

---

### 15. **S3 Access with Time Condition** *(Identity-Based Policy)*

A **temporary user** can access an S3 bucket only during business hours (e.g., 9 AM to 6 PM UTC).

#### ✅ Checklist:
- [ ] Research time-based access control in AWS IAM
- [ ] Understand date/time condition operators
- [ ] Research timezone handling in IAM policies
- [ ] Implement policy with time-based restrictions
- [ ] Test access during and outside allowed time periods

---

### 16. **S3 Bucket Versioning and Lifecycle Management** *(Identity-Based Policy)*

A **data management role** can manage S3 bucket versioning and lifecycle policies, but cannot delete objects or modify bucket settings.

#### ✅ Checklist:
- [ ] Research S3 versioning and lifecycle management permissions
- [ ] Understand the difference between object-level and bucket-level permissions
- [ ] Research how to implement granular S3 management permissions
- [ ] Implement policy allowing versioning and lifecycle management
- [ ] Test versioning operations and verify deletion is denied

---

### 17. **VPC Flow Logs Management** *(Identity-Based Policy)*

A **network monitoring group** can create, modify, and delete VPC Flow Logs, but cannot access the actual log data stored in S3.

#### ✅ Checklist:
- [ ] Research VPC Flow Logs permissions and requirements
- [ ] Understand the relationship between VPC Flow Logs and S3 storage
- [ ] Research how to separate Flow Logs management from data access
- [ ] Implement policy for Flow Logs management without S3 access
- [ ] Test Flow Logs operations and verify S3 access is denied

---

### 18. **VPC Endpoints for S3 Access** *(Identity-Based Policy)*

A **network architect** can create and manage VPC endpoints for S3, but cannot modify the VPC's route tables or security groups.

#### ✅ Checklist:
- [ ] Research VPC endpoint permissions and requirements
- [ ] Understand the relationship between VPC endpoints and routing
- [ ] Research how to separate endpoint management from network configuration
- [ ] Implement policy for VPC endpoint management
- [ ] Test endpoint creation and verify network modification is denied

---

### 19. **VPC Peering Route Management** *(Identity-Based Policy)*

A **network engineer** can manage routes in VPC peering connections, but cannot create or delete the peering connections themselves.

#### ✅ Checklist:
- [ ] Research VPC peering route management permissions
- [ ] Understand the difference between peering lifecycle and route management
- [ ] Research how to implement route-specific access controls
- [ ] Implement policy for route management without peering control
- [ ] Test route operations and verify peering lifecycle is denied

---

### 20. **Session Policy for Temporary S3 Access** *(Session Policy)*

Create a **session policy** that allows temporary access to S3 objects for a specific duration (e.g., 2 hours), with read-only permissions and IP restrictions.

#### ✅ Checklist:
- [ ] Research session policies and their use cases
- [ ] Understand the difference between session policies and regular IAM policies
- [ ] Research how to implement time-limited access controls
- [ ] Implement session policy with duration and IP restrictions
- [ ] Test session expiration and access revocation

---

### 21. **Organization SCP for Service Restrictions** *(Organization SCP)*

Create an **Organization Service Control Policy (SCP)** that prevents member accounts from creating or deleting IAM roles, while allowing them to manage users and groups.

#### ✅ Checklist:
- [ ] Research Organization SCPs and their purpose
- [ ] Understand the difference between SCPs and regular IAM policies
- [ ] Research how to implement service-level restrictions across accounts
- [ ] Implement SCP restricting IAM role management
- [ ] Test SCP enforcement in member accounts

---

### 22. **Cross-Account Resource-Based Policy** *(Resource-Based Policy)*

Create a **resource-based policy** for an S3 bucket that allows multiple external accounts to assume a specific role and access objects, but only during business hours.

#### ✅ Checklist:
- [ ] Research cross-account role assumption in resource policies
- [ ] Understand the relationship between resource policies and role assumption
- [ ] Research how to implement time-based conditions in resource policies
- [ ] Implement cross-account resource policy with time restrictions
- [ ] Test role assumption and time-based access controls

---

### 23. **Permissions Boundary for Cross-Service Access** *(Permissions Boundary)*

Create a **permissions boundary** that allows a role to access both S3 and DynamoDB, but prevents access to any other AWS services.

#### ✅ Checklist:
- [ ] Research permissions boundaries for multi-service access
- [ ] Understand how to implement service-specific restrictions in boundaries
- [ ] Research the interaction between boundaries and service policies
- [ ] Implement permissions boundary restricting access to specific services
- [ ] Test boundary enforcement across multiple services

---

## 🔴 Hard - Expert Level

**Designed for experienced professionals** preparing for advanced AWS certifications or implementing complex enterprise security requirements. These exercises challenge you with real-world scenarios involving multiple services and sophisticated access control patterns.

**What you'll learn:**
- Multi-service integration and complex permission orchestration
- Advanced AWS service features (encryption, replication, compliance)
- Cross-account and cross-region access patterns
- Enterprise security and compliance requirements
- Troubleshooting complex IAM scenarios
- Advanced Organization SCPs with conditions
- Complex session policies with multiple security controls
- Cross-account permissions boundaries
- Enterprise resource-based policies with encryption

**Prerequisites:** Completion of Intermediate exercises or 2+ years of AWS IAM experience
**Estimated time:** 4-6 hours per exercise
**Key skills developed:** Enterprise architecture, compliance design, advanced troubleshooting, security governance

### 24. **Peering Connections Management** *(Identity-Based Policy)*

Grant permissions to an **architects group** to create and accept peering connections between VPCs.

#### ✅ Checklist:
- [ ] Research VPC peering connection permissions
- [ ] Understand the difference between creating and accepting peering connections
- [ ] Research cross-account peering considerations
- [ ] Implement policy for peering connection management
- [ ] Test peering operations and cross-account scenarios

---

### 25. **S3 Cross-Region Replication Control** *(Identity-Based Policy)*

A **backup administrator** can configure S3 cross-region replication between specific buckets, but cannot modify the source bucket's replication settings.

#### ✅ Checklist:
- [ ] Research S3 cross-region replication permissions
- [ ] Understand the difference between source and destination bucket permissions
- [ ] Research how to implement replication-specific access controls
- [ ] Implement policy for replication configuration without source modification
- [ ] Test replication setup and verify source bucket protection

---

### 26. **S3 Bucket Encryption Management** *(Identity-Based Policy)*

A **security officer** can manage S3 bucket encryption settings and KMS keys, but cannot access the encrypted objects or modify bucket policies.

#### ✅ Checklist:
- [ ] Research S3 encryption and KMS permissions
- [ ] Understand the difference between encryption management and data access
- [ ] Research how to implement encryption-specific access controls
- [ ] Implement policy for encryption management without data access
- [ ] Test encryption operations and verify data access is denied

---

### 27. **S3 Transfer Acceleration Control** *(Identity-Based Policy)*

A **performance engineer** can enable and configure S3 Transfer Acceleration, but cannot modify bucket policies or access the accelerated endpoints.

#### ✅ Checklist:
- [ ] Research S3 Transfer Acceleration permissions
- [ ] Understand the relationship between acceleration and bucket policies
- [ ] Research how to implement acceleration-specific access controls
- [ ] Implement policy for acceleration management without policy access
- [ ] Test acceleration configuration and verify policy modification is denied

---

### 28. **VPC DNS Resolution Management** *(Identity-Based Policy)*

A **DNS administrator** can manage VPC DNS resolution settings and Route 53 private hosted zones, but cannot modify VPC peering or transit gateway configurations.

#### ✅ Checklist:
- [ ] Research VPC DNS and Route 53 private hosted zone permissions
- [ ] Understand the relationship between DNS management and VPC networking
- [ ] Research how to separate DNS management from network configuration
- [ ] Implement policy for DNS management without network modification
- [ ] Test DNS operations and verify network configuration is denied

---

### 29. **S3 Object Lock and Retention** *(Identity-Based Policy)*

A **compliance officer** can configure S3 Object Lock and retention policies, but cannot modify existing locked objects or change bucket versioning settings.

#### ✅ Checklist:
- [ ] Research S3 Object Lock and retention permissions
- [ ] Understand the relationship between Object Lock and versioning
- [ ] Research how to implement compliance-specific access controls
- [ ] Implement policy for Object Lock management without object modification
- [ ] Test Object Lock operations and verify object modification is denied

---

### 30. **VPC Transit Gateway Management** *(Identity-Based Policy)*

A **network architect** can create and manage VPC Transit Gateway attachments, but cannot modify the attached VPCs or their route tables.

#### ✅ Checklist:
- [ ] Research VPC Transit Gateway permissions and requirements
- [ ] Understand the relationship between Transit Gateway and VPC management
- [ ] Research how to separate Transit Gateway management from VPC control
- [ ] Implement policy for Transit Gateway management without VPC modification
- [ ] Test Transit Gateway operations and verify VPC modification is denied

---

### 31. **Advanced Organization SCP with Conditions** *(Organization SCP)*

Create an **Organization SCP** that allows member accounts to create S3 buckets only if they have specific tags (`Environment: Production` or `Environment: Development`), and prevents creation of buckets without these tags.

#### ✅ Checklist:
- [ ] Research advanced SCP conditions and tag-based restrictions
- [ ] Understand how to implement conditional logic in Organization SCPs
- [ ] Research tag-based access control in SCPs
- [ ] Implement SCP with tag-based bucket creation restrictions
- [ ] Test SCP enforcement with different tag combinations

---

### 32. **Complex Session Policy with MFA and Time** *(Session Policy)*

Create a **session policy** that requires MFA authentication and allows access to sensitive S3 objects only during business hours (9 AM - 5 PM UTC) and from specific IP ranges.

#### ✅ Checklist:
- [ ] Research session policies with multiple conditions
- [ ] Understand how to combine MFA, time, and IP restrictions in session policies
- [ ] Research the interaction between session policies and MFA requirements
- [ ] Implement complex session policy with multiple security conditions
- [ ] Test policy enforcement under different authentication and time scenarios

---

### 33. **Cross-Account Permissions Boundary** *(Permissions Boundary)*

Create a **permissions boundary** that allows a cross-account role to access resources in multiple accounts, but restricts the actions to read-only operations and limits access to specific resource types.

#### ✅ Checklist:
- [ ] Research cross-account permissions boundaries
- [ ] Understand how permissions boundaries work across multiple accounts
- [ ] Research how to implement action and resource restrictions in cross-account scenarios
- [ ] Implement cross-account permissions boundary with read-only restrictions
- [ ] Test boundary enforcement across multiple accounts

---

### 34. **Enterprise Resource-Based Policy with Encryption** *(Resource-Based Policy)*

Create a **resource-based policy** for an S3 bucket that allows external accounts to access objects only if they are encrypted with a specific KMS key, and includes audit logging requirements.

#### ✅ Checklist:
- [ ] Research resource-based policies with encryption requirements
- [ ] Understand the relationship between S3 bucket policies and KMS encryption
- [ ] Research how to implement encryption-based access controls in resource policies
- [ ] Implement resource policy requiring specific KMS encryption
- [ ] Test access with different encryption keys and verify audit logging
