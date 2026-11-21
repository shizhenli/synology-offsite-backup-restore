---
title: "Synology Backup Integrity Check: Diagnose a Damaged Index or Incomplete Backup"
description: "Troubleshoot a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup. Step-by-step diagnosis and recovery."
seo_title: "Synology Backup Integrity Check Fails: Fix Damaged Index or Incomplete Backup"
seo_description: "Troubleshoot a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup. Step-by-step diagnosis and recovery."
keywords:
  - "synology backup integrity check"
date: 2026-11-21T16:02:16+08:00
publishDate: 2026-11-21T16:02:16+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

## Understand the failure

You run a backup integrity check on your Synology NAS offsite Hyper Backup vault, and it stops with a damaged index or incomplete backup error before you can complete a controlled diagnosis. This guide walks you through isolating the cause and recovering safely.

## Check the vault and repository

First, confirm the remote vault is reachable and not full. In Hyper Backup, open the backup task and review the log for the exact error timestamp. A damaged index often points to an interrupted transfer or storage fault; an incomplete backup suggests the last job did not finish. Check the remote destination's free space and filesystem health. If the vault is on another Synology, run a storage pool check there. Interpret results precisely: a clean pool and sufficient space mean the fault is likely in the backup metadata, not the disk.

## Run a targeted verification test

Create a small test share with a few files and back it up to the same offsite vault. Then run the integrity check again. If the test passes, the original index is corrupt; if it fails, the vault itself is suspect. This isolates whether the problem is task-specific or repository-wide.

## Recover the backup

For a damaged index, use Hyper Backup's repair option on the task, which rebuilds metadata from existing data. If repair fails, restore the most recent good version to a temporary folder and verify file counts before overwriting anything. Keep the old vault intact until the restore is confirmed. Document the failure for your **synology backup integrity check** records so recurring patterns are visible.

## When to escalate

If repair and test backups both fail, the remote repository may need professional recovery.

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting any vault data.
