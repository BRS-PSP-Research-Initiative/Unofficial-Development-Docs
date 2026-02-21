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

### Data Types Found
* Bt* - battle data
* BtPc* - player character battle data?
* Ht* - not sure what this is but it seems to be the base level entity / interface system that other major data types build upon
* map* - map data
* lst_* - various lists of data
* *_tbl / tbl_* - various tables
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

## Update Eboot.Bin
* Font type used in game: "FTT-NewRodin Pro DB" - is possibly equivalent to [FOT-NewRodin Pro](https://www.cufonfonts.com/font/fot-newrodin-pro) from Fontworks Japan

---
