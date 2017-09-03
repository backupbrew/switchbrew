# Structure

These have been redesigned from the 3DS so that they fit within a
Aarch64 MOV instruction immediate most of the time (without requiring
the additional MOVK).

| Bits | Field       |
| ---- | ----------- |
| 8-0  | Module      |
| 21-9 | Description |

When a fatal-error is received the error code is outputted using the
following formatter:

` %04d-%04x`

.. where the first code is `2000 + Module`, and the other being
`Description`. Bits \>=22 from the error-code are unused when displaying
fatal-errors, since the Description ends with bit21.

# Modules

| Value | Name                                                   |
| ----- | ------------------------------------------------------ |
| 1     | Kernel                                                 |
| 2     | FS                                                     |
| 3     | NVIDIA                                                 |
| 5     | NCM                                                    |
| 6     | DD                                                     |
| 8     | LR                                                     |
| 9     | Loader                                                 |
| 10    | CMIF (IPC command interface)                           |
| 11    | HIPC (IPC)                                             |
| 15    | PM                                                     |
| 16    | NS                                                     |
| 18    | HTC                                                    |
| 21    | SM                                                     |
| 22    | RO userland                                            |
| 24    | SDMMC                                                  |
| 26    | SPL                                                    |
| 100   | ETHC                                                   |
| 101   | I2C                                                    |
| 105   | Settings                                               |
| 110   | NIFM                                                   |
| 114   | Display                                                |
| 116   | NTC                                                    |
| 117   | FGM                                                    |
| 120   | PCIE                                                   |
| 121   | Friends                                                |
| 123   | SSL                                                    |
| 124   | Account                                                |
| 126   | Mii                                                    |
| 128   | AM                                                     |
| 129   | Play Report                                            |
| 133   | PCV                                                    |
| 134   | OMM                                                    |
| 137   | NIM                                                    |
| 138   | PSC                                                    |
| 140   | USB                                                    |
| 143   | BTM                                                    |
| 147   | ERPT                                                   |
| 148   | APM                                                    |
| 154   | NPNS                                                   |
| 157   | ARP                                                    |
| 158   | BOOT                                                   |
| 161   | NFC                                                    |
| 162   | Userland assert                                        |
| 168   | Userland crash                                         |
| 203   | HID                                                    |
| 206   | Capture                                                |
| 651   | TC                                                     |
| 800   | [General web-applet](Internet%20Browser.md "wikilink") |
| 809   | [WifiWebAuthApplet](Internet%20Browser.md "wikilink")  |
| 810   | [Whitelisted-applet](Internet%20Browser.md "wikilink") |
| 811   | [ShopN](Internet%20Browser.md "wikilink")              |

8XX is for/includes system
applets.

# Error codes

| Value             | Description | Description                                                                                                                                                                          |
| ----------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x1C01            | 14          | Invalid kernel capability descriptor                                                                                                                                                 |
| 0xCA01            | 101         | Invalid size                                                                                                                                                                         |
| 0xCC01            | 102         | Invalid address                                                                                                                                                                      |
| 0xCE01            | 103         | Address is NULL / buffer size is too small.                                                                                                                                          |
| 0xD201            | 105         | Handle-table full.                                                                                                                                                                   |
| 0xD401            | 106         | Invalid memory state / invalid memory permissions.                                                                                                                                   |
| 0xD801            | 108         | When trying to set executable permission on memory.                                                                                                                                  |
| 0xDC01            | 110         | Stack address outside allowed range                                                                                                                                                  |
| 0xE001            | 112         | Invalid thread priority.                                                                                                                                                             |
| 0xE201            | 113         | Invalid processor id.                                                                                                                                                                |
| 0xE401            | 114         | Invalid handle.                                                                                                                                                                      |
| 0xE601            | 115         | Syscall copy from user failed.                                                                                                                                                       |
| 0xE801            | 116         | Invalid combination                                                                                                                                                                  |
| 0xEA01            | 117         | Time out? When you give 0 handles to svcWaitSynchronizationN.                                                                                                                        |
| 0xEE01            | 119         | Exceeding maximum                                                                                                                                                                    |
| 0xF001            | 120         | Invalid enum                                                                                                                                                                         |
| 0xF201            | 121         | No such entry                                                                                                                                                                        |
| 0xF401            | 122         | Irq already registered                                                                                                                                                               |
| 0xF601            | 123         | Port remote dead                                                                                                                                                                     |
| 0xF801            | 124         | Unhandled usermode exception                                                                                                                                                         |
| 0xFA01            | 125         | Wrong memory permission?                                                                                                                                                             |
| 0x10601           | 131         | Port max sessions exceeded                                                                                                                                                           |
| 0x10801           | 132         | Resource limit exceeded                                                                                                                                                              |
| 0xE02             | 7           | High byte in input u64 is zero.                                                                                                                                                      |
| 0x7802            | 60          | The specified [NCA](NCA.md "wikilink")-type doesn't exist for this title.                                                                                                            |
| 0x7D202           | 1001        | Process does not have RomFs                                                                                                                                                          |
| 0x7D402           | 1002        | Title-id not found / savedata not found.                                                                                                                                             |
| 0x13B002          | 2520        | Gamecard not inserted                                                                                                                                                                |
| 0x13DA02          | 2541        | Version check failed when mounting gamecard sysupdate partition?                                                                                                                     |
| 0x171402          | 2954        | Invalid gamecard handle.                                                                                                                                                             |
| 0x196002          | 3248        | Out of memory                                                                                                                                                                        |
| 0x196202          | 3249        | Out of memory                                                                                                                                                                        |
| 0x1A4A02          | 3365        | Out of memory                                                                                                                                                                        |
| 0x235E02          | 4527        | NCA-path used with the wrong titleID.                                                                                                                                                |
| 0x250E02          | 4743        | [Corrupted](NAX0.md "wikilink") NAX0 header.                                                                                                                                         |
| 0x251002          | 4744        | Invalid [NAX0](NAX0.md "wikilink") magicnum.                                                                                                                                         |
| 0x2EE202          | 6001        | Invalid input                                                                                                                                                                        |
| 0x2EE602          | 6003        | Path too long                                                                                                                                                                        |
| 0x2F5A02          | 6061        | Offset outside storage                                                                                                                                                               |
| 0x313802          | 6300        | Operation not supported                                                                                                                                                              |
| 0x320002          | 6400        | Permission denied                                                                                                                                                                    |
| 0x326602          | 6451        | Missing titlekey(?) required to mount content                                                                                                                                        |
| 0x3EA03           | 501         | Invalid handle                                                                                                                                                                       |
| 0x3EE03           | 503         | Invalid memory mirror                                                                                                                                                                |
| 0xA05             | 5           | [NcaID](Content%20Manager%20services.md "wikilink") not found. Returned when attempting to mount titles which exist that aren't \*8XX titles, the same way \*8XX titles are mounted. |
| 0xE05             | 7           | TitleId not found                                                                                                                                                                    |
| 0x1805            | 12          | Invalid StorageId                                                                                                                                                                    |
| 0xDC05            | 110         | Gamecard not inserted                                                                                                                                                                |
| 0x17C05           | 190         | Gamecard not initialized                                                                                                                                                             |
| 0x1F405           | 250         | Sdcard not inserted                                                                                                                                                                  |
| 0x20805           | 260         | Storage not mounted                                                                                                                                                                  |
| 0x408             | 2           | Not initialized.                                                                                                                                                                     |
| 0x608             | 3           | Invalid control StorageID.                                                                                                                                                           |
| 0x808             | 4           | Storage not found.                                                                                                                                                                   |
| 0xA08             | 5           | Access denied.                                                                                                                                                                       |
| 0xE08             | 7           | Title is not registered.                                                                                                                                                             |
| 0x409             | 2           | Maximum processes loaded.                                                                                                                                                            |
| 0x6609            | 51          | Invalid memory state/permission                                                                                                                                                      |
| 0x6A09            | 53          | Invalid NRR                                                                                                                                                                          |
| 0xA209            | 81          | Unaligned NRR address                                                                                                                                                                |
| 0xA409            | 82          | Bad NRR size                                                                                                                                                                         |
| 0xAA09            | 85          | Bad NRR address                                                                                                                                                                      |
| 0x1A80A           | 212         | Bad magic (expected 'SFCO')                                                                                                                                                          |
| 0x20B             | 1           | Size too big to fit to marshal.                                                                                                                                                      |
| 0x11A0B           | 141         | Went past maximum during marshalling.                                                                                                                                                |
| 0x1900B           | 200         | Session doesn't support domains.                                                                                                                                                     |
| 0x25A0B           | 301         | Remote process is dead.                                                                                                                                                              |
| 0x3D60B           | 491         | IPC Query 1 failed.                                                                                                                                                                  |
| 0x20F             | 1           | Pid not found                                                                                                                                                                        |
| 0x60F             | 3           | Process has no pending events                                                                                                                                                        |
| 0x410             | 2           | Title-id not found                                                                                                                                                                   |
| 0xF010            | 120         | Gamecard sysupdate not required                                                                                                                                                      |
| 0x1F610           | 251         | Unexpected StorageId                                                                                                                                                                 |
| 0x415             | 2           | Not initialized.                                                                                                                                                                     |
| 0x615             | 3           | Max sessions                                                                                                                                                                         |
| 0xC15             | 6           | Invalid name (all zeroes)                                                                                                                                                            |
| 0x1015            | 8           | Permission denied                                                                                                                                                                    |
| 0x416             | 2           | Address space is full                                                                                                                                                                |
| 0x616             | 3           | NRO already loaded                                                                                                                                                                   |
| 0x816             | 4           | Invalid NRO header values                                                                                                                                                            |
| 0xC16             | 6           | Bad NRR magic                                                                                                                                                                        |
| 0x1016            | 8           | Reached max NRR count                                                                                                                                                                |
| 0x1216            | 9           | Unable to verify NRO hash or NRR signature                                                                                                                                           |
| 0x80216           | 1025        | Address not page-aligned                                                                                                                                                             |
| 0x80416           | 1026        | Incorrect NRO size                                                                                                                                                                   |
| 0x80816           | 1028        | NRO not loaded                                                                                                                                                                       |
| 0x80A16           | 1029        | NRR not loaded                                                                                                                                                                       |
| 0x80C16           | 1030        | Already initialized                                                                                                                                                                  |
| 0x80E16           | 1031        | Not initialized                                                                                                                                                                      |
| 0x41A             | 2           | Argument is invalid                                                                                                                                                                  |
| 0xD01A            | 104         | All AES engines busy                                                                                                                                                                 |
| 0xD21A            | 105         | Invalid AES engine-id                                                                                                                                                                |
| 0x287C            | 20          | Argument is NULL                                                                                                                                                                     |
| 0x2C7C            | 22          | Argument is invalid                                                                                                                                                                  |
| 0x3C7C            | 30          | Bad input buffer size                                                                                                                                                                |
| 0x407C            | 32          | Invalid input buffer                                                                                                                                                                 |
| 0x3C9D            | 30          | Address is NULL                                                                                                                                                                      |
| 0x3E9D            | 31          | PID is NULL                                                                                                                                                                          |
| 0x549D            | 42          | Already bound                                                                                                                                                                        |
| 0xCC9D            | 102         | Invalid PID                                                                                                                                                                          |
| 0x3CF089          | 7800        | Unknown/invalid libcurl error.                                                                                                                                                       |
| 0x3E8289-0x3F4089 | 8001-8096   | libcurl error 1-96. Some of the libcurl errors in the error-table map to the above unknown-libcurl-error however.                                                                    |

## FS Error Codes

The following are the error codes recognized by
nn::fs::detail::LogErrorMessage found in some
[factory](Factory%20Setup.md "wikilink")
titles:

| Error Code          | Description                                               | Message                                                                                      |
| ------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 0x7802              | 60                                                        | Error: Specified mount name already exists.                                                  |
| 0xD401              | 106                                                       | Error: Passed buffer is not usable for fs library.                                           |
| 0x7D202             | 1001                                                      | Error: Specified partition is not found.                                                     |
| 0x7D402             | 1002                                                      | Error: Specified target is not found.                                                        |
| 0xFA002 - 0x138602  | 2000 - 2499                                               | Error: Failed to access SD card.                                                             |
| 0x136802 - 0x176E02 | 2500 - 2999                                               | Error: Failed to access game card.                                                           |
| 0x177202            | 3001                                                      | Error: Specified operation is not implemented.                                               |
| 0x177A02            | 3005                                                      | Error: Specified value is out of range.                                                      |
| 0x1B5802 - 0x1F3E02 | 3500 - 3999                                               | Error: Failed to access MMC.                                                                 |
| 0x1F4202 - 0x219602 | 4001 - 4299                                               | Error: ROM is corrupted.                                                                     |
| 0x219A02 - 0x232602 | 4301 - 4499                                               | Error: Save data is corrupted.                                                               |
| 0x232A02 - 0x23EE02 | 4501 - 4599                                               | Error: NCA is corrupted.                                                                     |
| 0x23F202 - 0x243E02 | 4601 - 4639                                               | Error: Integrity verification failed.                                                        |
| 0x244202 - 0x246602 | 4641 - 4659                                               | Error: Partition FS is corrupted.                                                            |
| 0x246A02 - 0x248E02 | 4661 - 4679                                               | Error: Built-in-storage is corrupted.                                                        |
| 0x249202 - 0x24B602 | 4681 - 4699                                               | Error: FAT FS is corrupted.                                                                  |
| 0x24BA02 - 0x24DE02 | 4701 - 4719                                               | Error: HOST FS is corrupted.                                                                 |
| 0x1F4002 - 0x270E02 | 4000, 4300, 4500, 4600, 4640, 4660, 4680, 4700, 4720-4999 | Error: Data is corrupted.                                                                    |
| 0x271002 - 0x2EDE02 | 5000-5999                                                 | Error: Unexpected failure occurred.                                                          |
| 0x2EE402 - 0x2F1A02 | 6002-6029                                                 | Error: Invalid path was specified.                                                           |
| 0x2F5A02            | 6061                                                      | Error: Invalid offset was specified.                                                         |
| 0x2F5C02            | 6062                                                      | Error: Invalid size was specified.                                                           |
| 0x2F5E02            | 6063                                                      | Error: Null pointer argument was specified.                                                  |
| 0x2EE002            | 6000                                                      | Error: Precondition violation.                                                               |
| 0x2EE202 - 0x306E02 | 6001-6199                                                 | Error: Invalid argument was specified.                                                       |
| 0x307202            | 6201                                                      | Error: OpenMode\_AllowAppend is required for implicit extension of file size by WriteFile(). |
| 0x307002 - 0x313602 | 6200, 6202 - 6299                                         | Error: Invalid operation for the open mode.                                                  |
| 0x313802 - 0x31FE02 | 6300-6399                                                 | Error: Unsupported operation.                                                                |
| 0x320002 - 0x32C602 | 6400-6499                                                 | Error: Permission denied.                                                                    |
| 0x346402            | 6706                                                      | Error: Enough journal space is not left.                                                     |
| 0x346A02            | 6709                                                      | Error: The open count of files and directories reached the limitation.                       |

# Fatal Errors

| Error     | Description                                                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2162-0002 | Can be triggered by running [svcBreak](SVC.md "wikilink"). The svcBreak params have no affect on the value of the thrown error-code.                                                               |
| 2168-0000 | Userland ARM undefined instruction exception                                                                                                                                                       |
| 2168-0001 | Userland ARM prefetch-abort due to PC set to non-executable region                                                                                                                                 |
| 2168-0002 | Userland ARM data abort. Also caused by abnormal process termination via [svcExitProcess](SVC.md "wikilink"). Note: directly jumping to nnMain()-retaddr from non-main-thread has the same result. |
| 2168-0003 | Userland PC address not aligned to 4 bytes                                                                                                                                                         |

# Support Errors

| Error | Module                     | Description | Notes               |
| ----- | -------------------------- | ----------- | ------------------- |
|       | {web-applets listed above} | 2750        | MP4 parsing failed. |

Normal error-codes displayed by the system also use the same format as
fatal-errors.
