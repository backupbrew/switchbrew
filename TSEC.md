TSEC (Tegra Security Co-processor) is a dedicated unit powered by a
NVIDIA Falcon microprocessor with crypto extensions.

# Driver

A host driver for communicating with the TSEC is mapped to physical
address 0x54500000 with a total size of 0x40000 bytes and exposes
several registers.

## Registers

Registers from 0x54500000 to 0x54501000 are used to configure values for
the host interface (HOST1X).

Registers from 0x54501000 to 0x54502000 are a MMIO window for
communicating with the Falcon microprocessor. From this range, the
subset of registers from 0x54501400 to 0x54501FE8 are specific to the
TSEC.

| Name                                                    | Address    | Width |
| ------------------------------------------------------- | ---------- | ----- |
| TSEC\_THI\_INT\_STATUS                                  | 0x54500078 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_HIGH\_A                      | 0x54500088 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_LOW\_A                       | 0x5450008C | 0x04  |
| TSEC\_THI\_CLK\_OVERRIDE                                | 0x54500E00 | 0x04  |
| FALCON\_IRQSSET                                         | 0x54501000 | 0x04  |
| FALCON\_IRQSCLR                                         | 0x54501004 | 0x04  |
| FALCON\_IRQSTAT                                         | 0x54501008 | 0x04  |
| FALCON\_IRQMODE                                         | 0x5450100C | 0x04  |
| [FALCON\_IRQMSET](#FALCON_IRQMSET "wikilink")           | 0x54501010 | 0x04  |
| FALCON\_IRQMCLR                                         | 0x54501014 | 0x04  |
| FALCON\_IRQMASK                                         | 0x54501018 | 0x04  |
| [FALCON\_IRQDEST](#FALCON_IRQDEST "wikilink")           | 0x5450101C | 0x04  |
| [FALCON\_SCRATCH0](#FALCON_SCRATCH0 "wikilink")         | 0x54501040 | 0x04  |
| [FALCON\_SCRATCH1](#FALCON_SCRATCH1 "wikilink")         | 0x54501044 | 0x04  |
| [FALCON\_ITFEN](#FALCON_ITFEN "wikilink")               | 0x54501048 | 0x04  |
| [FALCON\_IDLESTATE](#FALCON_IDLESTATE "wikilink")       | 0x5450104C | 0x04  |
| FALCON\_CURCTX                                          | 0x54501050 | 0x04  |
| FALCON\_NXTCTX                                          | 0x54501054 | 0x04  |
| FALCON\_SCRATCH2                                        | 0x54501080 | 0x04  |
| FALCON\_SCRATCH3                                        | 0x54501084 | 0x04  |
| FALCON\_CGCTL                                           | 0x545010A0 | 0x04  |
| FALCON\_ENGCTL                                          | 0x545010A4 | 0x04  |
| [FALCON\_CPUCTL](#FALCON_CPUCTL "wikilink")             | 0x54501100 | 0x04  |
| [FALCON\_BOOTVEC](#FALCON_BOOTVEC "wikilink")           | 0x54501104 | 0x04  |
| FALCON\_HWCFG                                           | 0x54501108 | 0x04  |
| [FALCON\_DMACTL](#FALCON_DMACTL "wikilink")             | 0x5450110C | 0x04  |
| [FALCON\_DMATRFBASE](#FALCON_DMATRFBASE "wikilink")     | 0x54501110 | 0x04  |
| [FALCON\_DMATRFMOFFS](#FALCON_DMATRFMOFFS "wikilink")   | 0x54501114 | 0x04  |
| [FALCON\_DMATRFCMD](#FALCON_DMATRFCMD "wikilink")       | 0x54501118 | 0x04  |
| [FALCON\_DMATRFFBOFFS](#FALCON_DMATRFFBOFFS "wikilink") | 0x5450111C | 0x04  |
| FALCON\_CPUCTL\_ALIAS                                   | 0x54501130 | 0x04  |
| FALCON\_EXTERRADDR                                      | 0x54501168 | 0x04  |
| FALCON\_EXTERRSTAT                                      | 0x5450116C | 0x04  |
| FALCON\_CG2                                             | 0x5450117C | 0x04  |
| FALCON\_CODE\_INDEX                                     | 0x54501180 | 0x04  |
| FALCON\_CODE                                            | 0x54501184 | 0x04  |
| FALCON\_CODE\_VIRT\_ADDR                                | 0x54501188 | 0x04  |
| FALCON\_DATA\_INDEX0                                    | 0x545011C0 | 0x04  |
| FALCON\_DATA0                                           | 0x545011C4 | 0x04  |
| FALCON\_DATA\_INDEX1                                    | 0x545011C8 | 0x04  |
| FALCON\_DATA1                                           | 0x545011CC | 0x04  |
| FALCON\_DATA\_INDEX2                                    | 0x545011D0 | 0x04  |
| FALCON\_DATA2                                           | 0x545011D4 | 0x04  |
| FALCON\_DATA\_INDEX3                                    | 0x545011D8 | 0x04  |
| FALCON\_DATA3                                           | 0x545011DC | 0x04  |
| FALCON\_DATA\_INDEX4                                    | 0x545011E0 | 0x04  |
| FALCON\_DATA4                                           | 0x545011E4 | 0x04  |
| FALCON\_DATA\_INDEX5                                    | 0x545011E8 | 0x04  |
| FALCON\_DATA5                                           | 0x545011EC | 0x04  |
| FALCON\_DATA\_INDEX6                                    | 0x545011F0 | 0x04  |
| FALCON\_DATA6                                           | 0x545011F4 | 0x04  |
| FALCON\_DATA\_INDEX7                                    | 0x545011F8 | 0x04  |
| FALCON\_DATA7                                           | 0x545011FC | 0x04  |
| FALCON\_ICD\_CMD                                        | 0x54501200 | 0x04  |
| FALCON\_ICD\_ADDR                                       | 0x54501204 | 0x04  |
| FALCON\_ICD\_WDATA                                      | 0x54501208 | 0x04  |
| FALCON\_ICD\_RDATA                                      | 0x5450120C | 0x04  |
| FALCON\_SCTL                                            | 0x54501240 | 0x04  |
| [TSEC\_SCP\_CTL\_STAT](#TSEC_SCP_CTL_STAT "wikilink")   | 0x54501408 | 0x04  |
| TSEC\_SCP\_CTL\_AUTH\_MODE                              | 0x5450140C | 0x04  |
| [TSEC\_SCP\_CTL\_PKEY](#TSEC_SCP_CTL_PKEY "wikilink")   | 0x54501418 | 0x04  |
| TSEC\_TFBIF\_MCCIF\_FIFOCTRL                            | 0x54501604 | 0x04  |
| TSEC\_DMA\_CMD                                          | 0x54501700 | 0x04  |
| TSEC\_DMA\_ADDR                                         | 0x54501704 | 0x04  |
| TSEC\_DMA\_VAL                                          | 0x54501708 | 0x04  |
| TSEC\_DMA\_UNK                                          | 0x5450170C | 0x04  |
| [TSEC\_TEGRA\_CTL](#TSEC_TEGRA_CTL "wikilink")          | 0x54501838 | 0x04  |
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

### FALCON\_IDLESTATE

| Bits | Description                     |
| ---- | ------------------------------- |
| 0    | FALCON\_IDLESTATE\_FALCON\_BUSY |
|      |                                 |

Used for detecting if Falcon is busy or not.

### FALCON\_CPUCTL

| Bits | Description              |
| ---- | ------------------------ |
| 0    | FALCON\_CPUCTL\_IINVAL   |
| 1    | FALCON\_CPUCTL\_STARTCPU |
| 2    | FALCON\_CPUCTL\_SRESET   |
| 3    | FALCON\_CPUCTL\_HRESET   |
| 4    | FALCON\_CPUCTL\_HALTED   |
| 5    | FALCON\_CPUCTL\_STOPPED  |
|      |                          |

Used for signaling the Falcon CPU.

### FALCON\_BOOTVEC

Takes the Falcon's boot vector address.

### FALCON\_DMACTL

| Bits | Description                     |
| ---- | ------------------------------- |
| 0    | FALCON\_DMACTL\_REQUIRE\_CTX    |
| 1    | FALCON\_DMACTL\_DMEM\_SCRUBBING |
| 2    | FALCON\_DMACTL\_IMEM\_SCRUBBING |
| 3-6  | FALCON\_DMACTL\_DMAQ\_NUM       |
| 7    | FALCON\_DMACTL\_SECURE\_STAT    |
|      |                                 |

Used for configuring the Falcon's DMA engine.

### FALCON\_DMATRFBASE

Takes the host's base address for transferring data to/from the Falcon
(DMA).

### FALCON\_DMATRFMOFFS

Takes the offset for the host's source memory being transferred.

### FALCON\_DMATRFCMD

| Bits  | Description                                                 |
| ----- | ----------------------------------------------------------- |
| 0     | FALCON\_DMATRFCMD\_FULL                                     |
| 1     | FALCON\_DMATRFCMD\_IDLE (this is set if the engine is idle) |
| 2-3   | FALCON\_DMATRFCMD\_SEC                                      |
| 4     | FALCON\_DMATRFCMD\_IMEM                                     |
| 5     | FALCON\_DMATRFCMD\_WRITE                                    |
| 8-10  | FALCON\_DMATRFCMD\_SIZE                                     |
| 12-14 | FALCON\_DMATRFCMD\_CTXDMA                                   |
|       |                                                             |

Used for configuring DMA transfers.

### FALCON\_DMATRFFBOFFS

Takes the offset for Falcon's target memory being transferred.

### TSEC\_SCP\_CTL\_STAT

| Bits | Description                       |
| ---- | --------------------------------- |
| 20   | TSEC\_SCP\_CTL\_STAT\_DEBUG\_MODE |
|      |                                   |

### TSEC\_SCP\_CTL\_PKEY

| Bits | Description                           |
| ---- | ------------------------------------- |
| 0    | TSEC\_SCP\_CTL\_PKEY\_REQUEST\_RELOAD |
| 1    | TSEC\_SCP\_CTL\_PKEY\_LOADED          |
|      |                                       |

### TSEC\_TEGRA\_CTL

| Bits | Description                                      |
| ---- | ------------------------------------------------ |
| 16   | TSEC\_TEGRA\_CTL\_TKFI\_KFUSE                    |
| 17   | TSEC\_TEGRA\_CTL\_TKFI\_RESTART\_FSM\_KFUSE      |
| 24   | TSEC\_TEGRA\_CTL\_TMPI\_FORCE\_IDLE\_INPUTS\_I2C |
| 25   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_HOST1X     |
| 26   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_APB        |
| 27   | TSEC\_TEGRA\_CTL\_TMPI\_DISABLE\_OUTPUT\_I2C     |
|      |                                                  |

# Boot Process

TSEC is configured and initialized by the first bootloader during key
generation (sub\_400114FC).

## Initialization

During this stage several clocks are
programmed.

`// Program the HOST1X clock and resets`  
`// Uses RST_DEVICES_L, CLK_OUT_ENB_L, CLK_SOURCE_HOST1X and CLK_L_HOST1X`  
`enable_host1x_clkrst();`  
  
`// Program the TSEC clock and resets`  
`// Uses RST_DEVICES_U, CLK_OUT_ENB_U, CLK_SOURCE_TSEC and CLK_U_TSEC`  
`enable_tsec_clkrst();`  
  
`// Program the SOR_SAFE clock and resets`  
`// Uses RST_DEVICES_Y, CLK_OUT_ENB_Y and CLK_Y_SOR_SAFE`  
`enable_sor_safe_clkrst();`  
  
`// Program the SOR0 clock and resets`  
`// Uses RST_DEVICES_X, CLK_OUT_ENB_X and CLK_X_SOR0`  
`enable_sor0_clkrst();`  
  
`// Program the SOR1 clock and resets`  
`// Uses RST_DEVICES_X, CLK_OUT_ENB_X, CLK_SOURCE_SOR1 and CLK_X_SOR1`  
`enable_sor1_clkrst();`  
  
`// Program the KFUSE clock resets`  
`// Uses RST_DEVICES_H, CLK_OUT_ENB_H and CLK_H_KFUSE`  
`enable_kfuse_clkrst();`

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

Falcon is booted up and the first bootloader waits for it to
finish.

`// Set something in unknown host1x channel 0 sync register (HOST1X_SYNC_UNK_300)`  
`// This appears to grant TSEC exclusive access to host1x`  
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
  
`// The bootloader allows the TSEC two seconds from this point to do its job`  
`u32 maximum_time = read_timer() + 2000000; `  
  
`while (!boot_res)`  
`{`  
`   // Read boot result from scratch1 MMIO`  
`   boot_res = *(u32 *)FALCON_SCRATCH1;`  
`   `  
`   // Read from TIMERUS_CNTR_1US (microseconds from boot)`  
`   u32 current_time = read_timer();`  
`   `  
`   // Booting is taking too long`  
`   if (current_time > maximum_time)`  
`      panic();`  
`}`  
  
`// Invalid boot result was returned`  
`if (boot_res != 0xB0B0B0B0)`  
`   panic();`

## Device key generation

The TSEC device key is generated by reading SOR1 registers modified by
the Falcon
CPU.

`// Clear something in unknown host1x channel 0 sync register (HOST1X_SYNC_UNK_300)`  
`// This appears to revoke TSEC's exclusive access to host1x`  
`*(u32 *)0x50003300 = 0;`  
  
`// Read TSEC device key`  
`u32 tsec_device_key[4]; `  
`tsec_device_key[0] = *(u32 *)NV_SOR_DP_HDCP_BKSV_LSB;`  
`tsec_device_key[1] = *(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB;`  
`tsec_device_key[2] = *(u32 *)NV_SOR_TMDS_HDCP_CN_MSB;`  
`tsec_device_key[3] = *(u32 *)NV_SOR_TMDS_HDCP_CN_LSB;`  
  
`// Clear SOR1 registers`  
`*(u32 *)NV_SOR_DP_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_MSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_LSB = 0;`  
  
`if (out_size < 0x10)`  
`   out_size = 0x10;`  
  
`// Copy back the TSEC device key`  
`memcpy(out_buf, tsec_device_key, out_size);`

## Cleanup

Clocks and resets are disabled before
returning.

`// Deprogram KFUSE clock and resets`  
`// Uses RST_DEVICES_H, CLK_OUT_ENB_H and CLK_H_KFUSE`  
`disable_kfuse_clkrst();`  
  
`// Deprogram SOR1 clock and resets`  
`// Uses RST_DEVICES_X, CLK_OUT_ENB_X, CLK_SOURCE_SOR1 and CLK_X_SOR1`  
`disable_sor1_clkrst();`  
  
`// Deprogram SOR0 clock and resets`  
`// Uses RST_DEVICES_X, CLK_OUT_ENB_X and CLK_X_SOR0`  
`disable_sor0_clkrst();`  
  
`// Deprogram SOR_SAFE clock and resets`  
`// Uses RST_DEVICES_Y, CLK_OUT_ENB_Y and CLK_Y_SOR_SAFE`  
`disable_sor_safe_clkrst();`  
  
`// Deprogram TSEC clock and resets`  
`// Uses RST_DEVICES_U, CLK_OUT_ENB_U, CLK_SOURCE_TSEC and CLK_U_TSEC`  
`disable_tsec_clkrst();`  
  
`// Deprogram HOST1X clock and resets`  
`// Uses RST_DEVICES_L, CLK_OUT_ENB_L, CLK_SOURCE_HOST1X and CLK_L_HOST1X`  
`disable_host1x_clkrst();`  
  
`return;`

# TSEC Firmware

The actual code loaded into TSEC is assembled in NVIDIA's proprietary
fuc5 ISA using crypto extensions. Stored inside the first bootloader,
this firmware binary is split into 4 blobs: Stage0, Stage1, Stage2 and
key data.

Firmware can be disassembled with
[envytools'](http://envytools.readthedocs.io/en/latest/)
[envydis](https://github.com/envytools/envytools/tree/master/envydis):

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
  
`         u32 crypt_reg_flag = 0x00060000;`  
`         u32 blob1_hash_addr = key_buf + 0x20; `  
  
`         // fuc5 crypt cauth instruction`  
`         // Set auth_addr to 0x300 and auth_size to blob1_size`  
`         cauth((blob1_size << 0x10) | (0x300 >> 0x08));`  
  
`         // fuc5 crypt cxset instruction`  
`         // The next 2 xfer instructions will be overridden`  
`         // and target changes from DMA to crypto`  
`         cxset(0x02);`  
`         `  
`         // Transfer data to crypto register c6`  
`    xdst(0, (blob1_hash_addr | crypt_reg_flag));`  
`               `  
`    // Wait for all data loads/stores to finish`  
`    xdwait();`  
`         `  
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
  
`// Write TSEC device key to registers`  
`set_device_key(key_data_buf);`  
  
`return boot_res;`

#### set\_device\_key

This method takes **key\_data\_buf** as argument and writes the TSEC key
to SOR1 registers.

`// This is TSEC_MMIO + 0x1000 + (0x1C300 / 0x40)`  
`*(u32 *)TSEC_DMA_UNK = 0xFFF;`  
  
`// Read the key's words`  
`u32 key0 = *(u32 *)(key_data_buf + 0x00);`  
`u32 key1 = *(u32 *)(key_data_buf + 0x04);`  
`u32 key2 = *(u32 *)(key_data_buf + 0x08);`  
`u32 key3 = *(u32 *)(key_data_buf + 0x0C);`  
  
`u32 result = 0;`  
  
`// Write to SOR1 register`  
`result = tsec_dma_write(NV_SOR_DP_HDCP_BKSV_LSB, key0);`  
  
`// Failed to write`  
`if (result)`  
`   return result;`  
  
`// Write to SOR1 register`  
`result = tsec_dma_write(NV_SOR_TMDS_HDCP_BKSV_LSB, key1);`  
  
`// Failed to write`  
`if (result)`  
`   return result;`  
  
`// Write to SOR1 register`  
`result = tsec_dma_write(NV_SOR_TMDS_HDCP_CN_MSB, key2);`  
  
`// Failed to write`  
`if (result)`  
`   return result;`  
  
`// Write to SOR1 register`  
`result = tsec_dma_write(NV_SOR_TMDS_HDCP_CN_LSB, key3);`  
  
`// Failed to write`  
`if (result)`  
`   return result;`  
  
`return result;`

##### tsec\_dma\_write

This method takes **addr** and **value** as arguments and performs a DMA
write using TSEC MMIO.

`u32 result = 0;`  
  
`// Wait for TSEC DMA engine`  
`// This waits for bit 0x0C in TSEC_DMA_CMD to be 0`  
`result = wait_tsec_dma();`  
  
`// Wait failed`  
`if (result)`  
`   return 1;`  
  
`// Set the destination address`  
`// This is TSEC_MMIO + 0x1000 + (0x1C100 / 0x40)`  
`*(u32 *)TSEC_DMA_ADDR = addr;`  
  
`// Set the value`  
`// This is TSEC_MMIO + 0x1000 + (0x1C200 / 0x40)`  
`*(u32 *)TSEC_DMA_VAL = value;`  
  
`// Start transfer?`  
`// This is TSEC_MMIO + 0x1000 + (0x1C000 / 0x40)`  
`*(u32 *)TSEC_DMA_CMD = 0x800000F2;`  
  
`// Wait for TSEC DMA engine`  
`// This waits for bit 0x0C in TSEC_DMA_CMD to be 0`  
`result = wait_tsec_dma();`  
  
`// Wait failed`  
`if (result)`  
`   return 1;`  
  
`return 0;`

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
`// Clear overrides?`  
`cxset(0x80);`  
  
`// fuc5 crypt cauth instruction`  
`// Clear bit 0x13 in cauth`  
`cauth(cauth_old & ~(1 << 0x13));`  
  
`// Set the target port for memory transfers`  
`xtargets(0);`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Wait for all code loads to finish`  
`xcwait();`  
  
`// fuc5 crypt cxset instruction`  
`// The next 2 xfer instructions will be overridden`  
`// and target changes from DMA to crypto`  
`cxset(0x02);`  
  
`// Transfer data to crypto register c0`  
`// This should clear any leftover data`  
`xdst(0, 0);`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Clear all crypto registers, except c6 which is used for auth`  
`cxor(c0, c0);`  
`cmov(c1, c0);`  
`cmov(c2, c0);`  
`cmov(c3, c0);`  
`cmov(c4, c0);`  
`cmov(c5, c0);`  
`cmov(c7, c0);`  
  
`// Clear TSEC_TEGRA_CTL_TKFI_KFUSE`  
`// This is TSEC_MMIO + 0x1000 + (0x20E00 / 0x40)`  
`*(u32 *)TSEC_TEGRA_CTL &= 0xEFFFF;`  
  
`// Set TSEC_SCP_CTL_PKEY_REQUEST_RELOAD`  
`// This is TSEC_MMIO + 0x1000 + (0x10600 / 0x40)`  
`*(u32 *)TSEC_SCP_CTL_PKEY |= 0x01;`  
  
`u32 is_pkey_loaded = 0;`  
  
`// Wait for TSEC_SCP_CTL_PKEY_LOADED`  
`while (!is_pkey_loaded)`  
`   is_pkey_loaded = (*(u32 *)TSEC_SCP_CTL_PKEY & 0x02);`  
  
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
  
`// Partially unknown fuc5 instruction`  
`// Likely forces a change of permissions`  
`acl_chmod(c0, c0);`  
  
`// Clear all crypto registers and propagate permissions`  
`cxor(c0, c0);`  
`cxor(c1, c1);`  
`cxor(c2, c2);`  
`cxor(c3, c3);`  
`cxor(c4, c4);`  
`cxor(c5, c5);`  
`cxor(c6, c6);`  
`cxor(c7, c7);`  
  
`// Exit Authenticated Mode`  
`// This is TSEC_MMIO + 0x1000 + (0x10300 / 0x40)`  
`*(u32 *)TSEC_SCP_CTL_AUTH_MODE = 0;`  
  
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
`if (memcmp(dst_addr, key_buf + 0x10, 0x10))`  
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
`// The next 2 xfer instructions will be overridden`  
`// and target changes from DMA to crypto`  
`cxset(0x02);`  
  
`u32 crypt_reg_flag = 0x00060000;`  
`u32 blob2_hash_addr = key_buf + 0x30;`  
  
`// Transfer data to crypto register c6`  
`xdst(0, (blob2_hash_addr | crypt_reg_flag));`  
`               `  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`// Save previous cauth value`  
`u32 c_old = cauth_old;`  
  
`// fuc5 crypt cauth instruction`  
`// Set auth_addr to blob2_virt_addr and auth_size to blob2_size`  
`cauth((blob2_virt_addr >> 0x08) | (blob2_size << 0x10));`  
  
`u32 hovi_key_addr = 0;`  
  
`// Select next stage key`  
`if (key_version == 0x01)       // Use HOVI_EKS_01`  
`  hovi_key_addr = key_buf + 0x50;`  
`else if (key_version == 0x02)          // Use HOVI_COMMON_01`  
`  hovi_key_addr = key_buf + 0x60;`  
`else if (key_version == 0x03)          // Use empty key`  
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
  
`// fuc5 crypt cauth instruction`  
`// Restore previous cauth value`  
`cauth(c_old);`  
  
`return res;`

#### keygen

This method takes **type** and **mode** as arguments and generates a
key.

`u32 seed_buf[0x10];`  
  
`// Read a 16 bytes seed based on supplied type`  
`/*`  
`   Type 0: "CODE_SIG_01" + null padding`  
`   Type 1: "CODE_ENC_01" + null padding`  
`*/`  
`get_seed(seed_buf, type);`  
  
`// This will write the seed into crypto register c0 `  
`crypt_store(0, seed_buf);`  
  
`// fuc5 csecret instruction`  
`// Load selected secret into crypto register c1`  
`csecret(c1, 0x26);`  
  
`// fuc5 ckeyreg instruction`  
`// Bind c1 register as the key for enc/dec operations`  
`ckeyreg(c1);`  
  
`// fuc5 cenc instruction`  
`// Encrypt seed_buf (in c0) using keyreg value as key into c1`  
`cenc(c1, c0);`  
  
`// fuc5 csigenc instruction`  
`// Encrypt c1 register with the auth signature stored in c6`  
`csigenc(c1, c1);`  
  
`// Copy the result into c4 (will be used as key)`  
`cmov(c4, c1);`  
  
`// Do key expansion (for decryption)`  
`if (mode != 0)`  
`   ckexp(c4, c4);      // fuc5 ckexp instruction`  
  
`return;`

#### enc\_buffer

This method takes **buf** (a 16 bytes buffer) and **size** as arguments
and encrypts the supplied buffer.

`// Set first 3 words to null`  
`*(u32 *)(buf + 0x00) = 0;`  
`*(u32 *)(buf + 0x04) = 0;`  
`*(u32 *)(buf + 0x08) = 0;`  
  
`// Swap halves (b16, b32 and b16 again)`  
`hswap(size);`  
  
`// Store the size as the last word`  
`*(u32 *)(buf + 0x0C) = size;`  
  
`// This will write buf into crypto register c3 `  
`crypt_store(0x03, buf);`  
  
`// fuc5 ckeyreg instruction`  
`// Bind c4 register (from keygen) as the key for enc/dec operations`  
`ckeyreg(c4);`  
  
`// fuc5 cenc instruction`  
`// Encrypt buf (in c3) using keyreg value as key into c5`  
`cenc(c5, c3);`  
  
`// This will read into buf from crypto register c5 `  
`crypt_load(0x05, buf);`  
  
`return;`

#### do\_crypto

This is the method responsible for all crypto operations performed
during Stage 1. It takes **src\_addr**, **src\_size**, **iv\_addr**,
**dst\_addr**, **mode** and **crypt\_ver** as
arguments.

`// Check for invalid source data size`  
`if (!src_size || (src_size & 0x0F))`  
`  exit();`  
  
`// Check for invalid source data address`  
`if (src_addr & 0x0F)`  
`  exit();`  
  
`// Check for invalid destination data address`  
`if (dst_addr & 0x0F)`  
`  exit();`  
  
`// Use IV if available`  
`if (iv_addr)`  
`{`  
`  // This will write the iv_addr into crypto register c5 `  
`  crypt_store(0x05, iv_addr);`  
`}`  
`else`  
`{`  
`  // Clear c5 register (use null IV)`  
`  cxor(c5, c5);`  
`}`  
  
`// Use key in c4`  
`ckeyreg(c4);`  
  
`// AES-128-ECB decrypt`  
`if (mode == 0x00)`  
`{`  
`  // Create crypto script with 5 instructions`  
`  cs0begin(0x05);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cdec(c2, c3);                // Decrypt from c3 into c2`  
`  cxor(c5, c2);                // XOR c2 with c5 and store in c5`  
`  cxsout(c5);                  // Write 0x10 bytes into crypto stream from c5`  
`  cmov(c5, c3);                // Move c3 into c5`  
`}`  
`else if (mode == 0x01)     // AES-128-ECB encrypt`  
`{`  
`  // Create crypto script with 4 instructions`  
`  cs0begin(0x04);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cxor(c3, c5);                // XOR c5 with c3 and store in c3`  
`  cenc(c5, c3);                // Encrypt from c3 into c5`  
`  cxsout(c5);                  // Write 0x10 bytes into crypto stream from c5`  
`}`  
`else if (mode == 0x02)     // AES-CMAC`  
`{`  
`  // Create crypto script with 3 instructions`  
`  cs0begin(0x03);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cxor(c5, c3);                // XOR c5 with c3 and store in c3`  
`  cenc(c5, c5);                // Encrypt from c5 into c5`  
`}`  
`else if (mode == 0x03)     // AES-128-ECB decrypt (no IV)`  
`{`  
`  // Create crypto script with 3 instructions`  
`  cs0begin(0x03);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cdec(c5, c3);                // Decrypt from c3 into c5`  
`  cxsout(c5);                  // Write 0x10 bytes into crypto stream from c5`  
`}`  
`else if (mode == 0x04)     // AES-128-ECB encrypt (no IV)`  
`{`  
`  // Create crypto script with 3 instructions`  
`  cs0begin(0x03);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cenc(c5, c3);                // Encrypt from c3 into c5`  
`  cxsout(c5);                  // Write 0x10 bytes into crypto stream from c5`  
`}`  
`else`  
`  return;`  
  
`// Main loop`  
`while (src_size > 0)`  
`{`  
`  u32 blk_count = (src_size >> 0x04);`  
`   `  
`  if (blk_count > 0x10)`  
`    blk_count = 0x10;`  
`  `  
`  // Check size align`  
`  if (blk_count & (blk_count - 0x01))`  
`    blk_count = 0x01;`  
  
`  u32 blk_size = (blk_count << 0x04);`  
`  `  
`  u32 crypt_xfer_src = 0;`  
`  u32 crypt_xfer_dst = 0;`  
`  `  
`  if (block_size == 0x20)`  
`  {`  
`     crypt_xfer_src = (0x00030000 | src_addr);`  
`     crypt_xfer_dst = (0x00030000 | dst_addr);`  
`     `  
`     // Execute crypto script 2 times (1 for each block)`  
`     cs0exec(0x02);`  
`  }`  
`  if (block_size == 0x40)`  
`  {`  
`     crypt_xfer_src = (0x00040000 | src_addr);`  
`     crypt_xfer_dst = (0x00040000 | dst_addr);`  
`     `  
`     // Execute crypto script 4 times (1 for each block)`  
`     cs0exec(0x04);`  
`  }`  
`  if (block_size == 0x80)`  
`  {`  
`     crypt_xfer_src = (0x00050000 | src_addr);`  
`     crypt_xfer_dst = (0x00050000 | dst_addr);`  
`     `  
`     // Execute crypto script 8 times (1 for each block)`  
`     cs0exec(0x08);`  
`  }`  
`  if (block_size == 0x100)`  
`  {`  
`     crypt_xfer_src = (0x00060000 | src_addr);`  
`     crypt_xfer_dst = (0x00060000 | dst_addr);`  
`     `  
`     // Execute crypto script 16 times (1 for each block)`  
`     cs0exec(0x10);`  
`  }`  
`  else`  
`  {`  
`     crypt_xfer_src = (0x00020000 | src_addr);`  
`     crypt_xfer_dst = (0x00020000 | dst_addr);`  
`     `  
`     // Execute crypto script 1 time (1 for each block)`  
`     cs0exec(0x01);`  
  
`     // Ensure proper block size`  
`     block_size = 0x10;`  
`  }`  
  
`  // fuc5 crypt cxset instruction`  
`  // The next xfer instruction will be overridden`  
`  // and target changes from DMA to crypto input/output stream`  
`  if (crypt_ver == 0x01)`  
`    cxset(0xA1);         // Flag 0xA0 is (0x80 | 0x20)`  
`  else`  
`    cxset(0x21);         // Flag 0x20 is external mem <-> crypto input/output stream`  
  
`  // Transfer data into the crypto input/output stream`  
`  xdst(crypt_xfer_src, crypt_xfer_src);`  
`  `  
`  // AES-CMAC only needs one more xfer instruction`  
`  if (mode == 0x02)`  
`  {`  
`     // fuc5 crypt cxset instruction`  
`     // The next xfer instruction will be overridden`  
`     // and target changes from DMA to crypto input/output stream`  
`     if (crypt_ver == 0x01)`  
`       cxset(0xA1);     // Flag 0xA0 is (0x80 | 0x20)`  
`     else`  
`       cxset(0x21);     // Flag 0x20 is external mem <-> crypto input/output stream`  
`       `  
`     // Wait for all data loads/stores to finish`  
`     xdwait();`  
`  }`  
`  else  // AES enc/dec needs 2 more xfer instructions`  
`  {`  
`     // fuc5 crypt cxset instruction`  
`     // The next 2 xfer instructions will be overridden`  
`     // and target changes from DMA to crypto input/output stream`  
`     if (crypt_ver == 0x01)`  
`       cxset(0xA2);            // Flag 0xA0 is (0x80 | 0x20)`  
`     else`  
`       cxset(0x22);            // Flag 0x20 is external mem <-> crypto input/output stream`  
  
`     // Transfer data from the crypto input/output stream`  
`     xdld(crypt_xfer_dst, crypt_xfer_dst);`  
`       `  
`     // Wait for all data loads/stores to finish`  
`     xdwait();`  
  
`     // Increase the destination address by block size`  
`     dst_addr += block_size;`  
`  }`  
`  `  
`  // Increase the source address by block size`  
`  src_addr += block_size;`  
  
`  // Decrease the source size by block size`  
`  src_size -= block_size;`  
`}`  
  
`// AES-CMAC result is in c5`  
`if (mode == 0x02)`  
`{`  
`   // This will read into dst_addr from crypto register c5 `  
`   crypt_load(0x05, dst_addr);`  
`}`  
  
`return;`

## Stage 2

This stage is decrypted by Stage 1 using a key generated by encrypting a
seed with an hardware secret (see
[keygen](TSEC#keygen.md##keygen "wikilink")).

## Key data

Small buffer stored after Stage 0's code and used across all stages.

| Offset | Size | Description      |
| ------ | ---- | ---------------- |
| 0x00   | 0x10 | Empty            |
| 0x10   | 0x10 | blob0 auth hash  |
| 0x20   | 0x10 | blob1 auth hash  |
| 0x30   | 0x10 | blob2 auth hash  |
| 0x40   | 0x10 | blob2 AES IV     |
| 0x50   | 0x10 | HOVI EKS seed    |
| 0x60   | 0x10 | HOVI COMMON seed |
| 0x70   | 0x04 | blob0 size       |
| 0x74   | 0x04 | blob1 size       |
| 0x78   | 0x04 | blob2 size       |
|        |      |                  |

## Notes

[mwk](https://wiki.0x04.net/wiki/Marcin_Ko%C5%9Bcielnicki) shared
additional info learned from RE of falcon processors over the years,
which hasn't made it into envytools documentation yet:

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
Entry to Authenticated Mode (also called "Secure Mode") computes a MAC
over the $cauth region and compares it to $c6 in order to perform the
signature check.

Exit from Authenticated Mode must poke a special register (this seems to
be I\[0x10300\] = 0) before leaving authenticated code pages. Failure to
do this would result in the Falcon core halting.
