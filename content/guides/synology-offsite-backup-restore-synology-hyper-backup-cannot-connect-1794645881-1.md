---
title: "Synology Hyper Backup Cannot Connect: Fix the Remote Vault Connection"
description: "Step-by-step fix for Synology Hyper Backup cannot connect errors when reaching an offsite vault. Check network, credentials, and service status, then verify with a test."
seo_title: "Synology Hyper Backup Cannot Connect: Troubleshoot Offsite Vault"
seo_description: "Step-by-step fix for Synology Hyper Backup cannot connect errors when reaching an offsite vault. Check network, credentials, and service status, then verify with a test."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-14T19:44:22+08:00
publishDate: 2026-11-14T19:44:22+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup task stops at the connection step and never reaches the remote vault, leaving the backup incomplete. Here is a controlled way to isolate the failure.

## Confirm the destination is reachable
Open Control Panel > Network > Network Test on the source NAS and ping the vault hostname or IP. A timeout means DNS or routing is the problem; a reply means the network path is fine. Next, verify the vault service is running on the destination NAS: open Hyper Backup Vault and confirm it is enabled and listening on the expected port (usually 6281). If the port is closed, the connection will fail before authentication.

## Validate credentials and permissions
In the backup task settings, re-enter the destination username and password. A common cause of **synology hyper backup cannot connect** is an expired password or a user lacking permission to the shared folder. Check the destination user's group membership and shared folder privileges. Also confirm the task is pointing to the correct vault name, not a renamed or deleted folder.

## Check certificates and time
If the vault uses HTTPS, an expired or mismatched certificate will block the connection. Compare the certificate dates on both NAS devices and ensure their system times are within a few minutes. A large clock skew breaks TLS handshakes silently.

## Verification test
Create a new temporary Hyper Backup task to the same vault with a small test folder. If it connects, the original task's settings are corrupt; delete and recreate it. If it also fails, the issue is at the destination or network layer, not the task.

## Rollback note
Before changing credentials or recreating tasks, export the current task configuration. If a change makes things worse, restore the exported settings and re-enable the original task.

If these checks do not resolve it,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) with your logs and network test results.
