
# psmd-re
**My findings while reverse-engineering Pokémon Super Mystery Dungeon for the 3DS. Includes writeups for discovered game mechanics and an importable Ghidra project XML that includes variable and function names etc.**

## Current major discoveries
- Speed stat mechanics
- Damage formula

## How to import the Ghidra project XML
1. Obtain the game ROM by for example dumping the cartridge using [GodMode9](https://github.com/d0k3/GodMode9).
2. Extract the ExeFS of the rom using a tool such as [.Net 3DS toolkit](https://projectpokemon.org/home/forums/topic/39082-net-3ds-toolkit-extract-and-repack-3ds-roms-and-cias/) .
3. Convert the 3DS executable into an ELF using [ctr-elf](https://github.com/archshift/ctr-elf). MD-5 checksum should be `818A4462B4D1977D2135AEC37956A375`.
4. Create a new Ghidra project, import the ELF-file, but do not analyze the file.
5. Go to File -> Add to program and choose the XML-file from this repository.

## Other tools used

- [CTRPluginFramework3DS](https://www.gamebrew.org/wiki/CTRPluginFramework_3DS) to perform narrowing RAM searches for values. These memory addresses can then be used as watchpoints for finding relevant functions in the code.
- The GDB stub in the [Luma 3DS custom firmware](https://github.com/LumaTeam/Luma3DS) to perform active analysis, i.e debug the game on console.
