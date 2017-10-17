System Flaws are used to execute unofficial code (homebrew) on the
Nintendo Switch. This page is a list of known and public Switch System
Flaws.

# List of Switch System Flaws

## Hardware

| Summary                     | Description | Fixed with hardware model/revision | Newest hardware model/revision this flaw was checked for | Timeframe this was discovered | Discovered by |
| --------------------------- | ----------- | ---------------------------------- | -------------------------------------------------------- | ----------------------------- | ------------- |
| No public hardware exploits |             |                                    |                                                          |                               |               |
|                             |             |                                    |                                                          |                               |               |

## System software

### Stage 1 Bootloader

<table>
<thead>
<tr class="header">
<th><p>Summary</p></th>
<th><p>Description</p></th>
<th><p>Successful exploitation result</p></th>
<th><p>Fixed in system version</p></th>
<th><p>Last system version this flaw was checked for</p></th>
<th><p>Timeframe this was discovered</p></th>
<th><p>Public disclosure timeframe</p></th>
<th><p>Discovered by</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Null-dereference in panic()</p></td>
<td><p>The Switch's stage 1 bootloader, on panic(), clears the stack and then attempts to clear the Security Engine. However, it does so by dereferencing a pointer to the SE in .bss (initially NULL), and this pointer doesn't get initialized until partway into the bootloader's main() after several functions that might panic() are called. Thus, a panic() caused prior to SE initialization would result in the SE pointer still being NULL when dereferenced. This would cause a data abort, causing the bootloader to clear the stack and then try to clear the security engine...dereferencing NULL again, over and over in a loop.</p>
<p>In 3.0.0, this was fixed by moving the security engine initialization earlier in main(), before the first function that could potentially panic().</p></td>
<td><p>Infinite clear-the-stack-then-data-abort loop very early in boot, before SBK/other keyslots are cleared. Probably useless for anything more interesting.</p></td>
<td><p><a href="3.0.0.md" title="wikilink">3.0.0</a></p></td>
<td><p><a href="3.0.0.md" title="wikilink">3.0.0</a></p></td>
<td><p>Early July, 2017</p></td>
<td><p>July 30, 2017</p></td>
<td><p>Everyone who diff'd 2.3.0 and 3.0.0 Package1</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### TrustZone

| Summary                          | Description | Successful exploitation result | Fixed in system version | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by |
| -------------------------------- | ----------- | ------------------------------ | ----------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | ------------- |
| No public ARM TrustZone exploits |             |                                |                         |                                               |                               |                             |               |
|                                  |             |                                |                         |                                               |                               |                             |               |

### Kernel

| Summary                                   | Description                                                                                                                                                                                                                                                                 | Successful exploitation result                                                                                                            | Fixed in system version | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | ------------- |
| GetLastThreadInfo UAF                     | GetLastThreadInfo syscall gets last-scheduled-KThread pointer from KScheduler object. This pointer is not reference counted, and can be pointing to a freed KThread.                                                                                                        | Nothing. There is a theoretical race that might leak from a KThread from a different process, but it's impossible to trigger practically. | Unfixed                 |                                               | 15 October                    | 17 October                  | plutoo        |
| Bad irq\_id check in CreateInterruptEvent | CreateInterruptEvent syscall is designed to work only for irq\_id \>= 32. All irq\_ids \< 32 are "per-core" and reserved for kernel use (watchdog/scheduling/core communications). On 1.0.0 you could supply irq\_id \< 32 and it would write outside the SharedIrqs table. | You can register irq's in the Core3Irqs table, and thus register per-core irqs for core3, that are normally reserved for kernel. Useless. | 2.0.0                   | 2.0.0                                         | ~October                      | 17 October                  | plutoo        |
|                                           |                                                                                                                                                                                                                                                                             |                                                                                                                                           |                         |                                               |                               |                             |               |

### FIRM-package System Modules

| Summary                                                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Successful exploitation result                               | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | ------------- |
| Service access control bypass (sm:h, smhax, probably other names) | Prior to [3.0.1](3.0.1.md "wikilink"), the *service manager* (sm) built-in system module treats a user as though it has full permissions if the user creates a new "sm:" port session but bypasses [initialization](Services%20API#Initialize.md##Initialize "wikilink"). This is due to the other sm commands skipping the service ACL check for Pids \<= 7 (i.e. all kernel bundled modules) and that skipping the initialization command leaves the Pid field uninitialized. In [3.0.1](3.0.1.md "wikilink"), sm returns error code 0x415 if [Initialize](Services%20API#Initialize.md##Initialize "wikilink") has not been called yet. | Acquiring, registering, and unregistering arbitrary services | [3.0.1](3.0.1.md "wikilink") | [3.0.1](3.0.1.md "wikilink")                  | May 2017                      | August 17, 2017             | Everyone      |

### System Modules

| Summary                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                   | Successful exploitation result                          | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe                      | Discovered by                                                                                            |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- | ---------------------------- | --------------------------------------------- | ----------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| Out-of-bounds array read for [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index | The [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index is not validated at all. This is handled before the RSA-signature(?) is ever used. Since the field is an u8, a total of 0x800-bytes relative to the array start can be accessed. This is not useful since the string loaded from this array is only involved with key-generation.                                                  |                                                         | Unknown                      | [2.0.0](2.0.0.md "wikilink")                  | August 4, 2017                | August 6, 2017                                   | [Shiny Quagsire](User:_shinyquagsire23 "wikilink"), [Yellows8](User:Yellows8 "wikilink") (independently) |
| OOB Read in NS system module (pl:utoohax, pl:utonium, maybe other names)                                            | Prior to [3.0.0](3.0.0.md "wikilink"), pl:u (Shared Font services implemented in the NS sysmodule) service commands 1,2,3 took in a signed 32-bit index and returned that index of an array but did not check that index at all. This allowed for an arbitrary read within a 34-bit range (33-bit signed) from NS .bss. In [3.0.0](3.0.0.md "wikilink"), sending out of range indexes causes error code 0x60A to be returned. | Dumping full NS .text, .rodata and .data, infoleak, etc | [3.0.0](3.0.0.md "wikilink") | [3.0.0](3.0.0.md "wikilink")                  | April 2017                    | On exploit's fix in [3.0.0](3.0.0.md "wikilink") | qlutoo, Reswitched team (independently)                                                                  |
| Unchecked domain ID in common IPC code                                                                              | Prior to [2.0.0](2.0.0.md "wikilink"), object IDs in [domain messages](IPC%20Marshalling#Domain%20message.md##Domain_message "wikilink") are not bounds checked. This out-of-bounds read could be exploited to brute-force ASLR and get PC control in some services that support domain messages.                                                                                                                             |                                                         | 2.0.0                        | 2.0.0                                         | ~July 2017                    | 20 July 2017‎                                    | hthh                                                                                                     |
