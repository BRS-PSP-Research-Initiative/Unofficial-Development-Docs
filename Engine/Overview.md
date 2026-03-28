# Engine Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Purpose: an overview of the Game Engine used in Black Rock Shooter: the Game
* Given Name: Stella Engine
* Developer: Imageepoch
* Platforms Supported:
    * Playstation Portable
    * Playstation 3 (Probable due to rumors and structure of data)
    * Xbox 360 (Theoretical due to Installation implementation using RSVC and RSVX file formats)
* Known Game Usage:
    * Black Rock Shooter: The Game
    * Arc Rise Fantasia (modified RTDP archive implementation only)
* Programming Languages Used:
    * Most likely C99 C
        * Multiplatform support and portability
        * Structure of data suggests optimization of formats and memory management prioritized over accepting the overhead that comes from taking advantage of the modern benefits that C++ brings
    * StellaScript
        * General purpose scripting language used in multiple Systems
        * Each System has its own custom flavor tailored to its needs
        * May be tied to StellaVM functionality but not fully confirmed yet
* Notable Implementations:
    * StellaVM:
        * handles a multitude of tasks, leveraging a static pointer, jump tables, and code substitution on main thread
        * known task types:
            * heap allocation stage 1
            * general callback tasks
            * suspected rigging, camera and cutscene Production leveraging complex math related to Projection Matrix data 
* Known Issues:
    * Much of the engine code is heavily duplicated between Systems with either slight differences or no changes at all to implementation

---
