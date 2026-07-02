# Azure Storage Account – Configure SFTP

## Overview

Azure Blob Storage supports secure file transfers using the **SSH File Transfer Protocol (SFTP)**.

By enabling SFTP on an Azure Storage Account, users can securely upload and download files without exposing Storage Account access keys or relying on SMB or traditional FTP services.

This guide explains how to:

- Create an Azure Storage Account for SFTP
- Enable the required Storage Account features
- Create a Blob Container
- Open the SFTP management page

Authentication using Local Users is covered in separate guides.

> **Note**
>
> Azure SFTP uses **Local Users** for authentication. These users are independent of Microsoft Entra ID accounts.

---

## Prerequisites

Before starting, ensure that:

- You have an Azure subscription.
- You have permission to create Azure Storage Accounts.
- The Storage Account will use **Standard** performance.
- A supported redundancy option (for example **LRS**) is selected.
- SFTP will be enabled during Storage Account creation.

---

# Step-by-Step Guide

---

## Step 1 – Create the Storage Account

Create a new Azure Storage Account.

Recommended settings:

| Setting | Value |
|---------|-------|
| Performance | Standard |
| Redundancy | Locally Redundant Storage (LRS) |
| Storage Type | Azure Blob Storage |
| Region | As required |

![Storage Account Basics](images/storage-account-basics.png)

---

## Step 2 – Enable Hierarchical Namespace and SFTP

Open the **Advanced** tab during Storage Account creation.

Enable the following options:

- ✅ Enable hierarchical namespace
- ✅ Enable SFTP

The **Hierarchical Namespace** is required because Azure SFTP is built on **Azure Data Lake Storage Gen2**.

Without enabling this feature, SFTP cannot be used.

![Storage Account Advanced](images/storage-account-advanced.png)

---

## Step 3 – Create a Blob Container

After the Storage Account has been deployed, create a Blob Container.

The container stores all files uploaded through SFTP and can also serve as the user's **Home Directory**.

Example:

```text
transfer
```

![Blob Container Overview](images/blob-container-overview.png)

---

## Step 4 – Open the SFTP Management Page

Navigate to:

```text
Storage Account
→ Settings
→ SFTP
```

The SFTP management page allows you to:

- Create Local Users
- Manage existing users
- Enable or disable SFTP
- Generate SSH key pairs

![SFTP Overview](images/sftp-overview.png)

---

# Next Steps

The Storage Account is now prepared for SFTP.

To allow clients to connect, create a Local User using one of the following authentication methods:

- **Password Authentication**
  - Configure a Local User with an SSH password.
  - See: **Azure Storage SFTP – Configure a Local User (Password Authentication)**

- **SSH Public Key Authentication**
  - Configure a Local User using an SSH public key.
  - See: **Azure Storage SFTP – Configure a Local User (SSH Key Authentication)**

---

# Security Considerations

- Enable SFTP only when required.
- Use the **Principle of Least Privilege** when assigning permissions.
- Create separate Blob Containers for different applications or users where appropriate.
- Prefer **SSH Public Key Authentication** over passwords whenever possible.
- Restrict network access using firewalls or private endpoints where appropriate.

---

# Related Articles

- Azure Storage SFTP – Configure a Local User (Password Authentication)
- Azure Storage SFTP – Configure a Local User (SSH Key Authentication)
- SSH Key Generation (RSA)
- SSH Key Generation (ED25519)
- WinSCP – Connect to Azure Storage using Password Authentication
- WinSCP – Connect to Azure Storage using SSH Key Authentication
