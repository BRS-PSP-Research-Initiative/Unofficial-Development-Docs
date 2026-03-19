# SC Model Container Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Self Containment
* Type: Management / Data archive
* Extension: .sc
* Header: SC
* Purpose: Field Module Micro and Macro Control Center
* System Equivalent:
    * Battle System: BXCB (top level SC only)
* Header Structure:
	* 0x00 - (2-byte) Magic Number
    * 0x02 - (1-byte) Hierarchy Attribute
		* Hierarchy (by Bit Flag; rest are internals)
			* 0x80 (Bit8) - Unknown
			* 0x40 (Bit7) - Field Event (Internal to 0x10)
			* 0x3D - Field Object/Enemy (Probably destructable or interactive)
			* 0x34 - Field Player Character
			* 0x20 (Bit6) - Field Map EFC
			* 0x1D - Field SUM00P
			* 0x16 - Field Enemy
			* 0x14 - Field Skill (?)
			* 0x10 (Bit4) - Field Event/Map Top Level (Probably related to Cutscenes) - Can contain multiple 0x40 SC's / SSCR's
			* 0x0A - Field SUM00
			* 0x0B - Field SUM (Rest of SUM's use this + RID Gimmicks)
			* 0x0C - Field Test
			* 0x09 - Same as 0x03 (Multiple TEST FEVTs)
			* 0x08 (Bit 3) - Field Character/Map Top Level (Can contain an internal STCM if a Map)
			* 0x04 (Bit2) - Unknown
			* 0x03 - Test Field Event with embedded Battle System data (FEVT_TEST_AOIK00)
			* 0x02 (Bit1) - Field Event PHD
			* 0x01 (Bit0) - Field Character
			* 0x00 - Field Event Unused SC data + types (FEVT_TEST_KAMI00) - There were multiple different data types unique to this section found here
	* 0x04 - Internal Container list start - Can be 0x3c; that's a bug that always needs to be read as 0x30
	* 0x08 - First internal object ends here but not guaranteed to help with any extra extraction
	* 0x10 - 0x28 - Relative chunk size for each internal SC structure; the binary modifies the value of each one at runtime
* Notable Data Structures:
	* 0x180:
        * First major memory blob splits off from here
        * Only applicable to the Character (FCHR) portions of Field Assets and not the Events (FEVT)

---
