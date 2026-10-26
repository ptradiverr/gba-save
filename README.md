# gba-save

A reverse-engineering project focused on understanding and making small
modifications to `GBA_Backup_Tool.nds`, the Nintendo DS GBA backup utility.

## Project status

The project is in its initial investigation stage. The repository currently
contains the tool's configuration file and an EEPROM save conversion utility.
Recovered source code, disassembly, patches, and a reproducible build process
are not yet available.

The `.nds` executable, game ROMs, save data, and generated build output are
excluded from version control and are not distributed with this repository.

## Contents

| File | Description |
| --- | --- |
| [GBA_Backup_Tool.ini](GBA_Backup_Tool.ini) | Backup directory, save size, ROM size, and trimming settings. |
| [EEPROM_cnv.vbs](EEPROM_cnv.vbs) | Windows Script Host utility for converting EEPROM save byte order. |

## Configuration

`GBA_Backup_Tool.ini` includes these settings:

| Setting | Default | Purpose |
| --- | --- | --- |
| `FileDir` | `/GBA_Backup` | Directory used for backups. |
| `SaveFile` | `0` | Save file size in KB; `0` selects automatic sizing. |
| `RomSize` | `0` | ROM backup size in MB; `0` selects automatic sizing. |
| `Trim` | Disabled | Optional ROM trimming, enabled by uncommenting `#Trim`. |

## EEPROM save converter

`EEPROM_cnv.vbs` reverses the byte order within each 8-byte block of a save
file. It accepts `.sav` and `.sv1` through `.sv5` files and requires Windows
Script Host with `ADODB.Stream` support.

```text
cscript //nologo EEPROM_cnv.vbs "path\to\save.sav"
```

When run without an argument, the script prompts for a file path.
**Conversion overwrites the input file**, so retain a backup of the original.
The converter is a separate utility and does not modify the `.nds` executable.
