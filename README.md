### 📸 macOS Photo Flag Picker & Auto-Importer for Lightroom Classic

A lightweight, lightning-fast Python script tailored for sports, event, and reportage photographers on macOS.

This tool automates the ingestion workflow by extracting only in-camera locked (flagged/protected) photos from your SD/CFexpress cards, automatically generating Adobe-compliant XMP sidecars (with metadata and 5-star ratings), and handing them over to Adobe Lightroom Classic via the Auto-Import feature.

Stop wasting time culling thousands of photos on your Mac. Lock your best shots directly in-camera during the game/event, run this app, and let Lightroom import only the winners.

🚀 Key Features

In-Camera Flag Detection: Scans connected memory cards mounted under /Volumes and copies only protected/locked files (supports .RW2, .ORF, and .JPG).

Automated XMP Sidecars: Automatically writes an .xmp sidecar alongside each image. It pre-tags files with a 5-star rating (xmp:Rating="5") and applies your creator credentials and copyright information.

macOS System Lock Removal: Strips native system immutability flags (UF_IMMUTABLE) and updates file permissions to 0777 so Lightroom Classic can move and catalog files seamlessly without permission errors.

EXIF-Based Duplicate Prevention: Identifies previously imported images by parsing exact EXIF capture timestamps and file names. Prevents duplicate ingestion even if you reuse the same card without formatting.

Zero External Dependencies: Built purely using the standard Python 3 library. No need to install pip packages, exiftool, or third-party libraries. It reads EXIF data directly via binary parsing for maximum speed on Apple Silicon (M1/M2/M3) and Intel Macs.

⚙️ Requirements

macOS (Tested on Apple Silicon & Intel)

Python 3.x (Pre-installed on most Macs, or via Homebrew)

Adobe Lightroom Classic (with Auto Import enabled)

🛠️ Setup & Configuration

1. Configure the Script

Open picker.py in any text editor and update the variables at the top to match your identity and folder structure:

# --- MAC CONFIGURATION ---
AUTHOR_NAME = "Michal Novák" 
COPYRIGHT_TEXT = f"© 2026 {AUTHOR_NAME}. All rights reserved."

# Folder monitored by Lightroom Classic Auto Import
WATCHED_FOLDER = os.path.join(HOME, "Pictures", "fotografie", "raw", "import")


2. Configure Lightroom Classic Auto Import

Open Adobe Lightroom Classic.

Go to File -> Auto Import -> Auto Import Settings...

Check Enable Auto Import.

Set the Watched Folder to the exact same path you defined in WATCHED_FOLDER in the script.

Set the Destination folder where you want Lightroom to permanently move the files.

Click OK.

💻 How to Run It

Option A: Via Terminal

Simply plug in your SD card, open Terminal, and run:

python3 picker.py


Option B: Create a Clickable macOS App (Recommended)

You don't need to open the Terminal every time. You can wrap this script into a native macOS app using Automator:

Open Automator on your Mac and create a new Application.

Search for the action Run Shell Script and drag it to the right pane.

Set the "Shell" dropdown to /bin/bash or /bin/zsh.

Paste the following command (update the path to where you saved the script):

/usr/bin/python3 /Users/YOUR_USERNAME/path/to/picker.py


Save the Automator document as "Photo Picker.app" in your Applications folder.

(Optional) You can copy any custom icon, select your new App, press Cmd + I (Get Info), and paste the new icon over the default Automator icon in the top left corner.

Done! Now, whenever you insert an SD card, just double-click your new app.

⚠️ Notes & Troubleshooting

Permissions: The first time you run the script (or the Automator app), macOS will ask for permission to access Removable Volumes. You must click Allow so the script can read your SD cards.

Supported Formats: The script currently looks for .rw2, .orf, and .jpg (case-insensitive). You can easily add more extensions like .cr3, .arw, or .nef by editing the .endswith() tuple in the code.
