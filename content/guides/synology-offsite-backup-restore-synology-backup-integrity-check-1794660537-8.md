---
title: "Synology Backup Integrity Check Fails: Isolate a Damaged Index from an Incomplete Backup"
description: "Step-by-step diagnosis when a Synology offsite Hyper Backup integrity check reports a damaged index or incomplete backup, with checks, result interpretation, a verification test, and recovery notes."
seo_title: "Synology Backup Integrity Check Fails: Diagnose Damaged Index vs Incomplete Backup"
seo_description: "Step-by-step diagnosis when a Synology offsite Hyper Backup integrity check reports a damaged index or incomplete backup, with checks, result interpretation, a verification test, and recovery notes."
keywords:
  - "synology backup integrity check"
date: 2026-11-17T08:14:51+08:00
publishDate: 2026-11-17T08:14:51+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

Your offsite Hyper Backup vault reports a damaged index or incomplete backup during the integrity check, and you want to know whether the data is recoverable before taking further action.

## Confirm the failure is reproducible and scoped

Run the integrity check again from Hyper Backup > Backup Explorer on the same vault. If it fails at the same percentage or file count, the fault is consistent. If it passes on the second run, suspect a transient network drop during the offsite transfer rather than corruption. Next, open the backup log and note the exact error: a damaged index usually names index or database files, while an incomplete backup names missing chunks or an interrupted job. Check the remote vault's free space and the NAS volume health in Storage Manager; a full destination or a degraded volume can produce both messages.

## Interpret the result precisely

A damaged index means the catalog cannot be read, but the data blocks may still be intact. An incomplete backup means the job ended before all blocks were written, so the last version is partial. Do not delete the vault on either result. Instead, compare the last successful backup timestamp with the failure time to see which version is affected.

## Verification test

Create a new Hyper Backup task to a temporary local folder using the same source share and run a full integrity check there. If the local check passes, the source data is sound and the fault lies in the offsite vault or transfer path. If it fails locally, investigate the source volume first.

## Recovery and rollback

If only the index is damaged, use Backup Explorer to browse versions and restore a known-good version to a test share before overwriting anything. If the backup is incomplete, restore the most recent complete version and re-run the offsite job. Keep the failed vault until the replacement backup verifies successfully. For a controlled diagnosis of your

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[**synology backup integrity check**](/#consult), ask for help before deleting any vault data.
