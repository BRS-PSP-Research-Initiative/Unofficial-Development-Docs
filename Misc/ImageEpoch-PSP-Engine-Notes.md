In an attempt to streamline and improve my current Black Rock Shooter the Game reverse engineering and research, I've started poking at all of ImageEpoch's PSP games a bit. Here's some random findings so far:

1. They created at least 3 different engines: IeEngine (built for Fate/Extra; uses CriWare middleware and Lua 5.1 and derivatives reference IePSPlib in their game binaries), Stella Engine (built for Black Rock Shooter: the Game; vol archives and asset management framework are unique), and the Crime Engine (built for Criminal Girls; TPK archives and some networking code strings left in binary)

2. 07th Dragon 2020 used IeEngine but had some of Stella Engine's asset management code stapled on

3. Last Ranker used a modified version of the Stella Engine with the most notable changes being asset streamlining, rewritten scripting engine, and custom archive formats

4. Fate/Extra CCC used an updated version of IeEngine; not fully sure what all was changed beyond updates to some of the middleware

5. Sol Trigger used a heavily rewritten Stella Engine packaged within the Crime Engine TPK archive format; out of all of these games, it has the least in common with anything else; there was a focus on 64-bit variable usage (ulonglongs, doubles and double-precision floats immediately showed up when I did a quick look at the binary, for example), memory management was completely overhauled, and further asset streamlining improvements made (Last Ranker kept the context sensitive nature of Black Rock Shooter but heavily reduced it to a more manageable state; Sol Trigger implemented a Unity Engine style streaming system instead with assets being read in bulk by type, for example, even if they aren't being used at that particular moment)
