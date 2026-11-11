# File Shepherd · File & Media Curator

A Grok Bot template that herds scattered downloads, photo offloads, screenshots, and backups into an organized archive — and hunts down exact, byte-for-byte duplicates along the way.

**by Ram** · published to the Grok Bot marketplace on October 27, 2026 as **File Shepherd · by Ram**.

This repo is a public, beginner-friendly write-up of that template: what it does, how to install it, how the first-run setup works, and the skills and safety rules it ships with. It is documentation and a portable copy of the skills, not a standalone app you run from the command line.

If you already use Grok Bot, you can import File Shepherd from the marketplace and start talking to it. If you are curious how it is put together, the skill files in this repo are the recipes it follows.

---

## What it is

File Shepherd is a file and media curator for your PC, external drives, and (optionally) Google Drive or OneDrive. On first chat it asks which folders you want it to look after. After that, you can ask it to:

- find exact duplicate files
- tidy a messy Downloads or Desktop folder
- report the biggest space hogs
- propose better names for generic screenshots and clips
- check an external backup drive for files that have not been copied yet

It always starts with a **read-only first pass** and shows you a clear plan before it moves, renames, or removes anything.

---

## Features

The template packs two skills and five core workflows.

### 1. Duplicate File & Media Hunter

Confirms which folders are the main archive versus staging or downloads, then looks for true duplicates only. Files are grouped by exact byte size first, and only size-matched files get a SHA-256 hash. That means "same name" is not enough — two files have to be byte-for-byte identical to be flagged.

For photo libraries (including iPhone offloads), it also watches for names like `IMG_XXXX (1)` or `Copy of…`, and it keeps Live Photo pairs (`.HEIC` + `.MOV`) together so a companion clip is never mistaken for a leftover duplicate.

The report tells you how many duplicate groups were found, how much space you could reclaim, which copy would be kept, and which copies could be moved or removed — then it waits for you.

### 2. Weekly Downloads & Desktop Sweep

Scans `Downloads` and `Desktop` for loose files and sorts them into buckets:

- **Installers & archives:** `.exe`, `.msi`, `.dmg`, `.pkg`, `.zip`, `.7z`, `.rar` (installers older than 7 days are called out)
- **Screenshots & captures:** `.png`, `.jpg`, `.webp`, `.gif`, `.mp4`, `.mov`
- **Documents & spreadsheets:** `.pdf`, `.docx`, `.xlsx`, `.csv`, `.txt`

You get a sorting plan before anything is moved into the folders you already use.

### 3. Storage Space Hog & Large-File Audit

Ranks the largest files and folders (for example, files over 250 MB or 1 GB: raw recordings, old zip archives, cached builds, leftover video exports). For each item it reports the path, size, last-modified date, and whether a backup already exists on another drive.

### 4. Screenshot & Clip Auto-Tagger

Looks at generic names like `IMG_4821.PNG`, `Screenshot (42).png`, or `2026-10-24_19-02-11.mp4`, reads the image or a video frame / metadata, and proposes searchable names in this format:

```text
YYYY-MM-DD_<ProjectOrTopic>_<ShortDescription>.<ext>
```

Renames happen in a batch only after you approve the proposed rename table.

### 5. External Drive Backup Diff

Compares your main folders to an external backup drive by relative path, file size, and SHA-256 hash when needed. The report lists:

- **New or unbacked-up files** that exist on the PC or offload folder but are missing from the backup drive
- **Already backed-up files**, so nothing gets copied twice

It copies only the missing or updated files, and only once you confirm.

A short getting-started skill also walks a new owner through naming the bot, choosing folders, and optionally setting up a weekly sweep or backup-check routine.

---

## How to install (from the Grok Bot marketplace)

File Shepherd is a **Grok Bot template**, not a program you `git clone` and run. Installing it creates your own copy of the bot.

1. Open **Grok Bot** and go to the **bot marketplace** (the catalog of shareable bot templates).
2. Search for **File Shepherd**.
3. Open the listing **File Shepherd · File & Media Curator**, credited as **File Shepherd · by Ram**.
4. Import or add the template. Grok Bot will create a new bot in your sidebar from the recipe — your own chat, your own folders, not the publisher's files or history.
5. Open that new bot and say hello. The getting-started skill should begin on the first conversation.

If you have a direct share link from the marketplace card, that link also works and can be faster than waiting for search results to catch up after a new publish.

You do not need this GitHub repo to use the bot. This repo is here so you can read the skills, cite the project, or adapt the workflows yourself.

---

## First-run setup

On the first conversation, File Shepherd introduces itself in one sentence, then asks these questions **one at a time**:

1. **Name & role.** Keep the name File Shepherd, or customize it for your setup.
2. **Primary folders & drives.** Which folders or drives should it look after? Typical answers are `Downloads`, `Desktop`, a photo or video offload folder, an external backup drive, or Google Drive.
3. **Archive structure.** Where should organized files and verified backups live? Do you already have folders for photos, videos, screenshots, and documents?
4. **Recurring sweeps.** Do you want a weekly Downloads & Desktop sweep, an external-drive backup check, or both?

As you answer, it should:

- save your folder paths, drive layout, and naming preferences
- connect Google Drive if you use it for cloud backups
- create any weekly sweep or backup-check routines you asked for
- offer a first **read-only** duplicate or space-hog scan on one of your folders, with a plan before anything is changed

---

## Example prompts

Once setup is done, you can talk to it like this:

- "Scan my Downloads folder for exact duplicates. Read-only first, and show me a cleanup plan before you change anything."
- "Do a weekly sweep of my Downloads and Desktop. Group the loose files into installers, screenshots, and documents."
- "What are the biggest files on this drive, and do I already have backups of them?"
- "These screenshots are all named IMG_ or Screenshot. Propose a rename table with dates and short descriptions, and wait for me to approve it."
- "Compare my photo offload folder to my external backup drive and tell me what is not backed up yet. Do not copy anything until I say so."
- "I have a messy staging folder and a main archive. Find byte-for-byte duplicates, keep one canonical copy, and show me what could be moved out."

---

## Safety notes

File Shepherd is built to be cautious with your files.

- **Read-only first.** The first pass is a scan and a report. Nothing is moved, renamed, copied, or deleted during that pass.
- **A plan before any action.** You should see counts, reclaimable space, which copy would be kept, and what would happen next.
- **Nothing is deleted without confirmation.** Moving, renaming, copying, or removing files only happens after you approve the plan.
- **Exact duplicates only.** Two files have to match in size and SHA-256 hash. Similar-looking photos or same-named files are not enough.
- **Live Photo pairs stay together.** A `.HEIC` still image and its `.MOV` clip are treated as a pair, not as leftover copies of each other.
- **You choose the folders.** It should confirm the target folders and which one is the main archive before it starts.

If a plan looks wrong, just say no. The files stay where they are.

---

## Folder structure

```text
file-shepherd/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   └── workflow-rules.md    # standing rules the template follows
└── skills/
    ├── duplicate-file-media-cleanup/
    │   └── SKILL.md         # the five curation workflows
    └── file-shepherd-getting-started/
        └── SKILL.md         # first-conversation setup
```

The `skills/` files are sanitized copies of the skills packed into the marketplace template. They do not contain anyone's personal folder paths, names, or accounts.

---

## License

This project is released under the [MIT License](LICENSE). Copyright (c) 2026 Ram.

---

## Credits

**File Shepherd · File & Media Curator** is by **Ram**.

It started as a personal file-and-media curator bot, then was packed as a public Grok Bot template on October 27, 2026 so other people could import the same workflows and point them at their own folders.
