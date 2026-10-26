📸 macOS Photo Flag Picker & Auto-Importer for Lightroom Classic

Import only your best shots. Straight from the camera to Lightroom Classic.

A lightweight, fast Python tool for sports, event, and reportage photographers using macOS. It scans mounted memory cards, identifies in-camera protected or locked photos, generates Adobe-compatible XMP sidecars, and prepares selected images for import into Adobe Lightroom Classic.

Skip the tedious task of culling thousands of images on your Mac. Flag your keepers in-camera, run the picker, and let Lightroom handle the rest.

✨ Features
In-Camera Flag Detection — Scans mounted volumes under /Volumes and selects protected or locked files. Supports .RW2, .ORF, and .JPG.
Automatic XMP Sidecars — Generates an XMP sidecar for each selected image, including a 5-star rating, creator metadata, and copyright information.
Lightroom Classic Auto Import — Copies selected images and their sidecars into a configured watched folder.
macOS File Permission Handling — Removes the UF_IMMUTABLE file flag when necessary and updates file permissions to help prevent import and file-movement issues.
Duplicate Prevention — Uses image filenames and EXIF capture timestamps to identify previously imported photos and reduce duplicate ingestion.
Zero External Dependencies — Uses only the Python 3 standard library. No pip packages, ExifTool, or third-party libraries required.
Apple Silicon & Intel Support — Designed for macOS systems running on both Apple Silicon and Intel processors.
🖥️ Requirements
macOS
Python 3.x
Adobe Lightroom Classic
A memory card reader or mounted camera storage
Lightroom Classic Auto Import configured and enabled
⚙️ Installation & Configuration
1. Download the Script

Clone the repository or download picker.py directly.

bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY


Replace YOUR_USERNAME and YOUR_REPOSITORY with your actual GitHub username and repository name.

2. Configure Your Metadata

Open picker.py and update the configuration variables near the top of the file.

python
# --- MAC CONFIGURATION ---

AUTHOR_NAME = "Michal Novák"
COPYRIGHT_TEXT = f"© 2026 {AUTHOR_NAME}. All rights reserved."

HOME = os.path.expanduser("~")

# Folder monitored by Lightroom Classic Auto Import
WATCHED_FOLDER = os.path.join(
    HOME,
    "Pictures",
    "fotografie",
    "raw",
    "import",
)


Adjust the author name, copyright text, and watched folder to match your workflow.

3. Configure Lightroom Classic Auto Import
Open Adobe Lightroom Classic.
Navigate to File → Auto Import → Auto Import Settings.
Enable Auto Import.
Set the Watched Folder to the same directory configured in WATCHED_FOLDER.
Choose a destination folder where Lightroom Classic should store imported images.
Confirm the settings.
Important: Lightroom Classic must be configured to watch the correct folder. The script's destination and Lightroom's watched folder must match.
🚀 Usage
Option A: Run from Terminal
Insert your SD or CFexpress card.
Open Terminal.
Navigate to the directory containing picker.py.
Run:
bash
python3 picker.py


The script scans mounted volumes, identifies eligible protected images, checks for duplicates, generates XMP sidecars, and copies selected files to the configured import folder.

Option B: Create a Clickable macOS Application

You can launch the script through a simple Automator application without opening Terminal manually.

Open Automator.
Create a new Application.
Search for Run Shell Script and add the action.
Select /bin/bash or /bin/zsh as the shell.
Enter the following command, updating the path to your script:
bash
/usr/bin/python3 "/Users/YOUR_USERNAME/path/to/picker.py"

Save the application as Photo Picker.app.
Optionally, customize the application icon using Get Info (⌘ + I).

You can now launch the picker by double-clicking the application.

Note: macOS may request permission to access removable volumes or files in protected folders. Grant only the permissions needed for your workflow.
📂 Supported Image Formats

The default supported extensions are:

Format	Extension
Panasonic RAW	.rw2
OM SYSTEM / Olympus RAW	.orf
JPEG	.jpg

Extensions are matched case-insensitively.

Additional formats, such as Canon RAW (.cr3), Sony RAW (.arw), and Nikon RAW (.nef), may be added by updating the script's supported-extension list.

Important: Adding an extension only enables file selection. It does not guarantee that every camera's protection flags or metadata will be interpreted correctly.

⭐ XMP Metadata

For each selected image, the script creates an accompanying XMP sidecar containing metadata intended for Adobe Lightroom Classic.

The default workflow includes:

A 5-star rating (xmp:Rating="5")
Creator information
Copyright information
Metadata associated with the original image

The sidecar is intended to let Lightroom recognize the selected images as pre-rated keepers during import.

🔁 Duplicate Prevention

The picker uses filenames and EXIF capture timestamps to help identify previously imported images.

This is particularly useful when reusing the same memory card across multiple events without formatting it after every shoot.

Duplicate detection depends on the metadata available in the image files and the implementation's matching logic. It should not be treated as a guarantee that every duplicate or filename collision will be detected.

🔐 File Permissions & Safety

The script may remove the macOS UF_IMMUTABLE file flag and update permissions on selected files to help Lightroom access them.

Use caution: Setting permissions to 0777 grants read, write, and execute permissions to all users. This is broader than most photo-import workflows require. Prefer the least-permissive settings that allow the script and Lightroom Classic to access the files.

The script should never modify or delete the originals on your memory card unless that behavior is explicitly implemented and intended.

🛠️ Troubleshooting
Lightroom does not import the images
Verify that Auto Import is enabled.
Check that WATCHED_FOLDER matches Lightroom's configured watched folder.
Ensure Lightroom can access the destination folder.
Confirm that the selected files and XMP sidecars are copied successfully.
No protected images are detected
Confirm that the camera marks the intended images as protected or locked.
Check that the memory card is mounted under /Volumes.
Verify that your camera model stores protection information in a format recognized by the script.
Confirm that the file extension is supported.
Permission errors occur
Check macOS privacy permissions for removable volumes and the relevant folders.
Verify file ownership and access permissions.
Avoid applying unnecessarily broad permissions to entire memory cards or directories.
Duplicate images are imported
Check whether the files contain readable EXIF capture timestamps.
Verify how the script compares filenames and timestamps.
Remember that different cameras may produce identical filenames or timestamps.
🗺️ Roadmap

Potential future improvements:

Support additional RAW formats (.CR3, .ARW, .NEF, and others).
Add a dry-run mode to preview selected files before copying.
Provide a configurable rating instead of a fixed 5-star rating.
Improve duplicate detection across different camera models.
Add structured logging and an import summary.
Add optional automatic monitoring of newly mounted memory cards.
Package the script as a standalone macOS application.
🤝 Contributing

Contributions, bug reports, and feature requests are welcome.

Fork the repository.
Create a feature branch.
Commit your changes.
Open a pull request with a clear description of the changes.

When reporting a bug, include your macOS version, Python version, camera model, image format, and any relevant error messages. Avoid sharing private photographs or sensitive metadata.

📄 License

No license has been specified yet.

Before publishing the project as open source, add a LICENSE file and select a license that matches your intended terms of use.

Built for photographers who know their keepers before they leave the camera. 📸
