# EFP/EFC Container Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Embedded Film framework
* Type: Multimedia
* Extension: .efp / .efc
* Header:
	* EFC - Contains a Animation object
	* EFP - Contains a Model object
* Purpose: Contains the Animation, Camera, Actor and Audio Pointer Table portions of all in-engine Cutscenes
* Notes:
	* Full purpose discovered on 09/16/2026 in Game Binary
	* Originally thought to be just VFX stuff (labeled as Effects File format)
* Structure:
	* 0x04 - 4-byte ID (0x64 or 0x65 in Binary)
	* 0x0c - 1-byte embedded esb count
	* 0x0d - 1-byte embedded mdl count
	* 0x0e - 1-byte embedded anm count
	* 0x0f - 1-byte Index Value in case of multiple EFCs being tied together (Example: `ef5600001.efc` and `eb506001.efc`)
	* 0x10 - 4-byte Offset from 0x30 to first INSA structure
  * 0x14 - 4-byte Action Flag (used for determining how to parse embedded structures)
	* 0x18 - 24-byte first internal INSM mdl or PTMD ptm name string
	* 0x30 - Address of first internal INSM mdl structure

---
