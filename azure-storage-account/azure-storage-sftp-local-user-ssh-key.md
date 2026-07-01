# Azure Storage SFTP – Configure a Local User (SSH Key Authentication)

## Overview

Azure Storage SFTP supports authentication using SSH public keys instead of passwords.

With SSH key authentication, the **public key** is uploaded to Azure Storage, while the **private key** remains securely stored on the client device. During authentication, Azure verifies that the client owns the corresponding private key without transmitting it over the network.

This guide explains how to:

- Create an SFTP local user
- Configure SSH key authentication
- Upload an existing SSH public key
- Assign container permissions
- Verify the created user

---

## Prerequisites

Before continuing, ensure that:

- Azure Storage SFTP is enabled
- A Blob Container already exists
- An SSH key pair has already been generated

Related articles:

- SSH Key Generation (ED25519)
- SSH Key Generation (RSA)
- Azure Storage Account – Configure SFTP

---

# Step-by-Step Guide

## Step 1 – Open the SFTP Configuration

Open your Azure Storage Account and navigate to:

```text
Storage Account
→ Settings
→ SFTP
→ Add local user
```

The SFTP page displays all configured local users.

![SFTP overview](images/sftp-overview.png)

---

## Step 2 – Configure the Local User

Enter a username for the SFTP user.

Under **Authentication methods**, enable:

- SSH Key pair

Leave **SSH Password** disabled if you only want to allow key-based authentication.

![Configure local user](images/sftp-local-user-overview.png)

> **Note**
>
> Azure Storage supports:
>
> - Password authentication
> - SSH key authentication
> - Both authentication methods simultaneously

---

## Step 3 – Upload the SSH Public Key

Click **Add key**.

For an existing SSH key pair select:

```text
Use existing public key
```

Paste the contents of your **public key** into the **Key name OR Public key** field.

Optionally enter a description to help identify the key later.

Example:

```powershell
Get-Content $HOME\.ssh\id_ed25519.pub
```

or

```powershell
Get-Content $HOME\.ssh\id_rsa.pub
```

Copy the complete output and paste it into Azure.

![Upload SSH public key](images/sftp-upload-public-key.png)

> **Important**
>
> Upload **only** the public key (`*.pub`).
>
> Never upload or share your private key.

---

## Step 4 – Configure Container Permissions

Switch to the **Permissions** tab.

Select the Blob Container that should be accessible via SFTP.

Typical permissions include:

| Permission | Description |
|------------|-------------|
| Read | Download files |
| Create | Upload new files |
| Write | Modify existing files |
| Delete | Delete files |
| List | List directory contents |

Configure the **Home Directory** to point to the Blob Container.

Example:

```text
transfer
```

![Container permissions](images/sftp-local-user-permissions.png)

### Optional ACL Settings

The ACL settings are only required for advanced scenarios using **Azure Data Lake Storage Gen2 (Hierarchical Namespace)** with POSIX-style access control.

| Setting | Description |
|----------|-------------|
| **User ID (UID)** | Numeric identifier assigned to the local user. |
| **Group ID (GID)** | Numeric identifier of the user's primary group. |
| **Allow ACL authorization** | Enables authorization using Azure Data Lake Storage ACLs instead of relying only on container permissions. |

> **Note**
>
> For most SFTP deployments these settings can remain unchanged. Container permissions are sufficient for typical file transfer scenarios.

> **Tip**
>
> Follow the Principle of Least Privilege and grant only the permissions required by the workload.

---

## Step 5 – Create the Local User

After reviewing the configuration, create the local user.

The user will appear in the SFTP overview.

The **Authentication method** should display:

```text
SSH Key pair
```

![Created local user](images/sftp-local-user-created.png)

This confirms that the user has been successfully configured for SSH key authentication.

---

# Security Best Practices

- Upload only the **public key**.
- Never disclose the private key.
- Store the private key securely.
- Prefer **ED25519** for modern environments.
- Use **RSA** only when compatibility with legacy systems is required.
- Use separate SSH key pairs for different environments whenever possible.

---

# Troubleshooting

## Authentication fails

Verify that:

- the correct public key has been uploaded
- the corresponding private key is being used by the SSH client
- the username matches the Azure Storage local user

---

## Permission denied

Verify that:

- the required container permissions have been assigned
- the Home Directory points to the correct Blob Container
- the uploaded public key matches the private key used for authentication

---

# Related Articles

- Azure Storage Account – Configure SFTP
- SSH Key Generation (ED25519)
- SSH Key Generation (RSA)
- WinSCP – Connect using SSH Key Authentication
