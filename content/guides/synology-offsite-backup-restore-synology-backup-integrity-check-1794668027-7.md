---
title: "When the Index Is Damaged: Fixing a Synology Backup Integrity Check Failure"
description: "Troubleshoot a Synology backup integrity check failure caused by a damaged index or incomplete backup. Follow step-by-step checks, interpret results, and verify recovery."
seo_title: "Synology Backup Integrity Check Fails: Damaged Index or Incomplete Backup"
seo_description: "Troubleshoot a Synology backup integrity check failure caused by a damaged index or incomplete backup. Follow step-by-step checks, interpret results, and verify recovery."
keywords:
  - "synology backup integrity check"
date: 2026-11-24T12:10:02+08:00
publishDate: 2026-11-24T12:10:02+08:00
draft: false
categories:
  - "Backup & Restore"
category_slug: "backup-restore"
---

You are running an offsite Hyper Backup vault on your Synology NAS, and the integrity check stops with a damaged index or incomplete backup message before you can diagnose it.  

## Check the backup task log and index status
Open Hyper Backup, select the offsite task, and choose Action > Check backup integrity. If it fails, go to the Log tab and note the exact error. A damaged index usually appears as "index file is corrupted" or "backup data is incomplete." Then open File Station and navigate to the vault folder. Verify that the .index and .info files exist and are not zero bytes. A missing or zero-byte index confirms the failure is index-related, not a network issue.

## Run a verification test on the vault
Create a new temporary backup task pointing to the same offsite vault, but do not enable integrity check yet. Run a manual backup of a small test folder. If that backup completes, the vault is reachable and the original task's index is the problem. If it also fails, the vault itself is incomplete and needs recovery.

## Rollback and recovery note
Before deleting or rebuilding anything, export the task configuration and copy the vault's .index files to a local folder. If the index is damaged, use Hyper Backup's restore function to restore the latest version to a temporary share. If restore succeeds, the backup data is intact and only the index needs rebuilding. If restore fails, treat the backup as incomplete and create a new offsite task after verifying the source data.  

After any repair, rerun the **synology backup integrity check** and confirm it completes without errors. For guided diagnosis of a persistent damaged index,

![A Synology backup task and a restored sample folder](/images/service-detail-960.webp "Synology backup restore verification")

[Ask for help](/#consult).
