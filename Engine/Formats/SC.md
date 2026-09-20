# SC Container Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Stage Container
* Type: Management / Container
* Extension: .sc
* Header: SC
* Purpose: Field Module Micro and Macro Control Center
* System Equivalent:
  * Battle System: BXCB (top level SC only)
* Notes:
  * Game Binary rarely cares what the exact value is for 0x02 (labeled Hierarchy); it's mostly context sensitive based on data types inside with my observation of it using bitflags being purely cosmetic
  * Probably used to visually track and debug sections but not directly important to how the game parses and processes the SC format
* Header Structure:
	* 0x00 - Has a dual purpose in this case: (2-byte) Magic Number; (4-byte) Float calculations base seed (needs further testing)
  * 0x02 - (1-byte) Hierarchy Attribute (by Bit Flag; rest are internals)
    * 0x80 (Bit7) - Not found in data on disc but most likely Debug / Test data
    * 0x44 - (spec) Field Event Debug (if offset 0x106 == 0xA)
    * 0x40 (Bit6) - Field Event (Internal to 0x10)
    * 0x3D - Field Object/Enemy (Probably destructable or interactive)
    * 0x34 - Field Player Character
    * 0x20 (Bit5) - Field Map EFC
    * 0x1D - Field SUM00P
    * 0x16 - Field Enemy
    * 0x14 - Field Skill (?)
    * 0x10 (Bit4) - Field Event/Map Top Level (Probably related to Cutscenes) - Can contain multiple 0x40 SC's / SSCR's
    * 0x0A - Field SUM00
    * 0x0B - Field SUM (Rest of SUM's use this + RID Gimmicks)
    * 0x0C - Field Test
    * 0x09 - Same as 0x03 (Multiple TEST FEVTs)
    * 0x08 (Bit 3) - Field Character/Map Top Level (Can contain an internal STCM if a Map)
    * 0x06 - Top-level Field Resident (`fld_resident.bin` in `SYSTEM.VOL`)
    * 0x05 - Unknown `fld_resident.bin`; possibly a duplicate of 0x01
    * 0x04 (Bit2) - Unknown
    * 0x03 - Test Field Event with embedded Battle System data (FEVT_TEST_AOIK00)
    * 0x02 (Bit1) - Field Event PHD (if not in `fld_resident.bin`); Possibly dead / removed EFC Cutscene data (`fld_resident.bin`)
    * 0x01 (Bit0) - Field Character / EFC Cutscene (in `fld_resident.bin`)
    * 0x00 - Field Event Unused SC data + types (FEVT_TEST_KAMI00) - There were multiple different data types unique to this section found here
  * 0x04 - Internal Container list with variable sizes depending on Hierarchy and data within
    * Each entry is an offset from the start of the container
    * 1st Entry can be 0x3c, 0x00, or any value between 0x10 and 0x20 - all of these must be greater than or equal to 0x10 and be evenly divisible by 0x10 (Binary uses `& 0xfffffff0`)
    * List ends with either a 4-byte Null terminator (such as 0x0), a known Magic Number, or a value that is less than the previous entry
    * Duplication of entries are there to pad the table but do not seem to act as extra internal offsets as originally assumed
* Notable Data Structures:
	* 0x180:
      * First major memory blob splits off from here
      * Only applicable to the Character (FCHR) portions of Field Assets and not the Events (FEVT)

---
