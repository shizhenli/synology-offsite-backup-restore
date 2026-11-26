---
title: "Synology Hyper Backup Index Corrupted: Diagnose a Failing Integrity Check"
description: "Troubleshoot a Synology Hyper Backup integrity check that reports a damaged index or incomplete backup on an offsite vault, with exact checks, result interpretation, and a verification test."
seo_title: "Fix Synology Hyper Backup Index Corrupted Integrity Check"
seo_description: "Troubleshoot a Synology Hyper Backup integrity check that reports a damaged index or incomplete backup on an offsite vault, with exact checks, result interpretation, and a verification test."
keywords:
  - "synology hyper backup index corrupted"
date: 2026-11-26T10:06:01+08:00
publishDate: 2026-11-26T10:06:01+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running an integrity check on your offsite Hyper Backup vault and it stops with a damaged index or incomplete backup message, leaving you unsure whether the data is recoverable. This is a controlled diagnosis, not a reason to delete the vault.

## Confirm the Exact Failure Point

Open Hyper Backup, select the task, and choose Action > Check backup integrity. Read the result panel rather than the summary popup. If it names a specific .idx file or index database, the index is damaged. If it says the backup is incomplete, the last version did not finish writing. Note the version timestamp and whether the message appears at the start or after several minutes. A failure at the start points to the index; a failure partway through points to missing blocks.

## Rule Out the Vault and Connection

On the remote Synology, open the shared folder holding the vault and confirm the .hbk directory and its index files are present and not zero bytes. Check Storage Manager for bad sectors or a degraded volume. Re-run the integrity check once after remounting the remote folder. If the same index file is flagged, the index is genuinely corrupted; if the error moves, suspect the connection or remote disk.

## Verification Test

Restore a single small file from the most recent version to a temporary folder. If the restore completes and the file opens, the data blocks are intact and only the index needs rebuilding. If the restore fails at the same point, treat the version as incomplete and restore from the previous version instead.

## Recovery and Rollback

Before any repair, copy the .hbk folder or take a snapshot on the remote NAS. Then run Action > Rebuild index if available; otherwise restore the previous known-good version and re-run the backup. If the index remains corrupted, stop and

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before deleting versions. A corrupted **synology hyper backup index corrupted** state is recoverable when you preserve the vault first.
