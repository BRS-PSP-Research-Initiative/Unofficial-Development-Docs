# System.VOL Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation covers a general overview of the System.VOL Archive in the Data on disc.

* Purpose: Contains shared Global data that multiple Systems rely on and build their data blobs from.
* Module Type: RTDP Vol Archive
* Contents:
    * ucs2jis.bin
    * ascii.ptm
    * font.lpk
    * db_resident.lpk
    * msg_system.bin
    * if_rsdsys.lpk
    * if_fldsys.lpk
    * if_btlsys.lpk
    * fld_resident.bin
    * fld_pack.bin
    * persisvision.ptm
    * btl_system.bin
    * btl_map_list.bin
    * enmgrp2.dat
    * btl_msg_tbl.bin
    * btl_atk_tbl.bin
    * btl_dummy.bin
    * eb000.efp
    * btl_dummy.bin
    * btl_skl_tbl.bin
    * btl_eff_tbl.bin
    * btl_finish_tbl.bin
    * pack.vol
    * btl_dummy.bin
    * instdat.vls
    * rec_script.ss
    * jin_pack.bin
    * tail.bin
* Implementation Notes:
    * Has two variations in the binary:
        * var2 - checks if current string has "disc0:" substring and nulls out heap[2]
        * var1 - allocates heap from start with no extra checking
    * Relies on Systems:
        * Audio - for handling At3 files within
        * Graphics - for handling Font rendering and UI elements
        * Parsing - for handling several tables and lists, the Installation implementation and data stored within pack.vol
        * Scripting - not fully sure what this is used for yet but there is an initial script here, probably related to saves or a test of some type

---
