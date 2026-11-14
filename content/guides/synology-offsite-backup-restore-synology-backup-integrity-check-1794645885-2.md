---
title: "Synology Backup Integrity Check Fails: Diagnose a Damaged Index or Incomplete Backup"
description: "Troubleshoot a Synology Hyper Backup integrity check failure on an offsite vault. Diagnose a damaged index or incomplete backup with practical checks and a verification test."
seo_title: "Synology Backup Integrity Check Fails: Fix Damaged Index or Incomplete Backup"
seo_description: "Troubleshoot a Synology Hyper Backup integrity check failure on an offsite vault. Diagnose a damaged index or incomplete backup with practical checks and a verification test."
keywords:
  - "synology backup integrity check"
date: 2026-11-14T19:44:22+08:00
publishDate: 2026-11-14T19:44:22+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running a Hyper Backup integrity check on your offsite vault, and it stops with a damaged index or incomplete backup message before you can finish a controlled diagnosis.

## First, read the exact result
In Hyper Backup, open the backup task and run the integrity check again. Record the exact wording and the timestamp. A damaged index usually means the local index database no longer matches the data blocks; an incomplete backup means the last version did not finish writing. If the log names a specific version or file count, note it.

## Check the vault and the task
On the destination NAS, open the shared folder that holds the vault and confirm it is mounted and not read-only. In Hyper Backup, verify the task still points to the correct remote path. Then check free space on the destination volume: if the volume is nearly full, the last backup may be incomplete. Compare the task's last run time with the log entry.

## Run a verification test
Create a small test share with one known file, back it up to the same offsite vault, and run the integrity check on that test task. If the test passes, the vault connection is healthy and the failure is isolated to the original task's index. If the test also fails, treat the vault as suspect and stop writing to it.

## Recovery and rollback note
Do not delete the vault. If the test passes, open the original task and use the option to re-index or repair the backup database, then rerun the check. If repair is unavailable, restore the last known good version to a spare folder before starting a fresh backup. Keep the old vault until the new one verifies.

If the **synology backup integrity check** still fails after these steps,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) with the exact log text and timestamps.
