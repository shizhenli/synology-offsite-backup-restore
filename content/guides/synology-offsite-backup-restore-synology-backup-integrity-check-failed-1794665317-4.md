---
title: "Synology Backup Integrity Check Failed: Isolate a Damaged Index from an Incomplete Backup"
description: "Step-by-step diagnosis for a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup, with verification and recovery notes."
seo_title: "Fix Synology Backup Integrity Check Failed: Damaged Index or Incomplete Backup"
seo_description: "Step-by-step diagnosis for a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup, with verification and recovery notes."
keywords:
  - "synology backup integrity check failed"
date: 2026-11-21T16:05:16+08:00
publishDate: 2026-11-21T16:05:16+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running an integrity check on your offsite Hyper Backup vault and it stops with a damaged index or incomplete backup message, leaving you unsure whether the data or the metadata is at fault.

## Confirm the failure scope
Open Hyper Backup, select the offsite task, and run the integrity check again. In the log, note whether the error names a specific .idx or index file, or reports missing chunks. A named index file points to metadata corruption; missing chunks point to an incomplete transfer. Check the remote vault's free space and the task's last successful run time. If the last run ended with a network interruption, treat it as incomplete first.

## Isolate index versus data
On the destination NAS, browse the vault folder and confirm the .hbk index files exist and are non-zero. Compare the task's reported backup size with the actual folder size. A large gap means the backup is incomplete; matching sizes with a failed index check means the index is damaged. Do not delete anything yet.

## Verification test
Create a new temporary backup task to a separate folder on the same offsite destination and run an integrity check on it. If that passes, the remote connection and destination are healthy and the fault is confined to the original vault. If it also fails, investigate the destination volume's health before touching the original task.

## Recovery note
If the index is damaged, use Hyper Backup's index repair option on the task; if repair is unavailable, restore the most recent version to a spare share and verify files before replacing the live task. If the backup is incomplete, re-run the backup to completion rather than deleting the vault. When the check still reports a **synology backup integrity check failed** result after these steps, preserve the logs and vault before making further changes. For guided diagnosis,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
