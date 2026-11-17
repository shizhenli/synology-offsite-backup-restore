---
title: "Synology Remote Backup Encryption: Fix a Rejected Key or Password on an Offsite Vault"
description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
seo_title: "Synology Remote Backup Encryption: Key or Password Rejected"
seo_description: "Troubleshoot a Synology offsite Hyper Backup vault that opens but rejects the encryption key or password. Step-by-step checks, verification, and recovery."
keywords:
  - "synology remote backup encryption"
date: 2026-11-17T10:07:28+08:00
publishDate: 2026-11-17T10:07:28+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

**synology remote backup encryption**. ## Understand the rejection

You are restoring from an offsite Hyper Backup vault, the vault opens, but the encryption key or password is rejected, so the remote backup is encrypted and cannot be opened. This usually means the credential does not match the one used when the task was created, not that the backup is damaged.

## Check the exact credential source

First confirm which password field you are filling. Hyper Backup asks for the encryption password, not your DSM account password. If the task used a key file, select the key file option and point to the original .pem file; a password typed into the key-file field will always fail. Next, verify the task's encryption settings in Hyper Backup on the source NAS: open the task, choose Edit, and inspect the encryption section without changing anything. Note whether it uses a password, a key file, or both.

## Interpret the result

If the same credential fails on a second restore attempt, treat it as a mismatch. If it succeeds, the earlier attempt had a typo or the wrong field. If the key file loads but the password is still rejected, the key file is likely from a different task.

## Verification test

Create a small test restore to a local folder using the same credential. A successful test restore confirms the credential is valid and the problem was entry-related. A failure confirms the credential itself is wrong.

## Rollback and recovery

Do not delete the vault or task. Locate the original encryption password or key file from your records; without it, the data cannot be decrypted. If it is lost, keep the vault intact and seek guided recovery before any changes. For a controlled diagnosis,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
