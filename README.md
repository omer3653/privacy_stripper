
# Privacy Stripper 🔍

> Expose and remove hidden metadata from your files before sharing them online.

**100% local processing — your files never leave your device.**

---

## What is this?

Every file you share contains hidden data you never consented to reveal. A photo taken on your phone embeds your exact GPS coordinates, device model, and the precise time it was taken. A Word document reveals who wrote it, which company they work for, and how many times it was edited. This tool exposes all of it — and strips it clean.

---

## Supported Formats

| Format | What it finds |
|--------|--------------|
| **JPG / JPEG** | GPS coordinates, device model & serial, photographer name, timestamps, camera settings |
| **PNG** | Text chunks (author, software, description), timestamps |
| **WEBP** | Full EXIF via RIFF chunk parsing, XMP metadata, ICC profiles |
| **PDF** | Author, company, creator software, creation/modification dates, title |
| **DOCX** | Author, last editor, company, revision count, tracked changes, embedded comments |
| **MP4 / MOV** | Creation date, GPS location, encoder, copyright, artist |
| **HEIC** | Full EXIF (GPS, device, timestamps) — iPhone's default format |

---

## Risk Levels

- 🔴 **CRITICAL** — directly identifies you (GPS, name, email, serial number)
- 🟡 **IDENTIFYING** — reveals device, software, or timestamps
- ⚪ **HARMLESS** — technical data with no privacy impact

---

## Steganography Scan

In addition to standard metadata, the tool runs a heuristic scan for steganographic anomalies:

- Oversized APP blocks in JPEG (possible hidden payloads)
- Unknown chunks in PNG
- Data appended after end-of-file markers
- Hidden JPEG comment markers

> ⚠️ This is heuristic detection — signals indicate anomalies, not confirmed hidden data. For definitive analysis use tools like [StegDetect](http://www.outguess.org/detection.php) or [Stegsolve](https://github.com/zardus/ctf-tools/tree/master/stegsolve).

---

## How it works

1. Drop a file onto the scanner
2. The tool reads raw bytes locally in your browser — no upload, no server
3. You see a full breakdown of every metadata field, categorized by risk
4. Click **PURGE & DOWNLOAD** to get a clean copy with all sensitive data removed

### What gets removed on clean

| Format | What is stripped |
|--------|-----------------|
| JPEG | All APP1 (EXIF), APP13 (IPTC), APP14 (Adobe) markers |
| PNG | tEXt, iTXt, zTXt, tIME chunks |
| WEBP | EXIF, XMP, ICCP chunks |
| PDF | Author, Title, Subject, Keywords, Creator, Producer, Dates |
| DOCX | Core properties (Author, Company, Dates, Revision count) |

---

## Technical Stack

- Vanilla HTML + JavaScript — zero dependencies for core parsing
- [`pdf-lib`](https://pdf-lib.js.org/) — PDF read & write
- Native browser `DecompressionStream` API — for DOCX (ZIP) parsing
- Native `DataView` API — for binary parsing of JPEG, PNG, WEBP, MP4, HEIC

---

## Privacy Guarantee

- No server. No upload. No analytics. No logs.
- All processing happens in-memory in your browser tab.
- The cleaned file is generated locally and downloaded directly to your device.

---

## Roadmap

- [ ] DOCX full metadata clean (deep ZIP rewrite)
- [ ] MP4 metadata strip
- [ ] Batch file processing
- [ ] Drag-and-drop multiple files
- [ ] Export full scan report as PDF

---

## Why this matters

A resume PDF sent from your work computer contains your work email in the Author field. A photo shared on social media reveals your home address via GPS. A document forwarded to a client shows every revision and who made it. Most people have no idea this data exists — this tool makes it visible.
