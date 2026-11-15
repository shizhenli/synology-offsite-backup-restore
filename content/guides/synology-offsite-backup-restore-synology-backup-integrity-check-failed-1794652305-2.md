---
title: "Synology Backup Integrity Check Failed: Diagnose a Damaged Index or Incomplete Backup"
description: "Troubleshoot a Synology backup integrity check failure caused by a damaged index or incomplete backup. Step-by-step diagnosis and recovery for offsite Hyper Backup vaults."
seo_title: "Synology Backup Integrity Check Failed: Fix Damaged Index"
seo_description: "Troubleshoot a Synology backup integrity check failure caused by a damaged index or incomplete backup. Step-by-step diagnosis and recovery for offsite Hyper Backup vaults."
keywords:
  - "synology backup integrity check failed"
date: 2026-11-15T19:03:00+08:00
publishDate: 2026-11-15T19:03:00+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running an integrity check on your offsite Hyper Backup vault, and it stops with a damaged index or incomplete backup message. This article walks you through a controlled diagnosis so you can confirm the cause and recover safely.

## Confirm the exact failure point

Open Hyper Backup, select the offsite task, and review the log. Look for the specific error: a damaged index usually appears as "index file is corrupted" or "cannot read index," while an incomplete backup shows "backup set is incomplete" or a missing version. Note the timestamp and the affected backup version. If the log only shows a generic failure, run the check again and capture the full message.

## Check vault health and free space

On the remote vault (the offsite NAS or rsync server), verify the repository folder is accessible and has sufficient free space. A full volume can truncate writes and leave an incomplete backup. Also confirm the network share is mounted read-write and that no antivirus or snapshot process is locking the index files.

## Run a targeted verification test

Create a new, small test backup task to the same offsite vault using a single folder. If that integrity check passes, the vault itself is healthy and the problem is isolated to the original backup set. If it also fails, the vault or connection is the culprit.

## Recovery and rollback note

If the index is damaged, use Hyper Backup's restore to a temporary folder and compare file counts before overwriting anything. If the backup is incomplete, delete only the affected version and let the next run create a fresh one. Do not delete the entire repository until you have confirmed a restorable copy exists. For persistent **synology backup integrity check failed** errors after these steps,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before making further changes.
