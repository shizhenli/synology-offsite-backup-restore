---
title: "Offsite Hyper Backup Restore Finishes but Files Are Missing: Check the Restore Scope"
description: "Restore completes but files are absent? Learn how to diagnose a partial offsite restore by checking the restore scope, filters, and target path, then verify with a test."
seo_title: "Synology Hyper Backup Restore Missing Files: Fix Offsite Restore Scope"
seo_description: "Restore completes but files are absent? Learn how to diagnose a partial offsite restore by checking the restore scope, filters, and target path, then verify with a test."
keywords:
  - "synology hyper backup restore missing files"
date: 2026-11-24T10:07:42+08:00
publishDate: 2026-11-24T10:07:42+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You restored from your offsite Hyper Backup vault, but the job finished and expected files are absent from the target.

## Check the restore scope before anything else

Open Hyper Backup, select Restore, and step through the wizard again without starting the job. At the folder selection screen, confirm the exact folders and subfolders you need are ticked. A common cause of a partial restore is a narrower selection than intended, especially when restoring to a different share. Note the total item count shown for your selection and compare it with what you expected.

## Inspect filters and the target path

In the same wizard, check whether any file filters or exclusions are active. Filters set during backup or restore can silently omit file types or folders. Also verify the destination path: if you restored into an existing folder, files may have landed in a nested subfolder rather than the root you are browsing. Use File Station search on the target share to look for one missing filename.

## Verification test

Pick one known-missing file, note its exact name and original path, and search the entire target volume. If it appears under a different path, the restore scope or destination was wrong. If it does not appear at all, run a backup integrity check on the vault from Hyper Backup and review the restore log for skipped items.

## Rollback and recovery note

Do not delete the restored data or overwrite the source share while diagnosing. If a second restore is needed, restore to a new empty share first, confirm the files, then move them into place. This preserves the first attempt for comparison.

If the scope looks correct but files remain absent, this is a **synology hyper backup restore missing files** case that needs log-level review.

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) with your restore log and selection details.
