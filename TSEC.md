TSEC (Tegra Security Co-processor) is a dedicated unit powered by a
NVIDIA Falcon microprocessor with crypto extensions.

# Driver

A host driver for communicating with the TSEC is mapped to physical
address 0x54500000 with a total size of 0x40000 bytes and exposes
several registers.

## Registers

Registers from 0x54500000 to 0x54501000 are used to configure the host
interface (HOST1X).

Registers from 0x54501000 to 0x54502000 are a MMIO window for
communicating with the Falcon microprocessor. From this range, the
subset of registers from 0x54501400 to 0x54501FE8 are specific to the
TSEC and are subdivided into:

  - 0x54501400 to 0x54501500: SCP (secure crypto processor?).
  - 0x54501500 to 0x54501600: Unknown.
  - 0x54501600 to 0x54501700: TFBIF (Tegra Framebuffer Interface).
  - 0x54501700 to 0x54501800: DMA.
  - 0x54501800 to 0x54501900: TEGRA (miscellaneous
interfaces).

| Name                                                                    | Address    | Width |
| ----------------------------------------------------------------------- | ---------- | ----- |
| TSEC\_THI\_INCR\_SYNCPT                                                 | 0x54500000 | 0x04  |
| TSEC\_THI\_INCR\_SYNCPT\_ERR                                            | 0x54500008 | 0x04  |
| TSEC\_THI\_CTXSW\_INCR\_SYNCPT                                          | 0x5450000C | 0x04  |
| TSEC\_THI\_CTXSW                                                        | 0x54500020 | 0x04  |
| TSEC\_THI\_CONT\_SYNCPT\_EOF                                            | 0x54500028 | 0x04  |
| [TSEC\_THI\_METHOD0](#TSEC_THI_METHOD0 "wikilink")                      | 0x54500040 | 0x04  |
| [TSEC\_THI\_METHOD1](#TSEC_THI_METHOD1 "wikilink")                      | 0x54500044 | 0x04  |
| [TSEC\_THI\_INT\_STATUS](#TSEC_THI_INT_STATUS "wikilink")               | 0x54500078 | 0x04  |
| [TSEC\_THI\_INT\_MASK](#TSEC_THI_INT_MASK "wikilink")                   | 0x5450007C | 0x04  |
| TSEC\_THI\_SLCG\_STATUS                                                 | 0x54500084 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_HIGH\_A                                      | 0x54500088 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_LOW\_A                                       | 0x5450008C | 0x04  |
| TSEC\_THI\_CLK\_OVERRIDE                                                | 0x54500E00 | 0x04  |
| [FALCON\_IRQSSET](#FALCON_IRQSSET "wikilink")                           | 0x54501000 | 0x04  |
| [FALCON\_IRQSCLR](#FALCON_IRQSCLR "wikilink")                           | 0x54501004 | 0x04  |
| [FALCON\_IRQSTAT](#FALCON_IRQSTAT "wikilink")                           | 0x54501008 | 0x04  |
| [FALCON\_IRQMODE](#FALCON_IRQMODE "wikilink")                           | 0x5450100C | 0x04  |
| [FALCON\_IRQMSET](#FALCON_IRQMSET "wikilink")                           | 0x54501010 | 0x04  |
| [FALCON\_IRQMCLR](#FALCON_IRQMCLR "wikilink")                           | 0x54501014 | 0x04  |
| [FALCON\_IRQMASK](#FALCON_IRQMASK "wikilink")                           | 0x54501018 | 0x04  |
| [FALCON\_IRQDEST](#FALCON_IRQDEST "wikilink")                           | 0x5450101C | 0x04  |
| FALCON\_GPTMR\_PERIOD                                                   | 0x54501020 | 0x04  |
| FALCON\_GPTMR\_TIME                                                     | 0x54501024 | 0x04  |
| FALCON\_GPTMR\_ENABLE                                                   | 0x54501028 | 0x04  |
| FALCON\_TIME\_LOW                                                       | 0x5450102C | 0x04  |
| FALCON\_TIME\_HIGH                                                      | 0x54501030 | 0x04  |
| FALCON\_WDTMR\_TIME                                                     | 0x54501034 | 0x04  |
| FALCON\_WDTMR\_ENABLE                                                   | 0x54501038 | 0x04  |
| [FALCON\_SCRATCH0](#FALCON_SCRATCH0 "wikilink")                         | 0x54501040 | 0x04  |
| [FALCON\_SCRATCH1](#FALCON_SCRATCH1 "wikilink")                         | 0x54501044 | 0x04  |
| [FALCON\_ITFEN](#FALCON_ITFEN "wikilink")                               | 0x54501048 | 0x04  |
| [FALCON\_IDLESTATE](#FALCON_IDLESTATE "wikilink")                       | 0x5450104C | 0x04  |
| FALCON\_CURCTX                                                          | 0x54501050 | 0x04  |
| FALCON\_NXTCTX                                                          | 0x54501054 | 0x04  |
| FALCON\_CMDCTX                                                          | 0x54501058 | 0x04  |
| FALCON\_STATUS\_MASK                                                    | 0x5450105C | 0x04  |
| FALCON\_VM\_SUPERVISOR                                                  | 0x54501060 | 0x04  |
| FALCON\_MTHD\_DATA                                                      | 0x54501064 | 0x04  |
| FALCON\_MTHD\_CMD                                                       | 0x54501068 | 0x04  |
| FALCON\_MTHD\_DATA\_WR                                                  | 0x5450106C | 0x04  |
| FALCON\_MTHD\_OCCUPIED                                                  | 0x54501070 | 0x04  |
| FALCON\_MTHD\_ACK                                                       | 0x54501074 | 0x04  |
| FALCON\_MTHD\_LIMIT                                                     | 0x54501078 | 0x04  |
| FALCON\_SUBENGINE\_RESET                                                | 0x5450107C | 0x04  |
| FALCON\_SCRATCH2                                                        | 0x54501080 | 0x04  |
| FALCON\_SCRATCH3                                                        | 0x54501084 | 0x04  |
| FALCON\_PM\_TRIGGER                                                     | 0x54501088 | 0x04  |
| FALCON\_PM\_MODE                                                        | 0x5450108C | 0x04  |
| FALCON\_DEBUG1                                                          | 0x54501090 | 0x04  |
| [FALCON\_DEBUGINFO](#FALCON_DEBUGINFO "wikilink")                       | 0x54501094 | 0x04  |
| FALCON\_BREAKPOINT0                                                     | 0x54501098 | 0x04  |
| FALCON\_BREAKPOINT1                                                     | 0x5450109C | 0x04  |
| FALCON\_CGCTL                                                           | 0x545010A0 | 0x04  |
| FALCON\_ENGCTL                                                          | 0x545010A4 | 0x04  |
| FALCON\_PM\_SEL                                                         | 0x545010A8 | 0x04  |
| FALCON\_HOST\_IO\_INDEX                                                 | 0x545010AC | 0x04  |
| [FALCON\_EXCI](#FALCON_EXCI "wikilink")                                 | 0x545010D0 | 0x04  |
| [FALCON\_CPUCTL](#FALCON_CPUCTL "wikilink")                             | 0x54501100 | 0x04  |
| [FALCON\_BOOTVEC](#FALCON_BOOTVEC "wikilink")                           | 0x54501104 | 0x04  |
| [FALCON\_HWCFG](#FALCON_HWCFG "wikilink")                               | 0x54501108 | 0x04  |
| [FALCON\_DMACTL](#FALCON_DMACTL "wikilink")                             | 0x5450110C | 0x04  |
| [FALCON\_DMATRFBASE](#FALCON_DMATRFBASE "wikilink")                     | 0x54501110 | 0x04  |
| [FALCON\_DMATRFMOFFS](#FALCON_DMATRFMOFFS "wikilink")                   | 0x54501114 | 0x04  |
| [FALCON\_DMATRFCMD](#FALCON_DMATRFCMD "wikilink")                       | 0x54501118 | 0x04  |
| [FALCON\_DMATRFFBOFFS](#FALCON_DMATRFFBOFFS "wikilink")                 | 0x5450111C | 0x04  |
| [FALCON\_DMATRFSTAT](#FALCON_DMATRFSTAT "wikilink")                     | 0x54501120 | 0x04  |
| [FALCON\_CRYPTTRFSTAT](#FALCON_CRYPTTRFSTAT "wikilink")                 | 0x54501124 | 0x04  |
| FALCON\_CPUSTAT                                                         | 0x54501128 | 0x04  |
| [FALCON\_HWCFG2](#FALCON_HWCFG2 "wikilink")                             | 0x5450112C | 0x04  |
| FALCON\_CPUCTL\_ALIAS                                                   | 0x54501130 | 0x04  |
| FALCON\_TLB\_CMD                                                        | 0x54501140 | 0x04  |
| FALCON\_TLB\_CMD\_RES                                                   | 0x54501144 | 0x04  |
| FALCON\_BRANCH\_HISTORY\_CTRL                                           | 0x54501148 | 0x04  |
| FALCON\_BRANCH\_HISTORY\_PC                                             | 0x5450114C | 0x04  |
| FALCON\_IMFILLRNG0                                                      | 0x54501150 | 0x04  |
| FALCON\_IMFILLRNG1                                                      | 0x54501154 | 0x04  |
| FALCON\_IMFILLCTL                                                       | 0x54501158 | 0x04  |
| FALCON\_EXTERRWIN                                                       | 0x54501160 | 0x04  |
| FALCON\_EXTERRCFG                                                       | 0x54501164 | 0x04  |
| FALCON\_EXTERRADDR                                                      | 0x54501168 | 0x04  |
| FALCON\_EXTERRSTAT                                                      | 0x5450116C | 0x04  |
| FALCON\_CG2                                                             | 0x5450117C | 0x04  |
| FALCON\_CODE\_INDEX                                                     | 0x54501180 | 0x04  |
| FALCON\_CODE                                                            | 0x54501184 | 0x04  |
| FALCON\_CODE\_VIRT\_ADDR                                                | 0x54501188 | 0x04  |
| FALCON\_DATA\_INDEX0                                                    | 0x545011C0 | 0x04  |
| FALCON\_DATA0                                                           | 0x545011C4 | 0x04  |
| FALCON\_DATA\_INDEX1                                                    | 0x545011C8 | 0x04  |
| FALCON\_DATA1                                                           | 0x545011CC | 0x04  |
| FALCON\_DATA\_INDEX2                                                    | 0x545011D0 | 0x04  |
| FALCON\_DATA2                                                           | 0x545011D4 | 0x04  |
| FALCON\_DATA\_INDEX3                                                    | 0x545011D8 | 0x04  |
| FALCON\_DATA3                                                           | 0x545011DC | 0x04  |
| FALCON\_DATA\_INDEX4                                                    | 0x545011E0 | 0x04  |
| FALCON\_DATA4                                                           | 0x545011E4 | 0x04  |
| FALCON\_DATA\_INDEX5                                                    | 0x545011E8 | 0x04  |
| FALCON\_DATA5                                                           | 0x545011EC | 0x04  |
| FALCON\_DATA\_INDEX6                                                    | 0x545011F0 | 0x04  |
| FALCON\_DATA6                                                           | 0x545011F4 | 0x04  |
| FALCON\_DATA\_INDEX7                                                    | 0x545011F8 | 0x04  |
| FALCON\_DATA7                                                           | 0x545011FC | 0x04  |
| [FALCON\_ICD\_CMD](#FALCON_ICD_CMD "wikilink")                          | 0x54501200 | 0x04  |
| FALCON\_ICD\_ADDR                                                       | 0x54501204 | 0x04  |
| FALCON\_ICD\_WDATA                                                      | 0x54501208 | 0x04  |
| FALCON\_ICD\_RDATA                                                      | 0x5450120C | 0x04  |
| [FALCON\_SCTL](#FALCON_SCTL "wikilink")                                 | 0x54501240 | 0x04  |
| [TSEC\_SCP\_CTL\_ACCESS](#TSEC_SCP_CTL_ACCESS "wikilink")               | 0x54501400 | 0x04  |
| TSEC\_SCP\_UNK0                                                         | 0x54501404 | 0x04  |
| [TSEC\_SCP\_CTL\_STAT](#TSEC_SCP_CTL_STAT "wikilink")                   | 0x54501408 | 0x04  |
| [TSEC\_SCP\_CTL\_MODE](#TSEC_SCP_CTL_MODE "wikilink")                   | 0x5450140C | 0x04  |
| TSEC\_SCP\_UNK1                                                         | 0x54501410 | 0x04  |
| [TSEC\_SCP\_CTL\_PKEY](#TSEC_SCP_CTL_PKEY "wikilink")                   | 0x54501418 | 0x04  |
| TSEC\_SCP\_UNK2                                                         | 0x54501420 | 0x04  |
| [TSEC\_SCP\_SEQ\_STAT](#TSEC_SCP_SEQ_STAT "wikilink")                   | 0x54501428 | 0x04  |
| [TSEC\_SCP\_INSN\_STAT](#TSEC_SCP_INSN_STAT "wikilink")                 | 0x54501430 | 0x04  |
| TSEC\_SCP\_UNK3                                                         | 0x54501454 | 0x04  |
| TSEC\_SCP\_AES\_STAT                                                    | 0x54501458 | 0x04  |
| TSEC\_SCP\_UNK4                                                         | 0x54501470 | 0x04  |
| [TSEC\_SCP\_IRQSTAT](#TSEC_SCP_IRQSTAT "wikilink")                      | 0x54501480 | 0x04  |
| [TSEC\_SCP\_IRQMASK](#TSEC_SCP_IRQMASK "wikilink")                      | 0x54501484 | 0x04  |
| TSEC\_SCP\_UNK5                                                         | 0x54501490 | 0x04  |
| [TSEC\_SCP\_ERR](#TSEC_SCP_ERR "wikilink")                              | 0x54501498 | 0x04  |
| TSEC\_UNK0                                                              | 0x54501500 | 0x04  |
| TSEC\_UNK1                                                              | 0x54501504 | 0x04  |
| TSEC\_UNK2                                                              | 0x5450150C | 0x04  |
| TSEC\_UNK3                                                              | 0x54501510 | 0x04  |
| TSEC\_UNK4                                                              | 0x54501514 | 0x04  |
| TSEC\_UNK5                                                              | 0x54501518 | 0x04  |
| TSEC\_UNK6                                                              | 0x5450151C | 0x04  |
| TSEC\_UNK7                                                              | 0x54501528 | 0x04  |
| TSEC\_UNK8                                                              | 0x5450152C | 0x04  |
| TSEC\_TFBIF\_UNK0                                                       | 0x54501600 | 0x04  |
| [TSEC\_TFBIF\_MCCIF\_FIFOCTRL](#TSEC_TFBIF_MCCIF_FIFOCTRL "wikilink")   | 0x54501604 | 0x04  |
| TSEC\_TFBIF\_UNK1                                                       | 0x54501608 | 0x04  |
| TSEC\_TFBIF\_UNK2                                                       | 0x5450160C | 0x04  |
| TSEC\_TFBIF\_UNK3                                                       | 0x54501630 | 0x04  |
| [TSEC\_TFBIF\_MCCIF\_FIFOCTRL1](#TSEC_TFBIF_MCCIF_FIFOCTRL1 "wikilink") | 0x54501634 | 0x04  |
| TSEC\_TFBIF\_UNK4                                                       | 0x54501640 | 0x04  |
| [TSEC\_TFBIF\_UNK5](#TSEC_TFBIF_UNK5 "wikilink")                        | 0x54501644 | 0x04  |
| [TSEC\_TFBIF\_UNK6](#TSEC_TFBIF_UNK6 "wikilink")                        | 0x54501648 | 0x04  |
| [TSEC\_DMA\_CMD](#TSEC_DMA_CMD "wikilink")                              | 0x54501700 | 0x04  |
| [TSEC\_DMA\_ADDR](#TSEC_DMA_ADDR "wikilink")                            | 0x54501704 | 0x04  |
| [TSEC\_DMA\_VAL](#TSEC_DMA_VAL "wikilink")                              | 0x54501708 | 0x04  |
| [TSEC\_DMA\_UNK](#TSEC_DMA_UNK "wikilink")                              | 0x5450170C | 0x04  |
| TSEC\_TEGRA\_FALCON\_IP\_VER                                            | 0x54501800 | 0x04  |
| TSEC\_TEGRA\_UNK0                                                       | 0x54501824 | 0x04  |
| TSEC\_TEGRA\_UNK1                                                       | 0x54501828 | 0x04  |
| TSEC\_TEGRA\_UNK2                                                       | 0x5450182C | 0x04  |
| [TSEC\_TEGRA\_CTL](#TSEC_TEGRA_CTL "wikilink")                          | 0x54501838 | 0x04  |

### TSEC\_THI\_METHOD0

| ID    | Method                               |
| ----- | ------------------------------------ |
| 0x200 | SET\_APPLICATION\_ID                 |
| 0x300 | EXECUTE                              |
| 0x500 | HDCP\_INIT                           |
| 0x504 | HDCP\_CREATE\_SESSION                |
| 0x508 | HDCP\_VERIFY\_CERT\_RX               |
| 0x50C | HDCP\_GENERATE\_EKM                  |
| 0x510 | HDCP\_REVOCATION\_CHECK              |
| 0x514 | HDCP\_VERIFY\_HPRIME                 |
| 0x518 | HDCP\_ENCRYPT\_PAIRING\_INFO         |
| 0x51C | HDCP\_DECRYPT\_PAIRING\_INFO         |
| 0x520 | HDCP\_UPDATE\_SESSION                |
| 0x524 | HDCP\_GENERATE\_LC\_INIT             |
| 0x528 | HDCP\_VERIFY\_LPRIME                 |
| 0x52C | HDCP\_GENERATE\_SKE\_INIT            |
| 0x530 | HDCP\_VERIFY\_VPRIME                 |
| 0x534 | HDCP\_ENCRYPTION\_RUN\_CTRL          |
| 0x538 | HDCP\_SESSION\_CTRL                  |
| 0x53C | HDCP\_COMPUTE\_SPRIME                |
| 0x540 | HDCP\_GET\_CERT\_RX                  |
| 0x544 | HDCP\_EXCHANGE\_INFO                 |
| 0x548 | HDCP\_DECRYPT\_KM                    |
| 0x54C | HDCP\_GET\_HPRIME                    |
| 0x550 | HDCP\_GENERATE\_EKH\_KM              |
| 0x554 | HDCP\_VERIFY\_RTT\_CHALLENGE         |
| 0x558 | HDCP\_GET\_LPRIME                    |
| 0x55C | HDCP\_DECRYPT\_KS                    |
| 0x560 | HDCP\_DECRYPT                        |
| 0x564 | HDCP\_GET\_RRX                       |
| 0x568 | HDCP\_DECRYPT\_REENCRYPT             |
| 0x56C |                                      |
| 0x570 |                                      |
| 0x574 |                                      |
| 0x578 |                                      |
| 0x57C |                                      |
| 0x700 | HDCP\_VALIDATE\_SRM                  |
| 0x704 | HDCP\_VALIDATE\_STREAM               |
| 0x708 | HDCP\_TEST\_SECURE\_STATUS           |
| 0x70C | HDCP\_SET\_DCP\_KPUB                 |
| 0x710 | HDCP\_SET\_RX\_KPUB                  |
| 0x714 | HDCP\_SET\_CERT\_RX                  |
| 0x718 | HDCP\_SET\_SCRATCH\_BUFFER           |
| 0x71C | HDCP\_SET\_SRM                       |
| 0x720 | HDCP\_SET\_RECEIVER\_ID\_LIST        |
| 0x724 | HDCP\_SET\_SPRIME                    |
| 0x728 | HDCP\_SET\_ENC\_INPUT\_BUFFER        |
| 0x72C | HDCP\_SET\_ENC\_OUTPUT\_BUFFER       |
| 0x730 | HDCP\_GET\_RTT\_CHALLENGE            |
| 0x734 | HDCP\_STREAM\_MANAGE                 |
| 0x738 | HDCP\_READ\_CAPS                     |
| 0x73C | HDCP\_ENCRYPT                        |
| 0x740 | \[6.0.0+\] HDCP\_GET\_CURRENT\_NONCE |

Used to encode and send a method's ID over HOST1X to TSEC. This register
mirrors the functionality of HOST1X's channel opcode submission.

### TSEC\_THI\_METHOD1

Used to encode and send a method's data over HOST1X to TSEC. This
register mirrors the functionality of HOST1X's channel opcode
submission.

### TSEC\_THI\_INT\_STATUS

| Bits | Description                         |
| ---- | ----------------------------------- |
| 0    | TSEC\_THI\_INT\_STATUS\_FALCON\_INT |

### TSEC\_THI\_INT\_MASK

| Bits | Description                       |
| ---- | --------------------------------- |
| 0    | TSEC\_THI\_INT\_MASK\_FALCON\_INT |

### FALCON\_IRQSSET

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQSSET\_GPTMR  |
| 1    | FALCON\_IRQSSET\_WDTMR  |
| 2    | FALCON\_IRQSSET\_MTHD   |
| 3    | FALCON\_IRQSSET\_CTXSW  |
| 4    | FALCON\_IRQSSET\_HALT   |
| 5    | FALCON\_IRQSSET\_EXTERR |
| 6    | FALCON\_IRQSSET\_SWGEN0 |
| 7    | FALCON\_IRQSSET\_SWGEN1 |
| 8-15 | FALCON\_IRQSSET\_EXT    |

Used for setting Falcon's IRQs.

### FALCON\_IRQSCLR

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQSCLR\_GPTMR  |
| 1    | FALCON\_IRQSCLR\_WDTMR  |
| 2    | FALCON\_IRQSCLR\_MTHD   |
| 3    | FALCON\_IRQSCLR\_CTXSW  |
| 4    | FALCON\_IRQSCLR\_HALT   |
| 5    | FALCON\_IRQSCLR\_EXTERR |
| 6    | FALCON\_IRQSCLR\_SWGEN0 |
| 7    | FALCON\_IRQSCLR\_SWGEN1 |
| 8-15 | FALCON\_IRQSCLR\_EXT    |

Used for clearing Falcon's IRQs.

### FALCON\_IRQSTAT

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQSTAT\_GPTMR  |
| 1    | FALCON\_IRQSTAT\_WDTMR  |
| 2    | FALCON\_IRQSTAT\_MTHD   |
| 3    | FALCON\_IRQSTAT\_CTXSW  |
| 4    | FALCON\_IRQSTAT\_HALT   |
| 5    | FALCON\_IRQSTAT\_EXTERR |
| 6    | FALCON\_IRQSTAT\_SWGEN0 |
| 7    | FALCON\_IRQSTAT\_SWGEN1 |
| 8-15 | FALCON\_IRQSTAT\_EXT    |

Used for getting the status of Falcon's IRQs.

### FALCON\_IRQMODE

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQMODE\_GPTMR  |
| 1    | FALCON\_IRQMODE\_WDTMR  |
| 2    | FALCON\_IRQMODE\_MTHD   |
| 3    | FALCON\_IRQMODE\_CTXSW  |
| 4    | FALCON\_IRQMODE\_HALT   |
| 5    | FALCON\_IRQMODE\_EXTERR |
| 6    | FALCON\_IRQMODE\_SWGEN0 |
| 7    | FALCON\_IRQMODE\_SWGEN1 |
| 8-15 | FALCON\_IRQMODE\_EXT    |

Used for changing the mode Falcon's IRQs. A value of 1 means level
triggered while a value of 0 means edge triggered.

### FALCON\_IRQMSET

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQMSET\_GPTMR  |
| 1    | FALCON\_IRQMSET\_WDTMR  |
| 2    | FALCON\_IRQMSET\_MTHD   |
| 3    | FALCON\_IRQMSET\_CTXSW  |
| 4    | FALCON\_IRQMSET\_HALT   |
| 5    | FALCON\_IRQMSET\_EXTERR |
| 6    | FALCON\_IRQMSET\_SWGEN0 |
| 7    | FALCON\_IRQMSET\_SWGEN1 |
| 8-15 | FALCON\_IRQMSET\_EXT    |

Used for setting the mask for Falcon's IRQs.

### FALCON\_IRQMCLR

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQMCLR\_GPTMR  |
| 1    | FALCON\_IRQMCLR\_WDTMR  |
| 2    | FALCON\_IRQMCLR\_MTHD   |
| 3    | FALCON\_IRQMCLR\_CTXSW  |
| 4    | FALCON\_IRQMCLR\_HALT   |
| 5    | FALCON\_IRQMCLR\_EXTERR |
| 6    | FALCON\_IRQMCLR\_SWGEN0 |
| 7    | FALCON\_IRQMCLR\_SWGEN1 |
| 8-15 | FALCON\_IRQMCLR\_EXT    |

Used for clearing the mask for Falcon's IRQs.

### FALCON\_IRQMASK

| Bits | Description             |
| ---- | ----------------------- |
| 0    | FALCON\_IRQMASK\_GPTMR  |
| 1    | FALCON\_IRQMASK\_WDTMR  |
| 2    | FALCON\_IRQMASK\_MTHD   |
| 3    | FALCON\_IRQMASK\_CTXSW  |
| 4    | FALCON\_IRQMASK\_HALT   |
| 5    | FALCON\_IRQMASK\_EXTERR |
| 6    | FALCON\_IRQMASK\_SWGEN0 |
| 7    | FALCON\_IRQMASK\_SWGEN1 |
| 8-15 | FALCON\_IRQMASK\_EXT    |

Used for getting the value of the mask for Falcon's IRQs.

### FALCON\_IRQDEST

| Bits  | Description                     |
| ----- | ------------------------------- |
| 0     | FALCON\_IRQDEST\_HOST\_GPTMR    |
| 1     | FALCON\_IRQDEST\_HOST\_WDTMR    |
| 2     | FALCON\_IRQDEST\_HOST\_MTHD     |
| 3     | FALCON\_IRQDEST\_HOST\_CTXSW    |
| 4     | FALCON\_IRQDEST\_HOST\_HALT     |
| 5     | FALCON\_IRQDEST\_HOST\_EXTERR   |
| 6     | FALCON\_IRQDEST\_HOST\_SWGEN0   |
| 7     | FALCON\_IRQDEST\_HOST\_SWGEN1   |
| 8-15  | FALCON\_IRQDEST\_HOST\_EXT      |
| 16    | FALCON\_IRQDEST\_TARGET\_GPTMR  |
| 17    | FALCON\_IRQDEST\_TARGET\_WDTMR  |
| 18    | FALCON\_IRQDEST\_TARGET\_MTHD   |
| 19    | FALCON\_IRQDEST\_TARGET\_CTXSW  |
| 20    | FALCON\_IRQDEST\_TARGET\_HALT   |
| 21    | FALCON\_IRQDEST\_TARGET\_EXTERR |
| 22    | FALCON\_IRQDEST\_TARGET\_SWGEN0 |
| 23    | FALCON\_IRQDEST\_TARGET\_SWGEN1 |
| 24-31 | FALCON\_IRQDEST\_TARGET\_EXT    |

Used for routing Falcon's IRQs.

### FALCON\_SCRATCH0

Scratch register for reading/writing data to Falcon.

### FALCON\_SCRATCH1

Scratch register for reading/writing data to Falcon.

### FALCON\_ITFEN

| Bits | Description           |
| ---- | --------------------- |
| 0    | FALCON\_ITFEN\_CTXEN  |
| 1    | FALCON\_ITFEN\_MTHDEN |

Used for enabling/disabling Falcon interfaces.

### FALCON\_IDLESTATE

| Bits | Description                     |
| ---- | ------------------------------- |
| 0    | FALCON\_IDLESTATE\_FALCON\_BUSY |
| 1-15 | FALCON\_IDLESTATE\_EXT\_BUSY    |

Used for detecting if Falcon is busy or not.

### FALCON\_DEBUGINFO

Used for UCODE self revocation. This register takes the base address of
the GSC carveout shifted right by 8.

\[6.0.0+\] [nvservices](NV%20services.md "wikilink") sets this to
0x8005FF00 \>\> 8 (physical DRAM address inside the GPU UCODE carveout)
before starting the nvhost\_tsec firmware.

### FALCON\_EXCI

Contains information about raised exceptions.

### FALCON\_CPUCTL

| Bits | Description              |
| ---- | ------------------------ |
| 0    | FALCON\_CPUCTL\_IINVAL   |
| 1    | FALCON\_CPUCTL\_STARTCPU |
| 2    | FALCON\_CPUCTL\_SRESET   |
| 3    | FALCON\_CPUCTL\_HRESET   |
| 4    | FALCON\_CPUCTL\_HALTED   |
| 5    | FALCON\_CPUCTL\_STOPPED  |
| 6    | FALCON\_CPUCTL\_SCP\_UNK |

Used for signaling the Falcon CPU.

### FALCON\_BOOTVEC

Takes the Falcon's boot vector address.

### FALCON\_HWCFG

| Bits  | Description                  |
| ----- | ---------------------------- |
| 0-8   | FALCON\_HWCFG\_IMEM\_SIZE    |
| 9-17  | FALCON\_HWCFG\_DMEM\_SIZE    |
| 18-25 | FALCON\_HWCFG\_MTHD\_SIZE    |
| 26-31 | FALCON\_HWCFG\_DMATRF\_SLOTS |

### FALCON\_DMACTL

| Bits | Description                     |
| ---- | ------------------------------- |
| 0    | FALCON\_DMACTL\_REQUIRE\_CTX    |
| 1    | FALCON\_DMACTL\_DMEM\_SCRUBBING |
| 2    | FALCON\_DMACTL\_IMEM\_SCRUBBING |
| 3-6  | FALCON\_DMACTL\_DMAQ\_NUM       |
| 7    | FALCON\_DMACTL\_SECURE\_STAT    |

Used for configuring the Falcon's DMA engine.

### FALCON\_DMATRFBASE

Takes the host's base address for transferring data to/from the Falcon
(DMA).

### FALCON\_DMATRFMOFFS

Takes the offset for the host's source memory being transferred.

### FALCON\_DMATRFCMD

| Bits  | Description               |
| ----- | ------------------------- |
| 0     | FALCON\_DMATRFCMD\_FULL   |
| 1     | FALCON\_DMATRFCMD\_IDLE   |
| 2-3   | FALCON\_DMATRFCMD\_SEC    |
| 4     | FALCON\_DMATRFCMD\_IMEM   |
| 5     | FALCON\_DMATRFCMD\_WRITE  |
| 8-10  | FALCON\_DMATRFCMD\_SIZE   |
| 12-14 | FALCON\_DMATRFCMD\_CTXDMA |

Used for configuring DMA transfers.

### FALCON\_DMATRFFBOFFS

Takes the offset for Falcon's target memory being transferred.

### FALCON\_DMATRFSTAT

| Bits  | Description                              |
| ----- | ---------------------------------------- |
| 0     | FALCON\_DMATRFSTAT\_PENDING              |
| 16-18 | FALCON\_DMATRFSTAT\_NUM\_STORES\_PENDING |
| 24-26 | FALCON\_DMATRFSTAT\_NUM\_LOADS\_PENDING  |

### FALCON\_CRYPTTRFSTAT

| Bits  | Description                                |
| ----- | ------------------------------------------ |
| 1     | FALCON\_CRYPTTRFSTAT\_PENDING              |
| 5     | FALCON\_CRYPTTRFSTAT\_ENABLED              |
| 16-18 | FALCON\_CRYPTTRFSTAT\_NUM\_STORES\_PENDING |
| 24-26 | FALCON\_CRYPTTRFSTAT\_NUM\_LOADS\_PENDING  |

### FALCON\_HWCFG2

| Bits  | Description                     |
| ----- | ------------------------------- |
| 0-3   | FALCON\_HWCFG2\_VERSION         |
| 4-5   | FALCON\_HWCFG2\_SCP\_MODE       |
| 6-7   | FALCON\_HWCFG2\_SUBVERSION      |
| 8-11  | FALCON\_HWCFG2\_IMEM\_PORTS     |
| 12-15 | FALCON\_HWCFG2\_DMEM\_PORTS     |
| 16-19 | FALCON\_HWCFG2\_VM\_PAGES\_LOG2 |

### FALCON\_ICD\_CMD

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-3</p></td>
<td><p>FALCON_ICD_CMD_OPC</p>
<p><code>0x0: BREAK</code><br />
<code>0x1: CONTINUE_FROM_PC</code><br />
<code>0x2: CONTINUE_FROM_ADDR</code><br />
<code>0x3: CONTINUE_UNK1_FROM_PC</code><br />
<code>0x4: CONTINUE_UNK1_FROM_ADDR</code><br />
<code>0x5: SINGLE_STEP_FROM_PC</code><br />
<code>0x6: SINGLE_STEP_FROM_ADDR</code><br />
<code>0x7: SET_BREAK_MASK</code><br />
<code>0x8: REG_READ</code><br />
<code>0x9: REG_WRITE</code><br />
<code>0xA: DATA_READ</code><br />
<code>0xB: DATA_WRITE</code><br />
<code>0xC: IO_READ</code><br />
<code>0xD: IO_WRITE</code><br />
<code>0xE: STATUS_READ</code></p></td>
</tr>
<tr class="even">
<td><p>6-7</p></td>
<td><p>FALCON_ICD_CMD_DATA_SIZE</p></td>
</tr>
<tr class="odd">
<td><p>8-12</p></td>
<td><p>FALCON_ICD_CMD_IDX</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p>FALCON_ICD_CMD_ERROR</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p>FALCON_ICD_CMD_DONE</p></td>
</tr>
<tr class="even">
<td><p>16-31</p></td>
<td><p>FALCON_ICD_CMD_BREAK_MASK</p></td>
</tr>
</tbody>
</table>

### FALCON\_SCTL

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-1</p></td>
<td><p>FALCON_SCTL_SEC_MODE</p>
<p><code>0: Non-secure</code><br />
<code>1: Light Secure</code><br />
<code>2: Heavy Secure</code></p></td>
</tr>
</tbody>
</table>

### TSEC\_SCP\_CTL\_ACCESS

| Bits | Description                           |
| ---- | ------------------------------------- |
| 20   | Enable TSEC\_SCP\_INSN\_STAT register |

### TSEC\_SCP\_CTL\_STAT

| Bits | Description                       |
| ---- | --------------------------------- |
| 20   | TSEC\_SCP\_CTL\_STAT\_DEBUG\_MODE |

### TSEC\_SCP\_CTL\_MODE

| Bits | Description                                 |
| ---- | ------------------------------------------- |
| 0    | Disable reads for the UNK register block    |
| 1    | Disable reads for the TFBIF register block  |
| 2    | Disable reads for the DMA register block    |
| 3    | Disable reads for the TEGRA register block  |
| 4    | Disable writes for the UNK register block   |
| 5    | Disable writes for the TFBIF register block |
| 6    | Disable writes for the DMA register block   |
| 7    | Disable writes for the TEGRA register block |

Controls accesses to the other sub-engines and can only be cleared in
Heavy Secure mode.

### TSEC\_SCP\_CTL\_PKEY

| Bits | Description                           |
| ---- | ------------------------------------- |
| 0    | TSEC\_SCP\_CTL\_PKEY\_REQUEST\_RELOAD |
| 1    | TSEC\_SCP\_CTL\_PKEY\_LOADED          |

### TSEC\_SCP\_SEQ\_STAT

| Bits  | Description                                                    |
| ----- | -------------------------------------------------------------- |
| 0     | Set if crypto sequence recording (cs0begin/cs1begin) is active |
| 4-7   | Number of instructions left for the crypto sequence            |
| 12-15 | Active crypto key register                                     |

Contains information on the last crypto sequence (cs0 or cs1) executed.

### TSEC\_SCP\_INSN\_STAT

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-7</p></td>
<td><p>Crypto fuc5 destination register or immediate value</p></td>
</tr>
<tr class="even">
<td><p>8-15</p></td>
<td><p>Crypto fuc5 source register or immediate value</p></td>
</tr>
<tr class="odd">
<td><p>16-30</p></td>
<td><p>Crypto fuc5 operation</p>
<p><code>0x0000: none (fuc5 opcode 0x00) </code><br />
<code>0x0010: cmov (fuc5 opcode 0x84)</code><br />
<code>0x0020: cxsin (fuc5 opcode 0x88) or xdst (with cxset)</code><br />
<code>0x0030: cxsout (fuc5 opcode 0x8C) or xdld (with cxset) </code><br />
<code>0x0040: crng (fuc5 opcode 0x90)</code><br />
<code>0x0050: cs0begin (fuc5 opcode 0x94)</code><br />
<code>0x0060: cs0exec (fuc5 opcode 0x98)</code><br />
<code>0x0070: cs1begin (fuc5 opcode 0x9C)</code><br />
<code>0x0080: cs1exec (fuc5 opcode 0xA0)</code><br />
<code>0x0090: invalid (fuc5 opcode 0xA4)</code><br />
<code>0x00A0: cchmod (fuc5 opcode 0xA8)</code><br />
<code>0x00B0: cxor (fuc5 opcode 0xAC)</code><br />
<code>0x00C0: cadd (fuc5 opcode 0xB0)</code><br />
<code>0x00D0: cand (fuc5 opcode 0xB4)</code><br />
<code>0x00E0: crev (fuc5 opcode 0xB8)</code><br />
<code>0x00F0: cprecmac (fuc5 opcode 0xBC)</code><br />
<code>0x0100: csecret (fuc5 opcode 0xC0)</code><br />
<code>0x0110: ckeyreg (fuc5 opcode 0xC4)</code><br />
<code>0x0120: ckexp (fuc5 opcode 0xC8)</code><br />
<code>0x0130: ckrexp (fuc5 opcode 0xCC)</code><br />
<code>0x0140: cenc (fuc5 opcode 0xD0)</code><br />
<code>0x0150: cdec (fuc5 opcode 0xD4)</code><br />
<code>0x0160: csigunk (fuc5 opcode 0xD8)</code><br />
<code>0x0170: csigenc (fuc5 opcode 0xDC)</code><br />
<code>0x0180: csigclr (fuc5 opcode 0xE0)</code></p></td>
</tr>
<tr class="even">
<td><p>31</p></td>
<td><p>Set if running in secure mode (cauth)</p></td>
</tr>
</tbody>
</table>

Contains information on the last crypto instruction executed.

### TSEC\_SCP\_IRQSTAT

| Bits | Description                      |
| ---- | -------------------------------- |
| 1    | Unknown                          |
| 8    | TSEC\_SCP\_IRQSTAT\_HALT         |
| 12   | Unknown                          |
| 16   | TSEC\_SCP\_IRQSTAT\_INSN\_ERROR  |
| 20   | TSEC\_SCP\_IRQSTAT\_SINGLE\_STEP |
| 24   | Unknown                          |
| 28   | Unknown                          |

Used for getting the status of crypto IRQs.

### TSEC\_SCP\_IRQMASK

| Bits | Description                      |
| ---- | -------------------------------- |
| 1    | Unknown                          |
| 8    | TSEC\_SCP\_IRQMASK\_HALT         |
| 12   | Unknown                          |
| 16   | TSEC\_SCP\_IRQMASK\_INSN\_ERROR  |
| 20   | TSEC\_SCP\_IRQMASK\_SINGLE\_STEP |
| 24   | Unknown                          |
| 28   | Unknown                          |

Used for getting the value of the mask for crypto IRQs.

### TSEC\_SCP\_ERR

| Bits | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 0    | Invalid instruction                                          |
| 4    | Empty crypto sequence                                        |
| 8    | Crypto sequence is too long                                  |
| 12   | Crypto sequence was not finished                             |
| 16   | Invalid cauth signature (during csigenc, csigclr or csigunk) |
| 24   | Forbidden instruction                                        |

Contains information on crypto errors generated by the
[TSEC\_SCP\_IRQSTAT\_INSN\_ERROR](#TSEC_SCP_IRQSTAT "wikilink") IRQ.

### TSEC\_TFBIF\_MCCIF\_FIFOCTRL

| Bits | Description                                   |
| ---- | --------------------------------------------- |
| 0    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_RCLK\_OVERRIDE  |
| 1    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_WCLK\_OVERRIDE  |
| 2    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_WRCL\_MCLE2X    |
| 3    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_RDMC\_RDFAST    |
| 4    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_WRMC\_CLLE2X    |
| 5    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_RDCL\_RDFAST    |
| 6    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_CCLK\_OVERRIDE  |
| 7    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_RCLK\_OVR\_MODE |
| 8    | TSEC\_TFBIF\_MCCIF\_FIFOCTRL\_WCLK\_OVR\_MODE |

### TSEC\_MCCIF\_FIFOCTRL1

| Bits  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| 0-15  | TSEC\_TFBIF\_MCCIF\_FIFOCTRL1\_SRD2MC\_REORDER\_DEPTH\_LIMIT |
| 16-31 | TSEC\_TFBIF\_MCCIF\_FIFOCTRL1\_SWR2MC\_REORDER\_DEPTH\_LIMIT |

### TSEC\_TFBIF\_UNK5

Used to control accesses to DRAM.

\[6.0.0+\] The nvhost\_tsec firmware sets this register to 0x10 or
0x111110 before reading memory from the GPU UCODE carveout.

### TSEC\_TFBIF\_UNK6

Used to control accesses to DRAM.

\[6.0.0+\] The nvhost\_tsec firmware sets this register to (data\_size
\<\< 4) before reading memory from the GPU UCODE carveout.

### TSEC\_DMA\_CMD

| Bits | Description           |
| ---- | --------------------- |
| 0    | TSEC\_DMA\_CMD\_READ  |
| 1    | TSEC\_DMA\_CMD\_WRITE |
| 4-7  | TSEC\_DMA\_CMD\_UNK   |
| 12   | TSEC\_DMA\_CMD\_BUSY  |
| 13   | TSEC\_DMA\_CMD\_ERROR |
| 31   | TSEC\_DMA\_CMD\_INIT  |

A DMA read/write operation requires bits TSEC\_DMA\_CMD\_INIT and
TSEC\_DMA\_CMD\_READ/TSEC\_DMA\_CMD\_WRITE to be set in TSEC\_DMA\_CMD.

During the transfer, the TSEC\_DMA\_CMD\_BUSY bit is set.

Accessing an invalid address causes bit TSEC\_DMA\_CMD\_ERROR to be set.

### TSEC\_DMA\_ADDR

Takes the address for DMA transfers between TSEC and HOST1X (master and
clients).

### TSEC\_DMA\_VAL

Takes the value for DMA transfers between TSEC and HOST1X (master and
clients).

### TSEC\_DMA\_UNK

Always 0xFFF.

### TSEC\_TEGRA\_CTL

| Bits | Description                                      |
| ---- | ------------------------------------------------ |
| 16   | TSEC\_TEGRA\_CTL\_TKFI\_KFUSE                    |
| 17   | TSEC\_TEGRA\_CTL\_TKFI\_RESTART\_FSM\_KFUSE      |
| 24   | TSEC\_TEGRA\_CTL\_TMPI\_FORCE\_IDLE\_INPUTS\_I2C |
| 25   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_HOST1X     |
| 26   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_APB        |
| 27   | TSEC\_TEGRA\_CTL\_TMPI\_DISABLE\_OUTPUT\_I2C     |

# Boot Process

TSEC is configured and initialized by the first bootloader during key
generation.

\[6.2.0+\] TSEC is now configured at the end of the first bootloader's
main function.

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

\[6.2.0+\] The transfer base address and size of the Falcon firmware
code changed.

`// Set DMA transfer base address to 0x40010E00 >> 0x08`  
`*(u32 *)FALCON_DMATRFBASE = 0x40010E;`  
  
`u32 trf_mode = 0;     // A value of 0 sets FALCON_DMATRFCMD_IMEM`  
`u32 dst_offset = 0;`  
`u32 src_offset = 0;`  
  
`// Load code into Falcon (0x100 bytes at a time)`  
`while (src_offset < 0x2900)`  
`{`  
`   flcn_load_firm(trf_mode, src_offset, dst_offset);`  
`   src_offset += 0x100;`  
`   dst_offset += 0x100;`  
`}`

## Firmware booting

Falcon is booted up and the first bootloader waits for it to
finish.

`// Set magic value in host1x scratch space`  
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

\[6.2.0+\] Falcon is booted up, but the first bootloader is left in an
infinite loop.

`// Set magic value in host1x scratch space`  
`*(u32 *)0x50003300 = 0x34C2E1DA;`  
  
`// Clear Falcon scratch1 MMIO`  
`*(u32 *)FALCON_SCRATCH1 = 0;`  
  
`// Set Falcon boot key version in scratch0 MMIO`  
`*(u32 *)FALCON_SCRATCH0 = 0x01;`  
  
`// Set Falcon's boot vector address`  
`*(u32 *)FALCON_BOOTVEC = 0;`  
  
`// Signal Falcon's CPU`  
`*(u32 *)FALCON_CPUCTL = 0x02;`  
  
`// Infinite loop`  
`deadlock();`

## TSEC key generation

The TSEC key is generated by reading SOR1 registers modified by the
Falcon CPU.

`// Clear magic value in host1x scratch space`  
`*(u32 *)0x50003300 = 0;`  
  
`// Read TSEC key`  
`u32 tsec_key[4]; `  
`tsec_key[0] = *(u32 *)NV_SOR_DP_HDCP_BKSV_LSB;`  
`tsec_key[1] = *(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB;`  
`tsec_key[2] = *(u32 *)NV_SOR_TMDS_HDCP_CN_MSB;`  
`tsec_key[3] = *(u32 *)NV_SOR_TMDS_HDCP_CN_LSB;`  
  
`// Clear SOR1 registers`  
`*(u32 *)NV_SOR_DP_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_BKSV_LSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_MSB = 0;`  
`*(u32 *)NV_SOR_TMDS_HDCP_CN_LSB = 0;`  
  
`if (out_size < 0x10)`  
`   out_size = 0x10;`  
  
`// Copy back the TSEC key`  
`memcpy(out_buf, tsec_key, out_size);`

\[6.2.0+\] This is now done inside an encrypted TSEC payload.

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
this firmware binary is split into 4 blobs (names are unofficial):
[Boot](#Boot "wikilink") (unencrypted and unauthenticated code),
[KeygenLdr](#KeygenLdr "wikilink") (unencrypted and authenticated code),
[Keygen](#Keygen "wikilink") (encrypted and authenticated code) and [key
data](#Key_data "wikilink").

\[6.2.0+\] There are now 6 blobs (names are unofficial):
[Boot](#Boot "wikilink") (unencrypted and unauthenticated code),
[Loader](#Loader "wikilink") (unencrypted and unauthenticated code),
[KeygenLdr](#KeygenLdr "wikilink") (unencrypted and authenticated code),
[Keygen](#Keygen "wikilink") (encrypted and authenticated code),
[Payload](#Payload "wikilink") (part unencrypted and unauthenticated
code, part encrypted and authenticated code) and [key
data](#Key_data "wikilink").

Firmware can be disassembled with
[envytools'](http://envytools.readthedocs.io/en/latest/)
[envydis](https://github.com/envytools/envytools/tree/master/envydis):

`envydis -i tsec_fw.bin -m falcon -V fuc5 -F crypt`

Note that the instruction set has variable length instructions, and the
disassembler is not very good at detecting locations it should start
disassembling from. One needs to disassemble multiple sub-regions and
join them together.

## Boot

During this stage, [key data](#Key_data "wikilink") is loaded and
[KeygenLdr](#KeygenLdr "wikilink") is authenticated, loaded and
executed. Before returning, this stage writes back to the host (using
MMIO registers) and sets the key used by the first bootloader.

\[6.2.0+\] During this stage, [key data](#Key_data "wikilink") is loaded
and execution jumps to [Loader](#Loader "wikilink").

### Initialization

Falcon sets up it's own stack pointer.

`// Read data segment size from IO space`  
`u32 data_seg_size = *(u32 *)UC_CAPS;`  
`data_seg_size >>= 0x09;`  
`data_seg_size &= 0x1FF;`  
`data_seg_size <<= 0x08;`  
  
`// Set the stack pointer`  
`*(u32 *)sp = data_seg_size;`

### Main

Falcon reads the [key data](#Key_data "wikilink") and then
authenticates, loads and executes [KeygenLdr](#KeygenLdr "wikilink")
which sets the TSEC
key.

`u32 boot_base_addr = 0;`  
`u8 key_data_buf[0x7C];`  
  
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
`     xdst(0, (blob1_hash_addr | crypt_reg_flag));`  
`               `  
`     // Wait for all data loads/stores to finish`  
`     xdwait();`  
`         `  
`         // Jump to KeygenLdr`  
`         u32 keygenldr_res = exec_keygenldr(key_buf, key_version, is_blob_dec);`  
`         is_blob_dec = true;  // Set this to prevent decrypting again`  
  
`         // Set boot finish magic on success`  
`     if (keygenldr_res == 0)`  
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
  
`// Overwrite the TSEC key in SOR1 registers`  
`// This has no effect because the KeygenLdr locks out the TSEC DMA engine`  
`tsec_set_key(key_data_buf);`  
  
`return boot_res;`

\[6.2.0+\] Falcon reads the [key data](#Key_data "wikilink") and jumps
to
[Loader](#Loader "wikilink").

`u8 key_data_buf[0x84];`  
  
`// Read the key data from memory`  
`u32 key_data_addr = 0x300;`  
`u32 key_data_size = 0x84;`  
`read_code(key_data_buf, key_data_addr, key_data_size);`  
  
`// Calculate the next blob's address`  
`u32 blob4_size = *(u32 *)(key_data_buf + 0x80);`  
`u32 blob0_size = *(u32 *)(key_data_buf + 0x70);`  
`u32 blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`u32 blob2_size = *(u32 *)(key_data_buf + 0x78);`  
`u32 blob3_addr = ((((blob0_size + blob1_size) + 0x100) + blob2_size) + blob4_size);`  
  
`// Jump to next blob`  
`(void *)blob3_addr();`  
` `  
`return 0;`

#### tsec\_set\_key

This method takes **key\_data\_buf** (a 16 bytes buffer) as argument and
writes its contents to SOR1 registers.

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

## KeygenLdr

This stage is responsible for reconfiguring the Falcon's crypto
co-processor and loading, decrypting, authenticating and executing
[Keygen](#Keygen "wikilink").

### Main

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
`  exit();`  
  
`// Decrypt and load Keygen stage`  
`load_keygen(key_buf, key_version, is_blob_dec);`  
  
`// fuc5 crypt csigclr instruction`  
`// Clears the cauth signature`  
`csigclr();`  
  
`// Clear all crypto registers`  
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

#### load\_keygen

`u32 res = 0;`  
  
`u32 boot_base_addr = 0;`  
`u32 blob0_addr = 0;`  
`u32 blob0_size = *(u32 *)(key_buf + 0x70); `  
  
`// Load blob0 code again`  
`read_code(boot_base_addr, blob0_addr, blob0_size);`  
  
`// Generate "CODE_SIG_01" key into c4 crypto register`  
`gen_usr_key(0, 0);`  
  
`// Encrypt buffer with c4`  
`u8 sig_key[0x10];`  
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
  
`// Decrypt Keygen blob if needed`  
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
`      // Read Keygen encrypted blob`  
`      read_code(boot_base_addr, blob2_addr, blob2_size);`  
  
`      // Generate "CODE_ENC_01" key into c4 crypt register`  
`      gen_usr_key(0x01, 0x01);`  
`      `  
`      u32 src_addr = boot_base_addr;`  
`      u32 src_size = blob2_size;`  
`      u32 iv_addr = key_buf + 0x40;`  
`      u32 dst_addr = boot_base_addr;`  
`      u32 mode = 0;   // AES-128-ECB`  
`      u32 version = 0;`  
`      `  
`      // Decrypt Keygen blob`  
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
`else if (key_version == 0x03)          // Use debug key (empty)`  
`  hovi_key_addr = key_buf + 0x00;`  
`else`  
`  res = 0xD0D0D0D0`  
`   `  
`// Jump to Keygen`  
`if (hovi_key_addr)`  
`  res = exec_keygen(hovi_key_addr, key_version);`  
`         `  
`// Clear out key data`  
`memset(key_buf, 0, 0x7C);`  
  
`// fuc5 crypt cauth instruction`  
`// Restore previous cauth value`  
`cauth(c_old);`  
  
`return res;`

##### gen\_usr\_key

This method takes **type** and **mode** as arguments and generates a
key.

`u8 seed_buf[0x10];`  
  
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

##### enc\_buffer

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

##### do\_crypto

This is the method responsible for all crypto operations performed
during [KeygenLdr](#KeygenLdr "wikilink"). It takes **src\_addr**,
**src\_size**, **iv\_addr**, **dst\_addr**, **mode** and **crypt\_ver**
as
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
  
`// AES-128-CBC decrypt`  
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
`else if (mode == 0x01)     // AES-128-CBC encrypt`  
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
`else if (mode == 0x03)     // AES-128-ECB decrypt`  
`{`  
`  // Create crypto script with 3 instructions`  
`  cs0begin(0x03);`  
`   `  
`  cxsin(c3);                   // Read 0x10 bytes from crypto stream into c3`  
`  cdec(c5, c3);                // Decrypt from c3 into c5`  
`  cxsout(c5);                  // Write 0x10 bytes into crypto stream from c5`  
`}`  
`else if (mode == 0x04)     // AES-128-ECB encrypt`  
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

## Keygen

This stage is decrypted by [KeygenLdr](#KeygenLdr "wikilink") using a
key generated by encrypting a seed with an hardware secret. It will
generate the final TSEC key.

## Loader

This stage starts by authenticating and executing
[KeygenLdr](#KeygenLdr "wikilink") which in turn authenticates, decrypts
and executes [Keygen](#Keygen "wikilink") (both blobs remain unchanged
from previous firmware versions). After the TSEC key has been generated,
execution returns to this stage which then parses and executes
[Payload](#Payload "wikilink").

### Main

`u8 key_data_buf[0x84];`  
`u8 tmp_key_data_buf[0x84];`  
  
`// Read the key data from memory`  
`u32 key_data_addr = 0x300;`  
`u32 key_data_size = 0x84;`  
`read_code(key_data_buf, key_data_addr, key_data_size);`  
  
`// Read the KeygenLdr blob from memory`  
`u32 boot_base_addr = 0;`  
`u32 blob1_addr = 0x400;`  
`u32 blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`read_code(boot_base_addr, blob1_addr, blob1_size);`  
` `  
`// Upload the next code segment into Falcon's CODE region`  
`u32 blob1_virt_addr = 0x300;`  
`bool use_secret = true;`  
`upload_code(blob1_virt_addr, boot_base_addr, blob1_size, blob1_virt_addr, use_secret);`  
  
`// Backup the key data`  
`memcpy(tmp_key_data_buf, key_data_buf, 0x84);`  
  
`// Save previous cauth value`  
`u32 c_old = cauth_old;`  
  
`// fuc5 crypt cauth instruction`  
`// Set auth_addr to 0x300 and auth_size to blob1_size`  
`cauth((blob1_size << 0x10) | (0x300 >> 0x08));`  
  
`// fuc5 crypt cxset instruction`  
`// The next 2 xfer instructions will be overridden`  
`// and target changes from DMA to crypto`  
`cxset(0x02);`  
  
`u32 crypt_reg_flag = 0x00060000;`  
`u32 blob1_hash_addr = tmp_key_data_buf + 0x20; `  
  
`// Transfer data to crypto register c6`  
`xdst(0, (blob1_hash_addr | crypt_reg_flag));`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`u32 key_version = 0x01;`  
`bool is_blob_dec = false;`  
  
`// Jump to KeygenLdr`  
`u32 keygenldr_res = exec_keygenldr(tmp_key_data_buf, key_version, is_blob_dec);`  
  
`// Set boot finish magic on success`  
`if (keygenldr_res == 0)`  
`  keygenldr_res = 0xB0B0B0B0`  
`      `  
`// Write result to FALCON_SCRATCH1`  
`*(u32 *)FALCON_SCRATCH1 = keygenldr_res;`  
  
`if (keygenldr_res != 0xB0B0B0B0)`  
`  return keygenldr_res;`  
  
`// fuc5 crypt cauth instruction`  
`// Restore previous cauth value`  
`cauth(c_old);`  
  
`u8 flcn_hdr_buf[0x18];`  
`u8 flcn_os_hdr_buf[0x10];`  
  
`blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`u32 blob2_size = *(u32 *)(key_data_buf + 0x78);`  
`u32 blob0_size = *(u32 *)(key_data_buf + 0x70);`  
  
`// Read the Payload blob's Falcon header from memory`  
`u32 blob4_flcn_hdr_addr = (((blob0_size + blob1_size) + 0x100) + blob2_size);`  
`read_code(flcn_hdr_buf, blob4_flcn_hdr_addr, 0x18);`  
  
`blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`blob2_size = *(u32 *)(key_data_buf + 0x78);`  
`blob0_size = *(u32 *)(key_data_buf + 0x70);`  
`u32 flcn_hdr_size = *(u32 *)(flcn_hdr_buf + 0x0C);`  
  
`// Read the Payload blob's Falcon OS header from memory`  
`u32 blob4_flcn_os_hdr_addr = ((((blob0_size + blob1_size) + 0x100) + blob2_size) + flcn_hdr_size);`  
`read_code(flcn_os_hdr_buf, blob4_flcn_os_hdr_addr, 0x10);`  
  
`blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`blob2_size = *(u32 *)(key_data_buf + 0x78);`  
`blob0_size = *(u32 *)(key_data_buf + 0x70);`  
`u32 flcn_code_hdr_size = *(u32 *)(flcn_hdr_buf + 0x10);`  
`u32 flcn_os_size = *(u32 *)(flcn_os_hdr_buf + 0x04);`  
  
`// Read the Payload blob's Falcon OS image from memory`  
`u32 blob4_flcn_os_addr = ((((blob0_size + blob1_size) + 0x100) + blob2_size) + flcn_code_hdr_size);`  
`read_code(boot_base_addr, blob4_flcn_os_hdr_addr, flcn_os_size);`  
  
`// Upload the Payload's Falcon OS image boot stub code segment into Falcon's CODE region`  
`u32 blob4_flcn_os_boot_virt_addr = 0;`  
`u32 blob4_flcn_os_boot_size = 0x100;`  
`use_secret = false;`  
`upload_code(blob4_flcn_os_boot_virt_addr, boot_base_addr, blob4_flcn_os_boot_size, blob4_flcn_os_boot_virt_addr, use_secret);`  
  
`flcn_os_size = *(u32 *)(flcn_os_hdr_buf + 0x04); `  
  
`// Upload the Payload blob's Falcon OS encrypted image code segment into Falcon's CODE region`  
`u32 blob4_flcn_os_img_virt_addr = 0x100;`  
`u32 blob4_flcn_os_img_size = (flcn_os_size - 0x100);`  
`use_secret = true;`  
`upload_code(blob4_flcn_os_img_virt_addr, boot_base_addr + 0x100, blob4_flcn_os_img_size, blob4_flcn_os_img_virt_addr, use_secret);`  
  
`// Wait for all code loads to finish`  
`xcwait();`  
  
`blob1_size = *(u32 *)(key_data_buf + 0x74);`  
`blob2_size = *(u32 *)(key_data_buf + 0x78);`  
`blob0_size = *(u32 *)(key_data_buf + 0x70);`  
`flcn_code_hdr_size = *(u32 *)(flcn_hdr_buf + 0x10);`  
`u32 flcn_os_code_size = *(u32 *)(flcn_os_hdr_buf + 0x08);`  
  
`// Read the Payload blob's falcon OS image's hash from memory`  
`u32 blob4_flcn_os_img_hash_addr = (((((blob0_size + blob1_size) + 0x100) + blob2_size) + flcn_code_hdr_size) + flcn_os_code_size);`  
`read_code(0, blob4_flcn_os_img_hash_addr, 0x10);`  
  
`// Read data segment size from IO space`  
`u32 data_seg_size = *(u32 *)UC_CAPS;`  
`data_seg_size >>= 0x03;`  
`data_seg_size &= 0x3FC0;`  
  
`u32 data_addr = 0x10;`  
  
`// Clear all data except the first 0x10 bytes (Payload blob's Falcon OS image's hash)`  
`for (int data_word_count = 0x04; data_word_count < data_seg_size; data_word_count++)`  
`{`  
`  *(u32 *)(data_addr) = 0; `  
`  data_addr += 0x04;`  
`}`  
  
`// Clear all crypto registers`  
`cxor(c0, c0);`  
`cxor(c1, c1);`  
`cxor(c2, c2);`  
`cxor(c3, c3);`  
`cxor(c4, c4);`  
`cxor(c5, c5);`  
`cxor(c6, c6);`  
`cxor(c7, c7);`  
  
`// fuc5 crypt csigclr instruction`  
`// Clears the cauth signature`  
`csigclr();`  
  
`// Jump to Payload`  
`exec_payload();`  
  
`return 0xB0B0B0B0;`

## Payload

This stage prepares the stack then authenticates, decrypts and executes
the Payload blob's Falcon OS
image.

### Main

`// Read data segment size from IO space`  
`u32 data_seg_size = *(u32 *)UC_CAPS;`  
`data_seg_size >>= 0x01;`  
`data_seg_size &= 0xFF00;`  
  
`// Set the stack pointer`  
`*(u32 *)sp = data_seg_size;`  
  
`// Jump to the Payload blob's Falcon OS image boot stub`  
`exec_flcn_os_boot();`  
  
`// Halt execution`  
`exit();`  
  
`return;`

#### exec\_flcn\_os\_boot

`// Read the transfer base address from IO space`  
`u32 xfer_ext_base_addr = *(u32 *)XFER_EXT_BASE;`  
  
`// Copy transfer base address to data memory`  
`u32 scratch_data_addr = 0x300;`  
`*(u32 *)scratch_data_addr = xfer_ext_base_addr;`  
  
`// Set the transfer base address`  
`xcbase(xfer_ext_base_addr);`  
  
`// fuc5 crypt cxset instruction`  
`// The next xfer instruction will be overridden`  
`// and target changes from DMA to crypto`  
`cxset(0x01);`  
  
`u32 crypt_reg_flag = 0x00060000;`  
`u32 blob4_flcn_os_img_hash_addr = 0; `  
  
`// Transfer data to crypto register c6`  
`xdst(0, (blob4_flcn_os_img_hash_addr | crypt_reg_flag));`  
  
`// fuc5 crypt cxset instruction`  
`// The next xfer instruction will be overridden`  
`// and target changes from DMA to crypto`  
`cxset(0x01);`  
  
`// Wait for all data loads/stores to finish`  
`xdwait();`  
  
`cmov(c7, c6);`  
`cxor(c7, c7);`  
  
`// fuc5 crypt cauth instruction`  
`// Set auth_addr to 0x100, auth_size to 0x1300,`  
`// bit 16 (is_secret) and bit 17 (is_encrypted)`  
`cauth((0x02 << 0x10) | (0x01 << 0x10) | (0x1300 << 0x10) | (0x100 >> 0x08));`  
  
`// Clear interrupt flags`  
`*(u8 *)flags_ie0 = 0;`  
`*(u8 *)flags_ie1 = 0;`  
  
`// Jump to the Payload blob's Falcon OS image`  
`exec_flcn_os_img();`  
  
`return 0x0F0F0F0F;`

## Key data

Small buffer stored after the [Boot](#Boot "wikilink") blob and used
across all
stages.

| Offset | Size | Description                                            |
| ------ | ---- | ------------------------------------------------------ |
| 0x00   | 0x10 | Debug key (empty)                                      |
| 0x10   | 0x10 | blob0 ([Boot](#Boot "wikilink")) auth hash             |
| 0x20   | 0x10 | blob1 ([KeygenLdr](#KeygenLdr "wikilink")) auth hash   |
| 0x30   | 0x10 | blob2 ([Keygen](#Keygen "wikilink")) auth hash         |
| 0x40   | 0x10 | blob2 ([Keygen](#Keygen "wikilink")) AES IV            |
| 0x50   | 0x10 | HOVI EKS seed                                          |
| 0x60   | 0x10 | HOVI COMMON seed                                       |
| 0x70   | 0x04 | blob0 ([Boot](#Boot "wikilink")) size                  |
| 0x74   | 0x04 | blob1 ([KeygenLdr](#KeygenLdr "wikilink")) size        |
| 0x78   | 0x04 | blob2 ([Keygen](#Keygen "wikilink")) size              |
| 0x7C   | 0x04 | \[6.2.0+\] blob3 ([Loader](#Loader "wikilink")) size   |
| 0x80   | 0x04 | \[6.2.0+\] blob4 ([Payload](#Payload "wikilink")) size |

## Notes

Part of the information here (which hasn't made it into envytools
documentation yet) was shared by
[mwk](https://wiki.0x04.net/wiki/Marcin_Ko%C5%9Bcielnicki) from reverse
engineering falcon processors over the years.

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

Exit from Authenticated Mode must poke a special register before leaving
authenticated code pages and a failure to do this would result in the
Falcon core halting. Every Falcon based unit (TSEC, NVDEC, VIC) must map
this register in their engine-specific subset of registers. In TSEC's
case, the register is
[TSEC\_SCP\_CTL\_MODE](#TSEC_SCP_CTL_MODE "wikilink").

### csigclr

`00000000: f5 3c 00 e0 csigclr`

This instruction takes no operands and appears to clear the saved cauth
signature used by the csigenc instruction.

### cchmod

`00000000: f5 3c XY a8 cchmod $cY 0X` or `00000000: f5 3c XY a9 cchmod
$cY 1X`

This instruction takes a crypto register and a 5 bit immediate value. It
appears to set the [crypto registers' ACL](#Register_ACLs "wikilink")
bits as follows:

| Bits | Description                                       |
| ---- | ------------------------------------------------- |
| 0    | Allow register to be used as key in NS or LS mode |
| 1    | Allow register to be used as key in HS mode       |
| 2    | Set register as readable in NS or LS mode         |
| 3    | Set register as readable in HS mode               |
| 4    | Set register as writable in NS or LS mode         |

### crng

`00000000: f5 3c 0X 90 crng $cX`

This instruction takes no operands and appears to initialize a crypto
register with random data.

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

| Value | Effect                                           |
| ----- | ------------------------------------------------ |
| 0b000 | falcon data mem \<-\> falcon $cX register        |
| 0b001 | external mem \<-\> crypto input/output stream    |
| 0b011 | falcon data mem \<-\> crypto input/output stream |
| 0b100 | unknown, but can be combined with other types    |

#### DMA-Related Instructions

At least the following instructions may have changed behavior, and count
against the cxset "count" argument: `xdwait`, `xdst`, `xdld`.

For example, if override type=0b000, then the "length" argument to
`xdst` is instead treated as the index of the target $cX register.

### Secrets

Falcon's Authenticated Mode has access to 64 128-bit keys which are
burned at factory. These keys can be loaded by using the $csecret
instruction which takes the target crypto register and the key index as
arguments.

| Index | Notes                                                                                                                                         |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x00  | Used by nvhost\_tsec, nvhost\_nvdec\_bl020\_prod, nvhost\_nvdec020\_prod, nvhost\_nvdec020\_ns and acr\_ucode firmwares. Debug mode only.     |
| 0x01  | Used by nvhost\_nvdec\_bl020\_prod firmware.                                                                                                  |
| 0x03  | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                              |
| 0x04  | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                              |
| 0x05  | Used by nvhost\_tsec, nvhost\_nvdec\_bl020\_prod, nvhost\_nvdec020\_prod, nvhost\_nvdec020\_ns and acr\_ucode firmwares.                      |
| 0x07  | Used by \[6.0.0+\] nvhost\_tsec firmware.                                                                                                     |
| 0x09  | Used by nvhost\_tsec firmware.                                                                                                                |
| 0x0B  | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                              |
| 0x0F  | Used by nvhost\_tsec firmware.                                                                                                                |
| 0x10  | Used by \[1.0.0-5.1.0\] nvhost\_tsec firmware.                                                                                                |
| 0x15  | Used by nvhost\_nvdec\_bl020\_prod, \[5.0.0+\] nvhost\_nvdec020\_prod, \[5.0.0+\] nvhost\_nvdec020\_ns and \[6.0.0+\] nvhost\_tsec firmwares. |
| 0x26  | Used by [KeygenLdr](#KeygenLdr "wikilink").                                                                                                   |
| 0x3C  | Used by nvhost\_tsec firmware.                                                                                                                |
| 0x3F  | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                              |
