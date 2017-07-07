This page documents the partitions that can mounted by
[Filesystem\_services\#MountGameCardPartition](Filesystem%20services#MountGameCardPartition.md##MountGameCardPartition "wikilink").

The below sections are for each partitionID.

# 0

Contains the gamecard sysupdate. Attempting to mount this results in
error 0x13DA02. Using certain
[NCM](Location%20Resolver%20services.md "wikilink") commands first might
be required?

# 2

Contains the game [NCAs](NCA.md "wikilink").

  - "<NcaId>.nca" ...
  - "<NcaId>.cnmt.nca" Encrypted [NCA](NCA.md "wikilink")-type0 content.
