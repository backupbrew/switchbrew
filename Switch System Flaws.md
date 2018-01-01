System Flaws are used to execute unofficial code (homebrew) on the
Nintendo Switch. This page is a list of known and public Switch System
Flaws.

# List of Switch System Flaws

## Hardware

| Summary         | Description                                                                                                                                                                                                                                                                | Fixed with hardware model/revision | Newest hardware model/revision this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by                                                                                             |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | -------------------------------------------------------- | ----------------------------- | --------------------------- | --------------------------------------------------------------------------------------------------------- |
| GMMU DMA attack | The Switch's GPU includes a separate MMU (GMMU) that is allowed to bypass the system's IOMMU (SMMU). By accessing the GPU's MMIO region and manipulating the page table entries in the GMMU, an attacker can read/write any portion of the DRAM (except memory carveouts). | None                               | HAC-001                                                  | Summer 2017                   | December 28, 2017           | [hexkyz](User:hexkyz "wikilink"), [SciresM](User:SciresM "wikilink") and [qlutoo](User:qlutoo "wikilink") |
|                 |                                                                                                                                                                                                                                                                            |                                    |                                                          |                               |                             |                                                                                                           |

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
<td><p>FUSE_DIS_PGM not written by package1</p></td>
<td><p>The switch's hardware fuse driver contains a write-once bit in a register called &quot;FUSE_DIS_PGM&quot;, which disables burning fuses until the next reboot. While Nintendo's bootloader code for waking up from sleep writes this on all firmware, the actual package1 initial bootloader forgets to write to it on cold reboot.</p>
<p>This isn't too big of a problem because another fuse is burnt on retail devices (production mode), which prevents burning *all* fuses other than ODM_RESERVED ones in hardware.</p>
<p>This was fixed in 3.0.0 by writing to the register on cold boot (although the write happens in TZ instead of package1 where it should take place, possibly to obfuscate the fact that they made this mistake).</p></td>
<td><p>Burning arbitrary ODM reserved fuses with TZ code execution, which should never be possible for non-bootloader code.</p>
<p>Warning: one could irreparably brick one's console by playing with this.</p></td>
<td><p><a href="3.0.0.md" title="wikilink">3.0.0</a></p></td>
<td><p><a href="3.0.0.md" title="wikilink">3.0.0</a></p></td>
<td><p>late summer/early fall 2017</p></td>
<td><p>December 31, 2017</p></td>
<td><p>SciresM, Motezazer</p></td>
</tr>
<tr class="odd">
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

| Summary                                    | Description                                                                                                                                                                                                                                                                 | Successful exploitation result                                                                                                            | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by                    |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | -------------------------------- |
| Syscall Infoleaks                          | Many syscalls leaked kernel pointers on sad paths (for example svcSetHeapSize and svcQueryMemory), until they landed a bunch of fixes in 2.0.0.                                                                                                                             | Nothing really.                                                                                                                           | Unfixed                      | 2.0.0                                         |                               |                             | ?                                |
| GetLastThreadInfo UAF                      | GetLastThreadInfo syscall gets last-scheduled-KThread pointer from KScheduler object. This pointer is not reference counted, and can be pointing to a freed KThread.                                                                                                        | Nothing. There is a theoretical race that might leak from a KThread from a different process, but it's impossible to trigger practically. | Unfixed                      |                                               | 15 October                    | 17 October                  | [qlutoo](User:qlutoo "wikilink") |
| Bad irq\_id check in CreateInterruptEvent  | CreateInterruptEvent syscall is designed to work only for irq\_id \>= 32. All irq\_ids \< 32 are "per-core" and reserved for kernel use (watchdog/scheduling/core communications). On 1.0.0 you could supply irq\_id \< 32 and it would write outside the SharedIrqs table. | You can register irq's in the Core3Irqs table, and thus register per-core irqs for core3, that are normally reserved for kernel. Useless. | 2.0.0                        | 2.0.0                                         | ~October                      | 17 October                  | [qlutoo](User:qlutoo "wikilink") |
| Kernel .text mapped executable in usermode | Prior to [3.0.2](3.0.2.md "wikilink") the kernel .text was [mapped](Memory%20layout.md "wikilink") in usermode as executable. This can be used for usermode ROP for bypassing ASLR, but SVCs/IPC are not usable by running kernel .text in usermode.                        | Executing kernel .text in usermode                                                                                                        | [3.0.2](3.0.2.md "wikilink") | [3.0.2](3.0.2.md "wikilink")                  |                               | 34c3 (December 28, 2017)    | [qlutoo](User:qlutoo "wikilink") |
|                                            |                                                                                                                                                                                                                                                                             |                                                                                                                                           |                              |                                               |                               |                             |                                  |

### FIRM-package System Modules

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
<td><p>Service access control bypass (sm:h, smhax, probably other names)</p></td>
<td><p>Prior to <a href="3.0.1.md" title="wikilink">3.0.1</a>, the <em>service manager</em> (sm) built-in system module treats a user as though it has full permissions if the user creates a new &quot;sm:&quot; port session but bypasses <a href="Services API#Initialize.md##Initialize" title="wikilink">initialization</a>. This is due to the other sm commands skipping the service ACL check for Pids &lt;= 7 (i.e. all kernel bundled modules) and that skipping the initialization command leaves the Pid field uninitialized. In <a href="3.0.1.md" title="wikilink">3.0.1</a>, sm returns error code 0x415 if <a href="Services API#Initialize.md##Initialize" title="wikilink">Initialize</a> has not been called yet.</p></td>
<td><p>Acquiring, registering, and unregistering arbitrary services</p></td>
<td><p><a href="3.0.1.md" title="wikilink">3.0.1</a></p></td>
<td><p><a href="3.0.1.md" title="wikilink">3.0.1</a></p></td>
<td><p>May 2017</p></td>
<td><p>August 17, 2017</p></td>
<td><p>Everyone</p></td>
</tr>
<tr class="even">
<td><p>Overly permissive SPL service</p></td>
<td><p>The concept behind the switch's <a href="SMC.md" title="wikilink">Secure Monitor</a> is that all cryptographic keydata is located in userspace, but stored as &quot;access keys&quot; encrypted with &quot;keks&quot; that never leave TrustZone. The <a href="SPL services.md" title="wikilink">spl</a> (&quot;security processor liaison&quot;?) service serves as an interface between the rest of the system and the secure monitor. Prior to <a href="4.0.0.md" title="wikilink">4.0.0</a>, spl exposed only a single service &quot;spl:&quot;, which provided all TrustZone wrapper functions to all sysmodules with access to it. Thus anyone with access to the spl: service (via smhax or by pwning a sysmodule with access) could do crypto with any access keys they knew.</p>
<p>This was fixed in <a href="4.0.0.md" title="wikilink">4.0.0</a> by splitting spl: into spl:, spl:mig, spl:ssl, spl:es, and spl:fs.</p></td>
<td><p>Arbitrary spl: crypto with any access keys one knows. For example, one could use the SSL module's access keys to decrypt their console's SSL certificate private key without having to pwn the SSL sysmodule.</p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p>Summer 2017 (after smhax was discovered).</p></td>
<td><p>December 23, 2017</p></td>
<td><p>Everyone</p></td>
</tr>
<tr class="odd">
<td><p>Single session services not really single session</p></td>
<td><p>Several &quot;critical&quot; services (like fsp-ldr, fsp-pr, sm:m, etc) are meant to only ever hold a single session with a specific sysmodule. However, when a sysmodule dies, all its service session handles are released -- and thus killing the holder of a single session handle would allow one (via sm:hax etc) to get access to that service.</p>
<p>This was fixed in <a href="4.0.0.md" title="wikilink">4.0.0</a> by adding a semaphore to these critical single-session services, so that even if one gets access to them an error code will be returned when attempting to use any of their commands.</p></td>
<td><p>With some way to access these services and kill their session holders: dumping sysmodule code, arbitrary service access, elevated filesystem permissions, etc.</p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p>May/June 2017 (basically immediately after smhax was discovered)</p></td>
<td><p>December 30, 2017</p></td>
<td><p>Everyone</p></td>
</tr>
</tbody>
</table>

### System Modules

| Summary                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                   | Successful exploitation result                          | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe                      | Discovered by                                                                                            |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- | ---------------------------- | --------------------------------------------- | ----------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| Out-of-bounds array read for [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index | The [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index is not validated at all. This is handled before the RSA-signature(?) is ever used. Since the field is an u8, a total of 0x800-bytes relative to the array start can be accessed. This is not useful since the string loaded from this array is only involved with key-generation.                                                  |                                                         | Unknown                      | [2.0.0](2.0.0.md "wikilink")                  | August 4, 2017                | August 6, 2017                                   | [Shiny Quagsire](User:_shinyquagsire23 "wikilink"), [Yellows8](User:Yellows8 "wikilink") (independently) |
| OOB Read in NS system module (pl:utoohax, pl:utonium, maybe other names)                                            | Prior to [3.0.0](3.0.0.md "wikilink"), pl:u (Shared Font services implemented in the NS sysmodule) service commands 1,2,3 took in a signed 32-bit index and returned that index of an array but did not check that index at all. This allowed for an arbitrary read within a 34-bit range (33-bit signed) from NS .bss. In [3.0.0](3.0.0.md "wikilink"), sending out of range indexes causes error code 0x60A to be returned. | Dumping full NS .text, .rodata and .data, infoleak, etc | [3.0.0](3.0.0.md "wikilink") | [3.0.0](3.0.0.md "wikilink")                  | April 2017                    | On exploit's fix in [3.0.0](3.0.0.md "wikilink") | [qlutoo](User:qlutoo "wikilink"), Reswitched team (independently)                                        |
| Unchecked domain ID in common IPC code                                                                              | Prior to [2.0.0](2.0.0.md "wikilink"), object IDs in [domain messages](IPC%20Marshalling#Domain%20message.md##Domain_message "wikilink") are not bounds checked. This out-of-bounds read could be exploited to brute-force ASLR and get PC control in some services that support domain messages.                                                                                                                             |                                                         | 2.0.0                        | 2.0.0                                         | ~July 2017                    | 20 July 2017‎                                    | [hthh](User:hthh "wikilink")                                                                             |
