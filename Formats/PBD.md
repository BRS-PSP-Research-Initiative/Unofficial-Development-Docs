# PBD Data Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* This Format is not a singular format; it's used for a variety of different things based on context in the data
* Context can be quickly assessed based on data within the same structure that PBD is found in
* Common examples:
	* PHD file of same name as PBD - most likely Packed Bottom-up Data
	* XTC and/or SDOa file - most likely Packed Bitmap or Blob Data
	* Found within EFP / EFC container - could be any one of these or all at one time if multiple PBDs found
---

* Name: Packed Bitmap Data
* Type: Asset Data
* Extension: .pbd
* Purpose: A complete texture blob consisting of three different sections
	* Notes:
		* First file found on 03/09/26 within the SYSTEM.VOL/font.lpk data as the final PBD file read in data structure
		* All regions have this file; the data has not been fully dissected for anomalies between regions
		* Other PBD structures have been found with SMS and other data only partially packed correctly leading me to assume that it's very possible that this file exists as a byproduct of an unexpected error in the tooling used for packing data
		* Could still be a real format for this type due to where it was found and how the data within is used
	* Tile Map:
		* Magic Header:
			* SBS - Sprite Bitmap Stream
		* Header Structure:
			* 0x04 - 2-byte Stream ID
			* 0x06 - 1-byte Unknown Value
			* 0x07 - 1-byte Unknown Value
		* Data Structure:
			* 0x12 - 2-byte Tail Address of Tile Map Stream; should be followed by 0x0F0F and then padding before the next section starts
		* Notes:
			* Tile Map Stream consists of a series of 2-byte Relative Offsets in the Pixel Data blob below delimeted by 0x0f0f
			* Offsets are read in the binary at runtime using the following base algorithm: stream[idx] = stream[idx] | 0x04
	* Bitmap Data:
		* Magic Header:
			* PTM - Packable Texture Metadata
		* Purpose:
			* Inform the stream that the next section contains a PTMD blob that must be packed
		* Data Structure:
			* 0x04 - 2-byte Stream ID (must match the ID of SMS)
			* 0x06 - 2-byte Relative Offset between large data blobs; needs to be tested but a naked eye test showed that the distance between the two major pixel data blobs were roughly equivalent
			* 0x10 - PTMD
				* This is the unpacked version of my noted PTMD format, so I'll be treating it as a separate format altogether until real tests can be ran
				* Header Structure:
					* 0x04 - 6-byte Unknown Value; Possibly a hash of some type
					* 0x0C - 4-byte Address to end of Pixel Data
				* Pixel Data:
					* Variable length blob of raw pixel data that can be viewed with the naked eye in a hex editor as 16x8 byte representations of the original texture
						* Example (Bottom half of a pressed Square Button for the UI)
							``` ASCII
							^d%%% %%%%% %%&d
							][%%% %%%%% %%(U
							]Y,%% %%%%% %%0Y
							] ?%%       %%D%
							]^U-%%%%%%%%%0M]
							]]eS-%%%%%%%0\e]
							]]]eX?-%%&-DXe]]
							]]]]] Y[d[Y ]]]]
							```
						* Data parsing needs to be fully explored with multiple test samples and further analysis of the game binary to fully understand how this is parsed
				* Unknown Variable Length Table consisting of probably index aligned 4-byte values with this structure: value + 3 0x00s
				* Palette Data:
					* ARGB or ABGR probably Color LookUp Table (CLUT)
					* Most likely mapped to the index values from previous table; these values will match up to an external table and convert the raw pixel into color data fed to the VFPU
	* Unknown Data Table:
		* Magic Header:
			* DAT
		* Purpose: Most likely used for connecting textures with other model data (including Animation and Sound)
	* EOFC - common code to tell a data stream parser that it's time to stop reading the data
---

* Name: Packed Blob Data
* Magic Header: none
* Purpose: Most likely stores keys or a table related to rendering text in UI System
* Header Structure:
	* 0x00 - 4-byte File Size
	* 0x04 - 2-byte U ID (from associated SDOa file)
	* 0x08 - 1-byte X ID (from associated XTC file) + 0x01
---

* Name: Packed Bottom-up Data
* Magic Header: none
* Purpose: Stream VIF (VFPU Interface Format) or GIF (GU Interface Format) friendly data using a common technique developed for the PS2 Emotion Engine architecture and frequently employed by mostly Japanese developers on the PSP
* Header Structure:
	* 16-byte zero data; both represents the end of the stream read and tells the game engine how to read and treat the data
* Footer Structure: (acts as the header in most other formats and always read Bottom to Top)
	* Base Address:
		* 0x00 - Should always be 0
		* 0x01 - 1-byte Instruction code - observed as 0x07
		* 0x02 - 14-byte Sentinel that confirms this format
	* 0x10-0x1f & 0x21-0x2f - Most likely padding to help align the stream in 16 byte chunks
	* 0x20 - 1-byte Instruction Code to look out for in the stream; unknown if it's specific to the file read or tied to an action
	* 0x30 - 1-byte Instruction Code for current 16-byte data
	* 0x32 - 14-byte Data chunk
* Notes:
	* Observed in the binary:
		* Data is read as two different streams at the same time from Right to Left
			1. Reads in 6-byte chunks
			2. Reads in 1-byte chunks
		* Most likely packed Vector data due to usage of 3.4028235e+38 as a key and the size of data being read in the first stream
		* Further notes incoming as more of the binary is parsed
---

* Name: Packed Buffer Data
* Magic Header: none
* Purpose: Theoretical Scratchpad style buffer data used for storing data that must be moved quickly due to the PSP's limited hardware
* Notes:
	* I've briefly observed almost completely empty PBD files of set sizes in various parts of the data
	* This theory is primarily tied to the first format and the idea that it may have been created in error but also comes from observing unknown empty data structures in the binary that seem to be only used for this purpose
---
