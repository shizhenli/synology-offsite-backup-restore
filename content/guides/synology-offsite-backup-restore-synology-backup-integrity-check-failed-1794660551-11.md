---
title: "Synology Backup Integrity Check Failed: Isolate a Damaged Index Before You Restore"
description: "Fix a Synology backup integrity check failure on an offsite Hyper Backup vault. Isolate a damaged index or incomplete backup with targeted checks and a safe verification test."
seo_title: "Synology Backup Integrity Check Failed: Diagnose a Damaged Index"
seo_description: "Fix a Synology backup integrity check failure on an offsite Hyper Backup vault. Isolate a damaged index or incomplete backup with targeted checks and a safe verification test."
keywords:
  - "synology backup integrity check failed"
date: 2026-11-17T11:07:29+08:00
publishDate: 2026-11-17T11:07:29+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

## Troubleshooting

You are running an integrity check on your offsite Hyper Backup vault, and it stops with a damaged index or incomplete backup message before you can trust a restore. Start by isolating whether the fault is in the local backup database or the remote vault data. In Hyper Backup, open the backup task and run the integrity check again while watching the log for the exact repository path it flags. If the log names a .idx or index file, the local database is suspect; if it names a chunk or segment file, the remote vault is incomplete. Next, confirm the remote vault is fully mounted and reachable: in File Station or the remote connection settings, verify the vault path resolves and that no scheduled job was interrupted mid-run. Check available space on both the NAS volume and the remote destination; a vault that filled during the last run often reports an incomplete backup. Then run a verification test: create a small test share, back it up to the same vault, and run an integrity check on that task alone. If the test passes, the original task's index is damaged; if it fails, the vault itself is compromised. For recovery, do not delete the vault. Instead, use Hyper Backup's restore browser to copy a known-good version to a staging share, then rebuild the task against a fresh vault folder. Keep the old vault until the new one verifies. If the **synology backup integrity check failed** persists after a clean test task, the index cannot be trusted and you should

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult) before overwriting any restore point.
