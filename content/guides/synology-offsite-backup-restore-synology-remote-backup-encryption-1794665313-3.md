---
title: "Synology Remote Backup Encryption: When the Vault Opens but the Key Is Rejected"
description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
seo_title: "Synology Remote Backup Encryption: Key or Password Rejected"
seo_description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
keywords:
  - "synology remote backup encryption"
date: 2026-11-21T16:05:16+08:00
publishDate: 2026-11-21T16:05:16+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup vault opens, but the encryption key or password is rejected, and you cannot proceed with the restore.

## Confirm the Vault Is Actually Encrypted

In Hyper Backup, select the remote vault and choose Restore. If the wizard prompts for an encryption key, the vault is encrypted. If it opens without a prompt, you are looking at a different vault or a local copy. Note the exact vault name and destination path shown.

## Check the Key Source and Format

Open the original backup configuration or the .bkpi file that was saved when the task was created. The key is a long alphanumeric string; copy it exactly, with no leading or trailing spaces. If you are typing a password instead, confirm the keyboard layout and that Caps Lock is off. A single transposed character will cause rejection.

## Interpret the Result

If the key is accepted, the restore wizard advances to version selection. If it is rejected again, the key does not match this vault. Do not retry repeatedly; instead, locate the correct key file or password record for this specific task.

## Verification Test

Create a small test restore to a temporary shared folder using the same key. If the test restore completes, the key is valid and the earlier failure was a copy error. If it fails identically, the key belongs to another vault.

## Rollback and Recovery

Before changing anything, export the current task configuration and keep a copy of the key file offline. If no matching key can be found, the encrypted data cannot be opened; document the vault path and key attempts, then

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting or recreating the task. This keeps your **synology remote backup encryption** recovery options intact.
