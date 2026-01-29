# MiKTeX Portable: Komplette Installationsanleitung für eingeschränkte Arbeitsrechner

🌐 **[English Version](README.md)**

Eine Schritt-für-Schritt-Anleitung zur Einrichtung einer vollständigen LaTeX-Umgebung auf Rechnern ohne Administratorrechte und mit Einschränkungen bei der Ausführung von `.exe`-, `.bat`- und `.cmd`-Dateien.

## 📋 Inhaltsverzeichnis

- [Übersicht](#übersicht)
- [Voraussetzungen](#voraussetzungen)
- [Teil 1: MiKTeX Portable erstellen](#teil-1-miktex-portable-erstellen)
- [Teil 2: Auf den Arbeitsrechner übertragen](#teil-2-auf-den-arbeitsrechner-übertragen)
- [Teil 3: TeXstudio konfigurieren](#teil-3-texstudio-konfigurieren)
- [Teil 4: Sumatra PDF einrichten (optional)](#teil-4-sumatra-pdf-einrichten-optional)
- [Befehlsreferenz](#befehlsreferenz)
- [Fehlerbehebung](#fehlerbehebung)
- [Lizenz](#lizenz)

---

## Übersicht

### Das Problem

Auf vielen Arbeitsrechnern (besonders in Unternehmen) gibt es folgende Einschränkungen:

- ❌ Keine Administratorrechte
- ❌ Ausführung von `.exe`-Installern blockiert
- ❌ Ausführung von `.bat`- und `.cmd`-Dateien blockiert
- ❌ Keine Möglichkeit, Software zu installieren

### Die Lösung

Diese Anleitung zeigt, wie man:

1. Auf einem **uneingeschränkten Rechner** (z.B. Privatrechner) eine vollständige MiKTeX-Installation erstellt
2. Diese als **ZIP-Datei** über einen Cloud-Dienst überträgt
3. Auf dem **eingeschränkten Arbeitsrechner** nur entpackt und konfiguriert

**Ergebnis:** Eine voll funktionsfähige LaTeX-Umgebung mit ~4.500 Paketen, ohne Installation.

### Größenangaben

| Komponente | Größe |
|------------|-------|
| MiKTeX Repository (Download) | ~5,5 GB |
| MiKTeX Portable (installiert) | ~10-11 GB |
| MiKTeX Portable (ZIP) | ~6-7 GB |
| TeXstudio Portable | ~150 MB |
| Sumatra PDF Portable | ~15 MB |

---

## Voraussetzungen

### Auf dem Hilfsrechner (z.B. Privatrechner)

- ✅ Windows 10/11 mit Administratorrechten
- ✅ Internetverbindung
- ✅ ~15 GB freier Speicherplatz
- ✅ 7-Zip (empfohlen) für schnelleres Packen
- ✅ Zugang zu einem Cloud-Dienst (Google Drive, Mega, Dropbox, etc.)

### Auf dem Arbeitsrechner

- ✅ Windows 10/11
- ✅ Möglichkeit, ZIP-Dateien mit Windows-Bordmitteln zu entpacken
- ✅ Schreibrechte in mindestens einem Ordner (z.B. `D:\` oder eigenes Benutzerverzeichnis)

---

## Teil 1: MiKTeX Portable erstellen

> ⚠️ **Alle Schritte in diesem Teil werden auf dem Hilfsrechner ausgeführt!**

### Schritt 1.1: Ordnerstruktur erstellen

Erstelle zwei Ordner:

```
C:\MiKTeX-Repo        (für den Download der Pakete)
C:\MiKTeX-Portable    (für die Installation)
```

### Schritt 1.2: MiKTeX Setup Utility herunterladen

1. Gehe auf https://miktex.org/download
2. Scrolle zu **"All downloads"**
3. Lade **"MiKTeX Setup Utility"** herunter (`miktexsetup_standalone.exe`)
4. Speichere die Datei in `C:\MiKTeX-Repo`

> 💡 Falls eine ZIP-Datei heruntergeladen wird, entpacke diese zuerst.

### Schritt 1.3: Eingabeaufforderung öffnen

1. Drücke `Windows + R`
2. Tippe `cmd` und drücke Enter
3. Navigiere zum Ordner:

```cmd
cd C:\MiKTeX-Repo
```

### Schritt 1.4: Alle Pakete herunterladen

Führe folgenden Befehl aus (alles in einer Zeile):

```cmd
miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://ftp.fau.de/ctan/systems/win32/miktex/tm/packages/ download
```

> 💡 **Alternative Mirror-Server** (falls der obige nicht funktioniert):
> 
> **Niederlande:**
> ```cmd
> miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://ftp.snt.utwente.nl/pub/software/tex/systems/win32/miktex/tm/packages/ download
> ```
> 
> **Automatische Mirror-Auswahl:**
> ```cmd
> miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --remote-package-repository=https://mirror.ctan.org/systems/win32/miktex/tm/packages/ download
> ```

⏱️ **Dauer:** 30-60 Minuten (je nach Internetgeschwindigkeit)

**Erwartetes Ergebnis:** ~5,5 GB im Ordner `C:\MiKTeX-Repo`

### Schritt 1.5: Portable Installation durchführen

Führe folgenden Befehl aus:

```cmd
miktexsetup_standalone.exe --verbose --local-package-repository=C:\MiKTeX-Repo --package-set=complete --portable=C:\MiKTeX-Portable install
```

⏱️ **Dauer:** 15-30 Minuten

**Erwartete Warnungen (können ignoriert werden):**
- `Windows API error 3` – nur eine Warnung, kein Abbruch
- `eptex engine not found` – betrifft nur japanische Schriften
- `not yet checked for updates` – normal bei frischer Installation

### Schritt 1.6: ZIP-Datei erstellen

**Mit 7-Zip (empfohlen, ~10-20 Minuten):**

1. Rechtsklick auf `C:\MiKTeX-Portable`
2. **7-Zip** → **"Zu Archiv hinzufügen..."**
3. Archivformat: **ZIP**
4. Klick **OK**

**Mit Windows-Bordmitteln (~1-3 Stunden):**

1. Rechtsklick auf `C:\MiKTeX-Portable`
2. **"Senden an"** → **"ZIP-komprimierter Ordner"**

### Schritt 1.7: In die Cloud hochladen

Lade die ZIP-Datei hoch zu:
- **Google Drive** (https://drive.google.com) – empfohlen, schnell und stabil
- **Mega** (https://mega.io)
- **Dropbox** (https://dropbox.com)
- **OneDrive** (https://onedrive.live.com)

Erstelle einen Freigabelink und speichere diesen.

### Schritt 1.8: Aufräumen (optional)

Nach erfolgreichem Upload können folgende Ordner gelöscht werden:
- `C:\MiKTeX-Repo` (~5,5 GB)
- `C:\MiKTeX-Portable` (~4 GB)
- Die erstellte ZIP-Datei

---

## Teil 2: Auf den Arbeitsrechner übertragen

> ⚠️ **Alle Schritte in diesem Teil werden auf dem Arbeitsrechner ausgeführt!**

### Schritt 2.1: Dateien herunterladen

Lade folgende Dateien herunter:

1. **MiKTeX Portable ZIP** (aus der Cloud)
2. **TeXstudio Portable:** https://github.com/texstudio-org/texstudio/releases → `texstudio-*-win-portable-qt6.zip`
3. **Sumatra PDF Portable (optional):** https://www.sumatrapdfreader.org/download-free-pdf-viewer → Portable Version

### Schritt 2.2: Ordnerstruktur erstellen

Erstelle einen Hauptordner für LaTeX:

```
D:\LaTeX\
├── MiKTeX-Portable\
├── TeXstudio\
└── SumatraPDF\        (optional)
```

### Schritt 2.3: Dateien entpacken

Entpacke alle ZIP-Dateien in die entsprechenden Ordner:

1. Rechtsklick auf ZIP → **"Alle extrahieren..."**
2. Zielordner auswählen

> ⚠️ **Hinweis:** Das Entpacken von MiKTeX mit Windows-Bordmitteln kann mehrere Stunden dauern. Am besten über Nacht laufen lassen.

---

## Teil 3: TeXstudio konfigurieren

### Einfache Einrichtung: MiKTeX zum PATH hinzufügen (empfohlen)

Anstatt alle Pfade manuell einzutragen, kannst du MiKTeX zur User-PATH-Variable hinzufügen:

1. In Windows: Suche nach "Umgebungsvariablen" → "Umgebungsvariablen für dieses Konto bearbeiten"
2. Wähle **Path** → **Bearbeiten**
3. Klick auf **Neu** und füge hinzu:
```
   D:\LaTeX\MiKTeX-Portable\texmfs\install\miktex\bin\x64
```
4. Klick **OK** zum Speichern
5. Starte TeXstudio – alle Befehle werden automatisch erkannt!

> 💡 Wenn das funktioniert, kannst du die Schritte 3.2 und 3.3 überspringen. Die manuelle Konfiguration unten ist nur nötig, falls PATH auf deinem System nicht funktioniert.

---

### Schritt 3.1: TeXstudio starten

1. Navigiere zu `D:\LaTeX\TeXstudio\`
2. Starte `texstudio.exe`
3. Bei der Warnung "Keine LaTeX-Distribution gefunden" → **OK** klicken

### Schritt 3.2: Befehle konfigurieren

1. Gehe zu **Optionen** → **TeXstudio konfigurieren...**
2. Klicke links auf **Befehle**
3. Trage folgende Pfade ein:

| Befehl | Eintrag |
|--------|---------|
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

> 💡 **Passe den Pfad an**, falls du MiKTeX in einem anderen Ordner entpackt hast!

### Schritt 3.3: Erzeugen-Einstellungen

1. Klicke links auf **Erzeugen**
2. Setze folgende Einstellungen:

| Einstellung | Wert |
|-------------|------|
| **Standard Compiler** | PdfLaTeX |
| **Standard Bibliographieprogramm** | BibTeX |
| **PDF Betrachter** | Eingebetteter PDF Betrachter |

### Schritt 3.4: Editor-Einstellungen (empfohlen)

1. Klicke links auf **Editor**
2. Aktiviere:
   - ✅ Zeilennummern anzeigen
   - ✅ Code-Faltung
   - ✅ Automatische Einrückung

### Schritt 3.5: Rechtschreibprüfung (empfohlen)

1. Klicke links auf **Sprache prüfen**
2. Setze:
   - **Standardsprache:** de_DE (Deutsch)
   - ✅ Rechtschreibung prüfen

### Schritt 3.6: Konfiguration speichern

Klicke **OK** um alle Einstellungen zu speichern.

---

## Teil 4: Sumatra PDF einrichten (optional)

Sumatra PDF ist ein schneller, leichtgewichtiger PDF-Viewer mit SyncTeX-Unterstützung – ideal für LaTeX.

### Schritt 4.1: Sumatra in TeXstudio einbinden

1. Gehe zu **Optionen** → **TeXstudio konfigurieren...**
2. Klicke links auf **Befehle**
3. Bei **Externer PDF Betrachter** trage ein:

```
D:\LaTeX\SumatraPDF\SumatraPDF.exe -reuse-instance -forward-search "%.tex" @ %.pdf
```

### Schritt 4.2: PDF Betrachter umstellen

1. Klicke links auf **Erzeugen**
2. Ändere **PDF Betrachter** zu: **Externer PDF Betrachter**

### Schritt 4.3: Inverse Suche in Sumatra konfigurieren (optional)

Um von Sumatra zurück zu TeXstudio zu springen:

1. Öffne Sumatra PDF
2. Gehe zu **Einstellungen** → **Optionen**
3. Bei **Befehl für inverse Suche** trage ein:

```
"D:\LaTeX\TeXstudio\texstudio.exe" "%f" -line %l
```

Jetzt kannst du:
- In TeXstudio: PDF öffnet sich an der richtigen Stelle
- In Sumatra: Doppelklick springt zur entsprechenden Stelle im Code

---

## Befehlsreferenz

### Compiler-Übersicht

| Compiler | Verwendung |
|----------|------------|
| **PdfLaTeX** | Standard für die meisten Dokumente |
| **XeLaTeX** | Für Systemschriften und Unicode |
| **LuaLaTeX** | Modernster Compiler, Lua-Scripting |
| **LaTeX** | Erzeugt DVI (selten benötigt) |

### Bibliographie-Tools

| Tool | Verwendung |
|------|------------|
| **BibTeX** | Klassisch, für `.bib`-Dateien |
| **Biber** | Modern, für `biblatex`-Paket |

### Index-Tools

| Tool | Verwendung |
|------|------------|
| **Makeindex** | Standard für Stichwortverzeichnisse |
| **Texindy** | Für mehrsprachige Indizes |
| **Makeglossaries** | Für Glossare und Abkürzungsverzeichnisse |

### Befehlsparameter erklärt

| Parameter | Bedeutung |
|-----------|-----------|
| `-synctex=1` | Aktiviert SyncTeX (Klick im PDF → springt zum Code) |
| `-interaction=nonstopmode` | Compiler läuft bei Fehlern durch, ohne anzuhalten |
| `-src` | Fügt Quelldatei-Informationen hinzu |
| `%.tex` | Platzhalter für den Dateinamen |
| `-reuse-instance` | Öffnet PDF im bereits laufenden Sumatra-Fenster |
| `-forward-search` | Aktiviert Vorwärtssuche in Sumatra |

---

## Fehlerbehebung

### Problem: "Keine LaTeX-Distribution gefunden"

**Lösung:** Die Pfade in TeXstudio sind falsch konfiguriert. Überprüfe, ob der Pfad zu `pdflatex.exe` korrekt ist.

### Problem: Server-Fehler 503 beim Download

**Lösung:** Der CTAN-Mirror ist überlastet. Verwende einen anderen Mirror (siehe Schritt 1.4).

### Problem: Entpacken mit Windows dauert sehr lange

**Lösung:** Normal bei großen ZIP-Dateien mit vielen kleinen Dateien. Entweder:
- Über Nacht laufen lassen
- Auf dem Hilfsrechner mit 7-Zip entpacken und den fertigen Ordner hochladen

### Problem: "eptex engine not found" Warnung

**Lösung:** Kann ignoriert werden – betrifft nur japanische Typographie.

### Problem: Pakete fehlen beim Kompilieren

**Lösung:** Bei der Complete-Installation sollten alle Pakete vorhanden sein. Falls doch etwas fehlt, kann es sein, dass die Installation unvollständig war.

---

## Lizenz

Diese Anleitung ist unter der [MIT-Lizenz](https://opensource.org/licenses/MIT) veröffentlicht.

**Verwendete Software:**
- [MiKTeX](https://miktex.org/) – MIT-Lizenz
- [TeXstudio](https://www.texstudio.org/) – GPL v2
- [Sumatra PDF](https://www.sumatrapdfreader.org/) – (A)GPL v3

---

## Mitwirken

Feedback, Korrekturen und Verbesserungsvorschläge sind willkommen! Erstelle einfach ein Issue oder einen Pull Request.

---

*Zuletzt aktualisiert: Januar 2026*
