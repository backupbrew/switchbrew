This is **control.nacp**, "nn::ns::ApplicationControlProperty".

Roughly equivalent to non-gfx areas of 3DS SMDH. All strings for
language-entries are UTF-8, unlike SMDH which uses UTF-16.

Total size is 0x4000-bytes.

# Structure

| Offset | Size                 | Description                                                                                         |
| ------ | -------------------- | --------------------------------------------------------------------------------------------------- |
| 0x0    | 0x3000 (0x300\*0x10) | [Title entries](#Title_Entry "wikilink")                                                            |
| 0x3000 | 0x25                 | Isbn                                                                                                |
| 0x3025 | 0x1                  | StartupUserAccount                                                                                  |
| 0x3026 | 0x1                  | UserAccountSwitchLock                                                                               |
| 0x3027 | 0x1                  | AddOnContentRegistrationType                                                                        |
| 0x3028 | 0x4                  | ApplicationAttribute                                                                                |
| 0x302C | 0x4                  | SupportedLanguages                                                                                  |
| 0x3030 | 0x4                  | ParentalControl                                                                                     |
| 0x3034 | 0x1                  | Screenshot                                                                                          |
| 0x3035 | 0x1                  | [\#VideoCaptureMode](#VideoCaptureMode "wikilink")                                                  |
| 0x3036 | 0x1                  | DataLossConfirmation                                                                                |
| 0x3037 | 0x1                  | [\#PlayLogPolicy](#PlayLogPolicy "wikilink")                                                        |
| 0x3038 | 0x8                  | PresenceGroupId                                                                                     |
| 0x3040 | 0x20                 | RatingAge                                                                                           |
| 0x3060 | 0x10                 | DisplayVersion                                                                                      |
| 0x3070 | 0x8                  | AddOnContentBaseId                                                                                  |
| 0x3078 | 0x8                  | SaveDataOwnerId                                                                                     |
| 0x3080 | 0x8                  | UserAccountSaveDataSize                                                                             |
| 0x3088 | 0x8                  | UserAccountSaveDataJournalSize                                                                      |
| 0x3090 | 0x8                  | DeviceSaveDataSize                                                                                  |
| 0x3098 | 0x8                  | DeviceSaveDataJournalSize                                                                           |
| 0x30A0 | 0x8                  | BcatDeliveryCacheStorageSize                                                                        |
| 0x30A8 | 0x8                  | ApplicationErrorCodeCategory                                                                        |
| 0x30B0 | 0x40 (0x8\*0x8)      | LocalCommunicationIds                                                                               |
| 0x30F0 | 0x1                  | LogoType                                                                                            |
| 0x30F1 | 0x1                  | LogoHandling                                                                                        |
| 0x30F2 | 0x1                  | RuntimeAddOnContentInstall                                                                          |
| 0x30F3 | 0x3                  | Reserved                                                                                            |
| 0x30F6 | 0x1                  | CrashReport                                                                                         |
| 0x30F7 | 0x1                  | Hdcp                                                                                                |
| 0x30F8 | 0x8                  | SeedForPseudoDeviceId                                                                               |
| 0x3100 | 0x41                 | [BcatPassphrase](BCAT%20Content%20Container.md "wikilink") (all-zero when unused)                   |
| 0x3141 | 0x1                  | StartupUserAccountOption                                                                            |
| 0x3142 | 0x6                  | ReservedForUserAccountSaveDataOperation                                                             |
| 0x3148 | 0x8                  | UserAccountSaveDataMaxSize                                                                          |
| 0x3150 | 0x8                  | UserAccountSaveDataMaxJournalSize                                                                   |
| 0x3158 | 0x8                  | DeviceSaveDataMaxSize                                                                               |
| 0x3160 | 0x8                  | DeviceSaveDataMaxJournalSize                                                                        |
| 0x3168 | 0x8                  | TemporaryStorageSize                                                                                |
| 0x3170 | 0x8                  | CacheStorageSize                                                                                    |
| 0x3178 | 0x8                  | CacheStorageJournalSize                                                                             |
| 0x3180 | 0x8                  | CacheStorageMaxSizeAndMaxJournalSize                                                                |
| 0x3188 | 0x8                  | CacheStorageMaxIndex                                                                                |
| 0x3190 | 0x80 (0x8\*0x10)     | PlayLogQueryableApplicationId                                                                       |
| 0x3210 | 0x1                  | PlayLogQueryCapability                                                                              |
| 0x3211 | 0x1                  | RepairFlag                                                                                          |
| 0x3212 | 0x1                  | ProgramIndex                                                                                        |
| 0x3213 | 0x1                  | RequiredNetworkServiceLicenseOnLaunchFlag                                                           |
| 0x3214 | 0x4                  | Reserved                                                                                            |
| 0x3218 | 0x18                 | [SendDataConfiguration](#SendDataConfiguration/ReceivableDataConfiguration_Entry "wikilink")        |
| 0x3230 | 0x180 (0x18 \* 0x10) | [ReceivableDataConfigurations](#SendDataConfiguration/ReceivableDataConfiguration_Entry "wikilink") |
| 0x33B0 | 0x8                  | JitConfigurationFlag                                                                                |
| 0x33B8 | 0x8                  | MemorySize                                                                                          |
| 0x33C0 | 0xC40                | Reserved                                                                                            |

## Title Entry

Total size is 0x300-bytes.

| Offset | Size  | Description                   |
| ------ | ----- | ----------------------------- |
| 0x0    | 0x200 | Application name strings      |
| 0x200  | 0x100 | Application publisher strings |

Entry index for each
[language](Settings%20services#LanguageCode.md##LanguageCode "wikilink"):

| Entry-index | Icon [language](NCA%20Content%20FS#FS-type3.md##FS-type3 "wikilink") filename |
| ----------- | ----------------------------------------------------------------------------- |
| 0           | "AmericanEnglish"                                                             |
| 1           | "BritishEnglish"                                                              |
| 2           | "Japanese"                                                                    |
| 3           | "French"                                                                      |
| 4           | "German"                                                                      |
| 5           | "LatinAmericanSpanish"                                                        |
| 6           | "Spanish"                                                                     |
| 7           | "Italian"                                                                     |
| 8           | "Dutch"                                                                       |
| 9           | "CanadianFrench"                                                              |
| 10          | "Portuguese"                                                                  |
| 11          | "Russian"                                                                     |
| 12          | "Korean"                                                                      |
| 13          | "TraditionalChinese"                                                          |
| 14          | "SimplifiedChinese"                                                           |

Official apps tend to have the title entries' strings set only to
English. Some apps don't have certain title entries set at all. In
addition, official apps usually (?) don't have the following title
entries set: Korean, Taiwanese, and Chinese.

## VideoCaptureMode

This is the enum used to determine how gameplay recording can occur, if
at all.

| Value | Meaning   |
| ----- | --------- |
| 0     | Disabled  |
| 1     | Enabled   |
| 2     | Automatic |

When this value is 0, gameplay cannot be recorded. When this value is 1,
the game must manually sacrifice some of its heap as transfer memory for
AM's IApplicationProxy-\>InitializeGamePlayRecording(). When this value
is 2, AM will call NS-\>BoostSystemMemoryResourceSize(), and allocate
the required memory for recording automatically without the usermode
process having to do anything.

## PlayLogPolicy

[AM](Applet%20Manager%20services.md "wikilink") passes
[this](Shared%20Database%20services#PlayLogPolicy.md##PlayLogPolicy "wikilink")
to [pdm:ntfy](Shared%20Database%20services.md "wikilink") cmd9.

## PlayLogQueryCapability

This is used with [AM](Applet%20Manager%20services.md "wikilink")
commands QueryApplicationPlayStatistics and
QueryApplicationPlayStatisticsByUid, to verify whether querying the
specified titleIDs are allowed. When not allowed, error 0x3E880 is
returned.

| Value | Meaning   | Description                                                                                                            |
| ----- | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| 0     | None      | The specified titleIDs must match the user-process titleID.                                                            |
| 1     | WhiteList | The specified titleIDs must match the user-process titleID, or one of the titleIDs from PlayLogQueryableApplicationId. |
| 2     | All       | All titleIDs are allowed.                                                                                              |

## SendDataConfiguration/ReceivableDataConfiguration Entry

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 0x8  | Id          |
| 0x8    | 0x10 | Key         |
