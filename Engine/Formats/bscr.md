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
	* Script entries for coordinates and other number based systems have extra labels that were never translated to English, some of which are direct references to the ancient Chinese myth Journey to the West (uses `shift_jisx0213` encoding)
	* Originally named Battle Module Script due to being found within BTL data but changed due to its usage within Stage Maps and a small handful of other places
* Stage Map Specific Notes:
	* Script function tier system:
		* func00 - Top level generic engine functions; shared between maps with possible variations in implementations
		* func01 - FLD functions (without FEVT); doesn't always exist
		* func02 - Interactive elements and objects functions (includes MOBS)
		* func03 - Enemy Encounter related functions (may be tied to enmgrp.dat in `SYSTEM.VOL`)
		* func04 - FEVT (Event), Mission and EVC related functions
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
  * 0x30 - 4-byte Arbitrary Count (that gets manipulated based on Script Opcode read)
	* 0x34 - Address of scripting payload (large blob of space-delimited string data)
	* 0x38 - Size of chunk at 0x3c
	* 0x3c - Offset to Implementation Chunk, padding or other file formats (these last 2 are probably related to left behind scripting code that doesn't do anything)
  * 0x68 - 4-byte BCHR Script Flag
  * `BTL/MAP` and sometimes in the pack file for other Systems (if not at Index 0 nor at beginning of Implementation section) only:
    * 0x318 - If not 0, start of Map Script Implementation and previous 4-byte chunk is 0
  * `BCHR_APL*.VOL` and `BCHR_CAT*.VOL`:
    * <0x04> + 0x648 - `LAND_PROCESS` debug string that gets flushed
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

# StellaScript bscr Interpretation Notes 

* Language Parsing Notes:
  * Binary Data and String Data are treated as two different streams in loading mechanism
  * Uses variable flags to drive interpreter
  * Code Structure (by 1-byte position):
    * 0x00 - Op Code (what action is being performed)
    * 0x01 - Jump Code (move cursor forward or backwards)
    * 0x02 - Jump Code / Parameter (can be either depending on opcode)
* Op Code with Function Name:
  * 0x02 - get_total
  * 0x03 - get_difference
  * 0x04 - get_product
  * 0x05 - get_fraction
  * 0x06 - get_modulo
  * 0x08 - get_bitwise_mask
  * 0x09 - get_bitwise_or
  * 0x0a - get_bitwise_xor
  * 0x0b - get_bitwise_left_shift_0x1f
  * 0x0c - get_bitwise_right_shift_0x1f
  * 0x0e - get_is_zero
  * 0x11 - shift_cursor_forward_by_idx
  * 0x12 - shift_cursor_backward_by_idx
  * 0x13 - run_assembly_call_by_action
  * 0x14 - throw_PCPU_MOVM_error
  * 0x15 - throw_PCPU_LEAS_error
  * 0x17 - throw_PCPU_PUSH_error
  * 0x18 - set_interpreter_out_offset_0x04
  * 0x19 - throw_PCPU_PUSHF_error
  * 0x1a - populate_interpreter_out_tbl_entries
  * 0x1b - test_interpreter_out_functions
  * 0x1c - set_dynamic_byte_by_offset_0x03
  * 0x1d - set_offset_0x03_by_dynamic_byte
  * 0x70 - get_less_than
  * 0x71 - get_less_than_or_equal
  * 0x72 - get_greater_than
  * 0x73 - get_greater_than_or_equal
  * 0x74 - get_equal_to
  * 0x75 - get_not_equal_to
  * 0x80 - get_boolean
  * 0x81 - recursively_reinterpret_script
  * 0x82 - run_BTL_function
  * 0x83 - flush_dynamic_bytes_with_count
  * 0x84 - shift_script_read_start
  * 0x85 - throw_PCPU_LABEL_error
  * 0x86 - run_BTL_function_offset_0x100
  * 0x87 - run_BTL_function
  * 0x88 - run_BTL_function_offset_0x100
---
