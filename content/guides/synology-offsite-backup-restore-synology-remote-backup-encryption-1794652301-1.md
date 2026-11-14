---
title: "Synology Remote Backup Encryption: When the Key or Password Is Rejected"
description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
seo_title: "Fix Synology Remote Backup Encryption Key Rejected"
seo_description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
keywords:
  - "synology remote backup encryption"
date: 2026-11-14T19:44:22+08:00
publishDate: 2026-11-14T19:44:22+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are trying to restore from an encrypted offsite Hyper Backup vault, but the vault opens and then rejects the encryption key or password, so you cannot proceed.

## Confirm the key and password match the vault

First, verify you are using the exact encryption key or password that was set when the backup task was created. Hyper Backup does not accept a re-typed or regenerated key. Open the original task settings on the source NAS if available, or locate the saved key file. Check for hidden characters, trailing spaces, or a wrong keyboard layout. The result you want: the key is accepted and the restore wizard advances past the encryption prompt. If it is still rejected, the key does not match this vault.

## Check the vault type and version

Confirm the remote vault was created by the same Hyper Backup version family and that you are restoring through Hyper Backup, not File Station. A vault that opens but rejects the key often means the key belongs to a different task or a re-created vault. Compare the vault name, destination path, and task ID.

## Verification test

Create a small test backup to the same remote destination with a new encryption key, then immediately restore it. If the test key is accepted, your original key is wrong for that vault. If the test also fails, the destination or vault metadata is the problem.

## Rollback and recovery

Do not delete the vault. Keep the rejected key recorded, then try the previous key if the task was re-encrypted. If no key works, the vault cannot be opened without the original key; recover data from another backup copy or the source NAS. For a controlled diagnosis of your **synology remote backup encryption** setup,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
