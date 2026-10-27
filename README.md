<div align="center">

# file converter

Current release: **v1.0.16**. Includes pinned FFmpeg binary verification and its matching source and license notices.

**Small installer:** Download the small installer ZIP, extract the entire folder, run `Installer.bat`, accept the Terms and bundled Tool License, wait for final checks, then open the folder-local shortcut. Setup keeps its runtime private without changing system Python or PATH or requiring administrator access. Rerun it to repair or refresh a moved shortcut. Keep the full path at most 72 characters, without percent signs. The small installer retains this tool's documented architecture support; File Converter remains x64-only.

**Ready-to-run (Windows x64):** A larger ZIP includes the private runtime already bundled. Extract the entire folder, open `File Converter.exe`, and accept the Terms and bundled Tool License on first use. There is no `Installer.bat` step and no system Python or PATH change. Keep the EXE with the rest of the folder. This option is x64, not native ARM64; the setup instructions below describe the small installer option.

A little tool I made with AI to quickly convert common image, audio, video, archive, and script files locally on 64-bit Windows.

<img src="File%20Converter.png" alt="File Converter app window" width="760">

</div>

## features

- Convert common image, audio, video, archive, and script formats
- Preserve image animation when the output format supports it
- Copy compatible media streams without re-encoding
- Extract audio from video files
- Convert archives or create new archives from files and folders
- Swap BAT/CMD and PY/PYW extensions without changing file contents
- Choose the output folder and follow progress in the built-in log
- Process every file locally without uploads or telemetry

## requirements

- 64-bit x64 Windows
- An internet connection during first setup
- Enough free space for private Python, packages, and FFmpeg
- No internet connection while using the installed app

## installation

1. Download the latest release ZIP.
2. Extract the complete folder.
3. Double-click `Installer.bat`.
4. Press **Y** once to accept the Terms and bundled Tool License and approve setup.
5. Leave the setup window open until every check passes.
6. Double-click the `File Converter` shortcut created in the folder.

Keep the full extracted folder path at 72 characters or fewer so Windows can install the private packages reliably.

Setup keeps the private Python runtime, dependencies, settings, and every app component inside the extracted folder. It does not require administrator access, change PATH, or install global Python packages. The generated folder-local shortcut starts the app directly with that private runtime, so Microsoft Store or system Python is not required.

Setup pins and verifies official Python 3.14.7, pip, the complete private PySide6-Essentials, Pillow, pillow-heif, and py7zr dependency set, FFmpeg, and FFprobe. Downloaded runtime archives are checked against pinned SHA-256 hashes before use.

Setup and repair also require the bundled, hash-verified dependency lock file. Every downloaded Python wheel must match its approved SHA-256 hash, including transitive dependencies. Keep the entire extracted folder together; no account or global Python installation is needed.

Before downloading private components, setup checks the bundled app source and Windows shortcut support. Once private Python is ready, it compiles the app before installing the larger packages. WinGet is not required.

Run `Installer.bat` again to repair the private components or after moving the complete folder. Setup preserves your files and recreates the shortcut for the folder's current location.

## usage

1. Choose a category.
2. Choose a file or drag it into the app.
3. Select the output format.
4. Choose the output folder.
5. Click **Convert**.

The original input is never overwritten. Animation is preserved when the output supports it, and compatible media streams are copied without re-encoding when possible.

## source code

Both download options use the same [Python app source](File%20Converter.pyw). [ReadyLauncher.cs](ReadyLauncher.cs) is the complete C# source of the ready-to-run EXE launcher; it starts that app with the bundled private Python runtime. The EXE does not replace the Python application with native machine code.

The release's [File-Converter-v1.0.16-Source.zip](https://github.com/fleecewtf/File-Converter/releases/download/v1.0.16/File-Converter-v1.0.16-Source.zip) includes both sources, setup/dependency definitions, licenses, and assets, without installed runtimes, user data, or developer tests. The same source is mirrored on GitLab. Fleece's source-available Tool License applies; this is not an open-source license.

To compile the x64 launcher with Windows .NET Framework:

```bat
"%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\csc.exe" /nologo /target:winexe /platform:x64 /optimize+ /out:"File Converter.exe" ReadyLauncher.cs
```

This builds the launcher only, not Python or its dependencies. Keep the matching app files and private runtime together as described above; `Installer.bat` records the pinned component versions. Adding a Windows icon when compiling is optional. No test or packaging-helper folder is required in the public source tree.

## built with

- [PySide6](https://doc.qt.io/qtforpython-6/)
- [Pillow](https://python-pillow.github.io/)
- [pillow-heif](https://github.com/bigcat88/pillow_heif)
- [py7zr](https://py7zr.readthedocs.io/)
- [FFmpeg](https://ffmpeg.org/)
- [Python](https://www.python.org/)

The FFmpeg/FFprobe runtime uses the pinned BtbN GPLv3 build identified in [FFMPEG-SOURCES.txt](FFMPEG-SOURCES.txt). Its exact corresponding source, dependency sources, and build recipes are available from the linked public source release. These third-party components retain their licenses and are not restricted by Fleece's app license.

## privacy and removal

The app has no telemetry, analytics, advertisements, accounts, uploads, or runtime network requests. Files are processed locally. Temporary archive staging stays in `.runtime\work` inside the extracted folder and is removed after each job; a later startup safely retries cleanup after an interrupted job. Setup logs can contain local folder paths, so review them before sharing.

To remove File Converter, close it and delete the extracted folder. This removes its folder-local shortcut, private runtime, dependencies, settings, and app files. The app does not install a background service, add itself to startup, or create an uninstaller entry.

## troubleshooting

If setup stops, the window immediately identifies the failed check and shows a short **How to fix** instruction. The same guidance is saved in `setup.log`. Correct the listed problem and run `Installer.bat` again. Setup reports success only after its dependencies, offline self-tests, and shortcut all pass.

If the `File Converter` shortcut does not open, run `Installer.bat` again and keep the complete extracted folder together. Setup recreates and validates the shortcut for the folder's current location.

BAT/CMD and PY/PYW conversions only change the extension. They do not translate or rewrite script contents.

Click **Cancel** to stop a job. Media probing and conversion stop their private child processes; image codecs and some archive operations may need to finish their current codec call before cancellation completes. Wait for the app to return to its idle state before closing it. Failed or cancelled jobs leave existing output files unchanged.

Installed components work offline. Repairing missing or damaged components with `Installer.bat` can require an internet connection; an offline conversion error is not a reason to upload the input file anywhere.

## license

Copyright 2026 Fleece. This project is source-available, not open source. The bundled [LICENSE](LICENSE) permits downloading, installing, and running an unmodified official release for lawful personal, non-commercial use. Modification, redistribution, sale, rebranding, and derivative versions remain prohibited. Third-party materials retain their own licenses.

## note

This project was made with AI.

Keep a backup of important files and verify converted output before deleting an original.
