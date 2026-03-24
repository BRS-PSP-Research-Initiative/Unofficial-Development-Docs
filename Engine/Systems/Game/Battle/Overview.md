# Battle Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a general overview of the entire Battle System. For more specific information on each individual part of it, such as Asset storage or how each System handles Production, those will be in separate sections of the System documentation.

* Purpose: Handle the entire Battle System Stack
* Production Type: Production of Individual Battle Assets that get Assembled Elsewhere
* Pipeline:
    * Read BXCB data
    * Read bscr data
    * Determine if all required Production Assets are available within module
    * Request other related modules to Produce missing dependencies
    * Assemble Asset from parts as they arrive
    * Keep checking Asset Production until entire Assembled Asset is complete
    * Deliver Asset to Pickup location in memory

---
