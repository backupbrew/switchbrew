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

## RomFS Override

The current strategy for providing RomFS to homebrew applications
depends on the application being able to find and open its own NRO file
via argv\[0\] and load RomFS from ASET. This is not practical for
several use cases that I am encountering:

\- The NRO file is not persisted to the SD card.

\- The NRO file is not stored somewhere that the homebrew library knows
how to access.

\- The application does not exist as an NRO file at all.

I'd like to propose a new HBABI key to allow homebrew applications to
access RomFS without needing to open their own NRO file via
argv\[0\].

`   ==== RomFSOverride ====`  
`   This is used to override an application's RomFS. If this key is passed and recognized, the application shall make no attempt to open itself via fopen(argv[0]).`  
`   `  
`   * `**`Key:`**` 15`  
`   * `**`Value[0]:`**` Handle to a session implementing `[`Filesystem_services#IFileSystem`](Filesystem%20services#IFileSystem.md##IFileSystem "wikilink")` for the application's RomFS.`  
`   * `**`Value[1]:`**` Ignored.`  
`   `  
`   The given handle must respond to IFileSystem commands 0-12.`

Possible alternatives include instead passing IFile/IStorage for the
RomFS section, or IFile/IStorage for the entire ASET section.

Concerns include ownership of the session handle. Should the application
be required to close the handle or leave it open? Personally, I'm
inclined to require that the application borrow the session from the
loader and leave it open in case closing the handle is not something
desirable. This also simplifies the logic in the loader, since if the
handle needs to be closed, the loader can always just close it instead
of having to figure out whether it was recognized or not. Possible
alternatives to this ownership scheme include either adding flags to
HBABI entries for which words contain handles that should be closed if
not recognized, or a flag that the application sets on each entry it
recognizes so that the loader can take care of closing the handle if the
application did not recognize it.

\--[Misson20000](User:Misson20000 "wikilink")
([talk](User%20talk:Misson20000.md "wikilink")) 00:36, 6 November 2018
(UTC)

  -   
    "- The NRO file is not persisted to the SD card." "- The NRO file is
    not stored somewhere that the homebrew library knows how to access."
    "- The application does not exist as an NRO file at all." The ABI
    requires the NRO to located on SD in the first place...
    --[Yellows8](User:Yellows8 "wikilink")
    ([talk](User%20talk:Yellows8.md "wikilink")) 19:34, 8 November 2018
    (UTC)

<!-- end list -->

  -   
    Like yellows8 said, the homebrew ABI is designed around NRO files
    stored on SD card. If we ever support other filesystems (such as
    hostio access), we'd just add support for host:/ paths being passed
    through argv (as well as support code in libnx which would be
    trivial) - homebrew apps would need a recompile anyway with or
    without new ABI keys. Also, for that use case (hostio), romfs
    doesn't really make sense because you could just use assets in a
    folder inside the host filesystem instead of having to go through
    the trouble of building romfs (which can get pretty large). Finally,
    homebrew by definition is NRO formatted. Other formats should not be
    supported or promoted. --[Fincs](User:Fincs "wikilink")
    ([talk](User%20talk:Fincs.md "wikilink")) 19:47, 8 November 2018
    (UTC)

yellows8: It says nowhere in the homebrew ABI document that the NRO is
required to be located on the SD card. If you are absolutely convinced
that that should be an HBABI requirement, I would encourage you to add
it to the document. I very much think that should not be an HBABI
requirement though. The only things keeping homebrew on the SD card are
libnx's behavior of reading its own executable combined with the small
set of default-mounted filesystems that libnx understands. Aside from
this behavior (which I'm trying to get changed), there is no reason to
require that homebrew applications be located on the SD card.

fincs: Apologies if I was unclear. When I said RomFS, I meant the
filesystem that is visible to libnx applications under `romfs:/*` paths.
For the hostio use case, if hostio were to be mounted under `hostio:`,
the application would need to be written to tell whether it's on hostio
or not and adjust its asset loading paths accordingly, whereas it would
be significantly more convenient if the homebrew loader could override
the `romfs:` mountpoint to use a hostio IFileSystem. I also disagree
that homebrew is "by definition" NRO formatted. By convention, sure, and
I'd even accept that this ABI does not apply to non-NRO formatted
homebrew. I invite you to ignore that use case.

Here's a different idea for
you.

`   ==== Mount ====`  
`   This is used to request that a filesystem be mounted by the homebrew application.`  
`   `  
`   * `**`Key:`**` 15`  
`   * `**`Value[0]:`**` Pointer to a NULL-terminated string representing the desired mountpoint.`  
`   * `**`Value[1]:`**` Handle to a session implementing `[`Filesystem_services#IFileSystem`](Filesystem%20services#IFileSystem.md##IFileSystem "wikilink")`.`  
`   `  
`   The length of the mountpoint shall be no longer than 32 characters, including the NULL terminator.`  
`   This key may be combined with the Argv key to specify the location of an application's executable.`  
`   `

This way, we can still override `romfs:/` with Mount\["romfs",
<IFileSystem>\], or we can mount an arbitrary filesystem (Mount\["myfs",
<IFileSystem>\]) and set argv\[0\] to a path on that new mountpoint
(`myfs:/application.nro`) so that the application can still find its NRO
file and read it back to provide the `romfs:/` mount even if the NRO is
not located on the SD card. I've even specified a length limit to match
fsdev requirements.

\--[Misson20000](User:Misson20000 "wikilink")
([talk](User%20talk:Misson20000.md "wikilink")) 23:42, 9 November 2018
(UTC)

[Homebrew\_ABI\#NextLoadPath](Homebrew%20ABI#NextLoadPath.md##NextLoadPath "wikilink")
"NRO" "should start with "sdmc:/". Of course nx-hbloader doesn't enforce
the latter besides only having sdmc mounted.
--[Yellows8](User:Yellows8 "wikilink")
([talk](User%20talk:Yellows8.md "wikilink")) 00:05, 10 November 2018
(UTC)

For NextLoadPath? Sure, if you want to use NextLoadPath, it's best to
give it a path to an NRO starting with "sdmc:/" *because that's all that
nx-hbloader understands* and all that you want it to understand, which
makes sense. But HBABI doesn't require that homebrew needs to be loaded
by passing NextLoadPath back to the loader. After all, nx-hbmenu isn't
loaded that way. That's besides the point, anyway. The point is that
whether or not this restriction is actually documented on the HBABI
page, I want you to evaluate why this restriction exists and whether
it's necessary or not.

\--[Misson20000](User:Misson20000 "wikilink")
([talk](User%20talk:Misson20000.md "wikilink")) 00:27, 10 November 2018
(UTC)
