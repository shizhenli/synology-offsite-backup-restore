---
title: "Synology Backup Task Stopped: Destination Full Diagnosis"
description: "Troubleshoot a Synology offsite Hyper Backup task that stops because the destination is full. Diagnose space, retention, and version conflicts with a verification test."
seo_title: "Synology Backup Task Stopped: Fix Destination Full"
seo_description: "Troubleshoot a Synology offsite Hyper Backup task that stops because the destination is full. Diagnose space, retention, and version conflicts with a verification test."
keywords:
  - "synology backup task stopped"
date: 2026-11-15T19:03:00+08:00
publishDate: 2026-11-15T19:03:00+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup task stops at the destination full step, and you need to confirm whether the vault is truly out of space before changing retention or deleting data. This is why your **synology backup task stopped** at that exact checkpoint.

## Check Destination Capacity and Quota

Open Hyper Backup, select the task, and view the destination details. Compare the reported used space against the vault's total capacity. If the vault is a shared folder on the remote NAS, also check that folder's quota in Control Panel > Shared Folder. A full quota presents as a full destination even when the volume has free space. If used space equals capacity or quota, the destination is genuinely full; proceed to the next section. If used space is well below capacity, the stop is likely a quota, permission, or version-retention issue rather than raw disk exhaustion.

## Check Retention and Version Conflicts

In the task's backup schedule, review the retention policy. Too many retained versions can fill a vault that was sized for fewer. Also confirm no other task writes to the same destination, because concurrent jobs can consume the remaining space mid-run. If retention is aggressive, reduce the number of versions and rerun the task.

## Verification Test

After adjusting retention or quota, run the task manually and watch the destination usage during the run. A successful pass should complete without stopping at the full step and should leave free space. If it stops again at the same point, the vault needs more capacity or a smaller backup scope.

## Rollback Note

Before deleting versions or expanding the vault, export the task configuration. If a retention change causes unexpected version loss, you can restore the previous settings and re-enable versions from the remaining backup set. For guided diagnosis,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
