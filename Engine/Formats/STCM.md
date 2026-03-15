# STCM Map File Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Tentative Name: Something That Can Map
* Extension: .bin, .sm
* Header: STCM
* Purpose: Stores stage and map data
* Notes:
	* Originally found in decrypted and extracted Map VOLs under `GAMEDATA\BTL\MAP`
* Header Structure:
    * 0x10 - Address to tail of table at 0x1c
	* 0x1c - Variable length table starts here with a 0x04 offset between entries
        * Each entry = mix of PTMD structures & other data types
        * Length of Table = based on amount of embedded data sections

---
