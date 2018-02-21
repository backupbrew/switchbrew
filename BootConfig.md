Installed into the first 0x4000 sector of the eMMC storage's [BCPKG2
partitions](Flash%20Filesystem#User%20Partitions.md##User_Partitions "wikilink"),
"BootConfig" contains data used to configure TrustZone/OS behaviors.

BootConfig is normally all-zero for retail units, however TrustZone
additionally sets the loaded configuration to all-zero when running on a
retail unit anyway.

# Format

Despite having 0x4000 for storage, the actual loaded BootConfig is only
0x640 bytes, with the following format:

| Offset | Size  | Description            |
| ------ | ----- | ---------------------- |
| 0x0    | 0x200 | Unsigned Configuration |
| 0x200  | 0x100 | RSA-PSS Signature      |
| 0x300  | 0x100 | Signed Configuration   |
| 0x400  | 0x240 | Reserved               |

# Signed Config

Most of this is currently awaiting better
documentation.

| Offset | Size | Description                                                                                                                                                                                             |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x8    | 0x1? | Package2 Configuration. Bit 0 set means Package2 is stored unencrypted. Bit 1 set means Package2 is unsigned.                                                                                           |
| 0x10   | 0x10 | Hardware Info. Must match the Hardware Info read from fuses, or else the loaded Signed Config will be memset to 0 even if signed. This allows Nintendo to set signed configuration on a per-unit basis. |
| 0x20   | 0x1? | [DisableProgramVerification](Filesystem%20services#SetEnabledProgramVerification.md##SetEnabledProgramVerification "wikilink"). Controls the default value for how to check NCA signatures.             |

# Unsigned Config
