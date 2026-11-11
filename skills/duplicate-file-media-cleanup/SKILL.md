---
name: Duplicate File & Media Cleanup
description: >-
  Use when scanning folders, external drives, or cloud storage to find and clean
  up duplicate files, sweep Downloads/Desktop, audit large space-hog files,
  auto-tag screenshots and clips, or diff backups against an external drive.
---
# Duplicate File & Media Library Cleanup

## Core Workflows

### 1. Duplicate File & Media Hunter
1. **Confirm Target Folders & Drives:** Verify which folders, external drives, or cloud folders (PC folders, external drives, OneDrive, or Google Drive) to scan, and which folder is the primary/canonical archive vs. staging or downloads folders.
2. **Hash & Compare Files (Read-Only First):**
   - Group candidate files by exact byte size first, then compute SHA-256 hashes on size-matched files so only true byte-for-byte duplicates are flagged.
   - For photo and media libraries (such as iPhone offloads), also check for `IMG_XXXX (1)` / `Copy of` naming patterns and keep Live Photo `.HEIC` + `.MOV` pairs together so companion clips are never mistaken for duplicates.
3. **Present a Cleanup Plan Before Acting:** Show how many duplicate groups and total reclaimable MB/GB were found, which canonical copy is kept, and which copies will be moved to a staging/archive folder or removed.

### 2. Weekly Downloads & Desktop Sweep
1. Scan `Downloads` and `Desktop` for loose files and group them into clear buckets:
   - **Installers & Archives:** `.exe`, `.msi`, `.dmg`, `.pkg`, `.zip`, `.7z`, `.rar` (flag installers older than 7 days that can be archived or removed).
   - **Screenshots & Captures:** `.png`, `.jpg`, `.webp`, `.gif`, `.mp4`, `.mov`.
   - **Documents & Spreadsheets:** `.pdf`, `.docx`, `.xlsx`, `.csv`, `.txt`.
2. Present a one-click sorting plan before moving files into the user's organized destination folders.

### 3. Storage Space Hog & Large-File Audit
1. Scan target drives/folders and rank the largest files and directories (e.g., files over 250 MB or 1 GB, such as raw OBS/gameplay recordings, old zip archives, cached builds, or duplicate video exports).
2. Report each item's path, size, last-modified date, and whether it already has a backup copy on another drive before taking any action.

### 4. Screenshot & Clip Auto-Tagger
1. Inspect generic filenames (like `IMG_4821.PNG`, `Screenshot (42).png`, or `2026-10-24_19-02-11.mp4`).
2. Read the image or video frame/metadata and propose clean, searchable names formatted as `YYYY-MM-DD_<ProjectOrTopic>_<ShortDescription>.<ext>`.
3. Rename in batch only after the user approves the proposed rename table.

### 5. External Drive Backup Diff
1. Compare the primary PC/offload folders against the external backup drive by relative path, file size, and SHA-256 hash when needed.
2. Report:
   - **New / Unbacked-up files** that exist on the PC or phone offload folder but are missing from the external drive.
   - **Already backed-up files** so nothing gets copied twice.
3. Copy only the missing or updated files once the user confirms.
