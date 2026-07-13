# General ImageEpoch PSP Engine / Tech Stack Doc

---

*Copyright 2026 - Brad D*

*See LICENSE for copyright information.*

*Please include this header and that license for any derivative works.*

*NOTE: Only the documentation, tools and anything that's not directly a part of the game's data fall under this copyright. I don't claim any ownership of the game or any of its assets*

---

* Name: IeEngine
* Known Games Developed:
  * Fate/Extra (version 1)
  * Fate/Extra CCC (version 2)
  * 07th Dragon 2020 (version 1.5)
  * 07th Dragon 2020-II (version 2.5)
* Version differences:
  * v1:
    * Named for the IeLibs and IePSPLibs strings found in binary
    * Heavy usage of CriWare middleware
    * (Proven false by Kotcrab; from a firmware update that I took was part of original binary) Scripted in Lua 5.1
    * (Proven false by Nemoumbra; uses the SN Systems Compiler) Debug strings in binary suggested that the standard GCC compiler that CriWare was built with was probably used to compile the game
  * v1.5:
    * Memory Card game installation required over normal game streaming
    * Stella Engine asset management and streaming strings found in binary; hence hybrid nomenclature (similar to Unreal Engine)
    * Same memory allocation implementation as Stella Engine
  * v2:
    * Updated CriWare modules
    * Possibly built with a newer version of GCC
  * v2.5:
    * Memory Card installation opted for CriPak instead of custom format used in original
---

* Name: Stella Engine
* Known Games Developed:
  * Black Rock Shooter: the Game (version 1)
  * Last Ranker (version 1 Capcom Variant)
  * Sol Trigger (version 2)
* Version differences:
  * v1:
    * Developed primarily for Black Rock Shooter's hybrid turn-based real-time third person shooter action combat
    * Uses a custom scripting implementation with flavors based on context
    * Heavily uses context for its formats; see individual formats for specifics
    * Designed with a multi-team, loose implementation structure so that each system and team could be somewhat independent with how they approached their needs
    * Memory allocation system seems to be custom
      * Remarkably similar to Visual Studio 2008's implementation (courtesy of the PC port for Criminal Girls)
      * Main shared part between Crime Engine and Stella Engine
      * Doesn't decompile correctly in Ghidra at the heap allocation level
      * Possibly based on the allocation system found within both the Every Extend Extra and Gunpey PSP prototypes in which one of the core programmers worked on prior
    * Vol encrypted archive format used primarily for Battle and main engine Systems (see RTDP format docs)
  * Capcom variant:
    * Debug strings and Memory allocation system seem almost exact
    * Context sensitive structure and many of the file formats left unmodified
    * Scripting engine rewritten from scratch
    * Asset management streamlined due to smaller team size and possibly smaller development time (unknown exactly how long game was in development)
    * Uses custom Capcom container formats instead of vol for most game archives
  * v2:
    * Full rewrite of many Systems with a focus on 2D assets and bulk asset streaming
    * Uses TPK format of Crime Engine archives but mostly Stella Engine formats for Assets
    * Unknown memory management system
    * 64-bit variables and C++ code referenced in debug strings
    * Possibly built with a PS Vita port in mind due to modern tech implemented
    * Compiler unknown but most likely one of the last ones released for the system
---

* Name: Crime Engine
* Known Games Developed:
  * Criminal Girls (version 1)
  * Criminal Girls: Invite Only (version 2 PS Vita)
  * Criminal Girls 2: Party Favors (version 2 NIS Variant)
* Version differences:
  * v1:
    * Shared memory allocation implementation with Stella Engine
    * Uses TPK archive format most likely based on the format used in Every Extend Extra (despite internally being zlib based and very similar to Stella Engine's CZAA format)
    * Suggested Live2D usage on PSP version
    * Heavy focus on 2D and 2.5D assets with 3D prerendered dungeons
  * v2:
    * PC version uses Visual Studio 2008 / 2005 memalloc for memory allocation
    * Many of the debug strings were almost exactly the same from v1
    * English and Japanese data blobs using the PS3ArcV1 format
    * Uses an unknown iMelody ring tone audio format version for many of its voice lines and other sound effects
    * Live2D version unknown but heavily implemented in the same way CriWare middleware was used in IeEngine (hence v1 probably using it)
    * NIS Japan through the Lead Programmer most likely have the full source code of either a release build or close to release prototype, meaning that at least the shared source code parts with the Stella Engine still exist
  * NIS variant:
    * Details unknown
---

### Original post from BRS Community Discord; kept for historical purposes. The above notes are more up to date and proper.
In an attempt to streamline and improve my current Black Rock Shooter the Game reverse engineering and research, I've started poking at all of ImageEpoch's PSP games a bit. Here's some random findings so far:

1. They created at least 3 different engines: IeEngine (built for Fate/Extra; uses CriWare middleware and Lua 5.1 and derivatives reference IePSPlib in their game binaries), Stella Engine (built for Black Rock Shooter: the Game; vol archives and asset management framework are unique), and the Crime Engine (built for Criminal Girls; TPK archives and some networking code strings left in binary)

2. 07th Dragon 2020 used IeEngine but had some of Stella Engine's asset management code stapled on

3. Last Ranker used a modified version of the Stella Engine with the most notable changes being asset streamlining, rewritten scripting engine, and custom archive formats

4. Fate/Extra CCC used an updated version of IeEngine; not fully sure what all was changed beyond updates to some of the middleware

5. Sol Trigger used a heavily rewritten Stella Engine packaged within the Crime Engine TPK archive format; out of all of these games, it has the least in common with anything else; there was a focus on 64-bit variable usage (ulonglongs, doubles and double-precision floats immediately showed up when I did a quick look at the binary, for example), memory management was completely overhauled, and further asset streamlining improvements made (Last Ranker kept the context sensitive nature of Black Rock Shooter but heavily reduced it to a more manageable state; Sol Trigger implemented a Unity Engine style streaming system instead with assets being read in bulk by type, for example, even if they aren't being used at that particular moment)
