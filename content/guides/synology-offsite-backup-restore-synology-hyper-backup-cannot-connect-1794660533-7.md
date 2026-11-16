---
title: "Hyper Backup Task Fails to Connect: Diagnose the Offsite Vault Link"
description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status, then verify with a test."
seo_title: "Fix Synology Hyper Backup Cannot Connect to Offsite Vault"
seo_description: "Troubleshoot a Synology Hyper Backup task that fails to connect to an offsite vault. Check network, credentials, and service status, then verify with a test."
keywords:
  - "synology hyper backup cannot connect"
date: 2026-11-16T12:27:19+08:00
publishDate: 2026-11-16T12:27:19+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

## Troubleshooting

Your offsite Hyper Backup task stops at the connection step and never reaches the remote vault, leaving the backup incomplete. Start by confirming the NAS can reach the destination at all. Open Control Panel > Network > Network Interface and note the default gateway. Then use Package Center to install or open a terminal tool, or use SSH, and run a ping to the vault's hostname or IP. If ping fails, the problem is local routing or DNS, not Hyper Backup. Next, verify the destination service is running: log in to the remote NAS or server and confirm the Hyper Backup Vault package is active and the shared folder exists. Check that the firewall on both sides allows the backup port (usually 6281 for Hyper Backup Vault). In the backup task settings, re-enter the destination address and credentials; a changed password or expired account will cause a silent connection failure. Look at the task log for the exact error code. If it says 'connection refused', the service is down or the port is blocked. If it says 'authentication failed', the account lacks permission or the password is wrong. A timeout points to network filtering. To verify, create a small test backup task to the same vault using a new folder. If that connects, the original task's settings are corrupt; delete and recreate it. If it also fails, the issue is the vault or network path. Before changing anything, export the task configuration so you can roll back. After any fix, run the test task again and confirm it completes. If the original task still shows **synology hyper backup cannot connect**, restore the exported configuration and review firewall logs. For guided diagnosis,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
