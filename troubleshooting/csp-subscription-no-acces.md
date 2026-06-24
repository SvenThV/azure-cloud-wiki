CSP Subscription – Customer Has No Permissions
Problem

After provisioning a new Azure CSP subscription, the customer can see the subscription but cannot manage resources.

Symptoms
Cannot create Resource Groups
Cannot create Storage Accounts
Cannot assign Azure RBAC roles
IAM shows limited or no permissions

Example error:

You do not have permissions to create resource groups under subscription ...
Root Cause

Microsoft Entra roles and Azure RBAC roles are separate permission systems.

Being assigned the role:

Global Administrator

does not automatically grant permissions on Azure subscriptions.

Example:

Microsoft Entra ID
└─ Global Administrator

Azure Subscription
└─ Owner / Contributor / Reader
Resolution
Enable Access Management for Azure Resources
Microsoft Entra ID
→ Properties
→ Access management for Azure resources
→ Yes
→ Save

This grants the Global Administrator temporary elevated permissions at tenant root scope.

Sign out and sign in again
Logout
→ Login

Wait a few minutes if necessary.

Assign Subscription Permissions
Subscriptions
→ Subscription
→ Access Control (IAM)
→ Add Role Assignment

Assign:

Owner

or

Contributor

depending on customer requirements.

Verification

Check:

Subscription
→ My Permissions

Expected result:

Role: Owner
Scope: Subscription

Customer should be able to:

Create Resource Groups
Create Azure resources
View IAM assignments
CSP Specific Notes

For newly created CSP subscriptions, ownership is often assigned only to the CSP partner.

Example:

Foreign Principal for <Partner Name>
Role: Owner

In this scenario either:

Customer assigns themselves Owner permissions using the procedure above
CSP partner assigns Owner or Contributor permissions
Screenshots
Access Management for Azure Resources

[screenshot]

Missing Subscription Permissions

[screenshot]

Successful Owner Assignment

[screenshot]

Lessons Learned

Always verify customer permissions immediately after CSP subscription provisioning.

Checklist:

Customer has Owner permissions
Customer can create a Resource Group
Customer can create a Storage Account
Customer can access IAM

Perform these checks before starting implementation activities.
