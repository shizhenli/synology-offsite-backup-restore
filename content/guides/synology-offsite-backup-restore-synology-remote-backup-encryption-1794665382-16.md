---
title: "Synology Remote Backup Encryption: Fix a Rejected Key or Password"
description: "Troubleshoot a Synology remote backup encryption vault that opens but rejects the key or password, with checks, result interpretation, and a verification test."
seo_title: "Synology Remote Backup Encryption: Key or Password Rejected"
seo_description: "Troubleshoot a Synology remote backup encryption vault that opens but rejects the key or password, with checks, result interpretation, and a verification test."
keywords:
  - "synology remote backup encryption"
date: 2026-11-22T11:07:48+08:00
publishDate: 2026-11-22T11:07:48+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are restoring an encrypted offsite Hyper Backup vault, the vault opens, but the encryption key or password is rejected before you can complete a controlled diagnosis.

## Confirm What the Prompt Is Asking For

Hyper Backup can ask for two different secrets: the vault password and the encryption key file or passphrase. Read the dialog title and field label carefully. If it asks for a key file, browse to the original .pem or key export; do not paste a password into that field. If it asks for a password, confirm keyboard layout and Caps Lock before retyping. A single leading or trailing space is enough to fail.

## Check the Key Against the Vault

Open the backup task details on the source NAS if it is still available and confirm the encryption type shown there. Compare it with the key you are supplying. If the task used a key file, the password alone will not unlock it. If the key file was regenerated or exported again after the task was created, it will not match. Use the exact file that was downloaded when encryption was enabled.

## Verification Test

Create a new temporary restore task pointing at the same remote vault, choose the same version, and enter the key or password once more. If the temporary task reaches the restore preview and lists folders, the original task entry was the problem, not the key. If it is rejected again, stop and preserve the vault; do not delete or reinitialize it.

## Recovery Note

If the key cannot be confirmed, keep the remote vault untouched and recover the original key export or password record before any further attempt. For a guided review of your **synology remote backup encryption** setup,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
