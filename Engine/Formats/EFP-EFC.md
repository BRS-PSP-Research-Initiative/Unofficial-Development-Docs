# EFP/EFC Container Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Event Format Pack / Container
* Type: Container
* Extension: .efp / .efc
* Header: EFP
* Purpose: Contains mostly Event System data for multiple major Systems
* Structure:
	* 0x04 - 4-byte Unknown Identifier
	* 0x0c - 1-byte embedded esb count
	* 0x0d - 1-byte embedded mdl count
	* 0x0e - 1-byte embedded anm count
	* 0x0f - 1-byte Index Value in case of multiple EFCs being tied together (Example: `ef5600001.efc` and `eb506001.efc`)
	* 0x10 - 4-byte Offset from 0x30 to first INSA structure
	* 0x18 - 24-byte first internal INSM mdl or PTMD ptm name string
	* 0x30 - Address of first internal INSM mdl structure

---
