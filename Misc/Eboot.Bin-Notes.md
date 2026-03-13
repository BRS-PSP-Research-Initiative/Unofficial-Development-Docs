# Eboot.Bin Notes

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is meant to help with theorizing about how the game was built and ran along with findings related to data formats that doing a visual look at didn't help with.

---

* Note: these initial notes were made using both the decoded Japanese base Eboot.Bin and Update/Eboot.Bin files and Ghidra to examine both

## Main Eboot.Bin
* 0x08973098 - mdlres_tbl loaded; guessing this data can be found within the scripting system somewhere in other data locations
* 0x0896e00c - fld9700 - hair animation; assuming this is just for BRS since she's the only Field Model character that has animated hair (could be wrong here)
* Almost all Vol archives look like they are just referenced directly in a table
* Battle Maps are pointer loaded and possibly use similar code to what Battle Models do since both have Actors
* PRX files are called and used; bet these could provide more information about how this game was built; see separate PRX Notes docs for findings
* Engine loads DXT1, DXT3 and DXT5 Compression types (are these used for textures?)
* Sounds, Movies, Gallery, Memory Card and Weapon assets all are loaded from the binary and possibly at launch
* Mem Card Data block size: 384KB
* Game loads Network module (part of why I think there may have been an initial Multiplayer complayer component; see SC_MP notes for more info on this)
* CZAA sections with `%s` sections - ZLIB compressed data that takes the next string as a parameter and then possibly uses a table or list for the second string (if more than one `%s` exists)
* 0x00168570 - looks like much of the player's battle data from the VOL archives are loaded here with the different parts from different archives linked together based on model type, sound effects, etc
* 0x0894b044 - All Model resources share the same general offsets when it comes to their table structures (not necessarily the same parsing mechanisms) - See below Model Resources section for further info

### Data Types Found
* Bt* - battle data
* BtPc* - player character battle data?
* Ht* - not sure what this is but it seems to be the base level entity / interface system that other major data types build upon
* map* - map data
* lst_* - various lists of data
* \*_tbl / tbl_\* - various tables
* fld* . *fld - field data (the area the player runs around in between combat)
* fld_io_main - main C++ entry point to field loading processes
* int_* (with a unique one called `int_tarminate`, a misspelling of `terminate`) - state flags to possibly pass to the scripting engine
* rec* - not sure what exactly these are but I'm guessing they're states that trigger a save when activated
* *_task - what the game should do (with or without a stack setup to determine proper order)
* scr* - scripting events
* BRSS.BIN / BRSC.BIN - Memory card save file block names
* MS* / MEMSAVE - Memory card save system
* EGXD / EGTB - haven't found these file types yet in data but can safely assume they are related to Maps / Enemy encounters since they load before BtMapActor
* page: 8 digit (not sure if bit flags or full letters) memory file of some type - guessing this is 64KB or 8 x 8byte sections
* .cam files are only explicity called in the binary for `chr_p_brs02`, the Player namespaced chr files

### Battle Data Structure
* State Tables with offsets of 0x10 between sections

### Field IO Game Data Structure
* 0x300000 - Field IO Game Data
* 0x0b - Offset to Field Thread data

### Event Handling
* Heavily uses callbacks to trigger these such as loading 3d and 2d assets with the following general ordering:
    * Pre
    * Main
    * Post

### Misc Findings
* Test data call found: `../data/effect/battle/efp/ebtest.efp` - this archive isn't found in the game data but instead gets called by a test function; the call wasn't removed from final binary
* Field Events and Minigames may use the same data buffer in memory

### Model Resources with Shared Table Parser
* State
* Stage
* Mdl (INSM with PTMD data)
* SM (probably Save Data or System Memory)
* AI
* Eff (Effects)
* Voice (probably mostly for bosses and NPCs)
* Chr (probably character table data, such as name, gender, etc. for bosses and NPCs)
* emy (enemy specific tables)
* trp (Traps?)

### Data Loader Function found at 0x088b0d58 in Ghidra
* Zlib compressed ZZZ archives byte embedded and encrypted in PTMD data
* Decompiled code snippet (not exactly 100% accurate but close enough):

```
void animation_data_loader(int param_1)

{
    int iVar1;
    
    iVar1 = *(int *)(param_1 + 0x4c);
    *(uint *)(param_1 + 0x2c) = *(uint *)(param_1 + 0x2c) | 4;
    for (; iVar1 != 0; iVar1 = *(int *)(iVar1 + 0x50)) {
         animation_data_loader(iVar1);
    }
    return;
}
```
* Possibly Debunked - Code takes PTMD or INSA data and does the following to decrypt the data (still somewhat theoretical)
    * Jump to 0x2c
    * Bitwise ORs the next 8 or so individual bytes by 4 to create a string (can be longer)
    * XOR decrypt that string with the decryption key used by the VOL archives
    * Read lower case string as a file extension type (test showed zzz)
    * Recursively read the next 0x50 bytes of code from start point (until you hit a 2 byte 0 value and stop)
    * Read that 0x50 byte section as data for that file type
    * Extract data based on file type
    * Repeat process until end of file

### PTMD_parser found at 0x0001052A (need to fully test this)
* Recursively runs through the PTMD data until any of the following occurs
    * The address value is 0
    * The address value is the same as the previous address
    * The address is outside of the end of the data chunk
* When any of these are triggered, check the PTMD value at offset 0x40
    * if not 0, run the value there as a function in the engine

### 3D Pipeline Updates - Courtesy of: https://ameblo.jp/pspdevblog/entry-10012233828.html
* Shaders, UV Maps, & other static assets that always begin with a set byte value - devs used a bitshift of << 0x8 to save space; then they restored the data at runtime directly from the main executable instead
    * This includes the matrix transfer commands and other rendering related data

### Shader Masks
* There are multiple switches in the code; use these for reference: https://github.com/pspdev/pspsdk/blob/800ce356bbe5ac884d87837e7553dfd5f70e4401/src/gu/guInternal.h#L551 & https://ameblo.jp/pspdevblog/entry-10012233828.html


### Data Region Offsets
* 0x206bc - Probably Assets

## Update Eboot.Bin
* Font type used in game: "FTT-NewRodin Pro DB" - is possibly equivalent to [FOT-NewRodin Pro](https://www.cufonfonts.com/font/fot-newrodin-pro) from Fontworks Japan

---
