## 📝 Practice Exercises

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

### 3. **Conditional S3 Access by IP**

A **role** should be able to list and read objects from a bucket, but only if the connection comes from your office IP (e.g., `203.0.113.0/24`).

#### ✅ Checklist:
- [ ] Research IAM roles and their characteristics
- [ ] Identify required S3 permissions for listing and reading
- [ ] Research IP-based access control conditions in IAM
- [ ] Implement the policy with IP restrictions
- [ ] Test access from different IP ranges

---

### 4. **VPC Creation Access but No Deletion**

Allow a **user** to create new VPCs and subnets, but explicitly deny the action to delete them.

#### ✅ Checklist:
- [ ] Research EC2 VPC and subnet permissions
- [ ] Understand the difference between allow and deny effects
- [ ] Research how to implement explicit deny statements
- [ ] Implement policy with creation permissions and deletion denials
- [ ] Test both creation and deletion scenarios

---

### 5. **Route Tables Access Within Specific VPC**

Give a **role** permissions to manage route tables, but only within VPC `vpc-123456`.

#### ✅ Checklist:
- [ ] Research EC2 route table management permissions
- [ ] Understand VPC-specific access control conditions
- [ ] Research how to construct VPC ARNs for conditions
- [ ] Implement policy with VPC-specific restrictions
- [ ] Test operations in both allowed and denied VPCs

---

### 6. **NACLs Read-Only Control**

Grant a **security group** read-only access to Network Access Control Lists (NACLs) across all VPCs.

#### ✅ Checklist:
- [ ] Research NACL permissions and read-only access patterns
- [ ] Understand the difference between describe and modify permissions
- [ ] Research resource patterns for cross-VPC access
- [ ] Implement read-only policy for NACLs
- [ ] Test access across multiple VPCs

---

### 7. **Restricted Security Groups Access**

A **junior user** can modify rules in security groups, but cannot delete them or create new ones.

#### ✅ Checklist:
- [ ] Research security group management permissions
- [ ] Understand the difference between rule modification and group management
- [ ] Research how to implement granular permission restrictions
- [ ] Implement policy allowing rule changes but preventing group management
- [ ] Test both allowed and denied operations

---

### 8. **S3 Bucket Accessible Only via Role**

Create a policy so that **only a specific role** (e.g., `FinanceRole`) can upload files to the `finance-reports` bucket.

#### ✅ Checklist:
- [ ] Research S3 bucket policies vs IAM policies
- [ ] Understand role-based access control in S3
- [ ] Research how to specify role principals in bucket policies
- [ ] Implement bucket policy with role-specific access
- [ ] Test access with the specified role and verify others are denied

---

### 9. **Tag-Based Access in VPC**

Allow a **group** to manage subnets, but only if they have the tag `"Environment": "Dev"`.

#### ✅ Checklist:
- [ ] Research tag-based access control in AWS
- [ ] Understand EC2 subnet management permissions
- [ ] Research how to implement resource tag conditions
- [ ] Implement policy with tag-based restrictions
- [ ] Test operations on resources with and without required tags

---

### 10. **Deny Bucket Access Except for One User**

Create an **explicit denial policy** for all users in a group, except one (`JuanDev`), who should be able to access the bucket.

#### ✅ Checklist:
- [ ] Research explicit deny policies and their precedence
- [ ] Understand username-based access control conditions
- [ ] Research how to implement user exceptions in deny policies
- [ ] Implement deny policy with user exception
- [ ] Test access for both the exception user and group members

---

### 11. **S3 Access Only with MFA Enabled**

Allow a **user** to access S3 objects only if they logged in with MFA.

#### ✅ Checklist:
- [ ] Research MFA implementation in AWS IAM
- [ ] Understand MFA-based access control conditions
- [ ] Research how to configure MFA for users
- [ ] Implement policy requiring MFA authentication
- [ ] Test access with and without MFA enabled

---

### 12. **Internet Gateways Management**

A **network role** should be able to attach and detach internet gateways to a VPC, but not create or delete them.

#### ✅ Checklist:
- [ ] Research internet gateway management permissions
- [ ] Understand the difference between gateway lifecycle and attachment operations
- [ ] Research how to implement selective permission grants
- [ ] Implement policy allowing attachment but preventing lifecycle management
- [ ] Test both allowed and denied operations

---

### 13. **Peering Connections Management**

Grant permissions to an **architects group** to create and accept peering connections between VPCs.

#### ✅ Checklist:
- [ ] Research VPC peering connection permissions
- [ ] Understand the difference between creating and accepting peering connections
- [ ] Research cross-account peering considerations
- [ ] Implement policy for peering connection management
- [ ] Test peering operations and cross-account scenarios

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

### 15. **Multiple Access Combination**

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
