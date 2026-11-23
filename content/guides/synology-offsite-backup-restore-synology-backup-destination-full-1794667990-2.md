---
title: "Synology Backup Destination Full: Diagnose and Recover an Offsite Hyper Backup Task"
description: "Troubleshoot a Synology offsite Hyper Backup task that stops because the destination is full. Check retention, quotas, and space, then verify and recover safely."
seo_title: "Synology Backup Destination Full: Fix Offsite Hyper Backup"
seo_description: "Troubleshoot a Synology offsite Hyper Backup task that stops because the destination is full. Check retention, quotas, and space, then verify and recover safely."
keywords:
  - "synology backup destination full"
date: 2026-11-23T12:07:53+08:00
publishDate: 2026-11-23T12:07:53+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup task stops at the destination full step, and you need to confirm why the remote vault has no free space before changing anything.

## Check the destination capacity and quota

On the remote Synology, open Storage Manager and note the volume's total and free space. Then open Control Panel > Shared Folder and check the quota on the shared folder that holds the Hyper Backup vault. A folder quota can report full even when the volume has space. Also confirm the task's retention settings in Hyper Backup: too many versions or a long retention period can consume the vault faster than expected.

## Interpret the results

If the volume is full, the vault cannot grow. If the volume has space but the shared folder quota is reached, the task fails at the folder level. If both have space, inspect the vault's .hbk folder size against the retention policy; a mismatch suggests old versions were not rotated. This is the common **synology backup destination full** pattern: the destination is genuinely out of room, not a connection fault.

## Verification test

Free a small amount of space by removing one obsolete backup version through Hyper Backup's version list, or raise the shared folder quota slightly. Run the task manually and watch whether it passes the destination full step. If it proceeds, the cause was capacity or quota; if it stops again immediately, recheck retention and folder size.

## Rollback and recovery note

Before deleting versions, confirm you can restore a test file from the remaining versions. If space was freed by mistake, restore the deleted version from a local copy or another vault. If the task still fails after these checks,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before removing more data.
