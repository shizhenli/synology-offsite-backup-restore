---
title: "Hyper Backup Task Fails to Connect: Diagnose the Offsite Vault Reachability Gap"
description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and vault status, then verify with a test backup."
seo_title: "Synology Hyper Backup Cannot Connect: Fix the Offsite Vault Reachability Gap"
seo_description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and vault status, then verify with a test backup."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-24T11:07:52+08:00
publishDate: 2026-11-24T11:07:52+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

## Understand the failure point

Your offsite Hyper Backup task stops at the connection step, so the NAS cannot reach the remote vault before any data transfer begins. This is a reachability problem, not a backup integrity issue.

## Check basic reachability

From the NAS, open Control Panel > Terminal & SNMP and enable SSH, or use the Hyper Backup log. First, confirm the NAS has outbound internet access by pinging a public address such as 8.8.8.8. If that fails, fix the NAS network or default gateway first. Next, verify the remote vault hostname or IP resolves correctly. A failed DNS lookup points to a DNS server or hostname typo. If you use a custom port, confirm it is open on the remote firewall and that the router forwards it.

## Validate credentials and vault state

Open Hyper Backup, select the task, and choose Edit. Re-enter the destination address, username, and password exactly. Check that the remote Synology NAS is powered on, its Hyper Backup Vault package is running, and the shared folder still exists. If the remote device uses a dynamic IP, confirm the DDNS entry is current. A locked or disabled account on the remote side will also reject the connection.

## Run a verification test

Create a small test task to the same vault using a new folder name. If it connects, the original task settings are corrupted; delete and recreate the original task. If the test also fails, the issue is network or remote-side configuration.

## Rollback and recovery

Before changing task settings, export the task configuration. If a new test task succeeds but the original still fails, remove only the broken task and recreate it, keeping the existing backup data intact. If you are unsure which change caused the failure, revert the last network or credential edit and retest. For guided diagnosis of this **synology hyper backup cannot connect** error,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
