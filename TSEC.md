TSEC (Tegra Security Co-processor) is a dedicated unit powered by a
NVIDIA Falcon microprocessor with crypto extensions.

# Driver

A host driver for communicating with the TSEC is mapped to physical
address 0x54500000 with a total size of 0x40000 bytes and exposes
several registers.

## Registers

The TSEC's MMIO space is divided as follows:

  - 0x54500000 to 0x54501000: THI (Tegra Host Interface)
  - 0x54501000 to 0x54501400: [FALCON (Falcon
    microcontroller)](#Falcon "wikilink")
  - 0x54501400 to 0x54501500: [SCP (Secure
    Co-processor)](#SCP "wikilink")
  - 0x54501500 to 0x54501600: RND (Random Number Generator)
  - 0x54501600 to 0x54501680: TFBIF (Tegra Framebuffer Interface)
  - 0x54501680 to 0x54501700: CG (Clock Gate)
  - 0x54501700 to 0x54501800: BAR0 (HOST1X device DMA)
  - 0x54501800 to 0x54501900: TEGRA (Miscellaneous interfaces)

| Name                                                                               | Address    | Width |
| ---------------------------------------------------------------------------------- | ---------- | ----- |
| TSEC\_THI\_INCR\_SYNCPT                                                            | 0x54500000 | 0x04  |
| TSEC\_THI\_INCR\_SYNCPT\_CTRL                                                      | 0x54500004 | 0x04  |
| TSEC\_THI\_INCR\_SYNCPT\_ERR                                                       | 0x54500008 | 0x04  |
| TSEC\_THI\_CTXSW\_INCR\_SYNCPT                                                     | 0x5450000C | 0x04  |
| TSEC\_THI\_CTXSW                                                                   | 0x54500020 | 0x04  |
| TSEC\_THI\_CTXSW\_NEXT                                                             | 0x54500024 | 0x04  |
| TSEC\_THI\_CONT\_SYNCPT\_EOF                                                       | 0x54500028 | 0x04  |
| TSEC\_THI\_CONT\_SYNCPT\_L1                                                        | 0x5450002C | 0x04  |
| TSEC\_THI\_STREAMID0                                                               | 0x54500030 | 0x04  |
| TSEC\_THI\_STREAMID1                                                               | 0x54500034 | 0x04  |
| TSEC\_THI\_THI\_SEC                                                                | 0x54500038 | 0x04  |
| [TSEC\_THI\_METHOD0](#TSEC_THI_METHOD0 "wikilink")                                 | 0x54500040 | 0x04  |
| [TSEC\_THI\_METHOD1](#TSEC_THI_METHOD1 "wikilink")                                 | 0x54500044 | 0x04  |
| TSEC\_THI\_CONTEXT\_SWITCH                                                         | 0x54500060 | 0x04  |
| [TSEC\_THI\_INT\_STATUS](#TSEC_THI_INT_STATUS "wikilink")                          | 0x54500078 | 0x04  |
| [TSEC\_THI\_INT\_MASK](#TSEC_THI_INT_MASK "wikilink")                              | 0x5450007C | 0x04  |
| TSEC\_THI\_CONFIG0                                                                 | 0x54500080 | 0x04  |
| TSEC\_THI\_DBG\_MISC                                                               | 0x54500084 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_HIGH\_A                                                 | 0x54500088 | 0x04  |
| TSEC\_THI\_SLCG\_OVERRIDE\_LOW\_A                                                  | 0x5450008C | 0x04  |
| TSEC\_THI\_CLK\_OVERRIDE                                                           | 0x54500E00 | 0x04  |
| [FALCON\_IRQSSET](#FALCON_IRQSSET "wikilink")                                      | 0x54501000 | 0x04  |
| [FALCON\_IRQSCLR](#FALCON_IRQSCLR "wikilink")                                      | 0x54501004 | 0x04  |
| [FALCON\_IRQSTAT](#FALCON_IRQSTAT "wikilink")                                      | 0x54501008 | 0x04  |
| [FALCON\_IRQMODE](#FALCON_IRQMODE "wikilink")                                      | 0x5450100C | 0x04  |
| [FALCON\_IRQMSET](#FALCON_IRQMSET "wikilink")                                      | 0x54501010 | 0x04  |
| [FALCON\_IRQMCLR](#FALCON_IRQMCLR "wikilink")                                      | 0x54501014 | 0x04  |
| [FALCON\_IRQMASK](#FALCON_IRQMASK "wikilink")                                      | 0x54501018 | 0x04  |
| [FALCON\_IRQDEST](#FALCON_IRQDEST "wikilink")                                      | 0x5450101C | 0x04  |
| FALCON\_GPTMRINT                                                                   | 0x54501020 | 0x04  |
| FALCON\_GPTMRVAL                                                                   | 0x54501024 | 0x04  |
| FALCON\_GPTMRCTL                                                                   | 0x54501028 | 0x04  |
| FALCON\_PTIMER0                                                                    | 0x5450102C | 0x04  |
| FALCON\_PTIMER1                                                                    | 0x54501030 | 0x04  |
| FALCON\_WDTMRVAL                                                                   | 0x54501034 | 0x04  |
| FALCON\_WDTMRCTL                                                                   | 0x54501038 | 0x04  |
| [FALCON\_IRQDEST2](#FALCON_IRQDEST2 "wikilink")                                    | 0x5450103C | 0x04  |
| [FALCON\_MAILBOX0](#FALCON_MAILBOX0 "wikilink")                                    | 0x54501040 | 0x04  |
| [FALCON\_MAILBOX1](#FALCON_MAILBOX1 "wikilink")                                    | 0x54501044 | 0x04  |
| [FALCON\_ITFEN](#FALCON_ITFEN "wikilink")                                          | 0x54501048 | 0x04  |
| [FALCON\_IDLESTATE](#FALCON_IDLESTATE "wikilink")                                  | 0x5450104C | 0x04  |
| FALCON\_CURCTX                                                                     | 0x54501050 | 0x04  |
| FALCON\_NXTCTX                                                                     | 0x54501054 | 0x04  |
| FALCON\_CTXACK                                                                     | 0x54501058 | 0x04  |
| FALCON\_FHSTATE                                                                    | 0x5450105C | 0x04  |
| FALCON\_PRIVSTATE                                                                  | 0x54501060 | 0x04  |
| FALCON\_MTHDDATA                                                                   | 0x54501064 | 0x04  |
| FALCON\_MTHDID                                                                     | 0x54501068 | 0x04  |
| FALCON\_MTHDWDAT                                                                   | 0x5450106C | 0x04  |
| FALCON\_MTHDCOUNT                                                                  | 0x54501070 | 0x04  |
| FALCON\_MTHDPOP                                                                    | 0x54501074 | 0x04  |
| FALCON\_MTHDRAMSZ                                                                  | 0x54501078 | 0x04  |
| FALCON\_SFTRESET                                                                   | 0x5450107C | 0x04  |
| FALCON\_OS                                                                         | 0x54501080 | 0x04  |
| FALCON\_RM                                                                         | 0x54501084 | 0x04  |
| FALCON\_SOFT\_PM                                                                   | 0x54501088 | 0x04  |
| FALCON\_SOFT\_MODE                                                                 | 0x5450108C | 0x04  |
| [FALCON\_DEBUG1](#FALCON_DEBUG1 "wikilink")                                        | 0x54501090 | 0x04  |
| [FALCON\_DEBUGINFO](#FALCON_DEBUGINFO "wikilink")                                  | 0x54501094 | 0x04  |
| FALCON\_IBRKPT1                                                                    | 0x54501098 | 0x04  |
| FALCON\_IBRKPT2                                                                    | 0x5450109C | 0x04  |
| FALCON\_CGCTL                                                                      | 0x545010A0 | 0x04  |
| FALCON\_ENGCTL                                                                     | 0x545010A4 | 0x04  |
| FALCON\_PMM                                                                        | 0x545010A8 | 0x04  |
| FALCON\_ADDR                                                                       | 0x545010AC | 0x04  |
| FALCON\_IBRKPT3                                                                    | 0x545010B0 | 0x04  |
| FALCON\_IBRKPT4                                                                    | 0x545010B4 | 0x04  |
| FALCON\_IBRKPT5                                                                    | 0x545010B8 | 0x04  |
| [FALCON\_EXCI](#FALCON_EXCI "wikilink")                                            | 0x545010D0 | 0x04  |
| [FALCON\_SVEC\_SPR](#FALCON_SVEC_SPR "wikilink")                                   | 0x545010D4 | 0x04  |
| [FALCON\_RSTAT0](#FALCON_RSTAT0 "wikilink")                                        | 0x545010D8 | 0x04  |
| [FALCON\_RSTAT3](#FALCON_RSTAT3 "wikilink")                                        | 0x545010DC | 0x04  |
| FALCON\_UNK\_E0                                                                    | 0x545010E0 | 0x04  |
| [FALCON\_CPUCTL](#FALCON_CPUCTL "wikilink")                                        | 0x54501100 | 0x04  |
| [FALCON\_BOOTVEC](#FALCON_BOOTVEC "wikilink")                                      | 0x54501104 | 0x04  |
| [FALCON\_HWCFG](#FALCON_HWCFG "wikilink")                                          | 0x54501108 | 0x04  |
| [FALCON\_DMACTL](#FALCON_DMACTL "wikilink")                                        | 0x5450110C | 0x04  |
| [FALCON\_DMATRFBASE](#FALCON_DMATRFBASE "wikilink")                                | 0x54501110 | 0x04  |
| [FALCON\_DMATRFMOFFS](#FALCON_DMATRFMOFFS "wikilink")                              | 0x54501114 | 0x04  |
| [FALCON\_DMATRFCMD](#FALCON_DMATRFCMD "wikilink")                                  | 0x54501118 | 0x04  |
| [FALCON\_DMATRFFBOFFS](#FALCON_DMATRFFBOFFS "wikilink")                            | 0x5450111C | 0x04  |
| [FALCON\_DMAPOLL\_FB](#FALCON_DMAPOLL_FB "wikilink")                               | 0x54501120 | 0x04  |
| [FALCON\_DMAPOLL\_CP](#FALCON_DMAPOLL_CP "wikilink")                               | 0x54501124 | 0x04  |
| FALCON\_DBG\_STATE                                                                 | 0x54501128 | 0x04  |
| [FALCON\_HWCFG1](#FALCON_HWCFG1 "wikilink")                                        | 0x5450112C | 0x04  |
| FALCON\_CPUCTL\_ALIAS                                                              | 0x54501130 | 0x04  |
| FALCON\_STACKCFG                                                                   | 0x54501138 | 0x04  |
| [FALCON\_IMCTL](#FALCON_IMCTL "wikilink")                                          | 0x54501140 | 0x04  |
| [FALCON\_IMSTAT](#FALCON_IMSTAT "wikilink")                                        | 0x54501144 | 0x04  |
| [FALCON\_TRACEIDX](#FALCON_TRACEIDX "wikilink")                                    | 0x54501148 | 0x04  |
| [FALCON\_TRACEPC](#FALCON_TRACEPC "wikilink")                                      | 0x5450114C | 0x04  |
| FALCON\_IMFILLRNG0                                                                 | 0x54501150 | 0x04  |
| FALCON\_IMFILLRNG1                                                                 | 0x54501154 | 0x04  |
| FALCON\_IMFILLCTL                                                                  | 0x54501158 | 0x04  |
| FALCON\_IMCTL\_DEBUG                                                               | 0x5450115C | 0x04  |
| FALCON\_CMEMBASE                                                                   | 0x54501160 | 0x04  |
| FALCON\_DMEMAPERT                                                                  | 0x54501164 | 0x04  |
| FALCON\_EXTERRADDR                                                                 | 0x54501168 | 0x04  |
| FALCON\_EXTERRSTAT                                                                 | 0x5450116C | 0x04  |
| FALCON\_CG2                                                                        | 0x5450117C | 0x04  |
| [FALCON\_IMEMC0](#FALCON_IMEMC0 "wikilink")                                        | 0x54501180 | 0x04  |
| [FALCON\_IMEMD0](#FALCON_IMEMD0 "wikilink")                                        | 0x54501184 | 0x04  |
| [FALCON\_IMEMT0](#FALCON_IMEMT0 "wikilink")                                        | 0x54501188 | 0x04  |
| FALCON\_IMEMC1                                                                     | 0x54501190 | 0x04  |
| FALCON\_IMEMD1                                                                     | 0x54501194 | 0x04  |
| FALCON\_IMEMT1                                                                     | 0x54501198 | 0x04  |
| FALCON\_IMEMC2                                                                     | 0x545011A0 | 0x04  |
| FALCON\_IMEMD2                                                                     | 0x545011A4 | 0x04  |
| FALCON\_IMEMT2                                                                     | 0x545011A8 | 0x04  |
| FALCON\_IMEMC3                                                                     | 0x545011B0 | 0x04  |
| FALCON\_IMEMD3                                                                     | 0x545011B4 | 0x04  |
| FALCON\_IMEMT3                                                                     | 0x545011B8 | 0x04  |
| [FALCON\_DMEMC0](#FALCON_DMEMC0 "wikilink")                                        | 0x545011C0 | 0x04  |
| [FALCON\_DMEMD0](#FALCON_DMEMD0 "wikilink")                                        | 0x545011C4 | 0x04  |
| FALCON\_DMEMC1                                                                     | 0x545011C8 | 0x04  |
| FALCON\_DMEMD1                                                                     | 0x545011CC | 0x04  |
| FALCON\_DMEMC2                                                                     | 0x545011D0 | 0x04  |
| FALCON\_DMEMD2                                                                     | 0x545011D4 | 0x04  |
| FALCON\_DMEMC3                                                                     | 0x545011D8 | 0x04  |
| FALCON\_DMEMD3                                                                     | 0x545011DC | 0x04  |
| FALCON\_DMEMC4                                                                     | 0x545011E0 | 0x04  |
| FALCON\_DMEMD4                                                                     | 0x545011E4 | 0x04  |
| FALCON\_DMEMC5                                                                     | 0x545011E8 | 0x04  |
| FALCON\_DMEMD5                                                                     | 0x545011EC | 0x04  |
| FALCON\_DMEMC6                                                                     | 0x545011F0 | 0x04  |
| FALCON\_DMEMD6                                                                     | 0x545011F4 | 0x04  |
| FALCON\_DMEMC7                                                                     | 0x545011F8 | 0x04  |
| FALCON\_DMEMD7                                                                     | 0x545011FC | 0x04  |
| [FALCON\_ICD\_CMD](#FALCON_ICD_CMD "wikilink")                                     | 0x54501200 | 0x04  |
| [FALCON\_ICD\_ADDR](#FALCON_ICD_ADDR "wikilink")                                   | 0x54501204 | 0x04  |
| [FALCON\_ICD\_WDATA](#FALCON_ICD_WDATA "wikilink")                                 | 0x54501208 | 0x04  |
| [FALCON\_ICD\_RDATA](#FALCON_ICD_RDATA "wikilink")                                 | 0x5450120C | 0x04  |
| [FALCON\_SCTL](#FALCON_SCTL "wikilink")                                            | 0x54501240 | 0x04  |
| [FALCON\_SSTAT](#FALCON_SSTAT "wikilink")                                          | 0x54501244 | 0x04  |
| FALCON\_UNK\_248                                                                   | 0x54501248 | 0x04  |
| FALCON\_UNK\_24C                                                                   | 0x5450124C | 0x04  |
| FALCON\_UNK\_250                                                                   | 0x54501250 | 0x04  |
| FALCON\_UNK\_260                                                                   | 0x54501260 | 0x04  |
| [FALCON\_SPROT\_IMEM](#FALCON_SPROT_IMEM "wikilink")                               | 0x54501280 | 0x04  |
| [FALCON\_SPROT\_DMEM](#FALCON_SPROT_DMEM "wikilink")                               | 0x54501284 | 0x04  |
| [FALCON\_SPROT\_CPUCTL](#FALCON_SPROT_CPUCTL "wikilink")                           | 0x54501288 | 0x04  |
| [FALCON\_SPROT\_MISC](#FALCON_SPROT_MISC "wikilink")                               | 0x5450128C | 0x04  |
| [FALCON\_SPROT\_IRQ](#FALCON_SPROT_IRQ "wikilink")                                 | 0x54501290 | 0x04  |
| [FALCON\_SPROT\_MTHD](#FALCON_SPROT_MTHD "wikilink")                               | 0x54501294 | 0x04  |
| [FALCON\_SPROT\_SCTL](#FALCON_SPROT_SCTL "wikilink")                               | 0x54501298 | 0x04  |
| [FALCON\_SPROT\_WDTMR](#FALCON_SPROT_WDTMR "wikilink")                             | 0x5450129C | 0x04  |
| FALCON\_DMAINFO\_FINISHED\_FBRD\_LOW                                               | 0x545012C0 | 0x04  |
| FALCON\_DMAINFO\_FINISHED\_FBRD\_HIGH                                              | 0x545012C4 | 0x04  |
| FALCON\_DMAINFO\_FINISHED\_FBWR\_LOW                                               | 0x545012C8 | 0x04  |
| FALCON\_DMAINFO\_FINISHED\_FBWR\_HIGH                                              | 0x545012CC | 0x04  |
| FALCON\_DMAINFO\_CURRENT\_FBRD\_LOW                                                | 0x545012D0 | 0x04  |
| FALCON\_DMAINFO\_CURRENT\_FBRD\_HIGH                                               | 0x545012D4 | 0x04  |
| FALCON\_DMAINFO\_CURRENT\_FBWR\_LOW                                                | 0x545012D8 | 0x04  |
| FALCON\_DMAINFO\_CURRENT\_FBWR\_HIGH                                               | 0x545012DC | 0x04  |
| FALCON\_DMAINFO\_CTL                                                               | 0x545012E0 | 0x04  |
| [TSEC\_SCP\_CTL0](#TSEC_SCP_CTL0 "wikilink")                                       | 0x54501400 | 0x04  |
| [TSEC\_SCP\_CTL1](#TSEC_SCP_CTL1 "wikilink")                                       | 0x54501404 | 0x04  |
| [TSEC\_SCP\_CTL\_STAT](#TSEC_SCP_CTL_STAT "wikilink")                              | 0x54501408 | 0x04  |
| [TSEC\_SCP\_CTL\_LOCK](#TSEC_SCP_CTL_LOCK "wikilink")                              | 0x5450140C | 0x04  |
| [TSEC\_SCP\_CFG](#TSEC_SCP_CFG "wikilink")                                         | 0x54501410 | 0x04  |
| TSEC\_SCP\_CTL\_SCP                                                                | 0x54501414 | 0x04  |
| [TSEC\_SCP\_CTL\_PKEY](#TSEC_SCP_CTL_PKEY "wikilink")                              | 0x54501418 | 0x04  |
| TSEC\_SCP\_CTL\_DBG                                                                | 0x5450141C | 0x04  |
| [TSEC\_SCP\_DBG0](#TSEC_SCP_DBG0 "wikilink")                                       | 0x54501420 | 0x04  |
| [TSEC\_SCP\_DBG1](#TSEC_SCP_DBG1 "wikilink")                                       | 0x54501424 | 0x04  |
| [TSEC\_SCP\_DBG2](#TSEC_SCP_DBG2 "wikilink")                                       | 0x54501428 | 0x04  |
| [TSEC\_SCP\_CMD](#TSEC_SCP_CMD "wikilink")                                         | 0x54501430 | 0x04  |
| [TSEC\_SCP\_STAT0](#TSEC_SCP_STAT0 "wikilink")                                     | 0x54501450 | 0x04  |
| [TSEC\_SCP\_STAT1](#TSEC_SCP_STAT1 "wikilink")                                     | 0x54501454 | 0x04  |
| [TSEC\_SCP\_STAT2](#TSEC_SCP_STAT2 "wikilink")                                     | 0x54501458 | 0x04  |
| [TSEC\_SCP\_RND\_STAT0](#TSEC_SCP_RND_STAT0 "wikilink")                            | 0x54501470 | 0x04  |
| TSEC\_SCP\_RND\_STAT1                                                              | 0x54501474 | 0x04  |
| [TSEC\_SCP\_IRQSTAT](#TSEC_SCP_IRQSTAT "wikilink")                                 | 0x54501480 | 0x04  |
| [TSEC\_SCP\_IRQMASK](#TSEC_SCP_IRQMASK "wikilink")                                 | 0x54501484 | 0x04  |
| [TSEC\_SCP\_ACL\_ERR](#TSEC_SCP_ACL_ERR "wikilink")                                | 0x54501490 | 0x04  |
| TSEC\_SCP\_SEC\_ERR                                                                | 0x54501494 | 0x04  |
| [TSEC\_SCP\_CMD\_ERR](#TSEC_SCP_CMD_ERR "wikilink")                                | 0x54501498 | 0x04  |
| [TSEC\_RND\_CTL0](#TSEC_RND_CTL0 "wikilink")                                       | 0x54501500 | 0x04  |
| [TSEC\_RND\_CTL1](#TSEC_RND_CTL1 "wikilink")                                       | 0x54501504 | 0x04  |
| TSEC\_RND\_CTL2                                                                    | 0x54501508 | 0x04  |
| TSEC\_RND\_CTL3                                                                    | 0x5450150C | 0x04  |
| TSEC\_RND\_CTL4                                                                    | 0x54501510 | 0x04  |
| TSEC\_RND\_CTL5                                                                    | 0x54501514 | 0x04  |
| TSEC\_RND\_CTL6                                                                    | 0x54501518 | 0x04  |
| TSEC\_RND\_CTL7                                                                    | 0x5450151C | 0x04  |
| TSEC\_RND\_CTL8                                                                    | 0x54501520 | 0x04  |
| TSEC\_RND\_CTL9                                                                    | 0x54501524 | 0x04  |
| TSEC\_RND\_CTL10                                                                   | 0x54501528 | 0x04  |
| TSEC\_RND\_CTL11                                                                   | 0x5450152C | 0x04  |
| [TSEC\_TFBIF\_CTL](#TSEC_TFBIF_CTL "wikilink")                                     | 0x54501600 | 0x04  |
| [TSEC\_TFBIF\_MCCIF\_FIFOCTRL](#TSEC_TFBIF_MCCIF_FIFOCTRL "wikilink")              | 0x54501604 | 0x04  |
| [TSEC\_TFBIF\_THROTTLE](#TSEC_TFBIF_THROTTLE "wikilink")                           | 0x54501608 | 0x04  |
| [TSEC\_TFBIF\_DBG\_STAT0](#TSEC_TFBIF_DBG_STAT0 "wikilink")                        | 0x5450160C | 0x04  |
| TSEC\_TFBIF\_DBG\_STAT1                                                            | 0x54501610 | 0x04  |
| TSEC\_TFBIF\_DBG\_RDCOUNT\_LO                                                      | 0x54501614 | 0x04  |
| TSEC\_TFBIF\_DBG\_RDCOUNT\_HI                                                      | 0x54501618 | 0x04  |
| TSEC\_TFBIF\_DBG\_WRCOUNT\_LO                                                      | 0x5450161C | 0x04  |
| TSEC\_TFBIF\_DBG\_WRCOUNT\_HI                                                      | 0x54501620 | 0x04  |
| TSEC\_TFBIF\_DBG\_R32COUNT                                                         | 0x54501624 | 0x04  |
| TSEC\_TFBIF\_DBG\_R64COUNT                                                         | 0x54501628 | 0x04  |
| TSEC\_TFBIF\_DBG\_R128COUNT                                                        | 0x5450162C | 0x04  |
| TSEC\_TFBIF\_UNK\_30                                                               | 0x54501630 | 0x04  |
| [TSEC\_TFBIF\_MCCIF\_FIFOCTRL1](#TSEC_TFBIF_MCCIF_FIFOCTRL1 "wikilink")            | 0x54501634 | 0x04  |
| TSEC\_TFBIF\_WRR\_RDP                                                              | 0x54501638 | 0x04  |
| [TSEC\_TFBIF\_SPROT\_EMEM](#TSEC_TFBIF_SPROT_EMEM "wikilink")                      | 0x54501640 | 0x04  |
| [TSEC\_TFBIF\_TRANSCFG](#TSEC_TFBIF_TRANSCFG "wikilink")                           | 0x54501644 | 0x04  |
| [TSEC\_TFBIF\_REGIONCFG](#TSEC_TFBIF_REGIONCFG "wikilink")                         | 0x54501648 | 0x04  |
| [TSEC\_TFBIF\_ACTMON\_ACTIVE\_MASK](#TSEC_TFBIF_ACTMON_ACTIVE_MASK "wikilink")     | 0x5450164C | 0x04  |
| [TSEC\_TFBIF\_ACTMON\_ACTIVE\_BORPS](#TSEC_TFBIF_ACTMON_ACTIVE_BORPS "wikilink")   | 0x54501650 | 0x04  |
| [TSEC\_TFBIF\_ACTMON\_ACTIVE\_WEIGHT](#TSEC_TFBIF_ACTMON_ACTIVE_WEIGHT "wikilink") | 0x54501654 | 0x04  |
| TSEC\_TFBIF\_ACTMON\_MCB\_MASK                                                     | 0x54501660 | 0x04  |
| TSEC\_TFBIF\_ACTMON\_MCB\_BORPS                                                    | 0x54501664 | 0x04  |
| TSEC\_TFBIF\_ACTMON\_MCB\_WEIGHT                                                   | 0x54501668 | 0x04  |
| TSEC\_TFBIF\_THI\_TRANSPROP                                                        | 0x54501670 | 0x04  |
| [TSEC\_CG](#TSEC_CG "wikilink")                                                    | 0x545016D0 | 0x04  |
| [TSEC\_BAR0\_CTL](#TSEC_BAR0_CTL "wikilink")                                       | 0x54501700 | 0x04  |
| [TSEC\_BAR0\_ADDR](#TSEC_BAR0_ADDR "wikilink")                                     | 0x54501704 | 0x04  |
| [TSEC\_BAR0\_DATA](#TSEC_BAR0_DATA "wikilink")                                     | 0x54501708 | 0x04  |
| [TSEC\_BAR0\_TIMEOUT](#TSEC_BAR0_TIMEOUT "wikilink")                               | 0x5450170C | 0x04  |
| TSEC\_TEGRA\_FALCON\_IP\_VER                                                       | 0x54501800 | 0x04  |
| TSEC\_TEGRA\_UNK\_04                                                               | 0x54501804 | 0x04  |
| TSEC\_TEGRA\_UNK\_08                                                               | 0x54501808 | 0x04  |
| TSEC\_TEGRA\_UNK\_0C                                                               | 0x5450180C | 0x04  |
| TSEC\_TEGRA\_UNK\_10                                                               | 0x54501810 | 0x04  |
| TSEC\_TEGRA\_UNK\_14                                                               | 0x54501814 | 0x04  |
| TSEC\_TEGRA\_UNK\_18                                                               | 0x54501818 | 0x04  |
| TSEC\_TEGRA\_UNK\_1C                                                               | 0x5450181C | 0x04  |
| TSEC\_TEGRA\_UNK\_20                                                               | 0x54501820 | 0x04  |
| TSEC\_TEGRA\_UNK\_24                                                               | 0x54501824 | 0x04  |
| TSEC\_TEGRA\_UNK\_28                                                               | 0x54501828 | 0x04  |
| TSEC\_TEGRA\_UNK\_2C                                                               | 0x5450182C | 0x04  |
| TSEC\_TEGRA\_UNK\_30                                                               | 0x54501830 | 0x04  |
| TSEC\_TEGRA\_UNK\_34                                                               | 0x54501834 | 0x04  |
| [TSEC\_TEGRA\_CTL](#TSEC_TEGRA_CTL "wikilink")                                     | 0x54501838 | 0x04  |

### TSEC\_THI\_METHOD0

| ID     | Method                               |
| ------ | ------------------------------------ |
| 0x100  | NOP                                  |
| 0x140  | PM\_TRIGGER                          |
| 0x200  | SET\_APPLICATION\_ID                 |
| 0x204  | SET\_WATCHDOG\_TIMER                 |
| 0x240  | SEMAPHORE\_A                         |
| 0x244  | SEMAPHORE\_B                         |
| 0x248  | SEMAPHORE\_C                         |
| 0x24C  |                                      |
| 0x250  |                                      |
| 0x300  | EXECUTE                              |
| 0x304  | SEMAPHORE\_D                         |
| 0x500  | HDCP\_INIT                           |
| 0x504  | HDCP\_CREATE\_SESSION                |
| 0x508  | HDCP\_VERIFY\_CERT\_RX               |
| 0x50C  | HDCP\_GENERATE\_EKM                  |
| 0x510  | HDCP\_REVOCATION\_CHECK              |
| 0x514  | HDCP\_VERIFY\_HPRIME                 |
| 0x518  | HDCP\_ENCRYPT\_PAIRING\_INFO         |
| 0x51C  | HDCP\_DECRYPT\_PAIRING\_INFO         |
| 0x520  | HDCP\_UPDATE\_SESSION                |
| 0x524  | HDCP\_GENERATE\_LC\_INIT             |
| 0x528  | HDCP\_VERIFY\_LPRIME                 |
| 0x52C  | HDCP\_GENERATE\_SKE\_INIT            |
| 0x530  | HDCP\_VERIFY\_VPRIME                 |
| 0x534  | HDCP\_ENCRYPTION\_RUN\_CTRL          |
| 0x538  | HDCP\_SESSION\_CTRL                  |
| 0x53C  | HDCP\_COMPUTE\_SPRIME                |
| 0x540  | HDCP\_GET\_CERT\_RX                  |
| 0x544  | HDCP\_EXCHANGE\_INFO                 |
| 0x548  | HDCP\_DECRYPT\_KM                    |
| 0x54C  | HDCP\_GET\_HPRIME                    |
| 0x550  | HDCP\_GENERATE\_EKH\_KM              |
| 0x554  | HDCP\_VERIFY\_RTT\_CHALLENGE         |
| 0x558  | HDCP\_GET\_LPRIME                    |
| 0x55C  | HDCP\_DECRYPT\_KS                    |
| 0x560  | HDCP\_DECRYPT                        |
| 0x564  | HDCP\_GET\_RRX                       |
| 0x568  | HDCP\_DECRYPT\_REENCRYPT             |
| 0x56C  |                                      |
| 0x570  |                                      |
| 0x574  |                                      |
| 0x578  |                                      |
| 0x57C  |                                      |
| 0x700  | HDCP\_VALIDATE\_SRM                  |
| 0x704  | HDCP\_VALIDATE\_STREAM               |
| 0x708  | HDCP\_TEST\_SECURE\_STATUS           |
| 0x70C  | HDCP\_SET\_DCP\_KPUB                 |
| 0x710  | HDCP\_SET\_RX\_KPUB                  |
| 0x714  | HDCP\_SET\_CERT\_RX                  |
| 0x718  | HDCP\_SET\_SCRATCH\_BUFFER           |
| 0x71C  | HDCP\_SET\_SRM                       |
| 0x720  | HDCP\_SET\_RECEIVER\_ID\_LIST        |
| 0x724  | HDCP\_SET\_SPRIME                    |
| 0x728  | HDCP\_SET\_ENC\_INPUT\_BUFFER        |
| 0x72C  | HDCP\_SET\_ENC\_OUTPUT\_BUFFER       |
| 0x730  | HDCP\_GET\_RTT\_CHALLENGE            |
| 0x734  | HDCP\_STREAM\_MANAGE                 |
| 0x738  | HDCP\_READ\_CAPS                     |
| 0x73C  | HDCP\_ENCRYPT                        |
| 0x740  | \[6.0.0+\] HDCP\_GET\_CURRENT\_NONCE |
| 0x1114 | PM\_TRIGGER\_END                     |

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
| 16   | FALCON\_IRQSSET\_DMA    |

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
| 16   | FALCON\_IRQSCLR\_DMA    |

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
| 16   | FALCON\_IRQSTAT\_DMA    |

Used for getting the status of Falcon's IRQs.

### FALCON\_IRQMODE

| Bits | Description                  |
| ---- | ---------------------------- |
| 0    | FALCON\_IRQMODE\_LVL\_GPTMR  |
| 1    | FALCON\_IRQMODE\_LVL\_WDTMR  |
| 2    | FALCON\_IRQMODE\_LVL\_MTHD   |
| 3    | FALCON\_IRQMODE\_LVL\_CTXSW  |
| 4    | FALCON\_IRQMODE\_LVL\_HALT   |
| 5    | FALCON\_IRQMODE\_LVL\_EXTERR |
| 6    | FALCON\_IRQMODE\_LVL\_SWGEN0 |
| 7    | FALCON\_IRQMODE\_LVL\_SWGEN1 |
| 8-15 | FALCON\_IRQMODE\_LVL\_EXT    |
| 16   | FALCON\_IRQMODE\_LVL\_DMA    |

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
| 16   | FALCON\_IRQMSET\_DMA    |

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
| 16   | FALCON\_IRQMCLR\_DMA    |

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
| 16   | FALCON\_IRQMASK\_DMA    |

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

### FALCON\_IRQDEST2

| Bits | Description                   |
| ---- | ----------------------------- |
| 0    | FALCON\_IRQDEST2\_HOST\_DMA   |
| 16   | FALCON\_IRQDEST2\_TARGET\_DMA |

Used for routing Falcon's IRQs.

### FALCON\_MAILBOX0

Scratch register for reading/writing data to Falcon.

### FALCON\_MAILBOX1

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

### FALCON\_DEBUG1

| Bits | Description                       |
| ---- | --------------------------------- |
| 0-15 | FALCON\_DEBUG1\_MTHD\_DRAIN\_TIME |
| 16   | FALCON\_DEBUG1\_CTXSW\_MODE       |
| 17   | FALCON\_DEBUG1\_TRACE\_FORMAT     |

### FALCON\_DEBUGINFO

Used for UCODE self revocation. This register takes the base address of
the GSC carveout shifted right by 8.

\[6.0.0+\] [nvservices](NV%20services.md "wikilink") sets this to
0x8005FF00 \>\> 8 (physical DRAM address inside the GPU UCODE carveout)
before starting the nvhost\_tsec firmware.

### FALCON\_EXCI

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-19</p></td>
<td><p>FALCON_EXCI_EXPC</p></td>
</tr>
<tr class="even">
<td><p>20-23</p></td>
<td><p>FALCON_EXCI_EXCAUSE</p>
<p><code>0x00: TRAP0</code><br />
<code>0x01: TRAP1</code><br />
<code>0x02: TRAP2</code><br />
<code>0x03: TRAP3</code><br />
<code>0x08: ILL_INS (invalid opcode)</code><br />
<code>0x09: INV_INS (authentication entry)</code><br />
<code>0x0A: MISS_INS (page miss)</code><br />
<code>0x0B: DHIT_INS (page multiple hit)</code><br />
<code>0x0F: BRKPT_INS (breakpoint hit)</code></p></td>
</tr>
</tbody>
</table>

Contains information about raised exceptions.

### FALCON\_SVEC\_SPR

| Bits | Description                |
| ---- | -------------------------- |
| 18   | FALCON\_SVEC\_SPR\_SIGPASS |

### FALCON\_RSTAT0

Mirror of the ICD status register 0.

### FALCON\_RSTAT3

Mirror of the ICD status register 3.

### FALCON\_CPUCTL

| Bits | Description               |
| ---- | ------------------------- |
| 0    | FALCON\_CPUCTL\_IINVAL    |
| 1    | FALCON\_CPUCTL\_STARTCPU  |
| 2    | FALCON\_CPUCTL\_SRESET    |
| 3    | FALCON\_CPUCTL\_HRESET    |
| 4    | FALCON\_CPUCTL\_HALTED    |
| 5    | FALCON\_CPUCTL\_STOPPED   |
| 6    | FALCON\_CPUCTL\_ALIAS\_EN |

Used for signaling the Falcon CPU.

### FALCON\_BOOTVEC

Takes the Falcon's boot vector address.

### FALCON\_HWCFG

| Bits  | Description                      |
| ----- | -------------------------------- |
| 0-8   | FALCON\_HWCFG\_IMEM\_SIZE        |
| 9-17  | FALCON\_HWCFG\_DMEM\_SIZE        |
| 18-26 | FALCON\_HWCFG\_METHODFIFO\_DEPTH |
| 27-31 | FALCON\_HWCFG\_DMAQUEUE\_DEPTH   |

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

Base address of the external memory buffer, shifted right by 8.

The current transfer address is calculated by adding
[FALCON\_DMATRFFBOFFS](#FALCON_DMATRFFBOFFS "wikilink") to the base.

### FALCON\_DMATRFMOFFS

For transfers to DMEM: the destination address. For transfers to IMEM:
the destination virtual IMEM page.

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

For transfers to IMEM: the destination physical IMEM page.

### FALCON\_DMAPOLL\_FB

| Bits  | Description                        |
| ----- | ---------------------------------- |
| 0     | FALCON\_DMAPOLL\_FB\_FENCE\_ACTIVE |
| 1     | FALCON\_DMAPOLL\_FB\_DMA\_ACTIVE   |
| 4     | FALCON\_DMAPOLL\_FB\_CFG\_R\_FENCE |
| 5     | FALCON\_DMAPOLL\_FB\_CFG\_W\_FENCE |
| 16-23 | FALCON\_DMAPOLL\_FB\_WCOUNT        |
| 24-31 | FALCON\_DMAPOLL\_FB\_RCOUNT        |

Contains the status of a DMA transfer between the Falcon and external
memory.

### FALCON\_DMAPOLL\_CP

| Bits  | Description                        |
| ----- | ---------------------------------- |
| 0     | FALCON\_DMAPOLL\_CP\_FENCE\_ACTIVE |
| 1     | FALCON\_DMAPOLL\_CP\_DMA\_ACTIVE   |
| 4     | FALCON\_DMAPOLL\_CP\_CFG\_R\_FENCE |
| 5     | FALCON\_DMAPOLL\_CP\_CFG\_W\_FENCE |
| 16-23 | FALCON\_DMAPOLL\_CP\_WCOUNT        |
| 24-31 | FALCON\_DMAPOLL\_CP\_RCOUNT        |

Contains the status of a DMA transfer between the Falcon and the SCP.

### FALCON\_HWCFG1

| Bits  | Description                           |
| ----- | ------------------------------------- |
| 0-3   | FALCON\_HWCFG1\_CORE\_REV             |
| 4-5   | FALCON\_HWCFG1\_SECURITY\_MODEL       |
| 6-7   | FALCON\_HWCFG1\_CORE\_REV\_SUBVERSION |
| 8-11  | FALCON\_HWCFG1\_IMEM\_PORTS           |
| 12-15 | FALCON\_HWCFG1\_DMEM\_PORTS           |
| 16-20 | FALCON\_HWCFG1\_TAG\_WIDTH            |
| 27    | FALCON\_HWCFG1\_DBG\_PRIV\_BUS        |
| 28    | FALCON\_HWCFG1\_CSB\_SIZE\_16M        |
| 29    | FALCON\_HWCFG1\_PRIV\_DIRECT          |
| 30    | FALCON\_HWCFG1\_DMEM\_APERTURES       |
| 31    | FALCON\_HWCFG1\_IMEM\_AUTOFILL        |

### FALCON\_IMCTL

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-23</p></td>
<td><p>FALCON_IMCTL_ADDR_BLK</p></td>
</tr>
<tr class="even">
<td><p>24-26</p></td>
<td><p>FALCON_IMCTL_CMD</p>
<p><code>0x00: NOP</code><br />
<code>0x01: IMINV (ITLB)</code><br />
<code>0x02: IMBLK (PTLB)</code><br />
<code>0x03: IMTAG (VTLB)</code><br />
<code>0x04: IMTAG_SETVLD</code></p></td>
</tr>
</tbody>
</table>

Controls the Falcon TLB.

### FALCON\_IMSTAT

Returns the result of the last command from
[FALCON\_IMCTL](#FALCON_IMCTL "wikilink").

### FALCON\_TRACEIDX

| Bits  | Description              |
| ----- | ------------------------ |
| 0-7   | FALCON\_TRACEIDX\_IDX    |
| 16-23 | FALCON\_TRACEIDX\_MAXIDX |
| 24-31 | FALCON\_TRACEIDX\_CNT    |

Controls the index for tracing with
[FALCON\_TRACEPC](#FALCON_TRACEPC "wikilink").

### FALCON\_TRACEPC

Returns the PC of the last call or branch executed.

### FALCON\_IMEMC0

| Bits | Description                 |
| ---- | --------------------------- |
| 2-7  | FALCON\_IMEMC\_OFFS         |
| 8-15 | FALCON\_IMEMC\_BLK          |
| 24   | FALCON\_IMEMC\_AINCW        |
| 25   | FALCON\_IMEMC\_AINCR        |
| 28   | FALCON\_IMEMC\_SECURE       |
| 29   | FALCON\_IMEMC\_SEC\_ATOMIC  |
| 30   | FALCON\_IMEMC\_SEC\_WR\_VIO |
| 31   | FALCON\_IMEMC\_SEC\_LOCK    |

Used for configuring access to Falcon's IMEM.

### FALCON\_IMEMD0

Returns or takes the value for an IMEM read/write operation.

### FALCON\_IMEMT0

Returns or takes the virtual page index for an IMEM read/write
operation.

### FALCON\_DMEMC0

| Bits | Description          |
| ---- | -------------------- |
| 2-7  | FALCON\_DMEMC\_OFFS  |
| 8-15 | FALCON\_DMEMC\_BLK   |
| 24   | FALCON\_DMEMC\_AINCW |
| 25   | FALCON\_DMEMC\_AINCR |

Used for configuring access to Falcon's DMEM.

### FALCON\_DMEMD0

Returns or takes the value for a DMEM read/write operation.

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
<p><code>0x00: STOP</code><br />
<code>0x01: RUN (run from PC)</code><br />
<code>0x02: JRUN (run from address)</code><br />
<code>0x03: RUNB (run from PC)</code><br />
<code>0x04: JRUNB (run from address)</code><br />
<code>0x05: STEP (step from PC)</code><br />
<code>0x06: JSTEP (step from address)</code><br />
<code>0x07: EMASK (set exception mask)</code><br />
<code>0x08: RREG (read register)</code><br />
<code>0x09: WREG (write register)</code><br />
<code>0x0A: RDM (read data memory)</code><br />
<code>0x0B: WDM (write data memory)</code><br />
<code>0x0C: RCM (read MMIO/configuration memory)</code><br />
<code>0x0D: WCM (write MMIO/configuration memory)</code><br />
<code>0x0E: RSTAT (read status)</code><br />
<code>0x0F: SBU</code></p></td>
</tr>
<tr class="even">
<td><p>6-7</p></td>
<td><p>FALCON_ICD_CMD_SZ</p>
<p><code>0x00: B (byte</code><br />
<code>0x01: HW (half word)</code><br />
<code>0x02: W (word)</code></p></td>
</tr>
<tr class="odd">
<td><p>8-12</p></td>
<td><p>FALCON_ICD_CMD_IDX</p>
<p><code>0x00: REG0 | RSTAT0 | WB0</code><br />
<code>0x01: REG1 | RSTAT1 | WB1</code><br />
<code>0x02: REG2 | RSTAT2 | WB2</code><br />
<code>0x03: REG3 | RSTAT3 | WB3</code><br />
<code>0x04: REG4 | RSTAT4</code><br />
<code>0x05: REG5 | RSTAT5</code><br />
<code>0x06: REG6</code><br />
<code>0x07: REG7</code><br />
<code>0x08: REG8</code><br />
<code>0x09: REG9</code><br />
<code>0x0A: REG10</code><br />
<code>0x0B: REG11</code><br />
<code>0x0C: REG12</code><br />
<code>0x0D: REG13</code><br />
<code>0x0E: REG14</code><br />
<code>0x0F: REG15</code><br />
<code>0x10: IV0</code><br />
<code>0x11: IV1</code><br />
<code>0x12: UNDEFINED</code><br />
<code>0x13: EV</code><br />
<code>0x14: SP</code><br />
<code>0x15: PC</code><br />
<code>0x16: IMB</code><br />
<code>0x17: DMB</code><br />
<code>0x18: CSW</code><br />
<code>0x19: CCR</code><br />
<code>0x1A: SEC</code><br />
<code>0x1B: CTX</code><br />
<code>0x1C: EXCI</code><br />
<code>0x1D: SEC1</code><br />
<code>0x1E: IMB1</code><br />
<code>0x1F: DMB1</code></p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p>FALCON_ICD_CMD_ERROR</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p>FALCON_ICD_CMD_RDVLD</p></td>
</tr>
<tr class="even">
<td><p>16-31</p></td>
<td><p>FALCON_ICD_CMD_PARM</p>
<p><code>0x0001: EMASK_TRAP0</code><br />
<code>0x0002: EMASK_TRAP1</code><br />
<code>0x0004: EMASK_TRAP2</code><br />
<code>0x0008: EMASK_TRAP3</code><br />
<code>0x0010: EMASK_EXC_UNIMP</code><br />
<code>0x0020: EMASK_EXC_IMISS</code><br />
<code>0x0040: EMASK_EXC_IMHIT</code><br />
<code>0x0080: EMASK_EXC_IBREAK</code><br />
<code>0x0100: EMASK_IV0</code><br />
<code>0x0200: EMASK_IV1</code><br />
<code>0x0400: EMASK_IV2</code><br />
<code>0x0800: EMASK_EXT0</code><br />
<code>0x1000: EMASK_EXT1</code><br />
<code>0x2000: EMASK_EXT2</code><br />
<code>0x4000: EMASK_EXT3</code><br />
<code>0x8000: EMASK_EXT4</code></p></td>
</tr>
</tbody>
</table>

Used for sending commands to the Falcon's in-chip debugger.

### FALCON\_ICD\_ADDR

Takes the target address for the Falcon's in-chip debugger.

### FALCON\_ICD\_WDATA

Takes the data for writing using the Falcon's in-chip debugger.

### FALCON\_ICD\_RDATA

Returns the data read using the Falcon's in-chip debugger.

When reading from an internal status register (STAT), the following
applies:

| Bits  | Description                   |
| ----- | ----------------------------- |
| 0     | RSTAT0\_MEM\_STALL            |
| 1     | RSTAT0\_DMA\_STALL            |
| 2     | RSTAT0\_FENCE\_STALL          |
| 3     | RSTAT0\_DIV\_STALL            |
| 4     | RSTAT0\_DMA\_STALL\_DMAQ      |
| 5     | RSTAT0\_DMA\_STALL\_DMWAITING |
| 6     | RSTAT0\_DMA\_STALL\_IMWAITING |
| 7     | RSTAT0\_ANY\_STALL            |
| 8     | RSTAT0\_SBFULL\_STALL         |
| 9     | RSTAT0\_SBHIT\_STALL          |
| 10    | RSTAT0\_FLOW\_STALL           |
| 11    | RSTAT0\_SP\_STALL             |
| 12    | RSTAT0\_BL\_STALL             |
| 13    | RSTAT0\_IPND\_STALL           |
| 14    | RSTAT0\_LDSTQ\_STALL          |
| 16    | RSTAT0\_NOINSTR\_STALL        |
| 20    | RSTAT0\_HALTSTOP\_FLUSH       |
| 21    | RSTAT0\_AFILL\_FLUSH          |
| 22    | RSTAT0\_EXC\_FLUSH            |
| 23-25 | RSTAT0\_IRQ\_FLUSH            |
| 28    | RSTAT0\_VALIDRD               |
| 29    | RSTAT0\_WAITING               |
| 30    | RSTAT0\_HALTED                |
| 31    | RSTAT0\_MTHD\_FULL            |

| Bits  | Description       |
| ----- | ----------------- |
| 0-3   | RSTAT1\_WB\_ALLOC |
| 4-7   | RSTAT1\_WB\_VALID |
| 8-9   | RSTAT1\_WB0\_SZ   |
| 10-11 | RSTAT1\_WB1\_SZ   |
| 12-13 | RSTAT1\_WB2\_SZ   |
| 14-15 | RSTAT1\_WB3\_SZ   |
| 16-19 | RSTAT1\_WB0\_IDX  |
| 20-23 | RSTAT1\_WB1\_IDX  |
| 24-27 | RSTAT1\_WB2\_IDX  |
| 28-31 | RSTAT1\_WB3\_IDX  |

| Bits  | Description         |
| ----- | ------------------- |
| 0-3   | RSTAT2\_DMAQ\_NUM   |
| 4     | RSTAT2\_DMA\_ENABLE |
| 5-7   | RSTAT2\_LDSTQ\_NUM  |
| 16-19 | RSTAT2\_EM\_BUSY    |
| 20-23 | RSTAT2\_EM\_ACKED   |
| 24-27 | RSTAT2\_EM\_ISWR    |
| 28-31 | RSTAT2\_EM\_DVLD    |

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>RSTAT3_MTHD_IDLE</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>RSTAT3_CTXSW_IDLE</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>RSTAT3_DMA_IDLE</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>RSTAT3_SCP_IDLE</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>RSTAT3_LDST_IDLE</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>RSTAT3_SBWB_EMPTY</p></td>
</tr>
<tr class="odd">
<td><p>6-8</p></td>
<td><p>RSTAT3_CSWIE</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>RSTAT3_CSWE</p></td>
</tr>
<tr class="odd">
<td><p>12-14</p></td>
<td><p>RSTAT3_CTXSW_STATE</p>
<p><code>0x00: IDLE</code><br />
<code>0x01: SM_CHECK</code><br />
<code>0x02: SM_SAVE</code><br />
<code>0x03: SM_SAVE_WAIT</code><br />
<code>0x04: SM_BLK_BIND</code><br />
<code>0x05: SM_RESET</code><br />
<code>0x06: SM_RESETWAIT</code><br />
<code>0x07: SM_ACK</code></p></td>
</tr>
<tr class="even">
<td><p>15</p></td>
<td><p>RSTAT3_CTXSW_PEND</p></td>
</tr>
<tr class="odd">
<td><p>17</p></td>
<td><p>RSTAT3_DMA_FBREQ_IDLE</p></td>
</tr>
<tr class="even">
<td><p>18</p></td>
<td><p>RSTAT3_DMA_ACKQ_EMPTY</p></td>
</tr>
<tr class="odd">
<td><p>19</p></td>
<td><p>RSTAT3_DMA_RDQ_EMPTY</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>RSTAT3_DMA_WR_BUSY</p></td>
</tr>
<tr class="odd">
<td><p>21</p></td>
<td><p>RSTAT3_DMA_RD_BUSY</p></td>
</tr>
<tr class="even">
<td><p>22</p></td>
<td><p>RSTAT3_LDST_XT_BUSY</p></td>
</tr>
<tr class="odd">
<td><p>23</p></td>
<td><p>RSTAT3_LDST_XT_BLOCK</p></td>
</tr>
<tr class="even">
<td><p>24</p></td>
<td><p>RSTAT3_ENG_IDLE</p></td>
</tr>
</tbody>
</table>

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
<td><p>RSTAT4_ICD_STATE</p>
<p><code>0x00: NORMAL</code><br />
<code>0x01: WAIT_ISSUE_CLEAR</code><br />
<code>0x02: WAIT_EXLDQ_CLEAR</code><br />
<code>0x03: FULL_DBG_MODE</code></p></td>
</tr>
<tr class="even">
<td><p>2-3</p></td>
<td><p>RSTAT4_ICD_MODE</p>
<p><code>0x00: SUPPRESSICD</code><br />
<code>0x01: ENTERICD_IBRK</code><br />
<code>0x02: ENTERICD_STEP</code></p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>RSTAT4_ICD_EMASK_TRAP0</p></td>
</tr>
<tr class="even">
<td><p>17</p></td>
<td><p>RSTAT4_ICD_EMASK_TRAP1</p></td>
</tr>
<tr class="odd">
<td><p>18</p></td>
<td><p>RSTAT4_ICD_EMASK_TRAP2</p></td>
</tr>
<tr class="even">
<td><p>19</p></td>
<td><p>RSTAT4_ICD_EMASK_TRAP3</p></td>
</tr>
<tr class="odd">
<td><p>20</p></td>
<td><p>RSTAT4_ICD_EMASK_EXC_UNIMP</p></td>
</tr>
<tr class="even">
<td><p>21</p></td>
<td><p>RSTAT4_ICD_EMASK_EXC_IMISS</p></td>
</tr>
<tr class="odd">
<td><p>22</p></td>
<td><p>RSTAT4_ICD_EMASK_EXC_IMHIT</p></td>
</tr>
<tr class="even">
<td><p>23</p></td>
<td><p>RSTAT4_ICD_EMASK_EXC_IBREAK</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>RSTAT4_ICD_EMASK_IV0</p></td>
</tr>
<tr class="even">
<td><p>25</p></td>
<td><p>RSTAT4_ICD_EMASK_IV1</p></td>
</tr>
<tr class="odd">
<td><p>26</p></td>
<td><p>RSTAT4_ICD_EMASK_IV2</p></td>
</tr>
<tr class="even">
<td><p>27</p></td>
<td><p>RSTAT4_ICD_EMASK_EXT0</p></td>
</tr>
<tr class="odd">
<td><p>28</p></td>
<td><p>RSTAT4_ICD_EMASK_EXT1</p></td>
</tr>
<tr class="even">
<td><p>29</p></td>
<td><p>RSTAT4_ICD_EMASK_EXT2</p></td>
</tr>
<tr class="odd">
<td><p>30</p></td>
<td><p>RSTAT4_ICD_EMASK_EXT3</p></td>
</tr>
<tr class="even">
<td><p>31</p></td>
<td><p>RSTAT4_ICD_EMASK_EXT4</p></td>
</tr>
</tbody>
</table>

| Bits | Description        |
| ---- | ------------------ |
| 0-7  | RSTAT5\_LRU\_STATE |

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
<tr class="even">
<td><p>4-5</p></td>
<td><p>FALCON_SCTL_OLD_SEC_MODE</p>
<p><code>0: Non-secure</code><br />
<code>1: Light Secure</code><br />
<code>2: Heavy Secure</code></p></td>
</tr>
<tr class="odd">
<td><p>12-13</p></td>
<td><p>Unknown</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p>Initialize the transition to LS mode</p></td>
</tr>
</tbody>
</table>

### FALCON\_SSTAT

| Bits | Description                        |
| ---- | ---------------------------------- |
| 31   | Set on memory protection violation |

### FALCON\_SPROT\_IMEM

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to Falcon IMEM.

### FALCON\_SPROT\_DMEM

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to Falcon DMEM.

### FALCON\_SPROT\_CPUCTL

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the [FALCON\_CPUCTL](#FALCON_CPUCTL "wikilink")
register.

### FALCON\_SPROT\_MISC

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the following registers:

  - FALCON\_PRIVSTATE
  - FALCON\_SFTRESET
  - FALCON\_ADDR
  - [FALCON\_DMACTL](#FALCON_DMACTL "wikilink")
  - [FALCON\_IMCTL](#FALCON_IMCTL "wikilink")
  - [FALCON\_IMSTAT](#FALCON_IMSTAT "wikilink")
  - FALCON\_UNK\_250
  - FALCON\_DMAINFO\_CTL

### FALCON\_SPROT\_IRQ

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the following registers:

  - [FALCON\_IRQMODE](#FALCON_IRQMODE "wikilink")
  - [FALCON\_IRQMSET](#FALCON_IRQMSET "wikilink")
  - [FALCON\_IRQMCLR](#FALCON_IRQMCLR "wikilink")
  - [FALCON\_IRQDEST](#FALCON_IRQDEST "wikilink")
  - FALCON\_GPTMRINT
  - FALCON\_GPTMRVAL
  - FALCON\_GPTMRCTL
  - FALCON\_IRQDEST2
  - FALCON\_UNK\_E0

### FALCON\_SPROT\_MTHD

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the following registers:

  - [FALCON\_ITFEN](#FALCON_ITFEN "wikilink")
  - FALCON\_CURCTX
  - FALCON\_NXTCTX
  - FALCON\_CTXACK
  - FALCON\_MTHDDATA
  - FALCON\_MTHDID
  - FALCON\_MTHDWDAT
  - FALCON\_MTHDCOUNT
  - FALCON\_MTHDPOP
  - FALCON\_MTHDRAMSZ
  - [FALCON\_DEBUG1](#FALCON_DEBUG1 "wikilink")

### FALCON\_SPROT\_SCTL

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the [FALCON\_SCTL](#FALCON_SCTL "wikilink")
register.

### FALCON\_SPROT\_WDTMR

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to the following registers:

  - FALCON\_WDTMRVAL
  - FALCON\_WDTMRCTL

### TSEC\_SCP\_CTL0

| Bits | Description                                                    |
| ---- | -------------------------------------------------------------- |
| 20   | Enable the [TSEC\_SCP\_CMD](#TSEC_SCP_CMD "wikilink") register |
| 16   | Enable the SEQ interface                                       |

### TSEC\_SCP\_CTL1

| Bits | Description              |
| ---- | ------------------------ |
| 0    | Flush SEQ interface      |
| 11   | Enable RND testing mode  |
| 12   | Enable the RND interface |

### TSEC\_SCP\_CFG

| Bits  | Description   |
| ----- | ------------- |
| 16-31 | Timeout value |

### TSEC\_SCP\_CTL\_STAT

| Bits | Description                       |
| ---- | --------------------------------- |
| 20   | TSEC\_SCP\_CTL\_STAT\_DEBUG\_MODE |

### TSEC\_SCP\_CTL\_LOCK

| Bits | Description          |
| ---- | -------------------- |
| 0    | Enable lockdown mode |
| 4    | Lock the SCP and RND |

Controls lockdown mode and can only be cleared in Heavy Secure mode.

### TSEC\_SCP\_CTL\_PKEY

| Bits | Description                           |
| ---- | ------------------------------------- |
| 0    | TSEC\_SCP\_CTL\_PKEY\_REQUEST\_RELOAD |
| 1    | TSEC\_SCP\_CTL\_PKEY\_LOADED          |

### TSEC\_SCP\_DBG0

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
<td><p>Index</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Automatic increment</p></td>
</tr>
<tr class="odd">
<td><p>5-6</p></td>
<td><p>Target</p>
<p><code>0: None</code><br />
<code>1: Unknown</code><br />
<code>2: Unknown</code><br />
<code>3: SEQ</code></p></td>
</tr>
<tr class="even">
<td><p>8-12</p></td>
<td><p>SEQ size</p></td>
</tr>
</tbody>
</table>

Used for debugging crypto interfaces such as the SEQ (crypto sequence).

### TSEC\_SCP\_DBG1

| Bits  | Description                      |
| ----- | -------------------------------- |
| 0-3   | SEQ instruction's first operand  |
| 4-9   | SEQ instruction's second operand |
| 10-14 | SEQ instruction's opcode         |

Used for retrieving debug data. Contains information on the last crypto
sequence created when debugging the SEQ interface.

### TSEC\_SCP\_DBG2

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
<td><p>SEQ state</p>
<p><code>0: Idle</code><br />
<code>1: Recording is active (cs0begin/cs1begin)</code></p></td>
</tr>
<tr class="even">
<td><p>4-7</p></td>
<td><p>Number of SEQ instructions left</p></td>
</tr>
<tr class="odd">
<td><p>12-15</p></td>
<td><p>Active crypto key register</p></td>
</tr>
</tbody>
</table>

Used for retrieving additional debug data associated with the SEQ
interface.

### TSEC\_SCP\_CMD

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
<td><p>Destination register</p></td>
</tr>
<tr class="even">
<td><p>8-13</p></td>
<td><p>Source register or immediate value</p></td>
</tr>
<tr class="odd">
<td><p>20-24</p></td>
<td><p>Command opcode</p>
<p><code>0x0:  nop (fuc5 opcode 0x00) </code><br />
<code>0x1:  cmov (fuc5 opcode 0x84)</code><br />
<code>0x2:  cxsin (fuc5 opcode 0x88) or xdst (with cxset)</code><br />
<code>0x3:  cxsout (fuc5 opcode 0x8C) or xdld (with cxset) </code><br />
<code>0x4:  crnd (fuc5 opcode 0x90)</code><br />
<code>0x5:  cs0begin (fuc5 opcode 0x94)</code><br />
<code>0x6:  cs0exec (fuc5 opcode 0x98)</code><br />
<code>0x7:  cs1begin (fuc5 opcode 0x9C)</code><br />
<code>0x8:  cs1exec (fuc5 opcode 0xA0)</code><br />
<code>0x9:  invalid (fuc5 opcode 0xA4)</code><br />
<code>0xA:  cchmod (fuc5 opcode 0xA8)</code><br />
<code>0xB:  cxor (fuc5 opcode 0xAC)</code><br />
<code>0xC:  cadd (fuc5 opcode 0xB0)</code><br />
<code>0xD:  cand (fuc5 opcode 0xB4)</code><br />
<code>0xE:  crev (fuc5 opcode 0xB8)</code><br />
<code>0xF:  cprecmac (fuc5 opcode 0xBC)</code><br />
<code>0x10: csecret (fuc5 opcode 0xC0)</code><br />
<code>0x11: ckeyreg (fuc5 opcode 0xC4)</code><br />
<code>0x12: ckexp (fuc5 opcode 0xC8)</code><br />
<code>0x13: ckrexp (fuc5 opcode 0xCC)</code><br />
<code>0x14: cenc (fuc5 opcode 0xD0)</code><br />
<code>0x15: cdec (fuc5 opcode 0xD4)</code><br />
<code>0x16: csigauth (fuc5 opcode 0xD8)</code><br />
<code>0x17: csigenc (fuc5 opcode 0xDC)</code><br />
<code>0x18: csigclr (fuc5 opcode 0xE0)</code></p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>Set if the command is valid</p></td>
</tr>
<tr class="odd">
<td><p>31</p></td>
<td><p>Set if running in HS mode</p></td>
</tr>
</tbody>
</table>

Contains information on the last crypto command executed.

### TSEC\_SCP\_STAT0

| Bits | Description             |
| ---- | ----------------------- |
| 2    | CMD interface is active |
| 6    | SEQ interface is active |
| 16   | RND interface is active |

Contains the status of the crypto interfaces.

### TSEC\_SCP\_STAT1

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
<td><p>Signature comparison result</p>
<p><code>0: None</code><br />
<code>1: Running</code><br />
<code>2: Failed</code><br />
<code>3: Succeeded</code></p></td>
</tr>
</tbody>
</table>

Contains the status of the last authentication attempt.

### TSEC\_SCP\_STAT2

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-4</p></td>
<td><p>Current SEQ opcode</p></td>
</tr>
<tr class="even">
<td><p>5-9</p></td>
<td><p>Unknown opcode</p></td>
</tr>
<tr class="odd">
<td><p>10-14</p></td>
<td><p>Pending CMD opcode</p></td>
</tr>
<tr class="even">
<td><p>15-16</p></td>
<td><p>AES operation</p>
<p><code>0: Encryption</code><br />
<code>1: Decryption</code><br />
<code>2: Key expansion</code><br />
<code>3: Key reverse expansion</code></p></td>
</tr>
<tr class="odd">
<td><p>27</p></td>
<td><p>RND operation is stalled</p></td>
</tr>
<tr class="even">
<td><p>29</p></td>
<td><p>AES operation is stalled</p></td>
</tr>
</tbody>
</table>

Contains the status of crypto operations.

### TSEC\_SCP\_RND\_STAT0

| Bits | Description  |
| ---- | ------------ |
| 0    | RND is ready |

Contains the status of the RND interface.

### TSEC\_SCP\_IRQSTAT

| Bits | Description |
| ---- | ----------- |
| 0    | RND ready   |
| 8    | ACL error   |
| 12   | SEC error   |
| 16   | CMD error   |
| 20   | Single step |
| 24   | RND unknown |
| 28   | Timeout     |

Used for getting the status of crypto IRQs.

### TSEC\_SCP\_IRQMASK

| Bits | Description |
| ---- | ----------- |
| 0    | RND ready   |
| 8    | ACL error   |
| 12   | SEC error   |
| 16   | CMD error   |
| 20   | Single step |
| 24   | RND unknown |
| 28   | Timeout     |

Used for getting the value of the mask for crypto IRQs.

### TSEC\_SCP\_ACL\_ERR

| Bits | Description                                            |
| ---- | ------------------------------------------------------ |
| 0    | Writing to a crypto register without the correct ACL   |
| 4    | Reading from a crypto register without the correct ACL |
| 8    | Invalid ACL change (cchmod)                            |
| 31   | ACL error occurred                                     |

Contains information on errors generated by the [ACL
error](#TSEC_SCP_IRQSTAT "wikilink") IRQ.

### TSEC\_SCP\_CMD\_ERR

| Bits | Description                                       |
| ---- | ------------------------------------------------- |
| 0    | Invalid command                                   |
| 4    | Empty crypto sequence                             |
| 8    | Crypto sequence is too long                       |
| 12   | Crypto sequence was not finished                  |
| 16   | Insecure signature (csigenc, csigclr or csigauth) |
| 20   | Invalid signature (csigauth in HS mode)           |
| 24   | Forbidden ACL change (cchmod in NS mode)          |

Contains information on errors generated by the [CMD
error](#TSEC_SCP_IRQSTAT "wikilink") IRQ.

### TSEC\_RND\_CTL0

| Bits | Description                   |
| ---- | ----------------------------- |
| 0-31 | RND clock trigger lower limit |

### TSEC\_RND\_CTL1

| Bits  | Description                   |
| ----- | ----------------------------- |
| 0-15  | RND clock trigger upper limit |
| 16-31 | RND clock trigger mask        |

### TSEC\_TFBIF\_CTL

| Bits | Description                      |
| ---- | -------------------------------- |
| 0    | TSEC\_TFBIF\_CTL\_CLR\_BWCOUNT   |
| 1    | TSEC\_TFBIF\_CTL\_ENABLE         |
| 2    | TSEC\_TFBIF\_CTL\_CLR\_IDLEWDERR |
| 3    | TSEC\_TFBIF\_CTL\_RESET          |
| 4    | TSEC\_TFBIF\_CTL\_IDLE           |
| 5    | TSEC\_TFBIF\_CTL\_IDLEWDERR      |
| 6    | TSEC\_TFBIF\_CTL\_SRTOUT         |
| 7    | TSEC\_TFBIF\_CTL\_CLR\_SRTOUT    |
| 8-11 | TSEC\_TFBIF\_CTL\_SRTOVAL        |
| 12   | TSEC\_TFBIF\_CTL\_VPR            |

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

### TSEC\_TFBIF\_MCCIF\_FIFOCTRL1

| Bits  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| 0-15  | TSEC\_TFBIF\_MCCIF\_FIFOCTRL1\_SRD2MC\_REORDER\_DEPTH\_LIMIT |
| 16-31 | TSEC\_TFBIF\_MCCIF\_FIFOCTRL1\_SWR2MC\_REORDER\_DEPTH\_LIMIT |

### TSEC\_TFBIF\_THROTTLE

| Bits  | Description                         |
| ----- | ----------------------------------- |
| 0-11  | TSEC\_TFBIF\_THROTTLE\_BUCKET\_SIZE |
| 16-27 | TSEC\_TFBIF\_THROTTLE\_LEAK\_COUNT  |
| 30-31 | TSEC\_TFBIF\_THROTTLE\_LEAK\_SIZE   |

### TSEC\_TFBIF\_DBG\_STAT0

| Bits | Description                                       |
| ---- | ------------------------------------------------- |
| 0    | TSEC\_TFBIF\_DBG\_STAT0\_1K\_TRANSFER             |
| 1    | TSEC\_TFBIF\_DBG\_STAT0\_RREQ\_ISSUED             |
| 2    | TSEC\_TFBIF\_DBG\_STAT0\_WREQ\_ISSUED             |
| 3    | TSEC\_TFBIF\_DBG\_STAT0\_TAGQ\_ISSUED             |
| 4    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_RDATQ             |
| 5    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_RACKQ             |
| 6    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_WREQQ             |
| 7    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_WDATQ             |
| 8    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_WACKQ             |
| 9    | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_RREQ\_PENDING     |
| 10   | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_WREQ\_PENDING     |
| 11   | TSEC\_TFBIF\_DBG\_STAT0\_STALL\_MREQ              |
| 12   | TSEC\_TFBIF\_DBG\_STAT0\_ENGINE\_IDLE             |
| 13   | TSEC\_TFBIF\_DBG\_STAT0\_RMCCIF\_IDLE             |
| 14   | TSEC\_TFBIF\_DBG\_STAT0\_WMCCIF\_IDLE             |
| 15   | TSEC\_TFBIF\_DBG\_STAT0\_CSB\_IDLE                |
| 16   | TSEC\_TFBIF\_DBG\_STAT0\_RU\_IDLE                 |
| 17   | TSEC\_TFBIF\_DBG\_STAT0\_WU\_IDLE                 |
| 19   | TSEC\_TFBIF\_DBG\_STAT0\_UNWEIGHT\_ACTMON\_ACTIVE |
| 20   | TSEC\_TFBIF\_DBG\_STAT0\_UNWEIGHT\_ACTMON\_MCB    |

### TSEC\_TFBIF\_SPROT\_EMEM

| Bits | Description        |
| ---- | ------------------ |
| 0-3  | Read access level  |
| 4-7  | Write access level |

Controls accesses to external memory regions. Accessible in HS mode
only.

### TSEC\_TFBIF\_TRANSCFG

| Bits | Description                       |
| ---- | --------------------------------- |
| 0    | TSEC\_TFBIF\_TRANSCFG\_ATT0\_SWID |
| 4    | TSEC\_TFBIF\_TRANSCFG\_ATT1\_SWID |
| 8    | TSEC\_TFBIF\_TRANSCFG\_ATT2\_SWID |
| 12   | TSEC\_TFBIF\_TRANSCFG\_ATT3\_SWID |
| 16   | TSEC\_TFBIF\_TRANSCFG\_ATT4\_SWID |
| 20   | TSEC\_TFBIF\_TRANSCFG\_ATT5\_SWID |
| 24   | TSEC\_TFBIF\_TRANSCFG\_ATT6\_SWID |
| 28   | TSEC\_TFBIF\_TRANSCFG\_ATT7\_SWID |

Configures the software ID per CTXDMA port for memory transactions.
Software ID 0 (HW\_SWID) forces all transactions to go through the SMMU
while software ID 1 (PHY\_SWID) bypasses it. Accessible in HS mode only.

\[6.0.0+\] The nvhost\_tsec firmware sets this register to 0x10 or
0x111110 before reading memory from the GPU UCODE carveout.

### TSEC\_TFBIF\_REGIONCFG

| Bits  | Description                           |
| ----- | ------------------------------------- |
| 0-2   | TSEC\_TFBIF\_REGIONCFG\_T0\_APERT\_ID |
| 3     | TSEC\_TFBIF\_REGIONCFG\_T0\_VPR       |
| 4-6   | TSEC\_TFBIF\_REGIONCFG\_T1\_APERT\_ID |
| 7     | TSEC\_TFBIF\_REGIONCFG\_T1\_VPR       |
| 8-10  | TSEC\_TFBIF\_REGIONCFG\_T2\_APERT\_ID |
| 11    | TSEC\_TFBIF\_REGIONCFG\_T2\_VPR       |
| 12-14 | TSEC\_TFBIF\_REGIONCFG\_T3\_APERT\_ID |
| 15    | TSEC\_TFBIF\_REGIONCFG\_T3\_VPR       |
| 16-18 | TSEC\_TFBIF\_REGIONCFG\_T4\_APERT\_ID |
| 19    | TSEC\_TFBIF\_REGIONCFG\_T4\_VPR       |
| 20-22 | TSEC\_TFBIF\_REGIONCFG\_T5\_APERT\_ID |
| 23    | TSEC\_TFBIF\_REGIONCFG\_T5\_VPR       |
| 24-26 | TSEC\_TFBIF\_REGIONCFG\_T6\_APERT\_ID |
| 27    | TSEC\_TFBIF\_REGIONCFG\_T6\_VPR       |
| 28-30 | TSEC\_TFBIF\_REGIONCFG\_T7\_APERT\_ID |
| 31    | TSEC\_TFBIF\_REGIONCFG\_T7\_VPR       |

Configures the aperture ID and VPR mode per CTXDMA port for memory
region accessing. Accessible in HS mode only.

\[6.0.0+\] The nvhost\_tsec firmware sets this register to 0x20 or 0x140
before reading memory from the GPU UCODE carveout.

### TSEC\_TFBIF\_ACTMON\_ACTIVE\_MASK

Takes the memory access mask for the Activity Monitor. Disconnected on
the TSEC, but available on NVDEC, NVENC and NVJPG.

### TSEC\_TFBIF\_ACTMON\_ACTIVE\_BORPS

Takes the billions of records per second count for the Activity Monitor.
Disconnected on the TSEC, but available on NVDEC, NVENC and NVJPG.

### TSEC\_TFBIF\_ACTMON\_ACTIVE\_WEIGHT

Controls the Activity Monitor. Disconnected on the TSEC, but available
on NVDEC, NVENC and NVJPG.

### TSEC\_CG

| Bits  | Description                  |
| ----- | ---------------------------- |
| 0-5   | TSEC\_CG\_IDLE\_CG\_DLY\_CNT |
| 6     | TSEC\_CG\_IDLE\_CG\_EN       |
| 16-18 | TSEC\_CG\_WAKEUP\_DLY\_CNT   |
| 19    | TSEC\_CG\_WAKEUP\_DLY\_EN    |

### TSEC\_BAR0\_CTL

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>TSEC_BAR0_CTL_READ</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>TSEC_BAR0_CTL_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>4-7</p></td>
<td><p>TSEC_BAR0_CTL_BYTE_MASK</p></td>
</tr>
<tr class="even">
<td><p>12-13</p></td>
<td><p>TSEC_BAR0_CTL_STATUS</p>
<p><code>0: Idle</code><br />
<code>1: Busy</code><br />
<code>2: Error</code><br />
<code>3: Disabled</code></p></td>
</tr>
<tr class="odd">
<td><p>31</p></td>
<td><p>TSEC_BAR0_CTL_INIT</p></td>
</tr>
</tbody>
</table>

A BAR0 DMA read/write operation requires bits TSEC\_BAR0\_CTL\_INIT and
TSEC\_BAR0\_CTL\_READ/TSEC\_BAR0\_CTL\_WRITE to be set in
TSEC\_BAR0\_CTL.

During the transfer, TSEC\_BAR0\_CTL\_STATUS is set to "Busy".

Accessing an invalid address sets TSEC\_BAR0\_CTL\_STATUS to "Error".

### TSEC\_BAR0\_ADDR

Takes the address for DMA transfers between TSEC and HOST1X (master and
clients).

### TSEC\_BAR0\_DATA

Takes the data for DMA transfers between TSEC and HOST1X (master and
clients).

### TSEC\_BAR0\_TIMEOUT

Takes the timeout value for DMA transfers between TSEC and HOST1X
(master and clients).

### TSEC\_TEGRA\_CTL

| Bits | Description                                      |
| ---- | ------------------------------------------------ |
| 16   | TSEC\_TEGRA\_CTL\_TKFI\_KFUSE                    |
| 17   | TSEC\_TEGRA\_CTL\_TKFI\_RESTART\_FSM\_KFUSE      |
| 24   | TSEC\_TEGRA\_CTL\_TMPI\_FORCE\_IDLE\_INPUTS\_I2C |
| 25   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_HOST1X     |
| 26   | TSEC\_TEGRA\_CTL\_TMPI\_RESTART\_FSM\_APB        |
| 27   | TSEC\_TEGRA\_CTL\_TMPI\_DISABLE\_OUTPUT\_I2C     |

## Falcon

"Falcon" (FAst Logic CONtroller) is a proprietary general purpose CPU
which can be found inside various hardware blocks that require some sort
of logic processing such as TSEC (TSECA and TSECB), NVDEC, NVENC, NVJPG,
VIC, GPU PMU and XUSB.

### Processor Registers

A total of 32 processor registers are available in the Falcon CPU.

#### REG0-REG15

These are 16 32-bit GPRs (general purpose registers).

#### IV0

This is a SPR (special purpose register) that holds the address for
interrupt vector 0.

#### IV1

This is a SPR (special purpose register) that holds the address for
interrupt vector 1.

#### IV2

This is a SPR (special purpose register) that holds the address for
interrupt vector 2. This register is considered "UNDEFINED" and appears
to be unused.

#### EV

This is a SPR (special purpose register) that holds the address for the
exception vector.

Alternative name (envytools): "tv".

#### SP

This is a SPR (special purpose register) that holds the current stack
pointer.

#### PC

This is a SPR (special purpose register) that holds the current program
counter.

#### IMB

This is a SPR (special purpose register) that holds the external base
address for IMEM transfers.

Alternative name (envytools): "xcbase".

#### DMB

This is a SPR (special purpose register) that holds the external base
address for DMEM transfers.

Alternative name (envytools): "xdbase".

#### CSW

This is a SPR (special purpose register) that holds various flag bits.

| Bits  | Description                          |
| ----- | ------------------------------------ |
| 0-7   | General purpose predicates           |
| 8     | ALU carry flag                       |
| 9     | ALU signed overflow flag             |
| 10    | ALU sign flag                        |
| 11    | ALU zero flag                        |
| 12-15 | Unused                               |
| 16    | Interrupt 0 enable                   |
| 17    | Interrupt 1 enable                   |
| 18    | Interrupt 2 enable (undefined)       |
| 19    | Unused                               |
| 20    | Interrupt 0 saved enable             |
| 21    | Interrupt 1 saved enable             |
| 22    | Interrupt 2 saved enable (undefined) |
| 23    | Unused                               |
| 24    | Exception active                     |
| 25    | Unused                               |
| 26    | Unknown                              |
| 27-28 | Unused                               |
| 29    | Unknown                              |
| 30-31 | Unused                               |

Alternative name (envytools): "flags".

#### CCR

This is a SPR (special purpose register) that holds configuration bits
for the SCP DMA override functionality. The value of this register is
set using the "cxset" instruction which provides a way to change the
behavior of a variable amount of successively executed DMA-related
instructions ("xdwait", "xdst" and "xdld").

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-4</p></td>
<td><p>Number of instructions the override is valid for (0x1F means infinite)</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>Crypto destination/source select</p>
<p><code>0: Crypto register</code><br />
<code>1: Crypto stream</code></p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>External memory override</p>
<p><code>0: Disabled</code><br />
<code>1: Enabled</code></p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>Internal memory select</p>
<p><code>0: DMEM</code><br />
<code>1: IMEM</code></p></td>
</tr>
<tr class="odd">
<td><p>8-31</p></td>
<td><p>Unused</p></td>
</tr>
</tbody>
</table>

Alternative name (envytools): "cx".

#### SEC

This is a SPR (special purpose register) that holds configuration bits
for the SCP authentication process.

| Bits  | Description                                      |
| ----- | ------------------------------------------------ |
| 0-7   | Start of region to authenticate (in 0x100 pages) |
| 8-15  | Unused                                           |
| 16    | Mark all subsequent code transfers as secret     |
| 17    | Region is encrypted                              |
| 18    | Unknown (set in HS mode)                         |
| 19    | Block traps and interrupts (set in HS mode)      |
| 20-23 | Unused                                           |
| 24-31 | Size of region to authenticate (in 0x100 pages)  |

Alternative name (envytools): "cauth".

#### CTX

This is a SPR (special purpose register) that holds configuration bits
for the CTXDMA ports.

| Bits  | Description                           |
| ----- | ------------------------------------- |
| 0-2   | CTXDMA port for code loads (xcld)     |
| 3     | Unused                                |
| 4-6   | CTXDMA port for code stores (invalid) |
| 7     | Unused                                |
| 8-10  | CTXDMA port for data loads (xdld)     |
| 11    | Unused                                |
| 12-14 | CTXDMA port for data stores (xdst)    |
| 15-31 | Unused                                |

Alternative name (envytools): "xtargets".

#### EXCI

This is a SPR (special purpose register) that holds information on
raised exceptions.

| Bits  | Description     |
| ----- | --------------- |
| 0-19  | Exception PC    |
| 20-23 | Exception cause |
| 24-31 | Unused          |

Alternative name (envytools): "tstatus".

#### SEC1

Unknown. Marked as "RESERVED".

#### IMB1

Unknown. Marked as "RESERVED".

#### DMB1

Unknown. Marked as "RESERVED".

## SCP

Part of the information here (which hasn't made it into envytools
documentation yet) was shared by
[mwk](https://wiki.0x04.net/wiki/Marcin_Ko%C5%9Bcielnicki) from reverse
engineering falcon processors over the years.

### Heavy Secure Mode

#### Entry

From non-secure mode, upon jumping to a page marked as secret, a secret
fault occurs. This causes the CPU to verify the region specified in
$cauth against the MAC loaded in $c6. If the comparison is successful,
the valid bit (bit0) is set on all pages in the $cauth region, and $pc
is set to the base of the $cauth region. If the comparsion fails, the
CPU is halted.

#### Exit

The CPU automatically goes back to non-secure mode when returning back
into non-secret pages. When this happens, the valid bit (bit0) in the
TLB flags is cleared for all secret pages.

#### Implementation

Under certain circumstances, it is possible to observe
[sigauth](#sigauth "wikilink") being briefly written to
[TSEC\_SCP\_CMD](#TSEC_SCP_CMD "wikilink") as "csigauth $c4 $c6" while
the opcodes in [TSEC\_SCP\_STAT2](#TSEC_SCP_STAT2 "wikilink") are set to
"cxsin" and "csigauth", respectively.

Via [TSEC\_SCP\_DBG0](#TSEC_SCP_DBG0 "wikilink") it can be observed that
a 3-sized macro sequence is loaded into cs0 during a secure mode
transition.

### Operations

| Opcode | Name                           | Operand0 | Operand1 | Operation                                                                    | Condition                      |
| ------ | ------------------------------ | -------- | -------- | ---------------------------------------------------------------------------- | ------------------------------ |
| 0      | nop                            | N/A      | N/A      |                                                                              |                                |
| 1      | mov                            | $cX      | $cY      | `$cX = $cY; ACL(X) = ACL(Y);`                                                |                                |
| 2      | sin                            | $cX      | N/A      | `$cX = read_stream(); ACL(X) = ???;`                                         |                                |
| 3      | sout                           | $cX      | N/A      | `write_stream($cX);`                                                         | ?                              |
| 4      | [rnd](#rnd "wikilink")         | $cX      | N/A      | `$cX = read_rnd(); ACL(X) = ???;`                                            |                                |
| 5      | s0begin                        | immX     | N/A      | `record_macro_for_N_instructions(0, immX);`                                  |                                |
| 6      | s0exec                         | immX     | N/A      | `execute_macro_N_times(0, immX);`                                            |                                |
| 7      | s1begin                        | immX     | N/A      | `record_macro_for_N_instructions(1, immX);`                                  |                                |
| 8      | s1exec                         | immX     | N/A      | `execute_macro_N_times(1, immX);`                                            |                                |
| 9      | <invalid>                      |          |          |                                                                              |                                |
| 0xA    | [chmod](#chmod "wikilink")     | $cX      | immY     | Complicated, see [ACL](#ACL "wikilink").                                     |                                |
| 0xB    | xor                            | $cX      | $cY      | `$cX ^= $cY;`                                                                | `(ACL(X) & 2) && (ACL(Y) & 2)` |
| 0xC    | add                            | $cX      | immY     | `$cX += immY;`                                                               | `(ACL(X) & 2)`                 |
| 0xD    | and                            | $cX      | $cY      | `$cX &= $cY;`                                                                | `(ACL(X) & 2) && (ACL(Y) & 2)` |
| 0xE    | rev                            | $cX      | $cY      | `$cX = endian_swap128($cY); ACL(X) = ACL(Y);`                                |                                |
| 0xF    | gfmul                          | $cX      | $cY      | `$cX = gfmul($cY); ACL(X) = ACL(Y);`                                         | `(ACL(Y) & 2)`                 |
| 0x10   | secret                         | $cX      | immY     | `$cX = load_secret(immY); ACL(X) = load_secret_acl(immY);`                   |                                |
| 0x11   | keyreg                         | immX     | N/A      | `active_key_idx = immX;`                                                     |                                |
| 0x12   | kexp                           | $cX      | $cY      | `$cX = aes_kexp($cY); ACL(X) = ACL(Y);`                                      |                                |
| 0x13   | krexp                          | $cX      | $cY      | `$cX = aes_kexp_reverse($cY); ACL(X) = ACL(Y);`                              |                                |
| 0x14   | enc                            | $cX      | $cY      | `$cX = aes_enc(active_key_idx, $cY); ACL(X) = ACL(active_key_idx) & ACL(Y);` |                                |
| 0x15   | dec                            | $cX      | $cY      | `$cX = aes_dec(active_key_idx, $cY); ACL(X) = ACL(active_key_idx) & ACL(Y);` |                                |
| 0x16   | [sigauth](#sigauth "wikilink") | $cX      | $cY      | `if (hash_verify($cX, $cY)) { has_sig = true; current_sig = $cX; }`          | ?                              |
| 0x17   | [sigclr](#sigclr "wikilink")   | N/A      | N/A      | `has_sig = false;`                                                           |                                |
| 0x18   | sigenc                         | $cX      | $cY      | `if (has_sig) { $cX = aes_enc($cY, current_sig); ACL(X) = 0x13; }`           |                                |

#### sigauth

`00000000: f5 3c XY d8 csigauth $cY $cX`

Takes 2 crypto registers as operands and is automatically executed when
jumping to a code region previously uploaded as secret. This instruction
does not work in secure mode.

#### sigclr

`00000000: f5 3c 00 e0 csigclr`

This instruction takes no operands and clears the saved cauth signature
used by the csigenc instruction.

#### chmod

`00000000: f5 3c XY a8 cchmod $cY 0X` or `00000000: f5 3c XY a9 cchmod
$cY 1X`

This instruction takes a crypto register and a 5 bit immediate value
which represents the [ACL](#ACL "wikilink") mask to set.

#### rnd

`00000000: f5 3c 0X 90 crnd $cX`

This instruction initializes a crypto register with random data.

Executing this instruction only succeeds if the RND interface is enabled
for the SCP, which requires taking the following steps:

  - Write 0x7FFF to [TSEC\_RND\_CTL0](#TSEC_RND_CTL0 "wikilink").
  - Write 0x3FF0000 to [TSEC\_RND\_CTL1](#TSEC_RND_CTL1 "wikilink").
  - Write 0xFF00 to TSEC\_RND\_CTL11.
  - Write 0x1000 to [TSEC\_SCP\_CTL1](#TSEC_SCP_CTL1 "wikilink").

Otherwise it hangs forever.

### ACL

| Bit | Meaning                                                                                                |
| --- | ------------------------------------------------------------------------------------------------------ |
| 0   | Secure key. Forced set if bit1 is set. Once cleared, cannot be set again.                              |
| 1   | Secure readable. Once cleared, cannot be set again.                                                    |
| 2   | Insecure key. Forced set if bit3 is set. Forced clear if bit0 is clear. Can be toggled back and forth. |
| 3   | Insecure readable. Forced clear if bit1 is clear. Can be toggled back and forth.                       |
| 4   | Insecure overwritable. Can be toggled back and forth.                                                  |

#### Initial values

On SCP boot, the ACL is 0x1F for all $cX.

Loading into $cX using xdst instruction sets ACL($cX) to 0x13 and 0x1F,
for secure and insecure mode respectively.

Spilling a $cX to DMEM using xdld instruction is allowed if (ACL($cX) &
2) or (ACL($cX) & 8), for secure and insecure mode respectively.

Loading a secret into $cX sets a per-secret ACL, unconditionally.

### Secrets

Falcon's Heavy Secure Mode has access to 64 128-bit keys which are
burned at factory. These keys can be loaded using the $csecret
instruction which takes the target crypto register and the key index as
arguments.

Secrets are specific to each Falcon unit with the exception of secret
0x3F. This secret is effectively empty (all zeros), but is configured to
be overwritten with the KFUSE private key once the KFUSE clock is
enabled. The KFUSE private key is console-unique.

| Index | ACL  | Notes                                                                                                                                                                            |
| ----- | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x00  | 0x13 | Used by [Keygen](TSEC%20Firmware#Keygen.md##Keygen "wikilink"), nvhost\_tsec, nvhost\_nvdec\_bl020\_prod, nvhost\_nvdec020\_prod, nvhost\_nvdec020\_ns and acr\_ucode firmwares. |
| 0x01  | 0x10 | Used by nvhost\_nvdec\_bl020\_prod firmware.                                                                                                                                     |
| 0x02  | 0x10 |                                                                                                                                                                                  |
| 0x03  | 0x11 | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                                                                 |
| 0x04  | 0x10 | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                                                                 |
| 0x05  | 0x13 | Used by nvhost\_tsec, nvhost\_nvdec\_bl020\_prod, nvhost\_nvdec020\_prod, nvhost\_nvdec020\_ns and acr\_ucode firmwares.                                                         |
| 0x06  | 0x11 |                                                                                                                                                                                  |
| 0x07  | 0x11 | Used by \[6.0.0+\] nvhost\_tsec firmware.                                                                                                                                        |
| 0x08  | 0x10 |                                                                                                                                                                                  |
| 0x09  | 0x13 | Used by nvhost\_tsec firmware.                                                                                                                                                   |
| 0x0A  | 0x11 |                                                                                                                                                                                  |
| 0x0B  | 0x10 | Used by nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                                                                                 |
| 0x0C  | 0x13 |                                                                                                                                                                                  |
| 0x0D  | 0x11 |                                                                                                                                                                                  |
| 0x0E  | 0x10 |                                                                                                                                                                                  |
| 0x0F  | 0x13 | Used by nvhost\_tsec firmware.                                                                                                                                                   |
| 0x10  | 0x11 | Used by \[1.0.0-5.1.0\] nvhost\_tsec firmware.                                                                                                                                   |
| 0x11  | 0x10 |                                                                                                                                                                                  |
| 0x12  | 0x13 |                                                                                                                                                                                  |
| 0x13  | 0x11 |                                                                                                                                                                                  |
| 0x14  | 0x10 |                                                                                                                                                                                  |
| 0x15  | 0x13 | Used by nvhost\_nvdec\_bl020\_prod, \[5.0.0+\] nvhost\_nvdec020\_prod, \[5.0.0+\] nvhost\_nvdec020\_ns and \[6.0.0+\] nvhost\_tsec firmwares.                                    |
| 0x16  | 0x11 |                                                                                                                                                                                  |
| 0x17  | 0x10 |                                                                                                                                                                                  |
| 0x18  | 0x13 |                                                                                                                                                                                  |
| 0x19  | 0x11 |                                                                                                                                                                                  |
| 0x1A  | 0x10 |                                                                                                                                                                                  |
| 0x1B  | 0x13 |                                                                                                                                                                                  |
| 0x1C  | 0x11 |                                                                                                                                                                                  |
| 0x1D  | 0x10 |                                                                                                                                                                                  |
| 0x1E  | 0x13 |                                                                                                                                                                                  |
| 0x1F  | 0x11 |                                                                                                                                                                                  |
| 0x20  | 0x10 |                                                                                                                                                                                  |
| 0x21  | 0x13 |                                                                                                                                                                                  |
| 0x22  | 0x11 |                                                                                                                                                                                  |
| 0x23  | 0x10 |                                                                                                                                                                                  |
| 0x24  | 0x13 |                                                                                                                                                                                  |
| 0x25  | 0x11 |                                                                                                                                                                                  |
| 0x26  | 0x10 | Used by [KeygenLdr](TSEC%20Firmware#KeygenLdr.md##KeygenLdr "wikilink") and [SecureBoot](TSEC%20Firmware#SecureBoot.md##SecureBoot "wikilink")                                   |
| 0x27  | 0x13 |                                                                                                                                                                                  |
| 0x28  | 0x11 |                                                                                                                                                                                  |
| 0x29  | 0x10 |                                                                                                                                                                                  |
| 0x2A  | 0x13 |                                                                                                                                                                                  |
| 0x2B  | 0x11 |                                                                                                                                                                                  |
| 0x2C  | 0x10 |                                                                                                                                                                                  |
| 0x2D  | 0x13 |                                                                                                                                                                                  |
| 0x2E  | 0x11 |                                                                                                                                                                                  |
| 0x2F  | 0x10 |                                                                                                                                                                                  |
| 0x30  | 0x13 |                                                                                                                                                                                  |
| 0x31  | 0x11 |                                                                                                                                                                                  |
| 0x32  | 0x10 |                                                                                                                                                                                  |
| 0x33  | 0x13 |                                                                                                                                                                                  |
| 0x34  | 0x11 |                                                                                                                                                                                  |
| 0x35  | 0x10 |                                                                                                                                                                                  |
| 0x36  | 0x13 |                                                                                                                                                                                  |
| 0x37  | 0x11 |                                                                                                                                                                                  |
| 0x38  | 0x10 |                                                                                                                                                                                  |
| 0x39  | 0x13 |                                                                                                                                                                                  |
| 0x3A  | 0x11 |                                                                                                                                                                                  |
| 0x3B  | 0x10 |                                                                                                                                                                                  |
| 0x3C  | 0x13 | Used by nvhost\_tsec firmware.                                                                                                                                                   |
| 0x3D  | 0x11 |                                                                                                                                                                                  |
| 0x3E  | 0x10 |                                                                                                                                                                                  |
| 0x3F  | 0x10 | Used by [Keygen](TSEC%20Firmware#Keygen.md##Keygen "wikilink"), nvhost\_tsec, nvhost\_nvdec020\_prod and nvhost\_nvdec020\_ns firmwares.                                         |
