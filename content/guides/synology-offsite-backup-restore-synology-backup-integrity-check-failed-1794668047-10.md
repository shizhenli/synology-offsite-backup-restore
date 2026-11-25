---
title: "Synology Backup Integrity Check Failed: Isolate the Damaged Index Before You Restore"
description: "Fix a Synology offsite Hyper Backup integrity check failure caused by a damaged index or incomplete backup. Step-by-step diagnosis and safe recovery."
seo_title: "Synology Backup Integrity Check Failed: Diagnose a Damaged Index"
seo_description: "Fix a Synology offsite Hyper Backup integrity check failure caused by a damaged index or incomplete backup. Step-by-step diagnosis and safe recovery."
keywords:
  - "synology backup integrity check failed"
date: 2026-11-25T09:07:46+08:00
publishDate: 2026-11-25T09:07:46+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running an offsite Hyper Backup vault on your Synology NAS, and the integrity check stops with a damaged index or incomplete backup message before you can complete a controlled diagnosis.

## Confirm the failure scope
Open Hyper Backup, select the offsite task, and run Action > Integrity check again. In the log, note the exact timestamp and whether the error names a specific .idx file or reports a missing chunk. A single index error usually means the local index is stale; multiple missing chunks point to an interrupted transfer. Write down the backup version number shown in the log.

## Check the vault and local index
On the remote Synology, open the shared folder that hosts the vault and confirm the .hbk directory exists and is readable. On the source NAS, go to Control Panel > Shared Folder and verify the task's database folder has free space; a full volume truncates the index silently. Then open Hyper Backup Vault on the remote unit and confirm the task is listed as healthy. If the remote vault shows the task as incomplete, the last backup did not commit.

## Verification test
Create a small test share with one text file, add it to a new temporary backup task pointing at the same remote vault, and run an integrity check on that task only. If the test passes, the vault and credentials are sound and the fault is isolated to the original task's index. If it fails, stop and treat the remote vault as suspect.

## Recovery note
Do not delete the existing versions. Instead, use Hyper Backup's backup explorer to restore a single file from the last known-good version; if that succeeds, the data is intact and only the index needs rebuilding. Keep the failed task disabled until you have verified a restore, so a partial write cannot overwrite good versions.

If the index cannot be rebuilt without risking the vault,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting anything. A failed **synology backup integrity check failed** result is recoverable when you isolate the index first.
