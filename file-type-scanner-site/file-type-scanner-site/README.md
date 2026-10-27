# File Type Scanner (web)

A browser-based forensics tool. Upload any file (images especially) and it checks whether the file's **real type**, read from its magic bytes, matches its extension.

**Live demo:** `https://YOUR-USERNAME.github.io/YOUR-REPO/` (after you enable GitHub Pages)

## Features
- Verdicts: **OK**, **MISMATCH**, **HIGH RISK** (executable disguised as another type), **UNKNOWN**
- Detects 15+ formats (PNG, JPEG, GIF, PDF, ZIP, EXE, ELF, SQLite, and more)
- Shows first bytes in hex and the SHA-256 hash
- Checks PNG/JPEG files for data hidden after the image end marker
- Safe image preview (based on detected type, not the extension)
- 100% client-side: files never leave your browser
- Built-in demo files (an EXE disguised as `.jpg`, a PDF disguised as `.png`)

## Run locally
Open `index.html` in any modern browser. No build step, no dependencies.

## Deploy with GitHub Pages
1. Push this folder to a GitHub repository.
2. Go to **Settings > Pages**.
3. Under **Source**, choose **Deploy from a branch**, select `main` and `/ (root)`, then click **Save**.
4. After a minute your site appears at `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

## How it works
Most file formats begin with a fixed byte sequence (PNG: `89 50 4E 47`, PDF: `%PDF`, Windows executables: `MZ`). The page reads the first 32 bytes, matches them against a signature table, and compares the result with the extension. For PNG and JPEG it also looks for bytes after the end marker (`IEND` / `FFD9`).

## Limitations
- Limited signature table; unknown formats are reported as UNKNOWN
- Plain-text formats have no magic bytes and can't be verified
- Attackers can prepend valid headers, so this is a triage tool, not proof of safety
- ZIP-based formats (docx, xlsx, jar) share a signature
- Files over 100 MB are skipped

## Related
A command-line Python version of this tool is available in the `file-type-identifier` project.

## Disclaimer
Only scan files you own or have permission to analyze.

## License
MIT
