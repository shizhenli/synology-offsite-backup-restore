---
title: "Synology Backup Integrity Check Failed: Is the Index or the Backup Incomplete?"
description: "Step-by-step diagnosis when a Synology Hyper Backup integrity check fails on an offsite vault. Check index health, verify backup completeness, and recover safely."
seo_title: "Fix Synology Backup Integrity Check Failed: Damaged Index vs Incomplete Backup"
seo_description: "Step-by-step diagnosis when a Synology Hyper Backup integrity check fails on an offsite vault. Check index health, verify backup completeness, and recover safely."
keywords:
  - "synology backup integrity check failed"
date: 2026-11-22T12:08:04+08:00
publishDate: 2026-11-22T12:08:04+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running a Hyper Backup integrity check on your offsite vault and it stops with a damaged index or incomplete backup message, leaving you unsure whether the data or the metadata is at fault.

## First, separate index damage from an incomplete backup

Open Hyper Backup, select the offsite task, and choose Action > Check backup integrity. When it fails, read the exact line: "damaged index" points to the .idx files, while "incomplete backup" means the last version did not finish writing. Note the version timestamp shown. If only the newest version is flagged, the older versions are likely intact and usable.

## Run the targeted checks

1. In File Station, browse the vault's @img folder and confirm the .idx and .info files exist for the flagged version. Missing or zero-byte files confirm index damage.
2. Check the task log for a prior error such as a network drop, full volume, or power loss during the last run. An incomplete backup almost always has a matching log entry.
3. On the destination NAS, verify free space and volume health in Storage Manager. A full or degraded volume corrupts index writes.

Interpretation: if the log shows an interrupted run and older versions pass, treat it as an incomplete backup. If files are missing with no log event, treat it as index damage.

## Verification test

Restore a single small folder from the version before the flagged one to a test share. If it restores and opens, the backup chain is sound and only the latest version needs repair. If the restore also fails, stop and seek help before deleting anything.

## Recovery and rollback note

For index damage, run Action > Rebuild index, then repeat the integrity check. For an incomplete backup, delete only the flagged version and rerun the task. Never delete the vault until a test restore succeeds. If the check still reports **synology backup integrity check failed**, preserve logs and

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before further changes.
