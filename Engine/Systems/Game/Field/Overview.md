# Battle Overview Doc

---

*Copyright 2025 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

This documentation is just a general overview of the entire Field System. For more specific information on each individual part of it, such as Asset storage or how each System handles Production, those will be in separate sections of the System documentation.

* Purpose: Handle the entire Field System Stack
* Production Type: Self-contained Production all the way down the Stack
* Pipeline:
    * Read Top Level SC Hierarchy attribute to determine what kind of Field Module this is
    * Read SSCR data for Instruction and Implementation data
    * Find all individual SC parts within data and determine what they do by Hierarchy Attribute
    * Start Asset Production based on Hierarchy and type of data each SC part contains with SSCR data
    * Assemble each part as they are produced
    * Deliver complete Asset to Pickup location in Memory

---
