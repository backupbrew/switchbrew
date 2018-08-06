Exploits are used to execute unofficial code (homebrew) on the Nintendo
Switch. This page is a list of publicly known Switch system flaws.

For userland applications/applets flaws see
[here](Switch%20Userland%20Flaws.md "wikilink").

# System flaws

## Hardware

Flaws in this category pertain to the underlying hardware that powers
the Switch.

This includes components shared across Tegra based devices such as the
[TSEC](TSEC.md "wikilink"), the [Security
Engine](Security%20Engine.md "wikilink"), the [GPU](GPU.md "wikilink")
and so on.

<table>
<thead>
<tr class="header">
<th><p>Summary</p></th>
<th><p>Description</p></th>
<th><p>Fixed with hardware model/revision</p></th>
<th><p>Newest hardware model/revision this flaw was checked for</p></th>
<th><p>Timeframe this was discovered</p></th>
<th><p>Public disclosure timeframe</p></th>
<th><p>Discovered by</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CVE-2018-6242 (leveraged by the ShofEL2 and Fusée Gelée exploits)</p></td>
<td><p>The USB software stack provided inside the boot instruction rom (IROM/bootROM) contains a copy operation whose length can be controlled by an attacker. By carefully constructing a USB control request, an attacker can leverage this vulnerability to copy the contents of an attacker-controlled buffer over the active execution stack, gaining control of the Boot and Power Management processor (BPMP) before any lock-outs or privilege reductions occur. This execution can then be used to exfiltrate secrets and to load arbitrary code onto the main CPU Complex (CCPLEX) &quot;application processors&quot; at the highest possible level of privilege (typically as the TrustZone Secure Monitor at PL3/EL3).</p></td>
<td><p>Unknown (Tegra186 and Tegra214)</p></td>
<td><p>HAC-001 (Tegra210)</p></td>
<td><p>January 2018</p></td>
<td><p>April 23, 2018</p></td>
<td><p><a href="User:Shuffle2" title="wikilink">shuffle2</a> and fail0verflow (originally),<br />
<a href="User:Ktemkin" title="wikilink">ktemkin</a> and ReSwitched Team (independently),<br />
<a href="User:Naehrwert" title="wikilink">naehrwert</a> (independently),<br />
<a href="User:Hexkyz" title="wikilink">hexkyz</a> (independently),<br />
st4rk with <a href="User:Shinyquagsire23" title="wikilink">Shiny Quagsire</a> and Dazzozo (independently),<br />
and many others (independently).</p></td>
</tr>
<tr class="even">
<td><p>GMMU DMA attack</p></td>
<td><p>The Switch's GPU includes a separate MMU (GMMU) that is allowed to bypass the system's IOMMU (SMMU). By accessing the GPU's MMIO region and manipulating the page table entries in the GMMU, an attacker can read/write any portion of the DRAM (except memory carveouts).</p>
<p>[5.0.0+] Works around this hardware flaw by using memory pool partitioning. You can no longer escalate into sysmodules with GPU DMA because all their memory is allocated using heap that's carved out.</p></td>
<td><p>None</p></td>
<td><p>HAC-001 (Tegra210)</p></td>
<td><p>Summer 2017</p></td>
<td><p>December 28, 2017</p></td>
<td><p><a href="User:hexkyz" title="wikilink">hexkyz</a>, <a href="User:SciresM" title="wikilink">SciresM</a> and <a href="User:qlutoo" title="wikilink">qlutoo</a></p></td>
</tr>
<tr class="odd">
<td><p>Weak Security Engine context validation</p></td>
<td><p>The Tegra X1 supports a &quot;deep sleep&quot; feature, where everything but DRAM and the PMC registers lose their content (and the SoC loses power). Upon awaking, the bootrom re-executes, restoring system state. Among these stored states is the Security Engine's saved state, which uses AES-128-CBC with a random key and all-zeroes IV. However, the bootrom doesn't perform a MAC on this data, and only validates the last block. This allows one to control most of security engine's state upon wakeup, if one has a way to modify the encrypted state buffer.</p>
<p>With a way to modify the encrypted state buffer, one can thus dump keys from &quot;write-only&quot; keyslots, etc.</p>
<p>This also bypasses the SBK protection of the bootROM: indeed, at warmboot, bootROM will always clear keyslot 0xE to prevent malicious code from saving the SBK. Moving the SBK to another keyslot in the saved context renders this protection moot.</p></td>
<td><p>None</p></td>
<td><p>HAC-001 (Tegra210)</p></td>
<td><p>December 2017</p></td>
<td><p>January 20, 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a> and <a href="User:motezazer" title="wikilink">motezazer</a></p></td>
</tr>
<tr class="even">
<td><p>Security Engine keyslots vulnerable to partial overwrite attack</p></td>
<td><p>The Tegra X1 security engine supports writing keyslot data to the engine with syntax as follows:</p>
<p>SECURITY_ENGINE-&gt;AES_KEYTABLE_ADDR = (keyslot &lt;&lt; 4) | (dword_index_in_keyslot);</p>
<p>SECURITY_ENGINE-&gt;AES_KEYTABLE_DATA = readle32(key, dword_index_in_keyslot * 4);</p>
<p>However, the Security Engine flushes writes to the internal key tables immediately when AES_KEYTABLE_DATA is written -- this allows one to overwrite a single dword of a key at a time, and thus brute force the contents of keyslots in time (2^32 * 8) = 2^35 instead of 2^256.</p></td>
<td><p>None</p></td>
<td><p>HAC-001 (Tegra210)</p></td>
<td><p>Theorized Summer 2017 due to suggestive syntax, confirmed April 9, 2018</p></td>
<td><p>April 9, 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a>, almost surely others (independently).</p></td>
</tr>
</tbody>
</table>

## Software

### Bootloader

Flaws in this category pertain to any bootloader component such as the
[package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink"), the [NX
bootloader](Package1#Section%201.md##Section_1 "wikilink") or the
[warmboot binary](Package1#Section%200.md##Section_0 "wikilink").

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
<td><p>The Switch's stage 1 bootloader, on panic(), clears the stack and then attempts to clear the Security Engine. However, it does so by dereferencing a pointer to the SE in .bss (initially NULL), and this pointer doesn't get initialized until partway into the bootloader's main() after several functions that might panic() are called. Thus, a panic() caused prior to SE initialization would result in the SE pointer still being NULL when dereferenced. The BPMP doesn't have an active MPU and the bus won't data abort on an invalid address, so no exception will be entered: it'll end up overwriting some exception vectors with NULL before halting.</p>
<p>In 3.0.0, this was fixed by moving the security engine initialization earlier in main(), before the first function that could potentially panic().</p></td>
<td><p>Some exception vectors overwritten with NULL, before SBK/other keyslots are cleared. Probably useless for anything more interesting.</p></td>
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
<td><p>Late summer/early fall 2017</p></td>
<td><p>December 31, 2017</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a>, <a href="User:motezazer" title="wikilink">motezazer</a></p></td>
</tr>
<tr class="odd">
<td><p>TSEC firmware compromises itself</p></td>
<td><p>Package1ldr loads a firmware blob into TSEC early on boot. This piece of code runs on the TSEC in Authenticated Mode and has the sole purpose of generating the per-console TSEC key (see <a href="Cryptosystem.md" title="wikilink">Cryptosystem</a>).</p>
<p>As a way to mitigate attacks, the TSEC firmware blob is split into 3 stages: <a href="TSEC#Stage 0.md##Stage_0" title="wikilink">Stage 0</a> which is unencrypted and unsigned, <a href="TSEC#Stage 1.md##Stage_1" title="wikilink">Stage 1</a> which is unencrypted but signed and <a href="TSEC#Stage 2.md##Stage_2" title="wikilink">Stage 2</a> which is encrypted and signed. Stage 0 loads a static pre-generated signature into the Falcon's CPU crypto registers, loads Stage 1 into the Falcon's CODE region and jumps to it. Execution will proceed into Stage 1 in Authenticated Mode if, and only if, the loaded signature matches the one Falcon calculates internally for Stage 1.</p>
<p>Among various things, Stage 1 will attempt to do a &quot;backwards&quot; security check by calculating a CMAC over Stage 0 and comparing it with a known hash stored in the TSEC firmware's key data (a small buffer stored after Stage 0's code). If the hashes don't match, execution aborts.</p>
<p>Stage 1 stores the calculated Stage 0's CMAC in the stack, but forgets to clear it. Since the stack is located in Falcon's DATA region, loading the TSEC firmware blob and dumping the DATA region afterwards (via MMIO) will reveal the calculated hash. This allows using Stage 1 as an oracle to generate a valid CMAC for arbitrary Stage 0 code. Replacing the CMAC in the TSEC firmware's key data region results in Stage 1 accepting any Stage 0 code, thus rendering this security measure useless.</p>
<p>Additionally, since signed Falcon code can't be revoked without an hardware revision, an attacker can always reuse the flawed Stage 1 code even if a fix is issued.</p></td>
<td><p>Running TSEC firmware's Stage 1 in a user controlled environment. Mostly useless, but may aid in side-channel attacks.</p></td>
<td><p>None</p></td>
<td><p><a href="5.0.2.md" title="wikilink">5.0.2</a></p></td>
<td><p>January 2018</p></td>
<td><p>April 29, 2018</p></td>
<td><p><a href="User:Hexkyz" title="wikilink">hexkyz</a></p></td>
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

Flaws in this category pertain exclusively to the [Secure
Monitor](Package1#Section%202.md##Section_2 "wikilink").

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
<td><p>Non-atomic mutexes</p></td>
<td><p>When an <a href="SMC.md" title="wikilink">SMC</a> is called, TrustZone sets a global variable to mark that an SMC is in progress, so that two SMCs using shared resources (like the security engine) do not trample on one another. On 1.0.0, this global variable was written using non-atomic writes, and thus a race condition is possible.</p>
<p>However, the SMC handler enforces that all SMCs must be called from core #3, unless the top-level handler ID is 1 (SMCs internal to the kernel). Thus, the only SMCs that can be run side-by-side are [any userland smc] and smcGetRandomBytesForKernel, and this turns out to not really be abusable.</p></td>
<td><p>Mostly useless. Maybe some oob-write into unused (and thus useless) memory if running smcGetRandomBytesForKernel and smcGetRandomBytesForUser at the same time.</p></td>
<td><p><a href="2.0.0.md" title="wikilink">2.0.0</a></p></td>
<td><p><a href="2.0.0.md" title="wikilink">2.0.0</a></p></td>
<td><p>December 2017 (Probably earlier by others)</p></td>
<td><p>January 18, 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a>, probably others.</p></td>
</tr>
<tr class="even">
<td><p>jamais vu (non-secure world access to PMC MMIO and pre-deep sleep firmware)</p></td>
<td><p>On <a href="1.0.0.md" title="wikilink">1.0.0</a>, one could map in the PMC registers in userland. In addition, <a href="AM services.md" title="wikilink">am</a> ran a little-kernel based firmware on the BPMP at runtime. With code execution under am, one could modify the BPMP's little-kernel firmware to hook deep sleep entry, and modify TrustZone/Security engine state.</p>
<p>This was fixed in <a href="2.0.0.md" title="wikilink">2.0.0</a> by making the PMC secure-world only, blacklisting the BPMP's exception vectors from being mapped, and thoroughly checking for malicious behavior on deep sleep entry.</p></td>
<td><p>Arbitrary TrustZone code execution.</p></td>
<td><p><a href="2.0.0.md" title="wikilink">2.0.0</a></p></td>
<td><p><a href="2.0.0.md" title="wikilink">2.0.0</a></p></td>
<td><p>December, 2017</p></td>
<td><p>January 20, 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a> and <a href="User:motezazer" title="wikilink">motezazer</a></p></td>
</tr>
<tr class="odd">
<td><p>Missed BPMP Exception Vector Writes</p></td>
<td><p>Starting in <a href="2.0.0.md" title="wikilink">2.0.0</a>, the BPMP is asleep at runtime, and is turned on by TrustZone during <a href="SMC.md" title="wikilink">smcCpuSuspend</a> in order to initiate the deep sleep process. When it does so, it is held in RESET, and TrustZone attempts to write to the BPMP exception vectors at 0x6000F200 to register EVP_RESET = lp0_entry_fw_crt0, and all other EVPs to a function that simply reboots. However, while they successfully write EVP_RESET, they miss all the other vectors, accidentally writing to the 0x6000F004-0x6000F020 region instead of the 0x6000F204-0x6000F220 region they want to write to. This results in all the exception vectors for the BPMP other than RESET being &quot;undefined&quot; (attacker controlled).</p>
<p>With some way of causing an exception vector to be taken at the right time, this would give pre-sleep code execution (and thus arbitrary TrustZone code execution, via the security engine flaw). However, none of the abort vectors are really triggerable, and interrupts are disabled for the BPMP when it is taken out of reset. Thus, this is useless in practice.</p>
<p>This was fixed in <a href="4.0.0.md" title="wikilink">4.0.0</a> by writing to the correct registers.</p></td>
<td><p>Theoretically: Arbitrary TrustZone code execution. In practice: Useless.</p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p>January, 2018</p></td>
<td><p>February 23, 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a> and <a href="User:motezazer" title="wikilink">motezazer</a>, <a href="User:Naehrwert" title="wikilink">naehrwert</a>, <a href="User:Hexkyz" title="wikilink">hexkyz</a>, probably others, independently.</p></td>
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

### Kernel

Flaws in this category pertain exclusively to the [HorizonOS
Kernel](Package2#Section%200.md##Section_0 "wikilink").

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
<td><p>Syscall Infoleaks</p></td>
<td><p>Many syscalls leaked kernel pointers on sad paths (for example svcSetHeapSize and svcQueryMemory), until they landed a bunch of fixes in 2.0.0.</p></td>
<td><p>Nothing really.</p></td>
<td><p>2.0.0</p></td>
<td><p>2.0.0</p></td>
<td></td>
<td></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p>svcWaitSynchronization/svcReplyAndReceive bad cleanup on error</p></td>
<td><p>If there is a page fault when fetching handles from the userspace array, it cleans up by dereferencing all objects despite having only loaded first N. Allows the attacker to make arbitrary decrefs on any kernel synchronization object, and thus can be used to get UAF. Haven't actually been tried on real HW though, but should work (tm).</p></td>
<td><p>Kernel code execution</p></td>
<td><p>2.0.0</p></td>
<td><p>2.0.0</p></td>
<td></td>
<td><p>24 April</p></td>
<td><p><a href="User:qlutoo" title="wikilink">qlutoo</a></p></td>
</tr>
<tr class="odd">
<td><p>Bad irq_id check in CreateInterruptEvent</p></td>
<td><p>CreateInterruptEvent syscall is designed to work only for irq_id &gt;= 32. All irq_ids &lt; 32 are &quot;per-core&quot; and reserved for kernel use (watchdog/scheduling/core communications). On 1.0.0 you could supply irq_id &lt; 32 and it would write outside the SharedIrqs table.</p></td>
<td><p>You can register irq's in the Core3Irqs table, and thus register per-core irqs for core3, that are normally reserved for kernel. Useless.</p></td>
<td><p>2.0.0</p></td>
<td><p>2.0.0</p></td>
<td><p>~October</p></td>
<td><p>17 October</p></td>
<td><p><a href="User:qlutoo" title="wikilink">qlutoo</a></p></td>
</tr>
<tr class="even">
<td><p>Kernel .text mapped executable in usermode</p></td>
<td><p>Prior to <a href="3.0.2.md" title="wikilink">3.0.2</a> the kernel .text was <a href="Memory layout.md" title="wikilink">mapped</a> in usermode as executable. This can be used for usermode ROP for bypassing ASLR, but SVCs/IPC are not usable by running kernel .text in usermode.</p></td>
<td><p>Executing kernel .text in usermode</p></td>
<td><p><a href="3.0.2.md" title="wikilink">3.0.2</a></p></td>
<td><p><a href="3.0.2.md" title="wikilink">3.0.2</a></p></td>
<td></td>
<td><p>34c3 (December 28, 2017)</p></td>
<td><p><a href="User:qlutoo" title="wikilink">qlutoo</a></p></td>
</tr>
<tr class="odd">
<td><p>Memory Controller not properly secured</p></td>
<td><p>The Switch OS originally had the memory controller not set to be accessible only by the secure-world, which was problematic because insecure access can compromise the kernel.</p>
<p>This was fixed partially in <a href="2.0.0.md" title="wikilink">2.0.0</a> by blacklisting the memory controller from being mapped by user-processes, and was fixed entirely in <a href="4.0.0.md" title="wikilink">4.0.0</a> by making the memory controller TZ-only and making all kernel accesses go through <a href="SMC.md" title="wikilink">smcReadWriteRegister</a>.</p></td>
<td><p>With some way to access the memory controller MMIO, arbitrary kernel code execution.</p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p>January 2018</p></td>
<td><p>January 2018</p></td>
<td><p><a href="User:SciresM" title="wikilink">SciresM</a>, <a href="User:Yellows8" title="wikilink">yellows8</a></p></td>
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

### FIRM-package System Modules

Flaws in this category pertain to any of the [built-in system
modules](Package2#Section%201.md##Section_1 "wikilink").

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
<td><p>With some way to access these services and kill their session holders (like expLDR): dumping sysmodule code, arbitrary service access, elevated filesystem permissions, etc.</p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p><a href="4.0.0.md" title="wikilink">4.0.0</a></p></td>
<td><p>May/June 2017 (basically immediately after smhax was discovered)</p></td>
<td><p>December 30, 2017</p></td>
<td><p>Everyone</p></td>
</tr>
<tr class="even">
<td><p>nspwn</p></td>
<td><p>fsp-ldr command 0 &quot;MountCode&quot; takes in a Content Path (retrieved from NCM by Loader), and returns an IFileSystem for the resulting ExeFS. These content paths, are normally NCAs, but MountCode also supports a number of other formats, including &quot;.nsp&quot; -- which is just a PFS0.</p>
<p>When a path ending in &quot;.nsp&quot; is parsed by MountCode, the PFS0 is treated as a raw ExeFS. Because there is no NCA header, the ACID signatures are not validated -- and because there are no other signatures in a PFS0, this results in no signature checking happening at all.</p>
<p>The actual .nsp handling is eventually done by {content mounting function} called by MountCode and other FS commands.</p>
<p>Thus, by placing an ExeFS (NSOs + &quot;main.npdm&quot;) and setting one's desired title ID to &quot;@Sdcard:/some_title.nsp&quot; or &quot;@User:/some_title.nsp&quot; etc one can launch arbitrary unsigned code, with arbitrary unsigned NPDMs.</p>
<p>This appears to have been fixed by only allowing .nsp when the input fstype==7 for the internal content-mounting function, returning 0x2EE202 otherwise.</p></td>
<td><p>With access to &quot;lr&quot;: Arbitrary code execution with full system privileges.</p></td>
<td><p><a href="5.0.0.md" title="wikilink">5.0.0</a></p></td>
<td><p><a href="5.0.0.md" title="wikilink">5.0.0</a></p></td>
<td><p>Late 2017</p></td>
<td><p>April 23, 2018</p></td>
<td><p>Everyone</p></td>
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

### System Modules

Flaws in this category pertain to any non-built-in system
module.

| Summary                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Successful exploitation result                                                                                                                                                                                                 | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe                      | Discovered by                                                                                            |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | --------------------------------------------- | ----------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| Out-of-bounds array read for [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index | The [BCAT\_Content\_Container](BCAT%20Content%20Container.md "wikilink") secret-data index is not validated at all. This is handled before the RSA-signature(?) is ever used. Since the field is an u8, a total of 0x800-bytes relative to the array start can be accessed. This is not useful since the string loaded from this array is only involved with key-generation.                                                                                                                              |                                                                                                                                                                                                                                | Unknown                      | [2.0.0](2.0.0.md "wikilink")                  | August 4, 2017                | August 6, 2017                                   | [Shiny Quagsire](User:_shinyquagsire23 "wikilink"), [yellows8](User:Yellows8 "wikilink") (independently) |
| OOB Read in NS system module (pl:utoohax, pl:utonium, maybe other names)                                            | Prior to [3.0.0](3.0.0.md "wikilink"), pl:u (Shared Font services implemented in the NS sysmodule) service commands 1,2,3 took in a signed 32-bit index and returned that index of an array but did not check that index at all. This allowed for an arbitrary read within a 34-bit range (33-bit signed) from NS .bss. In [3.0.0](3.0.0.md "wikilink"), sending out of range indexes causes error code 0x60A to be returned.                                                                             | Dumping full NS .text, .rodata and .data, infoleak, etc                                                                                                                                                                        | [3.0.0](3.0.0.md "wikilink") | [3.0.0](3.0.0.md "wikilink")                  | April 2017                    | On exploit's fix in [3.0.0](3.0.0.md "wikilink") | [qlutoo](User:qlutoo "wikilink"), ReSwitched Team (independently)                                        |
| Unchecked domain ID in common IPC code                                                                              | Prior to [2.0.0](2.0.0.md "wikilink"), object IDs in [domain messages](IPC%20Marshalling#Domain%20message.md##Domain_message "wikilink") are not bounds checked. This out-of-bounds read could be exploited to brute-force ASLR and get PC control in some services that support domain messages.                                                                                                                                                                                                         |                                                                                                                                                                                                                                | 2.0.0                        | 2.0.0                                         | ~July 2017                    | 20 July 2017‎                                    | [hthh](User:hthh "wikilink")                                                                             |
| expLDR (sysmodule handle table exhaustion)                                                                          | Most sysmodules share common template code to handle IPC control messages. The command DuplicateSession (type 5 command 2)'s template code will abort() if it fails to duplicate a session's handle for the requester. Because many sysmodules have limited handle table size (smaller than the browser/other entrypoints), repeatedly requesting to duplicate one's session will cause the sysmodule to run out of handle table space and abort, causing the service to release all its handles cleanly. | Sysmodule crashes. Most usefully, crashing ldr allows access to fsp-ldr and crashing pm allows access to fsp-pr. Useless after [4.0.0](4.0.0.md "wikilink"), which mitigated a number of single-session service access issues. | Unfixed                      | 4.1.0                                         | 24 June 2017                  | 8 March 2018                                     | [daeken](User:daeken "wikilink")                                                                         |
