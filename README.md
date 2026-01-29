# MiKTeX Portable: Complete Installation Guide for Restricted Work Computers

🌐 **[Deutsche Version / German Version](README.de.md)**

A step-by-step guide to setting up a complete LaTeX environment on computers without administrator rights and with restrictions on executing `.exe`, `.bat`, and `.cmd` files.

## 📋 Table of Contents

- [Overview](#overview)
- [Requirements](#requirements)
- [Part 1: Creating MiKTeX Portable](#part-1-creating-miktex-portable)
- [Part 2: Transferring to the Work Computer](#part-2-transferring-to-the-work-computer)
- [Part 3: Configuring TeXstudio](#part-3-configuring-texstudio)
- [Part 4: Setting up Sumatra PDF (optional)](#part-4-setting-up-sumatra-pdf-optional)
- [Command Reference](#command-reference)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

### The Problem

Many work computers (especially in corporate environments) have the following restrictions:

- ❌ No administrator rights
- ❌ Execution of `.exe` installers blocked
- ❌ Execution of `.bat` and `.cmd` files blocked
- ❌ No ability to install software

### The Solution

This guide shows how to:

1. Create a complete MiKTeX installation on an **unrestricted computer** (e.g., home PC)
2. Transfer it as a **ZIP file** via a cloud service
3. Simply unpack and configure on the **restricted work computer**

**Result:** A fully functional LaTeX environment with ~4,500 packages, without installation.

### Size Information

| Component | Size |
|-----------|------|
| MiKTeX Repository (download) | ~5.5 GB |
| MiKTeX Portable (installed) | ~10-11 GB |
| MiKTeX Portable (ZIP) | ~6-7 GB |
| TeXstudio Portable | ~150 MB |
| Sumatra PDF Portable | ~15 MB |

---

## Requirements

### On the Helper Computer (e.g., home PC)

- ✅ Windows 10/11 with administrator rights
- ✅ Internet connection
- ✅ ~15 GB free disk space
- ✅ 7-Zip (recommended) for faster compression
- ✅ Access to a cloud service (Google Drive, Mega, Dropbox, etc.)

### On the Work Computer

- ✅ Windows 10/11
- ✅ Ability to unpack ZIP files with Windows built-in tools
- ✅ Write permissions in at least one folder (e.g., `D:\` or your user directory)

---

## Part 1: Creating MiKTeX Portable

> ⚠️ **All steps in this part are performed on the helper computer!**

### Step 1.1: Create Folder Structure

Create two folders:

```
C:\MiKTeX-Repo        (for downloading packages)
C:\MiKTeX-Portable    (for the installation)
```

### Step 1.2: Download MiKTeX Setup Utility

1. Go to https://miktex.org/download
2. Scroll to **"All downloads"**
3. Download **"MiKTeX Setup Utility"** (`miktexsetup_standalone.exe`)
4. Save the file to `C:\MiKTeX-Repo`

> 💡 If a ZIP file is downloaded, unpack it first.

### Step 1.3: Open Command Prompt

1. Press `Windows + R`
2. Type `cmd` and press Enter
3. Navigate to the folder:

```cmd
cd C:\MiKTeX-Repo
```

### Step 1.4: Download All Packages

Run the following command (all in one line):

```cmd
miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://ftp.fau.de/ctan/systems/win32/miktex/tm/packages/ download
```

> 💡 **Alternative Mirror Servers** (if the above doesn't work):
> 
> **Netherlands:**
> ```cmd
> miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://ftp.snt.utwente.nl/pub/software/tex/systems/win32/miktex/tm/packages/ download
> ```
> 
> **Automatic Mirror Selection:**
> ```cmd
> miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://mirror.ctan.org/systems/win32/miktex/tm/packages/ download
> ```

⏱️ **Duration:** 30-60 minutes (depending on internet speed)

**Expected Result:** ~5.5 GB in the folder `C:\MiKTeX-Repo`

### Step 1.5: Perform Portable Installation

Run the following command:

```cmd
miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --portable=C:\MiKTeX-Portable install
```

⏱️ **Duration:** 15-30 minutes

**Expected Warnings (can be ignored):**
- `Windows API error 3` – just a warning, not a failure
- `eptex engine not found` – only affects Japanese fonts
- `not yet checked for updates` – normal for fresh installation

### Step 1.6: Create ZIP File

**With 7-Zip (recommended, ~10-20 minutes):**

1. Right-click on `C:\MiKTeX-Portable`
2. **7-Zip** → **"Add to archive..."**
3. Archive format: **ZIP**
4. Click **OK**

**With Windows built-in tools (~1-3 hours):**

1. Right-click on `C:\MiKTeX-Portable`
2. **"Send to"** → **"Compressed (zipped) folder"**

### Step 1.7: Upload to Cloud

Upload the ZIP file to:
- **Google Drive** (https://drive.google.com) – recommended, fast and stable
- **Mega** (https://mega.io)
- **Dropbox** (https://dropbox.com)
- **OneDrive** (https://onedrive.live.com)

Create a sharing link and save it.

### Step 1.8: Clean Up (optional)

After successful upload, the following folders can be deleted:
- `C:\MiKTeX-Repo` (~5.5 GB)
- `C:\MiKTeX-Portable` (~4 GB)
- The created ZIP file

---

## Part 2: Transferring to the Work Computer

> ⚠️ **All steps in this part are performed on the work computer!**

### Step 2.1: Download Files

Download the following files:

1. **MiKTeX Portable ZIP** (from the cloud)
2. **TeXstudio Portable:** https://github.com/texstudio-org/texstudio/releases → `texstudio-*-win-portable-qt6.zip`
3. **Sumatra PDF Portable (optional):** https://www.sumatrapdfreader.org/download-free-pdf-viewer → Portable version

### Step 2.2: Create Folder Structure

Create a main folder for LaTeX:

```
D:\LaTeX\
├── MiKTeX-Portable\
├── TeXstudio\
└── SumatraPDF\        (optional)
```

### Step 2.3: Unpack Files

Unpack all ZIP files to the corresponding folders:

1. Right-click on ZIP → **"Extract All..."**
2. Select destination folder

> ⚠️ **Note:** Unpacking MiKTeX with Windows built-in tools can take several hours. Best to let it run overnight.

---

## Part 3: Configuring TeXstudio

### Step 3.1: Start TeXstudio

1. Navigate to `D:\LaTeX\TeXstudio\`
2. Start `texstudio.exe`
3. When the warning "No LaTeX distribution found" appears → click **OK**

### Step 3.2: Configure Commands

1. Go to **Options** → **Configure TeXstudio...**
2. Click **Commands** on the left
3. Enter the following paths:

| Command | Entry |
|---------|-------|
| **LaTeX** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\latex.exe -src -interaction=nonstopmode %.tex` |
| **PdfLaTeX** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\pdflatex.exe -synctex=1 -interaction=nonstopmode %.tex` |
| **XeLaTeX** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\xelatex.exe -synctex=1 -interaction=nonstopmode %.tex` |
| **LuaLaTeX** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\lualatex.exe -synctex=1 -interaction=nonstopmode %.tex` |
| **BibTeX** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\bibtex.exe %.aux` |
| **Biber** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\biber.exe %` |
| **Makeindex** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\makeindex.exe %.idx` |
| **Texindy** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\texindy.exe %.idx` |
| **Makeglossaries** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\makeglossaries.exe %` |
| **Asymptote** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\asy.exe %.asy` |
| **dvips** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\dvips.exe -o %.ps %.dvi` |
| **ps2pdf** | `D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64\ps2pdf.exe %.ps` |

> 💡 **Adjust the path** if you unpacked MiKTeX to a different folder!

### Step 3.3: Build Settings

1. Click **Build** on the left
2. Set the following options:

| Setting | Value |
|---------|-------|
| **Default Compiler** | PdfLaTeX |
| **Default Bibliography Tool** | BibTeX |
| **PDF Viewer** | Internal PDF Viewer |

### Step 3.4: Editor Settings (recommended)

1. Click **Editor** on the left
2. Enable:
   - ✅ Show line numbers
   - ✅ Code folding
   - ✅ Auto indentation

### Step 3.5: Spell Check (recommended)

1. Click **Language Checking** on the left
2. Set:
   - **Default Language:** en_US (English) or your preferred language
   - ✅ Check spelling

### Step 3.6: Save Configuration

Click **OK** to save all settings.

---

## Part 4: Setting up Sumatra PDF (optional)

Sumatra PDF is a fast, lightweight PDF viewer with SyncTeX support – ideal for LaTeX.

### Step 4.1: Integrate Sumatra in TeXstudio

1. Go to **Options** → **Configure TeXstudio...**
2. Click **Commands** on the left
3. For **External PDF Viewer** enter:

```
D:\LaTeX\SumatraPDF\SumatraPDF.exe -reuse-instance -forward-search "%.tex" @ %.pdf
```

### Step 4.2: Switch PDF Viewer

1. Click **Build** on the left
2. Change **PDF Viewer** to: **External PDF Viewer**

### Step 4.3: Configure Inverse Search in Sumatra (optional)

To jump from Sumatra back to TeXstudio:

1. Open Sumatra PDF
2. Go to **Settings** → **Options**
3. For **Set inverse search command line** enter:

```
"D:\LaTeX\TeXstudio\texstudio.exe" "%f" -line %l
```

Now you can:
- In TeXstudio: PDF opens at the correct position
- In Sumatra: Double-click jumps to the corresponding position in the code

---

## Command Reference

### Compiler Overview

| Compiler | Usage |
|----------|-------|
| **PdfLaTeX** | Standard for most documents |
| **XeLaTeX** | For system fonts and Unicode |
| **LuaLaTeX** | Most modern compiler, Lua scripting |
| **LaTeX** | Produces DVI (rarely needed) |

### Bibliography Tools

| Tool | Usage |
|------|-------|
| **BibTeX** | Classic, for `.bib` files |
| **Biber** | Modern, for `biblatex` package |

### Index Tools

| Tool | Usage |
|------|-------|
| **Makeindex** | Standard for creating indices |
| **Texindy** | For multilingual indices |
| **Makeglossaries** | For glossaries and acronym lists |

### Command Parameters Explained

| Parameter | Meaning |
|-----------|---------|
| `-synctex=1` | Enables SyncTeX (click in PDF → jumps to code) |
| `-interaction=nonstopmode` | Compiler runs through on errors without stopping |
| `-src` | Adds source file information |
| `%.tex` | Placeholder for the filename |
| `-reuse-instance` | Opens PDF in already running Sumatra window |
| `-forward-search` | Enables forward search in Sumatra |

---

## Troubleshooting

### Problem: "No LaTeX distribution found"

**Solution:** The paths in TeXstudio are incorrectly configured. Check if the path to `pdflatex.exe` is correct.

### Problem: Server error 503 during download

**Solution:** The CTAN mirror is overloaded. Use a different mirror (see Step 1.4).

### Problem: Unpacking with Windows takes very long

**Solution:** Normal for large ZIP files with many small files. Either:
- Let it run overnight
- Unpack with 7-Zip on the helper computer and upload the finished folder

### Problem: "eptex engine not found" warning

**Solution:** Can be ignored – only affects Japanese typography.

### Problem: Packages missing during compilation

**Solution:** With the Complete installation, all packages should be present. If something is still missing, the installation may have been incomplete.

---

## License

This guide is published under the [MIT License](https://opensource.org/licenses/MIT).

**Software used:**
- [MiKTeX](https://miktex.org/) – MIT License
- [TeXstudio](https://www.texstudio.org/) – GPL v2
- [Sumatra PDF](https://www.sumatrapdfreader.org/) – (A)GPL v3

---

## Contributing

Feedback, corrections, and suggestions for improvement are welcome! Simply create an issue or a pull request.

---

*Last updated: January 2026*
