Like most Tegra based devices, the Switch's GPU also includes a Falcon
microprocessor. TSEC is a NVIDIA Falcon microprocessor with crypto
extensions.

# Driver

A host driver for communicating with the TSEC/Falcon is mapped to
physical address 0x54500000 with a total size of 0x40000 bytes and
exposes several
registers.

## Registers

| Name                                                    | Address    | Width |
| ------------------------------------------------------- | ---------- | ----- |
| [FALCON\_IRQMSET](#FALCON_IRQMSET "wikilink")           | 0x54501010 | 0x04  |
| [FALCON\_IRQDEST](#FALCON_IRQDEST "wikilink")           | 0x5450101C | 0x04  |
| [FALCON\_SCRATCH0](#FALCON_SCRATCH0 "wikilink")         | 0x54501040 | 0x04  |
| [FALCON\_SCRATCH1](#FALCON_SCRATCH1 "wikilink")         | 0x54501044 | 0x04  |
| [FALCON\_ITFEN](#FALCON_ITFEN "wikilink")               | 0x54501048 | 0x04  |
| [FALCON\_CPUCTL](#FALCON_CPUCTL "wikilink")             | 0x54501100 | 0x04  |
| [FALCON\_BOOTVEC](#FALCON_BOOTVEC "wikilink")           | 0x54501104 | 0x04  |
| [FALCON\_DMACTL](#FALCON_DMACTL "wikilink")             | 0x5450110C | 0x04  |
| [FALCON\_DMATRFBASE](#FALCON_DMATRFBASE "wikilink")     | 0x54501110 | 0x04  |
| [FALCON\_DMATRFMOFFS](#FALCON_DMATRFMOFFS "wikilink")   | 0x54501114 | 0x04  |
| [FALCON\_DMATRFCMD](#FALCON_DMATRFCMD "wikilink")       | 0x54501118 | 0x04  |
| [FALCON\_DMATRFFBOFFS](#FALCON_DMATRFFBOFFS "wikilink") | 0x5450111C | 0x04  |
|                                                         |            |       |

### FALCON\_IRQMSET

Used for configuring Falcon's IRQs.

### FALCON\_IRQDEST

Used for configuring Falcon's IRQs.

### FALCON\_SCRATCH0

MMIO register for reading/writing data to Falcon.

### FALCON\_SCRATCH1

MMIO register for reading/writing data to Falcon.

### FALCON\_ITFEN

| Bits | Description           |
| ---- | --------------------- |
| 0    | FALCON\_ITFEN\_CTXEN  |
| 1    | FALCON\_ITFEN\_MTHDEN |
|      |                       |

Used for enabling/disabling Falcon interfaces.

### FALCON\_CPUCTL

| Bits | Description              |
| ---- | ------------------------ |
| 0    | FALCON\_CPUCTL\_STARTCPU |
|      |                          |

Used for signaling Falcon's CPU.

### FALCON\_BOOTVEC

Takes the Falcon's boot vector address.

### FALCON\_DMACTL

| Bits | Description                     |
| ---- | ------------------------------- |
| 1    | FALCON\_DMACTL\_DMEM\_SCRUBBING |
| 2    | FALCON\_DMACTL\_IMEM\_SCRUBBING |
|      |                                 |

Used for configuring the Falcon's DMA engine.

### FALCON\_DMATRFBASE

Takes the host's base address for transferring data to/from the Falcon
(DMA).

### FALCON\_DMATRFMOFFS

Takes the offset for the host's source memory being transferred.

### FALCON\_DMATRFCMD

| Bits | Description                                                 |
| ---- | ----------------------------------------------------------- |
| 1    | FALCON\_DMATRFCMD\_IDLE (this is set if the engine is idle) |
| 4    | FALCON\_DMATRFCMD\_IMEM                                     |
| 9-10 | FALCON\_DMATRFCMD\_SIZE\_256B                               |
|      |                                                             |

Used for configuring DMA transfers.

### FALCON\_DMATRFFBOFFS

Takes the offset for Falcon's target memory being transferred.

# Boot Process

The Falcon is configured and initialized by the first bootloader during
key generation (sub\_400114FC).

## Initialization

During this stage several clocks are programmed.

`// Program the HOST1X clock and resets`  
`set_host1x_clkrst();`  
  
`// Program the TSEC clock and resets`  
`set_tsec_clkrst();`  
  
`// Program the QSPI clock and resets (no source)`  
`set_qspi_clkrst();`  
  
`// Program the SOR1 clock and resets (no source)`  
`set_sor1_clkrst0();`  
  
`// Program the SOR1 clock and resets`  
`set_sor1_clkrst1();`  
  
`// Enable clock and resets for H group`  
`set_h_clkrst();`

## Configuration

In this stage the Falcon IRQs, interfaces and DMA engine are configured.

`// Clear the Falcon DMA control register`  
`*(u32 *)FALCON_DMACTL = 0;`  
  
`// Enable Falcon IRQs`  
`*(u32 *)FALCON_IRQMSET = 0xFFF2;`  
  
`// Enable Falcon IRQs`  
`*(u32 *)FALCON_IRQDEST = 0xFFF0;`  
  
`// Enable Falcon interfaces`  
`*(u32 *)FALCON_ITFEN = 0x03;`  
  
`// Wait for Falcon's DMA engine to be idle`  
`wait_flcn_dma_idle();`

## Firmware loading

The Falcon firmware code is stored in the first bootloader's data
segment in IMEM.

`// Set DMA transfer base address to 0x40011900 >> 0x08`  
`*(u32 *)FALCON_DMATRFBASE = 0x400119;`  
  
`u32 trf_mode = 0;     // A value of 0 sets FALCON_DMATRFCMD_IMEM`  
`u32 dst_offset = 0;`  
`u32 src_offset = 0;`  
  
`// Load code into Falcon (0x100 bytes at a time)`  
`while (src_offset < 0xF00)`  
`{`  
`   flcn_load_firm(trf_mode, src_offset, dst_offset);`  
`   src_offset += 0x100;`  
`   dst_offset += 0x100;`  
`}`

## Firmware booting

Falcon is booted up and the first bootloader waits for it to finish.

`// Set host1x sync config`  
`*(u32 *)0x50003300 = 0x34C2E1DA;`  
  
`// Clear Falcon scratch1 MMIO`  
`*(u32 *)FALCON_SCRATCH1 = 0;`  
  
`// Set Falcon boot key version in scratch0 MMIO`  
`*(u32 *)FALCON_SCRATCH0 = 0x01;`  
  
`// Set Falcon's boot vector address`  
`*(u32 *)FALCON_BOOTVEC = 0;`  
  
`// Signal Falcon's CPU`  
`*(u32 *)FALCON_CPUCTL = 0x02;`  
  
`// Wait for Falcon's DMA engine to be idle`  
`wait_flcn_dma_idle();`  
  
`u32 boot_res = 0;`  
`u32 time = 0;`  
  
`while (!boot_res)`  
`{`  
`   // Read boot result from scratch1 MMIO`  
`   boot_res = *(u32 *)FALCON_SCRATCH1;`  
`   `  
`   // Read from RTC_MILLISECONDS`  
`   time = rtc_read();`  
`   `  
`   // Booting is taking too long`  
`   if (time > 2000000)`  
`      panic();`  
`}`  
  
`// Invalid boot result was returned`  
`if (boot_res != 0xB0B0B0B0)`  
`   panic();`

## Keygen

In this final stage the Falcon device key is generated by reading SOR
registers modified by Falcon.

`// Clear host1x sync config`  
`*(u32 *)0x50003300 = 0;`  
  
`// Generate Falcon device key`  
`u32 falcon_device_key[4]; `  
`falcon_device_key[0] = *(u32 *)NV_SOR_DP_HDCP_BKSV_LSB;`  
`falcon_device_key[1] = *(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB;`  
`falcon_device_key[2] = *(u32 *)NV_SOR_TMDS_HDCP_CN_MSB;`  
`falcon_device_key[3] = *(u32 *)NV_SOR_TMDS_HDCP_CN_LSB;`  
  
`// Clear SOR registers`  
`*(u32 *)NV_SOR_DP_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_MSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_LSB = 0;`  
  
`if (out_size < 0x10)`  
`   out_size = 0x10;`  
  
`// Copy back the Falcon key`  
`memcpy(out_buf, falcon_device_key, out_size);`  
  
`// Deprogram UARTC and I2C5 clock and resets`  
`unset_uartc_i2c5_clkrst();`  
  
`// Deprogram SOR1 clock and resets`  
`unset_sor1_clkrst1();`  
  
`// Deprogram SOR1 clock and resets (no source)`  
`unset_sor1_clkrst0();`  
  
`// Deprogram QSPI clock and resets (no source)`  
`unset_qspi_clkrst();`  
  
`// Deprogram TSEC clock and resets`  
`unset_tsec_clkrst();`  
  
`// Deprogram HOST1X clock and resets`  
`unset_host1x_clkrst()`  
  
`return;`

# TSEC Firmware

The actual code loaded into TSEC is assembled in NVIDIA's proprietary
fuc5 ISA using crypto extensions. Stored inside the first bootloader,
this firmware binary is split into 4 blobs: Stage0, Stage1, Stage2 and
key data.

Firmware can be disassembled with
[http:x//envytools.readthedocs.io/en/latest/](Http:x%20%20envytools.readthedocs.io%20en%20latest%20.md)"
envytools'
[https:x//github.com/envytools/envytools/tree/master/envydis](Https:x%20%20github.com%20envytools%20envytools%20tree%20master%20envydis.md)
envydis:

`envydis -i tsec_fw.bin -m falcon -V fuc5 -F crypt`

Note that the instruction set has variable length instructions, and the
disassembler is not very good at detecting locations it should start
disassembling from. One needs to disassemble multiple sub-regions and
join them together.

## Stage 0

During this stage key data is loaded and Stage 1 is authenticated,
loaded and executed. Before returning, this stage writes back to the
host (using MMIO registers) and sets the device key used by the first
bootloader.

### Initialization

Falcon sets up it's own stack
pointer.

`// Read data segment size from IO space`  
`u32 data_seg_size = *(u32 *)UC_CAPS;`  
`data_seg_size >>= 0x09;`  
`data_seg_size &= 0x1FF;`  
`data_seg_size <<= 0x08;`  
  
`// Set the stack pointer`  
`*(u32 *)sp = data_seg_size;`

### Stage 1 loading

`u32 boot_base_addr = 0;`  
`u32 key_data_buf[0x7C];`  
  
`// Read the key data from memory`  
`u32 key_data_addr = 0x300;`  
`u32 key_data_size = 0x7C;`  
`read_code(key_data_buf, key_data_addr, key_data_size);`  
  
`// Read the next code segment into boot base`  
`u32 blob1_addr = 0x400;`  
`u32 blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`read_code(boot_base_addr, blob1_addr, blob1_size);`  
  
`// Upload the next code segment into Falcon's CODE region`  
`u32 blob1_virt_addr = 0x300;`  
`bool use_secret = true;`  
`upload_code(blob1_virt_addr, boot_base_addr, blob1_size, blob1_virt_addr, use_secret);`  
  
`u32 boot_res = 0;`  
`bool is_done = false;`  
`u32 time = 0;`  
`bool is_blob_dec = false;`  
  
`while (!is_done)`  
`{`  
`   if (time > 4000000)`  
`   {`  
`      // Write boot failed (timeout) magic to FALCON_SCRATCH1`  
`      boot_res = 0xC0C0C0C0;`  
`      *(u32 *)FALCON_SCRATCH1 = boot_res;`  
`      `  
`      break;`  
`   }`  
`   `  
`   // Load key version from FALCON_SCRATCH0 (bootloader sends 0x01)`  
`   u32 key_version = *(u32 *)FALCON_SCRATCH0;`  
  
`   if (key_version == 0x64)`  
`   {`  
`      // Skip all next stages`  
`      boot_res = 0xB0B0B0B0;`  
`      *(u32 *)FALCON_SCRATCH1 = boot_res;`  
`      `  
`      break;`  
`   }`  
`   else`  
`   {`  
`      if (key_version > 0x03)`  
`         boot_res = 0xD0D0D0D0;    // Invalid key version`  
`      else if (key_version == 0)`  
`         boot_res = 0xB0B0B0B0;    // No keys used`  
`      else`  
`      {`  
`         u32 key_buf[0x7C];`  
`         `  
`         // Copy key data`  
`         memcpy(key_buf, key_data_buf, 0x7C);`  
  
`         u32 xfer_size_flag = 0x00060000;`  
`         u32 blob1_hash_addr = key_buf + 0x20; `  
  
`         // fuc5 crypt cauth instruction`  
`         // Set auth_addr to 0x300 and auth_size to blob1_size`  
`         *(u32 *)cauth = ((blob1_size << 0x10) | (0x300 >> 0x08));`  
  
`         // fuc5 crypt cxset instruction`  
`         // Set crypto transfer mode`  
`         *(u32 *)cx = 0x02;`  
`         `  
`         // Transfer data from/to Falcon`  
`     xdst(0, (blob1_hash_addr | xfer_size_flag));`  
`                   `  
`     // Wait for all data loads/stores to finish`  
`     xdwait();`  
  
`         // Jump to Stage1`  
`         u32 stage1_res = exec_stage1(key_buf, key_version, is_blob_dec);`  
`         is_blob_dec = true;  // Set this to prevent decrypting again`  
  
`         // Set boot finish magic on success`  
`     if (stage1_res == 0)`  
`            boot_res = 0xB0B0B0B0`  
`      }`  
`      `  
`      // Write result to FALCON_SCRATCH1`  
`      *(u32 *)FALCON_SCRATCH1 = boot_res;`  
  
`      if (boot_res == 0xB0B0B0B0)`  
`         is_done = true;`  
`   }`  
  
`   time++;`  
`}`  
  
`// Write Falcon device key to registers`  
`set_device_key(key_data_buf);`  
  
`return boot_res;`

## Stage 1

This stage is responsible for reconfiguring the Falcon's crypto
co-processor and loading, decrypting, authenticating and executing Stage
2.

### Crypto setup

`// Clear interrupt flags`  
`*(u8 *)flags_ie0 = 0;`  
`*(u8 *)flags_ie1 = 0;`  
`*(u8 *)flags_ie2 = 0;`  
  
`// fuc5 crypt cxset instruction`  
`// Set crypto transfer mode`  
`*(u32 *)cx = 0x80;`  
  
`// fuc5 crypt cauth instruction`  
`*(u32 *)cauth &= 0x7FFFF;`  
  
`// Set the target port for memory transfers`  
`// Target will now be 0 (crypto)`  
`xtargets(0);`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Wait for all code loads to finish`  
`xcwait();`  
  
`// fuc5 crypt cxset instruction`  
`// Set crypto transfer mode`  
`*(u32 *)cx = 0x02;`  
  
`// Transfer data from/to Falcon`  
`// This should clear all previous hashes`  
`xdst(0, 0);`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Clear crypto registers`  
`*(u32 *)c0 ^= *(u32 *)c0;`  
`*(u32 *)c1 = *(u32 *)c0;`  
`*(u32 *)c2 = *(u32 *)c0;`  
`*(u32 *)c3 = *(u32 *)c0;`  
`*(u32 *)c4 = *(u32 *)c0;`  
`*(u32 *)c5 = *(u32 *)c0;`  
`*(u32 *)c7 = *(u32 *)c0;`  
  
`// Update engine specific IO (crypto?)`  
`*(u32 *)0x00020E00 &= 0xEFFFF;`  
  
`// Update engine specific IO (crypto?)`  
`*(u32 *)0x00010600 |= 0x01;`  
  
`u32 wait_10600 = 0;`  
  
`// Wait for some device`  
`while (wait_10600 == 0)`  
`   wait_10600 = (*(u32 *)0x00010600 & 0x02);`  
  
`// Read data segment size from IO space`  
`u32 data_seg_size = *(u32 *)UC_CAPS;`  
`data_seg_size >>= 0x09;`  
`data_seg_size &= 0x1FF;`  
`data_seg_size <<= 0x08;`  
  
`// Check stack bounds`  
`if ((*(u32 *)sp >= data_seg_size) || (*(u32 *)sp < 0x800))`  
`  return;`  
  
`// Decrypt and load Stage2`  
`load_stage2(key_buf, key_version, is_blob_dec);`  
  
`// Clear crypto registers`  
`*(u32 *)c0 ^= *(u32 *)c0;`  
`*(u32 *)c1 ^= *(u32 *)c1;`  
`*(u32 *)c2 ^= *(u32 *)c2;`  
`*(u32 *)c3 ^= *(u32 *)c3;`  
`*(u32 *)c4 ^= *(u32 *)c4;`  
`*(u32 *)c5 ^= *(u32 *)c5;`  
`*(u32 *)c6 ^= *(u32 *)c6;`  
`*(u32 *)c7 ^= *(u32 *)c7;`  
  
`// Signal unknown engine`  
`*(u32 *)0x00010300 = 0;`  
  
`return;`

### Stage 2 loading

`u32 res = 0;`  
  
`u32 boot_base_addr = 0;`  
`u32 blob0_addr = 0;`  
`u32 blob0_size = *(u32 *)(key_buf + 0x70); `  
  
`// Load blob0 code again`  
`read_code(boot_base_addr, blob0_addr, blob0_size);`  
  
`// Generate "CODE_SIG_01" key into c4 crypto register`  
`keygen(0, 0);`  
  
`// Encrypt buffer with c4`  
`u32 sig_key[0x10];`  
`enc_buf(sig_key, blob0_size);`  
  
`u32 src_addr = boot_base_addr;`  
`u32 src_size = blob0_size;`  
`u32 iv_addr = sig_key;`  
`u32 dst_addr = sig_key;`  
`u32 mode = 0x02;   // AES-CMAC`  
`u32 version = 0;`  
  
`// Do AES-CMAC over blob0 code`  
`do_crypto(src_addr, src_size, iv_addr, dst_addr, mode, version);`  
  
`// Compare the hashes`  
`if (memcmp(sig_key, key_buf + 0x10, 0x10))`  
`{`  
`  res = 0xDEADBEEF;`  
`  return res;`  
`}`  
  
`u32 blob1_size = *(u32 *)(key_buf + 0x74);`  
  
`// Decrypt Stage2 blob if needed`  
`if (!is_blob_dec)`  
`{`  
`   // Read Stage2's size from key buffer`  
`   u32 blob2_size = *(u32 *)(key_buf + 0x78);`  
  
`   // Check stack bounds`  
`   if (*(u32 *)sp > blob2_size)`  
`   {`  
`      u32 boot_base_addr = 0;`  
`      u32 blob2_virt_addr = blob0_size + blob1_size;`  
`      u32 blob2_addr = blob2_virt_addr + 0x100;`  
`      `  
`      // Read Stage2's encrypted blob`  
`      read_code(boot_base_addr, blob2_addr, blob2_size);`  
  
`      // Generate "CODE_ENC_01" key into c4 crypt register`  
`      keygen(0x01, 0x01);`  
`      `  
`      u32 src_addr = boot_base_addr;`  
`      u32 src_size = blob2_size;`  
`      u32 iv_addr = key_buf + 0x40;`  
`      u32 dst_addr = boot_base_addr;`  
`      u32 mode = 0;   // AES-128-ECB`  
`      u32 version = 0;`  
`      `  
`      // Decrypt Stage2`  
`      do_crypto(src_addr, src_size, iv_addr, dst_addr, mode, version);`  
`      `  
`      // Upload the next code segment into Falcon's CODE region`  
`      bool use_secret = true;`  
`      upload_code(blob2_virt_addr, boot_base_addr, blob2_size, blob2_virt_addr, use_secret);`  
  
`      // Clear out the decrypted blob`  
`      memset(boot_base_addr, 0, blob2_size);`  
`   }`  
`}`  
  
`// fuc5 crypt cxset instruction`  
`// Set crypto transfer mode`  
`*(u32 *)cx = 0x02;`  
  
`u32 xfer_size_flag = 0x00060000;`  
`u32 blob2_hash_addr = key_buf + 0x30;`  
  
`// Transfer data from/to Falcon`  
`xdst(0, (blob2_hash_addr | xfer_size_flag));`  
`               `  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Save previous cauth value`  
`u32 cauth_old = *(u32 *)cauth;`  
  
`// fuc5 crypt cauth instruction`  
`// Set auth_addr to blob2_virt_addr and auth_size to blob2_size`  
`*(u32 *)cauth = ((blob2_virt_addr >> 0x08) | (blob2_size << 0x10));`  
  
`u32 hovi_key_addr = 0;`  
  
`// Select next stage key`  
`if (key_version == 0x01)       // Use HOVI_EKS_01`  
`  hovi_key_addr = key_buf + 0x50;`  
`else if (key_version == 0x02)          // Use HOVI_COMMON_01`  
`  hovi_key_addr = key_buf + 0x60;`  
`else if (key_version == 0x03)          // Use device key`  
`  hovi_key_addr = key_buf + 0x00;`  
`else`  
`  res = 0xD0D0D0D0`  
`   `  
`// Jump to Stage2`  
`if (hovi_key_addr)`  
`  res = exec_stage2(hovi_key_addr, key_version);`  
`         `  
`// Clear out key data`  
`memset(key_buf, 0, 0x7C);`  
  
`// Restore previous cauth value`  
`*(u32 *)cauth = cauth_old;`  
  
`return res;`

## Stage 2

This stage is decrypted by Stage 1 using an hardware secret. It is
likely to be the main firmware code that stays running on the Falcon
after the Switch's kernel is loaded (HOVI == Horizon VI?).

## Key data

Small buffer stored after Stage 0's code and used across all
stages.

## Notes

[https:x//wiki.0x04.net/wiki/Marcin\_Ko%C5%9Bcielnicki](Https:x%20%20wiki.0x04.net%20wiki%20Marcin%20Ko%C5%9Bcielnicki.md)
mwk shared additional info learned from RE of falcon processors over the
years, which hasn't made it into envytools documentation yet:

### cxset

cxset instruction provides a way to change behavior of a variable amount
of successively executed DMA-related instructions.

for example: `000000de: f4 3c 02 cxset 0x2`

can be read as: `dma_override(type=crypto_reg, count=2)`

The argument to cxset specifies the type of behavior change in the top 3
bits, and the number of DMA-related instructions the effect lasts for in
the lower 5 bits.

#### Override Types

Unlisted values are unknown, but probably do something.

| Value | Effect                                        |
| ----- | --------------------------------------------- |
| 0b000 | falcon data mem \<-\> falcon $cX register     |
| 0b001 | external mem \<-\> crypto input/output stream |

#### DMA-Related Instructions

At least the following instructions may have changed behavior, and count
against the cxset "count" argument: `xdwait`, `xdst`, `xdld`.

For example, if override type=0b000, then the "length" argument to
`xdst` is instead treated as the index of the target $cX register.

### Register ACLs

Falcon tracks permission metadata about each crypto reg. Permissions
include read/write ability per execution mode, as well as ability to use
the reg for encrypt/decrypt, among other permissions. Permissions are
propagated when registers are referenced by instructions (e.g. moving a
value from read-protected $cX to $cY will result in $cY also being
read-protected).

### Authenticated Mode Entry/Exit

Entry to Authenticated Mode always sets $pc to the address supplied in
$cauth (ie the base of the signature-checked region). This takes effect
when trying to branch to any address within the range covered by $cauth.

Exit from Authenticated Mode must poke a special register (this seems to
be I\[0x10300\] = 0) before leaving authenticated code pages. Failure to
do this would result in the Falcon core halting.
