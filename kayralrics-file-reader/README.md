# kayralrics.com - file reader

A browser-only, offline, private file-inspection application. No backend, build step, CDN, login, telemetry, service worker or external runtime API.

## Start

1. Extract the ZIP file.
2. Double-click `index.html` in a modern desktop or mobile browser.
3. Select **Open files**, **Open folder** (where supported), or drag files onto the application.

For the simplest deployment, use the separately provided `file-reader-offline.html`: it embeds the entire application (including its local compression libraries) in one HTML file.

All selected files are read through your browser's File and Blob APIs and are **not uploaded**. Browser codecs/PDF rendering may differ between browsers. Nothing is retained after you close the tab.

## Release 2.0 — final standalone build

The upper-left decorative `k.` logo has been removed completely; only the product name and site text remain. New quality-of-life features include:

- File sorting by added order, name, size and modified time.
- Navigate previous/next file with buttons or `Alt+↑` and `Alt+↓`.
- Remove a single file from the current session without changing the original file.
- Search filenames (`Ctrl+K`) and open new files (`Ctrl+O` / `Cmd+O`).
- Find matching text inside the decoded text view, with offsets and context excerpts.
- Open/inspect binary data with sample byte-distribution visualization, entropy and readable-string discovery.
- Copy the current hex page and navigate directly to the final page.
- Export a local JSON analysis report, including available SHA-256 fingerprint.
- Compute and copy the selected file's SHA-256 fingerprint on demand (up to 256 MB and where browser Web Crypto is available).
- Preserve archive member paths when opening individual entries.
- Responsive layouts with reduced-motion support.

## Views

- **Preview**: semantic reading/rendering where a decoder is available.
- **Structure**: parsed metadata, archives, binary fields, scene graph, type information and database structures.
- **Text**: inspect text and textual sequences, including unknown files.
- **Hex**: page through **any** readable file using small byte-range reads, even extremely large files.
- **Details**: signature, size, type, first bytes, timestamps and detection method.

## Supported decoding and inspection

| Format family | Capabilities |
| --- | --- |
| Text and code | TXT, MD, CSV, TSV, JSON, JSONL, XML, HTML, CSS, JS, TS, Python, SQL, YAML, TOML, scripts, configuration and many text-like formats; JSON tree, CSV spreadsheet-like grid, safe extracted HTML/XML text, Markdown reading view |
| Standard images | PNG, JPEG, GIF, WebP, BMP, ICO, SVG, AVIF and browser-native formats; decoded by browser if supported; header metadata for several formats |
| PDF | Inline native browser PDF reader where available |
| Audio and video | HTML audio/video playback when a compatible browser codec is installed (MP3, WAV, FLAC, MP4, WebM, etc.) |
| ZIP and ZIP-derived formats | ZIP, DOCX, XLSX, PPTX, ODT, ODS, ODP, EPUB, CBZ, APK, JAR, IPA, VSIX, KMZ, AAB, XPI and similar; directory listing and per-entry extraction, preview/open archive members |
| Office and EPUB | Extracted DOCX document text; XLSX worksheet grids; PPTX slide text; ODF text; EPUB chapters; no guaranteed pixel-perfect layout |
| Legacy Office/OLE | OLE/CFB directory and stream metadata for DOC, XLS, PPT and similar compound files |
| Archives | ZIP, TAR and GZIP/TAR.GZ extraction; GZIP Blender-project detection |
| Blender | `.blend` header, version, pointer size, endianness, BHead blocks, embedded Structure DNA (SDNA), inferred block identifiers; **not full Blender scene rendering** |
| 3D models | OBJ, STL, ASCII PLY, OFF and embedded GLB geometry: interactive sampled wireframe rotation and zoom, mesh statistics; glTF JSON metadata |
| Databases | Read-only SQLite3 header, schema, standard rowid-table record inspection; no SQLite virtual machine/SQL execution |
| Fonts | TTF, OTF, WOFF, WOFF2 browser-native font preview |
| Binary formats | ELF, Windows PE, WAV, MIDI, WebAssembly, PSD and other binary headers/strings/hex where recognized |
| Unknown file formats | Universal hex viewer, text decoding fallback, signatures, offsets, printable ASCII, sampled byte frequency and entropy inspection |

## Important limitations

**No single browser program can completely decode, interpret, display or render every existing and future file format.** Many are encrypted, proprietary, undocumented, hardware-dependent, or require large specialist runtime engines. Here, *opening* any readable file means that at minimum its raw bytes are accessible through the Hex view; *full semantic decoding* applies only to implemented decoders above.

Unsupported codecs and file versions may not display, even when a format is recognized. Some parsers intentionally cap in-memory expansions and file sizes to reduce tab crashes and archive-bomb risk. The Hex viewer works in 512-byte pages without loading the entire file. Embedded scripts in documents are **not executed**. The application is a file inspector, not a secure malware sandbox: avoid actively opening or installing suspicious extracted files in other apps.

## Local runtime libraries

- JSZip — bundled and licensed under the MIT license (see `LICENSES/JSZip-LICENSE.md`).
- Pako — bundled and licensed under its original terms (see `LICENSES/Pako-LICENSE.txt`).

No runtime network connections, external fonts or third-party CDNs are required.
