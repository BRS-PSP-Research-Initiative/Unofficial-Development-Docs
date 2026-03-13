# PTMD Mesh Data Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Packed Texture Model Data
* Type: Asset Data
* Extension: .ptm
* Header: PTMD, PTM, PTMD-XP
* Purpose: Contains bit encrypted texture and model data with the decryption keys inside of the main binary
* Notes:
    * Mostly debunked
        * The compression file signature was left in the debug models and found using Signsearch (from the same developer of QuickBMS)
        * This signature was stripped out of all texture files and was only found by complete accident
        * Subject to scrutiny until further tests are performed:
            * Imageepoch used the Dynamic Markov Compression algorithm written about [here](https://plg.uwaterloo.ca/~gvcormac/manuscripts/dmc.pdf)
            * This format wasn't used much since its inception in 1986
            * The Tentative Name was originally `Plot Thickens, My Dear` but feedback suggested I name this something more correct
            * A 6MB texture file was compressed into 200KB
        * Contains a PTR Texture file
        * Assuming data is read as 2 byte chunks that get parsed with Bitwise OR of 4 and then moves forward two bytes until it hits 0000 or 0x50 byte chunks have been read
    * From Eboot.bin decompilation
        * 2D Assets
            * Don't contain CLUT (Color LookUp Table)
            * Still decompress texture_mode data
* Header Structure:
	* 0x08 - (1-byte) Compressed data start address (with an offset of 0x8 in most occurrences)
    * 0x09 - (1-byte) Texture mode key - gets further processed into becoming the full key once other data has been decompressed
	* 0x0c - (4-byte) Address to end of file or beginning of padding section (which may contain extra data); expect this to be around 0x400 off of what the file system shows for size
* Data Structure (by region)
    * CLUT

---
