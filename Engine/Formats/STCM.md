# STCM Map File Format Docs

---

*Copyright 2024 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: Stage Type Contained Map data
* Type: Container
* Extension: .bin, .sm
* Header: STCM
* Purpose: Stores Stage and Map data
* System Implementation Differences:
  * Shared:
  * 2/3 Parts of Disc Layout:
  * bscr Script - contains implementation for loading and structuring some of the Map data
  * Sky - contains the Skybox and possibly non-interactive elements like tall buildings, chains, etc
  * Battle:
    * Uses `.bin` extension
    * Sky portion named Arena file name + `_sky` before extension
    * 1/3 Parts of Disc Layout:
      * Arena - where the fight takes place in
  * Field (Stage):
    * SC containers normally do not list extensions or original filenames in data but engine associates internal STCM's with `.sm` extension
    * 1/3 Parts of Disc Layout:
      * Ground - Similar to Arena but much larger scale (may also have different data structure within)
* Notes:
  * Originally found in decrypted and extracted Map VOLs under `GAMEDATA\BTL\MAP`
  * Parsed from Game Binary Generic Asset Loader:
    * Arbitrary `.bin` files that do not have an `LPK` or `BXCB` Magic Header fallback to being checked as either a Map, an MDL or NULL data
* Header Structure:
  * 0x08 - Offset from <0x1c> to CLIM or next STCM section
  * 0x1c - Offset to First Embedded Data section (usually PTMD)
---
