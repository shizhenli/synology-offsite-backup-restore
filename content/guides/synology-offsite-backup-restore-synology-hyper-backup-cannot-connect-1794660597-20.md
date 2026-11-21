---
title: "Hyper Backup Cannot Connect: Diagnose the Remote Vault Connection"
description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status with clear steps and a verification test."
seo_title: "Fix Synology Hyper Backup Cannot Connect to Remote Vault"
seo_description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status with clear steps and a verification test."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-21T16:02:16+08:00
publishDate: 2026-11-21T16:02:16+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your Hyper Backup task stops at the connection step and cannot reach the offsite vault, leaving the backup incomplete.

## Check network and service reachability

First, confirm the NAS can reach the remote server. From the NAS, open Control Panel > Terminal & SNMP and enable SSH, then connect and run `ping your.remote.host`. If ping fails, the issue is network-level: check the default gateway, DNS settings, and any firewall rules on both sides. If ping succeeds, test the Hyper Backup service port (usually 6281) with `telnet your.remote.host 6281`. A successful connection shows a blank screen; a refusal or timeout means the port is blocked or the service is down.

## Verify credentials and vault status

Next, open Hyper Backup and edit the task. Re-enter the destination username and password exactly, watching for trailing spaces. Confirm the remote vault exists and is not full or in maintenance. On the remote NAS, open Hyper Backup Vault and check that the vault is running and the user has read/write permission. If the remote uses a different port, update it in the task settings.

## Run a verification test

Create a new temporary backup task to the same destination with a small folder. If it connects, the original task settings are corrupted; delete and recreate the original task. If it also fails, the problem is environmental—network, firewall, or vault service.

## Rollback and recovery note

Before changing task settings, export the task configuration. If a recreated task behaves unexpectedly, delete it and re-import the saved configuration to return to the prior state. If the connection still fails after these checks, **synology hyper backup cannot connect** may require deeper log analysis.

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) for a guided diagnosis.
