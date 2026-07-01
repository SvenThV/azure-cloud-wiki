# SSH Key Generation (ED25519)

## Overview

SSH key authentication provides a secure alternative to password-based authentication.

This guide explains how to generate an **ED25519** SSH key pair using **OpenSSH** on Windows.

ED25519 is the recommended SSH key algorithm for modern systems because it provides excellent security, small key sizes, and fast authentication.

---

## Why Use ED25519

ED25519 is the recommended SSH key algorithm for modern systems.

Typical advantages include:

- Smaller key size
- Faster key generation
- Faster authentication
- Strong modern cryptography
- Supported by most current SSH implementations

> **Note**
>
> Only use RSA when working with legacy systems that do not support ED25519.

---

## Prerequisites

Before generating an SSH key, ensure that:

- Windows 10 or Windows 11 is installed
- PowerShell is available
- OpenSSH Client is installed (included by default on modern Windows versions)

---

# Step-by-Step Guide

## Step 1 – Verify OpenSSH Installation

Open PowerShell and verify that OpenSSH is installed.

```powershell
ssh -V
```

Expected output:

```text
OpenSSH_for_Windows_...
```

If the command is not recognized, install the optional Windows feature **OpenSSH Client** before continuing.

---

## Step 2 – Generate the ED25519 Key Pair

Generate a new ED25519 SSH key pair.

```powershell
ssh-keygen -t ed25519
```

The command starts the interactive key generation wizard.

---

## Step 3 – Choose the Storage Location

The wizard asks where the key should be stored.

```text
Enter file in which to save the key
(C:\Users\<username>\.ssh\id_ed25519):
```

Press **Enter** to use the default location.

Alternatively, specify another filename if multiple SSH keys are required.

---

## Step 4 – Configure an Optional Passphrase

Next, OpenSSH asks for a passphrase.

```text
Enter passphrase (empty for no passphrase):
```

### Without Passphrase

- Convenient
- No additional password required
- Suitable for automated scenarios

### With Passphrase

- Additional protection
- Recommended for production environments
- Requires entering the passphrase whenever the key is used

---

## Step 5 – Verify Successful Key Generation

After completion, OpenSSH displays information similar to:

```text
Your identification has been saved in ...

Your public key has been saved in ...

The key fingerprint is ...
```

This confirms that the ED25519 key pair has been created successfully.

---

## Step 6 – Verify the Generated Files

Display the contents of the `.ssh` directory.

```powershell
dir $HOME\.ssh
```

Expected output:

```text
id_ed25519
id_ed25519.pub
```

![Generated ED25519 key files](images/ssh-key-files-ed25519.png)

> **Note**
>
> Depending on your Windows file associations, the `.pub` file may appear as a *Microsoft Publisher Document*. Despite the icon, it is an SSH public key and **not** a Publisher file.

---

## Step 7 – Display the Public Key

Display the public key.

```powershell
Get-Content $HOME\.ssh\id_ed25519.pub
```

Example:

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA...
```

Only the **public key** should be shared with remote systems.

---

## Step 8 – Display the Key Fingerprint (Optional)

Display the fingerprint of the generated public key.

```powershell
ssh-keygen -lf $HOME\.ssh\id_ed25519.pub
```

Example:

```text
256 SHA256:xxxxxxxxxxxxxxxxxxxxxxxx
```

Fingerprints uniquely identify SSH keys without exposing the complete public key.

---

# Understanding the Generated Files

After successful generation, the following files exist:

| File | Description |
|------|-------------|
| `id_ed25519` | Private key. Keep this file secret and never share it. |
| `id_ed25519.pub` | Public key. Upload this file to SSH servers and services. |

---

# Security Considerations

- Never share the private key.
- Protect the private key with appropriate file permissions.
- Consider using a passphrase whenever possible.
- Back up the private key securely.
- Use different key pairs for different environments if appropriate.

---

# Troubleshooting

## ssh-keygen is not recognized

Install the Windows **OpenSSH Client**.

---

## Permission denied

Verify that:

- the correct private key is being used
- the corresponding public key is installed on the remote server

---

## Existing key already present

If `id_ed25519` already exists, either:

- overwrite the existing key
- specify another filename during creation

---

# Related Articles

- SSH Key Generation (RSA)
- Azure Storage Account – Enable SFTP
- Azure Blob Storage – Configure Local Users
- Azure Blob Storage – Upload an SSH Public Key
- WinSCP – Connect to Azure Blob Storage using SFTP
