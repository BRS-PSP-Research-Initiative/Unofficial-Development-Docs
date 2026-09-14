# SSCR Scripting Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Stage Script
* Type: Scripting
* Extension: .ss
* Header: SSCR
* Purpose: Contains Generic Stage Script data
* System Equivalent:
    Battle System: No direct equivalent
* Notes:
	* This was first discovered on a random hunch while out for food. A quick script to check for vertex values found BRS's model pretty quickly under the `BTL\FLD\FCHR` directory
	* Always found within SC containers
	* Uses context for implementation and type of data expected:
		* All types contain a `head_fdat` script container - tells engine that this is the top-most script
		* Map Data contains exactly 3 SSCR scripts, consisting of 2 extra scripts:
			* `res_header`/`res_buffer` - next SC section will contain at least 1 STCM Map Data File
			* `init_scene` - bottom most script that can contain multiple `RCs` and have other data within
* Structure:
	* 0x0c - Scripted Data Section Start
	* 0x10 - Scripted Data String End Address
	* 0x14 - Scripted Data Section End Address
	* 0x18 - Relative Offset to End of Data Chunk
    * 0x20-0x50 - Possible Padding before Script Names Table
---
