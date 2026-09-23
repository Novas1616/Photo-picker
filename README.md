# macOS Photo Flag Picker & Auto-Importer for Lightroom Classic

A lightweight Python script tailored for sports and reportage photographers on macOS. It automates and accelerates the ingestion workflow by extracting only in-camera locked (flagged) photos from SD cards, applying initial metadata sidecars, and handing them over to Adobe Lightroom Classic.

## 🚀 Key Features

- **In-Camera Flag Detection:** Scans connected memory cards mounted under `/Volumes` and copies only protected/locked files (supports `.RW2`, `.ORF`, and `.JPG`).
- **EXIF-Based Duplicate Prevention:** Identifies previously imported images across your Lightroom storage by parsing exact EXIF capture timestamps and file names, preventing duplicate ingestion even across card re-use.
- **Automated XMP Sidecars:** Automatically writes an Adobe-compliant `.xmp` sidecar alongside each image, pre-tagging files with a 5-star rating (`xmp:Rating="5"`), creator credentials, and copyright information.
- **macOS System Lock Removal:** Strips native system immutability flags (`UF_IMMUTABLE`) and updates file permissions to `0777` so Lightroom Classic can move and catalog files seamlessly.
- **Zero External Dependencies:** Built purely using the standard Python 3 library—no additional pip packages required.

## ⚙️ Requirements

- macOS
- Python 3.x
- Adobe Lightroom Classic (with *Auto Import* enabled)

## 🛠️ Configuration & Usage

### 1. Configure the Script
Edit the configuration variables at the top of `picker.py` to match your environment:

```python
AUTHOR_NAME = "Michal Novák"
COPYRIGHT_TEXT = f"© 2026 {AUTHOR_NAME}. All rights reserved."

# Folder monitored by Lightroom Classic Auto Import
WATCHED_FOLDER = os.path.join(HOME, "Pictures", "fotografie", "raw", "import")
