---
title: "Synology Backup Integrity Check Fails: Isolate a Damaged Index from an Incomplete Offsite Backup"
description: "Troubleshoot a Synology backup integrity check failure on an offsite Hyper Backup vault. Isolate a damaged index from an incomplete backup and verify recovery."
seo_title: "Synology Backup Integrity Check Fails: Fix a Damaged Index"
seo_description: "Troubleshoot a Synology backup integrity check failure on an offsite Hyper Backup vault. Isolate a damaged index from an incomplete backup and verify recovery."
keywords:
  - "synology backup integrity check"
date: 2026-11-22T09:07:38+08:00
publishDate: 2026-11-22T09:07:38+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running a Synology NAS with an offsite Hyper Backup vault, and the integrity check stops with a damaged index or incomplete backup message before you can diagnose it.

## Confirm the Failure Scope

Open Hyper Backup, select the offsite task, and run the integrity check again. Record the exact message and the timestamp. A damaged index usually names the index file; an incomplete backup points to missing or truncated data blocks. Do not delete the task or vault yet.

## Check the Index and Data Separately

In the remote vault, inspect the index folder and compare its size and modification time with the last successful backup. If the index is present but unreadable, the index is damaged. If index entries reference files absent from the data folders, the backup is incomplete. Note which condition applies, because recovery differs.

## Run a Verification Test

Create a small test share, back it up to the same offsite vault, and run an integrity check on that new task. If the new task passes, the vault connection and destination are healthy and the fault is isolated to the original backup set. If it also fails, stop and inspect the remote storage health.

## Recovery and Rollback

For a damaged index, use Hyper Backup's restore to a temporary folder and confirm the expected files are readable before replacing anything. For an incomplete backup, restore the most recent complete version instead of repairing the damaged set. Keep the failed set until the restore is verified, so you can roll back if needed.

If the check still fails after these steps,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting the vault. A controlled **synology backup integrity check** diagnosis prevents unnecessary data loss.
