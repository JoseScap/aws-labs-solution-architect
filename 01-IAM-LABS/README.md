## 📝 Practice Exercises

### 1. **Full S3 Access Within Account Only**

Create a policy that allows a **specific user** complete access to all S3 buckets within the account, but not to buckets from other accounts.

#### ✅ Checklist:
- [ ] Create IAM policy with S3 permissions
- [ ] Use `"Resource": "arn:aws:s3:::*"` for account-level access
- [ ] Ensure policy doesn't grant cross-account access
- [ ] Test policy by creating/attaching to user
- [ ] Verify user can access S3 buckets in current account
- [ ] Verify user cannot access buckets from other accounts

---

### 2. **S3 Read-Only Access Restricted by Prefix**

Grant a **group** read-only access to objects within a bucket, but only if they start with `reports/2025/`.

#### ✅ Checklist:
- [ ] Create IAM group
- [ ] Create policy with `s3:GetObject` permission
- [ ] Use condition `"StringLike": {"s3:prefix": "reports/2025/*"}`
- [ ] Attach policy to group
- [ ] Add users to the group
- [ ] Test access to objects with correct prefix
- [ ] Test that access is denied for other prefixes

---

### 3. **Conditional S3 Access by IP**

A **role** should be able to list and read objects from a bucket, but only if the connection comes from your office IP (e.g., `203.0.113.0/24`).

#### ✅ Checklist:
- [ ] Create IAM role
- [ ] Create policy with S3 list and read permissions
- [ ] Add IP condition: `"IpAddress": {"aws:SourceIp": "203.0.113.0/24"}`
- [ ] Attach policy to role
- [ ] Test access from allowed IP range
- [ ] Test that access is denied from other IPs
- [ ] Document the office IP range

---

### 4. **VPC Creation Access but No Deletion**

Allow a **user** to create new VPCs and subnets, but explicitly deny the action to delete them.

#### ✅ Checklist:
- [ ] Create IAM policy with `ec2:CreateVpc` and `ec2:CreateSubnet` permissions
- [ ] Add explicit deny for `ec2:DeleteVpc` and `ec2:DeleteSubnet`
- [ ] Use `"Effect": "Deny"` for deletion actions
- [ ] Attach policy to user
- [ ] Test VPC and subnet creation
- [ ] Verify deletion attempts are denied
- [ ] Document the policy behavior

---

### 5. **Route Tables Access Within Specific VPC**

Give a **role** permissions to manage route tables, but only within VPC `vpc-123456`.

#### ✅ Checklist:
- [ ] Create IAM role
- [ ] Create policy with EC2 route table permissions
- [ ] Add condition: `"StringEquals": {"ec2:vpc": "arn:aws:ec2:region:account:vpc/vpc-123456"}`
- [ ] Include permissions: `ec2:CreateRoute`, `ec2:DeleteRoute`, `ec2:ModifyRouteTable`
- [ ] Attach policy to role
- [ ] Test route table operations in specified VPC
- [ ] Verify access is denied for other VPCs
- [ ] Update VPC ID to match your environment

---

### 6. **NACLs Read-Only Control**

Grant a **security group** read-only access to Network Access Control Lists (NACLs) across all VPCs.

#### ✅ Checklist:
- [ ] Create IAM group
- [ ] Create policy with `ec2:DescribeNetworkAcls` permission
- [ ] Use `"Resource": "*"` for all VPCs
- [ ] Attach policy to group
- [ ] Add users to the group
- [ ] Test NACL listing and description
- [ ] Verify users cannot modify NACLs
- [ ] Test across multiple VPCs

---

### 7. **Restricted Security Groups Access**

A **junior user** can modify rules in security groups, but cannot delete them or create new ones.

#### ✅ Checklist:
- [ ] Create IAM policy with `ec2:AuthorizeSecurityGroupIngress` and `ec2:AuthorizeSecurityGroupEgress`
- [ ] Add `ec2:RevokeSecurityGroupIngress` and `ec2:RevokeSecurityGroupEgress`
- [ ] Explicitly deny `ec2:CreateSecurityGroup` and `ec2:DeleteSecurityGroup`
- [ ] Attach policy to user
- [ ] Test security group rule modifications
- [ ] Verify creation and deletion are denied
- [ ] Document the restricted permissions

---

### 8. **S3 Bucket Accessible Only via Role**

Create a policy so that **only a specific role** (e.g., `FinanceRole`) can upload files to the `finance-reports` bucket.

#### ✅ Checklist:
- [ ] Create IAM role named `FinanceRole`
- [ ] Create bucket policy for `finance-reports` bucket
- [ ] Use `"Principal": {"AWS": "arn:aws:iam::account:role/FinanceRole"}`
- [ ] Grant `s3:PutObject` and `s3:PutObjectAcl` permissions
- [ ] Apply bucket policy to S3 bucket
- [ ] Test upload with the role
- [ ] Verify other users/roles cannot upload
- [ ] Document the role-based access

---

### 9. **Tag-Based Access in VPC**

Allow a **group** to manage subnets, but only if they have the tag `"Environment": "Dev"`.

#### ✅ Checklist:
- [ ] Create IAM group
- [ ] Create policy with subnet management permissions
- [ ] Add condition: `"StringEquals": {"ec2:ResourceTag/Environment": "Dev"}`
- [ ] Include permissions: `ec2:CreateSubnet`, `ec2:ModifySubnetAttribute`, `ec2:DeleteSubnet`
- [ ] Attach policy to group
- [ ] Test subnet operations on Dev-tagged resources
- [ ] Verify access is denied for non-Dev resources
- [ ] Document the tag-based access control

---

### 10. **Deny Bucket Access Except for One User**

Create an **explicit denial policy** for all users in a group, except one (`JuanDev`), who should be able to access the bucket.

#### ✅ Checklist:
- [ ] Create IAM group
- [ ] Create policy with `"Effect": "Deny"` for S3 access
- [ ] Add exception condition: `"StringNotEquals": {"aws:username": "JuanDev"}`
- [ ] Apply to all users in the group
- [ ] Create separate allow policy for JuanDev
- [ ] Test access for JuanDev (should work)
- [ ] Test access for other group members (should be denied)
- [ ] Document the exception-based access control

---

### 11. **S3 Access Only with MFA Enabled**

Allow a **user** to access S3 objects only if they logged in with MFA.

#### ✅ Checklist:
- [ ] Enable MFA for the user
- [ ] Create IAM policy with S3 permissions
- [ ] Add MFA condition: `"Bool": {"aws:MultiFactorAuthPresent": "true"}`
- [ ] Attach policy to user
- [ ] Test access with MFA authentication
- [ ] Verify access is denied without MFA
- [ ] Document MFA requirement
- [ ] Test with different S3 operations

---

### 12. **Internet Gateways Management**

A **network role** should be able to attach and detach internet gateways to a VPC, but not create or delete them.

#### ✅ Checklist:
- [ ] Create IAM role for network operations
- [ ] Create policy with `ec2:AttachInternetGateway` and `ec2:DetachInternetGateway`
- [ ] Explicitly deny `ec2:CreateInternetGateway` and `ec2:DeleteInternetGateway`
- [ ] Attach policy to role
- [ ] Test internet gateway attachment/detachment
- [ ] Verify creation and deletion are denied
- [ ] Test with different VPCs
- [ ] Document the restricted permissions

---

### 13. **Peering Connections Management**

Grant permissions to an **architects group** to create and accept peering connections between VPCs.

#### ✅ Checklist:
- [ ] Create IAM group for architects
- [ ] Create policy with peering permissions
- [ ] Include: `ec2:CreateVpcPeeringConnection`, `ec2:AcceptVpcPeeringConnection`
- [ ] Add: `ec2:DescribeVpcPeeringConnections` for visibility
- [ ] Attach policy to group
- [ ] Add users to the group
- [ ] Test peering connection creation
- [ ] Test peering connection acceptance
- [ ] Test across different AWS accounts if needed
- [ ] Document the peering workflow

---

### 14. **S3 Access with Time Condition**

A **temporary user** can access an S3 bucket only during business hours (e.g., 9 AM to 6 PM UTC).

#### ✅ Checklist:
- [ ] Create IAM user for temporary access
- [ ] Create policy with S3 permissions
- [ ] Add time condition: `"DateGreaterThan": {"aws:CurrentTime": "2024-01-01T09:00:00Z"}`
- [ ] Add time condition: `"DateLessThan": {"aws:CurrentTime": "2024-01-01T18:00:00Z"}`
- [ ] Use `aws:CurrentTime` with proper timezone handling
- [ ] Attach policy to user
- [ ] Test access during allowed hours
- [ ] Test access outside allowed hours (should be denied)
- [ ] Document the time-based access control

---

### 15. **Multiple Access Combination**

An **auditor role** can:

* Read objects in all S3 buckets.
* View VPC, subnets, and route table configurations.
* Cannot modify anything.

#### ✅ Checklist:
- [ ] Create IAM role for auditors
- [ ] Create policy with S3 read permissions (`s3:GetObject`, `s3:ListBucket`)
- [ ] Add EC2 describe permissions (`ec2:DescribeVpcs`, `ec2:DescribeSubnets`, `ec2:DescribeRouteTables`)
- [ ] Explicitly deny all modify/write actions
- [ ] Use `"Effect": "Deny"` for write operations
- [ ] Attach policy to role
- [ ] Test S3 object reading
- [ ] Test VPC configuration viewing
- [ ] Verify modification attempts are denied
- [ ] Document the read-only auditor permissions
