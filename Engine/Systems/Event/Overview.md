# Event Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a general overview of the Event System. Not all other Systems are driven by it and each one has its own flavor.

* Purpose: Loosely handle requests from Systems
* Real Life Counterpart: Document Courier
* Types (in order of Priority):
    * Engine - Deals with Events that drive the top level Systems that run Game's backend (parts that don't affect what Player experiences in Game)
    * System - Uses associated Data blob that gets passed to StellaVM and used to track which System Events are completed
    * Gameplay - Handles Player experience in Game
* Notable Task Data Blobs:
    * High-Level Task Data:
        * Uses prefix: `Ht`
        * Engine Task Type
    * BATTLE TASK Data:
        * Uses prefix: `Bt`
        * Functions as both Battle System and Gameplay Task Types
    * FEVT
        * Doesn't have an associated prefix
        * Gameplay Task Type
        * Uses location in Data on disc as its Identifier: `PSP_GAME/USRDIR/GAMEDATA/FLD/FEVT`
* General Event Pointer Structure (by Index):
    * 0 - 32-byte String Name
    * 1 - 4-byte Start Value; 1 if Base, 0 if Everything else
    * 2 - Event Task Callback function
    * 3 - Copy of full structure at current point in process
* Scene Pointer Structure:
    * 0 - "HtScene"

---
