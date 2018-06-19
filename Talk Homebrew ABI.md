## StdioSockets

Currently, there's a broken link in the [Loader Config
Keys](Homebrew%20ABI#Loader%20Config%20Keys.md##Loader_Config_Keys "wikilink")
section on the StdioSockets key, caused by a [recent removal of the
section](http://switchbrew.org/index.php?title=Homebrew_ABI&curid=284&diff=4772&oldid=3846).
I understand the temptation to remove StdioSockets, since it wasn't very
well designed in the first place, and nobody uses it anymore, but I
don't think that it makes sense to remove it from the ABI specification.
The key shouldn't be erased entirely, because that would indicate that
it is unreserved. A backwards-incompatible change like that defeats one
of the purposes of the ABI. Removing the link and adding a label that
the key is deprecated would be acceptable, but it'd leave no
specification on the key. I think that, unless I'm misinterpreting the
original intent of the edit, it should be reverted and labels should be
added to the key's specification that it is deprecated and no longer in
use.

Mentioning [WinterMute](User:WinterMute "wikilink").

\--[Misson20000](User:Misson20000 "wikilink")
([talk](User%20talk:Misson20000.md "wikilink")) 17:50, 18 June 2018
(CDT)

Probably better to just reserve it for future use I guess. Had someone
interrogate me about why nxlink didn't use the homebrew ABI "properly"
so it seemed better to remove it rather than leave it there confusing
people.

[WinterMute](User:WinterMute "wikilink")
([talk](User%20talk:WinterMute.md "wikilink")) 04:26, 19 June 2018 (CDT)
