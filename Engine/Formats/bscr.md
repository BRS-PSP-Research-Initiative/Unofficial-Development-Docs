# bscr Scripting Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Binary Module Script
* Type: Scripting
* Extension: .bms
* Header: bscr
* System Equivalent:
    * Field System: Stage Map bscr
* Purpose: General purpose main binary-encoded StellaScript implementation
* Notes:
	* Script Data values can be found in the padding data section; see Script structure section below
	* Each script file has a somewhat different structure based on purpose
	* May or may not use the same binary encoded structure as SSCR (Stage Script StellaScript flavor); has a hardcoded function in game binary that isn't shared with FLD implementations
	* Script entries for coordinates and other number based systems have extra labels that were never translated to English, some of which are direct references to the ancient Chinese myth Journey to the West (uses `shift-jisx021` encoding)
	* Originally named Battle Module Script due to being found within BTL data but changed due to its usage within Stage Maps and a small handful of other places
* Stage Map Specific Notes:
	* Script function tier system:
		* func00 - Top level generic engine functions; shared between maps with possible variations in implementations
		* func01 - FLD functions (without FEVT); doesn't always exist
		* func02 - Interactive elements and objects functions (includes MOBS)
		* func03 - Enemy Encounter related functions (may be tied to enmgrp.dat in `SYSTEM.VOL`)
		* func04 - FEVT (Event), Mission and EVC related functions
* Binary Implementation:
    * Load bms script file (multistage process) (Still speculative for some of this):
		* Allocate memory for entire data blob
		* Split data blob and string blob of entire file into two separate pieces
		* Pass both to script_loader method
		* Dirty (use mask - & - math) to modify first 4-byte chunk (leader) of data blob
		* Store string blob pointer address in second 4-byte chunk of data blob; this may not exist yet in memory until the next step
		* Use Sony's default libheap allocator to allocate memory for the string blob
		* NOTE: 0x5A is used for alignment padding and separating data chunks
* Data Sections:
	* Header
	* String Data
	* Implementation Data
	* Extra (possibly exists in special cases)
* Header structure:
	* 0x04 - 1-byte Script Type Flag:
		* 0x24 - Battle Script
		* 0x22 - Map Script / system.pack Script
	* 0x06 - 32-byte script file string name; first byte begins with any Ascii character followed by a blank space and then the full name of the bms file in the archive to write the script to
	* 0x24 - size of file
	* 0x2c - Address of function string start (All of 0x34 is here but separated by 0x2c bytes from the next one)
	* 0x34 - Address of scripting payload (large blob of space-delimited string data)
	* 0x38 - Size of chunk at 0x3c
	* 0x3c - Offset to Implementation Chunk, padding or other file formats (these last 2 are probably related to left behind scripting code that doesn't do anything)
	* 0x318 - If not 0, start of Map Script Implementation and previous 4-byte chunk is 0; can be System.pack version only if this is not at beginning of Implementation section
* Script Data structure (starting from offsets at 0x2c to 0x34)
	* 0x00 - 2-byte Offset to next script string chunk (up to where 0x34 points to)
	* 0x02 - Unknown 2-byte value; usually 0xe0 or 0xe1 (but needs more testing)
	* 0x04 - 28-byte scripting function string (uses a stripping method to remove trailing 0s)
	* 0x20 - 4-byte Offset in Implementation Chunk
	* 0x24 - Unknown 4-byte value
	* 0x28 - Default initial value of function at 0x04
	* 0x2c - Same as 0x24 unless value is 0x81
* Map Implementation Data structure
	* 0x00 - 2-byte Magic Header (0x1?F0 - lower bit of first byte seems to be a flag of some type) with 0x5A5A as alignment padding
	* 0x04 - 4-byte Embedded Tables Max Size (Tables can have less than this amount and skip indices but never be larger than this)
	* 0x20 - Start of PROPERTY_INIT Table Data
		* Table Entry structure (should apply to all other Tables in this section):
			* 0x00 - Same 2-byte Magic Header as section start (used for each entry)
			* 0x04 - 4-byte Table Entry Index
---
