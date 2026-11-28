---
title: "Synology Backup Integrity Check Fails: Repair a Damaged Index Before Restore"
description: "Troubleshoot a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup, with exact checks and a recovery path."
seo_title: "Synology Backup Integrity Check Fails: Fix Damaged Index"
seo_description: "Troubleshoot a Synology offsite Hyper Backup vault when the integrity check reports a damaged index or incomplete backup, with exact checks and a recovery path."
keywords:
  - "synology backup integrity check"
date: 2026-11-28T22:22:13+08:00
publishDate: 2026-11-28T22:22:13+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

## Understand the failure before you act

You run an offsite Hyper Backup vault and the integrity check stops with a damaged index or incomplete backup message, so you cannot trust the restore yet. Treat this as a diagnostic step, not a verdict on the whole vault.

## Run the targeted checks

1. Confirm the vault path and repository name in Hyper Backup match the remote folder exactly. A renamed or moved vault folder produces index errors that look like corruption.
2. Check free space on the remote NAS. If the vault volume is full, the last backup set may be incomplete; compare the last successful task log timestamp with the reported failure.
3. Verify the integrity check ran against the correct version. In Hyper Backup, open Backup Explorer, select the latest version, and run the check again. If only older versions fail, the damage is historical, not active.
4. Review the remote volume health in Storage Manager. A degraded volume or bad sector can corrupt the index file even when the backup task itself succeeded.

## Interpret the results

If the check passes on the latest version but fails on an older one, keep the latest and exclude the damaged version from restore planning. If it fails on every version with the same index error, the repository index is damaged. If it reports incomplete backup, the last transfer was interrupted; the previous version is usually intact.

## Verification test

Restore a single small folder from the latest version to a temporary shared folder. Open the restored files and confirm they match the source. A clean single-file restore is your proof that the vault is usable.

## Recovery note

Before repairing, export the Hyper Backup configuration and copy the vault index file to a safe location. If repair fails, recreate the vault and seed a fresh full backup rather than overwriting the only copy. For a controlled **synology backup integrity check** on a damaged repository,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting any version.
