---
title: "Synology Hyper Backup Cannot Connect: Diagnose the Remote Vault Connection"
description: "Troubleshoot Synology Hyper Backup when the task fails to connect to an offsite vault. Step-by-step checks for network, credentials, and service status."
seo_title: "Synology Hyper Backup Cannot Connect: Fix Remote Vault Connection"
seo_description: "Troubleshoot Synology Hyper Backup when the task fails to connect to an offsite vault. Step-by-step checks for network, credentials, and service status."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-22T08:07:43+08:00
publishDate: 2026-11-22T08:07:43+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup task fails at the connection step, leaving the backup incomplete and the cause unclear.

## Check network reachability first

From the NAS, open Control Panel > Terminal & SNMP and enable SSH if needed, or use a package like Download Station to test connectivity. Try to reach the remote vault's hostname or IP on the required port (usually 6281 for Hyper Backup Vault). If the test times out, the problem is network-level: verify the remote NAS is powered on, its firewall allows the port, and no ISP block exists. If it resolves but refuses connection, the vault service may be stopped.

## Verify credentials and vault status

In Hyper Backup, edit the task and re-enter the destination username and password. Ensure the account has permission to access the shared folder used as the vault. On the remote NAS, open Hyper Backup Vault and confirm the vault is enabled and the shared folder is intact. If the remote NAS recently updated DSM, the vault service may need restarting.

## Confirm the backup task settings

Check that the destination address in the task matches the current remote IP or DDNS. A changed IP or expired DDNS record is a common cause of **synology hyper backup cannot connect**. Also confirm the encryption key or password has not been altered.

## Run a verification test

Create a new temporary Hyper Backup task to the same remote vault with a small test folder. If it connects, the original task's settings are corrupted; delete and recreate it. If it also fails, the issue is environmental (network or vault service).

## Rollback and recovery

Before deleting the original task, export its configuration. If recreating the task, use the same vault and credentials to avoid orphaning existing backup versions. If the remote vault is inaccessible, do not delete local backup data until connectivity is restored.

If these steps do not resolve the connection failure,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) for a guided diagnosis.
