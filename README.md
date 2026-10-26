# GBA Backup Tool NDS

This repository is a workspace for investigating and modifying the Nintendo DS
ROM image `GBA_Backup_Tool.nds`. The current contents are a prebuilt ROM, its
configuration file, and a Windows Script Host utility for converting save
files. No source code, disassembly, or reproducible build process is included
yet.

## Repository contents

- `GBA_Backup_Tool.nds` — the ROM image under investigation. ROM images are
  ignored by Git; keep your local working copy in the repository root.
- `GBA_Backup_Tool.ini` — configuration for the backup tool. `FileDir` sets
  the backup directory; `SaveFile` and `RomSize` support automatic sizing with
  `0`; uncomment `#Trim` to enable trimming.
- `EEPROM_cnv.vbs` — Windows Script Host script that reverses the byte order
  of each 8-byte block in a `.sav` or `.sv1`–`.sv5` file, modifying that file
  in place.
- `src/` — place recovered or recreated source here.
- `patches/` — document and store modifications here.
- `build/` — generated build output; ignored by Git.
- `config/`, `docs/`, `scripts/` — configuration, research notes, and helper
  scripts for the project.

## Working safely

1. Keep an untouched, legally obtained copy of the ROM outside the working
   tree. Do not distribute ROM images or save files unless you have the rights
   to do so.
2. Before analysis or modification, record a checksum and work on a duplicate:

   ```sh
   shasum -a 256 GBA_Backup_Tool.nds
   mkdir -p build
   cp GBA_Backup_Tool.nds build/GBA_Backup_Tool-working.nds
   ```

3. Record the tools, versions, file offsets, and steps used to inspect or
   modify the image so the work can be repeated.
4. Keep original and modified checksums, and test changes in an appropriate
   emulator or on hardware only when you are authorized to do so.

The repository does not currently define extraction, disassembly, patching, or
rebuild commands. Add documented commands here as those steps become known.

## Save converter

`EEPROM_cnv.vbs` requires Windows Script Host. It accepts a save-file path as
its first argument, or prompts for one when started without arguments. It
rewrites the selected file in place, so make a backup before running it:

```text
cscript //nologo EEPROM_cnv.vbs "path\to\save.sav"
```

## Version control

The `.gitignore` excludes ROM and save images, macOS metadata, and generated
build output. Keep research notes, scripts, patches, and source changes
tracked; do not add copyrighted binary assets unless you have permission.
