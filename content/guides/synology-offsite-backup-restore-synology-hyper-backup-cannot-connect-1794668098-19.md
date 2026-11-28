---
title: "Synology Hyper Backup Cannot Connect: Diagnose the Remote Vault Connection Failure"
description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status, then verify with a test backup."
seo_title: "Synology Hyper Backup Cannot Connect: Fix Remote Vault Connection"
seo_description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status, then verify with a test backup."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-28T22:22:13+08:00
publishDate: 2026-11-28T22:22:13+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup task stops at the connection step, and the log simply says it cannot reach the remote vault.

## Confirm the failure point
Open Hyper Backup, select the task, and click Action > View Log. Look for entries around the failure time. If you see "connection timeout," "authentication failed," or "destination unreachable," note the exact message. This tells you whether the problem is network, credentials, or the remote service.

## Check network reachability
From the NAS, open Control Panel > Terminal & SNMP and enable SSH, or use a package like Download Station to test connectivity. A simpler check: go to Control Panel > Network > Network Test and ping the remote vault's hostname or IP. If ping fails, the NAS cannot route to the destination. Verify the default gateway, DNS servers, and any firewall rules on both sides. If ping succeeds but the backup still fails, the issue is likely at the application layer.

## Verify credentials and vault status
In Hyper Backup, edit the task and re-enter the destination username and password. Confirm the remote vault is online and that its shared folder exists. If the vault uses a different port, ensure it is correct. Also check that the remote NAS user has read/write permission to the vault folder. A common cause of **synology hyper backup cannot connect** is an expired password or a changed permission on the remote side.

## Run a verification test
Create a small test backup task to the same vault using a single folder. If it connects, the original task's settings are corrupt—delete and recreate it. If the test also fails, the problem is environmental; revisit network and credentials.

## Rollback and recovery
Before changing settings, export the task configuration. If a change makes things worse, restore the previous configuration and re-enable the original task. Keep a local backup of the vault index if possible.

If these steps do not resolve it,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) with your log excerpts.
