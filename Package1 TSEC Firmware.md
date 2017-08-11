TSEC is a nvidia falcon processor with crypto extensions.

Firmware can be disassembled with
[envytools'](http://envytools.readthedocs.io/en/latest/)
[envydis](https://github.com/envytools/envytools/tree/master/envydis):

`envydis -i tsec_fw.bin -m falcon -V fuc5 -F crypt`

Note that the instruction set has variable length instructions, and the
disassembler is not very good at detecting locations it should start
disassembling from. One needs to disassemble multiple sub-regions and
join them together.

## Additional Notes on Crypto Extensions

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

## Annotated Assembly

Keep in mind the architecture is not officially documented, so some
things may be
    incorrect.

    00000000: 4d 00 42              mov $r13 0x4200                     ; UC_CAPS
    00000003: cf dd 00              iord $r13 I[$r13]
    00000006: b6 d5 09              shr b32 $r13 0x9
    00000009: f1 d4 ff 01           and $r13 0x1ff
    0000000d: b6 d4 08              shl b32 $r13 0x8                    ; r13 = falcon data segment size
    00000010: fe d4 00              mov $sp $r13                        ; put stack top all the way at the end
    00000013: 7e 19 00 00           lcall 0x19
    00000017: f8 02                 exit
    
    00000019: 0f f0              C  mov $r15 -0x10
    0000001b: f5 30 e4 fe           add $sp -0x11c
    0000001f: f9 82                 mpush $r8
    00000021: fe 49 01              mov $r9 $sp
    00000024: 90 99 c4              add b32 $r9 $r9 0xc4
    00000027: ff 9f 34              and $r3 $r9 $r15                    ; r3 = (sp + 0xc4) & ~0xf
    0000002a: 92 99 8b              sub b32 $r9 $r9 0x8b
    0000002d: 85 00 03 00           mov $r5 0x300
    00000031: ff 9f 44              and $r4 $r9 $r15                    ; r4 = (sp + 0x39) & ~0xf
    00000034: b2 5b                 mov b32 $r11 $r5
    00000036: 0c 7c                 mov $r12 0x7c
    00000038: b2 3a                 mov b32 $r10 $r3
    0000003a: 7e 0b 02 00           lcall 0x20b                         ; memcpy_i2d(dst=r3{local}, src=0x300, len=0x7c)
    0000003e: 98 3c 1d              ld b32 $r12 D[$r3+TSecLoaderInfo.secure_loader_len] ; r12 = 0x600
    00000041: 95 59 08              shr b32 $r9 $r5 0x8
    00000044: 8b 00 04 00           mov $r11 0x400
    00000048: b0 91 09              st b32 D[$sp+0x24] $r9
    0000004b: bd a4                 clear b32 $r10                      ; temp copy for next step
    0000004d: 7e 0b 02 00           lcall 0x20b                         ; memcpy_i2d(dst=0, src=0x400, len=0x600)
    00000051: 98 3c 1d              ld b32 $r12 D[$r3+TSecLoaderInfo.secure_loader_len] ; r12 = 0x600
    00000054: b2 5a                 mov b32 $r10 $r5
    00000056: bd b4                 clear b32 $r11
    00000058: b2 5d                 mov b32 $r13 $r5
    0000005a: 0e 01                 mov $r14 0x1                        ; copy the code originally @ I:0x400 to I:0x300 and mark secret
    0000005c: 7e c2 01 00           lcall 0x1c2                         ; memcpy_d2i_ex(dst_page_offset=0x300, src=0, len=0x600, dst=0x300, is_secret=1)
    00000060: 89 00 00 06           mov $r9 0x60000                     ; will be used as size bits for xdst @ 000000e1
    00000064: 90 4f 20              add b32 $r15 $r4 0x20               ; TSecLoaderInfo.field_20
    00000067: bd 64                 clear b32 $r6
    00000069: ff f9 75              or $r7 $r15 $r9
    0000006c: bd 24                 clear b32 $r2                       ; loop_count = 0
    0000006e: bd 94                 clear b32 $r9
    00000070: bd 84                 clear b32 $r8                       ; ext_offset = 0
    00000072: 3e 78 00 00           lbra 0x78
    loop_set_ignored_cmd:
    00000076: b2 19               B mov b32 $r9 $r1                     ; i guess this is because SCRATCH0 retains the old cmd
    loop:
    00000078: 90 22 01            B add b32 $r2 $r2 0x1
    0000007b: 8f 01 09 3d           mov $r15 0x3d0901   ; 4000001
    0000007f: a6 2f                 cmp b32 $r2 $r15
    00000081: f4 1b 17              bra ne 0x98                         ; for (u32 r2 = 0; r2 < 4000000; r2++) {
    set_status_c0_loop_expired:
    00000084: df c0 c0 c0 c0        mov $r15 0xc0c0c0c0
    00000089: 49 00 11              mov $r9 0x1100
    0000008c: fa 9f 00              iowr I[$r9] $r15                    ; SCRATCH1 = 0xc0c0c0c0
    0000008f: d0 c0 c0 c0 c0        mov $r0 0xc0c0c0c0
    00000094: 3e 0c 01 00           lbra 0x10c                          ; -> writeback_key_and_ret
    read_next_command:
    00000098: 4f 00 10            B mov $r15 0x1000
    0000009b: ff f8 1f              iord $r1 I[$r15+$r8*0x4]            ; r1 = SCRATCH0 (cmd)
    0000009e: b3 14 64 18           bra b32 $r1 0x64 ne 0xb6            ; -> dispatch_command
    handle_command_0x64:
    000000a2: df b0 b0 b0 b0        mov $r15 0xb0b0b0b0
    000000a7: 49 00 11              mov $r9 0x1100
    000000aa: fa 9f 00              iowr I[$r9] $r15                    ; SCRATCH1 = 0xb0b0b0b0
    000000ad: d0 b0 b0 b0 b0        mov $r0 0xb0b0b0b0
    000000b2: 3e 0c 01 00           lbra 0x10c                          ; -> writeback_key_and_ret
    dispatch_command:
    000000b6: a6 19               B cmp b32 $r1 $r9
    000000b8: f4 0b c0              bra e 0x78                          ; if (cmd == ignored_cmd) continue;
    000000bb: b3 10 00 3b           bra b32 $r1 0x0 e 0xf6              ; if (cmd == 0) set_status_b0_ok_and_continue;
    000000bf: b0 16 03              cmp b32 $r1 0x3
    000000c2: f4 0c 56              bra a 0x118                         ; if (cmd > 3) return BAD_CMD;
    000000c5: b2 4a                 mov b32 $r10 $r4
    000000c7: b2 3b                 mov b32 $r11 $r3
    000000c9: 0c 7c                 mov $r12 0x7c                       ; make another copy of the ldr_info (secure_loader will zero it before return)
    000000cb: 7e 37 02 00           lcall 0x237                         ; memcpy_d2d(dst=r4{local}, src=r3{local}, len=0x7c)
    000000cf: 98 49 1d              ld b32 $r9 D[$r4+TSecLoaderInfo.secure_loader_len]  ; code_size = 0x600
    000000d2: b4 f0 09              ld b32 $r15 D[$sp+0x24]             ; secure_loader_dst_page = 0x300 >> 8
    000000d5: b6 94 10              shl b32 $r9 0x10
    000000d8: fd 9f 05              or $r9 $r15
    000000db: fe 9a 00              mov $cauth $r9                      ; cauth = (code_size << 16) | secure_loader_dst_page
    000000de: f4 3c 02              cxset 0x2                           ; dma_override(type=crypto_reg, count=2)
    000000e1: fa 87 06              xdst $r8 $r7                        ; crypto_reg_load(crypto_reg=$c6, local_address=r4+0x20)
    000000e4: f8 03                 xdwait
    000000e6: b2 6c                 mov b32 $r12 $r6
    000000e8: b2 4a                 mov b32 $r10 $r4
    000000ea: b2 1b                 mov b32 $r11 $r1
    000000ec: 06 01                 mov $r6 0x1                         ; set loader_called=1 for next iterations
    000000ee: f9 55                 call $r5                            ; secure_loader_thunk(ldr_info{r4 local}, cmd, skip_copy_and_decrypt=loader_called)
    000000f0: b2 a0                 mov b32 $r0 $r10
    000000f2: b3 a4 00 09           bra b32 $r10 0x0 ne 0xfb            ; if (rv != 0) { SCRATCH1 = rv; return; }
    set_status_b0_ok_and_continue:
    000000f6: d0 b0 b0 b0 b0      B mov $r0 0xb0b0b0b0                  ; else { SCRATCH1 = 0xb0b0b0b0; continue; }
    write_status_and_key: // returns if status != 0xb0b0b0b0
    000000fb: 49 00 11            B mov $r9 0x1100
    000000fe: fa 90 00              iowr I[$r9] $r0                     ; SCRATCH1 = rv
    00000101: df b0 b0 b0 b0        mov $r15 0xb0b0b0b0
    00000106: a6 0f                 cmp b32 $r0 $r15
    00000108: f5 0b 6e ff           bra e 0x76                          ; -> loop_set_ignored_cmd (continue)
    writeback_key_and_ret:
    0000010c: b2 3a               B mov b32 $r10 $r3                    ; somehow secure_payload writes back to this..?
    0000010e: 7e 77 01 00           lcall 0x177                         ; write128_via_SOR(r3{local})
    00000112: b2 0a                 mov b32 $r10 $r0
    00000114: fb 83 1c 01           mpopaddret $r8, 0x11c               ; was: mpopunk [unknown: 00 80 1c 01]
    set_status_d0_bad_cmd:
    00000118: d0 d0 d0 d0 d0      B mov $r0 0xd0d0d0d0                  ; rv = 0xd0d0d0d0
    0000011d: 3e fb 00 00           lbra 0xfb
    
    // wait_1c000()
    // 0x1c000 == mmio + 0x700
    while (((*(u32 *)0x1c000 >> 12) & 7) == 1) {
        ; // expect it to clear to 0
    }
    00000121: 8f 00 c0 01        C  mov $r15 0x1c000
    00000125: cf f9 00            B iord $r9 I[$r15]
    00000128: c7 9a 4c              extr $r10 $r9 0xc:0xe
    0000012b: b3 a0 01 fa           bra b32 $r10 0x1 e 0x125
    0000012f: f8 00                 ret
    
    // write_1c000_indirect(addr=r10, val=r11)
    00000131: f9 12              C  mpush $r1
    00000133: b2 a0                 mov b32 $r0 $r10
    00000135: b2 b1                 mov b32 $r1 $r11
    00000137: 7e 21 01 00           lcall 0x121
    0000013b: 09 01                 mov $r9 0x1
    0000013d: b3 a4 00 2d           bra b32 $r10 0x0 ne 0x16a           ; if (wait_1c000() != STATUS_OK) return 1;
    00000141: 89 00 c1 01           mov $r9 0x1c100
    00000145: fa 90 00              iowr I[$r9] $r0                     ; 0x1c100 = addr
    00000148: b8 99 00 01 00        add b32 $r9 $r9 0x100
    0000014d: fa 91 00              iowr I[$r9] $r1                     ; 0x1c200 = val
    00000150: df f2 00 00 80        mov $r15 0x800000f2
    00000155: b8 99 00 02 02        sub b32 $r9 $r9 0x200
    0000015a: fa 9f 00              iowr I[$r9] $r15                    ; 0x1c000 = 0x800000f2
    0000015d: 7e 21 01 00           lcall 0x121                         ; wait_1c000()
    00000161: b0 a6 00              cmp b32 $r10 0x0
    00000164: f0 9c 0b              xbit $r9 $flags z
    00000167: f0 96 01              xor $r9 0x1                         ; return (wait_1c000() == STATUS_OK) ? 0 : 1;
    0000016a: b2 9a               B mov b32 $r10 $r9
    0000016c: fb 11                 mpopret $r1
    
    // write_1c300(val=r10)
    ; unused function?
    0000016e: 89 00 c3 01           mov $r9 0x1c300
    00000172: fa 9a 00              iowr I[$r9] $r10                    ; 0x1c300 = r10
    00000175: f8 00                 ret
    
    // throw the key material in "random" HDCP key regs...
    void write128_via_SOR(u32 *data) {
        0x1c300 = 0xfff;
        if (write_1c000_indirect(0x545801e8, data[0])) {
            return;
        }
        if (write_1c000_indirect(0x5458021c, data[1])) {
            return;
        }
        if (write_1c000_indirect(0x54580208, data[2])) {
            return;
        }
        if (write_1c000_indirect(0x5458020c, data[3])) {
            return;
        }
    }
    00000177: f9 02              C  mpush $r0
    00000179: 4f ff 0f              mov $r15 0xfff
    0000017c: b2 a0                 mov b32 $r0 $r10
    0000017e: 89 00 c3 01           mov $r9 0x1c300
    00000182: fa 9f 00              iowr I[$r9] $r15
    00000185: bf ab                 ld b32 $r11 D[$r10]
    00000187: da e8 01 58 54        mov $r10 0x545801e8
    0000018c: 7e 31 01 00           lcall 0x131
    00000190: b3 a4 00 30           bra b32 $r10 0x0 ne 0x1c0
    00000194: 98 0b 01              ld b32 $r11 D[$r0+0x4]
    00000197: da 1c 02 58 54        mov $r10 0x5458021c
    0000019c: 7e 31 01 00           lcall 0x131
    000001a0: b3 a4 00 20           bra b32 $r10 0x0 ne 0x1c0
    000001a4: 98 0b 02              ld b32 $r11 D[$r0+0x8]
    000001a7: da 08 02 58 54        mov $r10 0x54580208
    000001ac: 7e 31 01 00           lcall 0x131
    000001b0: b3 a4 00 10           bra b32 $r10 0x0 ne 0x1c0
    000001b4: 98 0b 03              ld b32 $r11 D[$r0+0xc]
    000001b7: da 0c 02 58 54        mov $r10 0x5458020c
    000001bc: 7e 31 01 00           lcall 0x131
    000001c0: fb 01               B mpopret $r0
    
    // memcpy_d2i_ex(dst_page_offset=r10, src=r11, len=r12, dst=r13, is_secret=r14)
    000001c2: f9 02              C  mpush $r0
    000001c4: b2 b0                 mov b32 $r0 $r11                ; src, data
    000001c6: b2 cb                 mov b32 $r11 $r12               ; len, bytes
    000001c8: b2 dc                 mov b32 $r12 $r13               ; dst, insn
    000001ca: 33 00 00 0a           bra b8 $r0 0x0 e 0x1d4          ; assert((src & 0xff) == 0)
    000001ce: f8 02                 exit
    000001d0: 3e d0 01 00         B lbra 0x1d0
    000001d4: 33 b0 00 0a         B bra b8 $r11 0x0 e 0x1de         ; assert((len & 0xff) == 0)
    000001d8: f8 02                 exit
    000001da: 3e da 01 00         B lbra 0x1da
    000001de: 33 c0 00 0a         B bra b8 $r12 0x0 e 0x1e8         ; assert((dst & 0xff) == 0)
    000001e2: f8 02                 exit
    000001e4: 3e e4 01 00         B lbra 0x1e4
    000001e8: b3 e0 00 0d         B bra b32 $r14 0x0 e 0x1f5
    000001ec: d9 00 00 00 11        mov $r9 0x11000000
    000001f1: 3e fa 01 00           lbra 0x1fa
    000001f5: d9 00 00 00 01      B mov $r9 0x1000000
    000001fa: ff a9 95            B or $r9 $r10 $r9
    000001fd: 4f 00 60              mov $r15 0x6000                 ; 
    00000200: fa f9 00              iowr I[$r15] $r9                ; CODE_INDEX = r10 | AUTO_INC_WRITE | ((r14) ? SECRET : 0)
    00000203: b2 0a                 mov b32 $r10 $r0
    00000205: 7e 4f 02 00           lcall 0x24f                     ; memcpy_d2i(src=r10, len=r11, dst=r12)
    00000209: fb 01                 mpopret $r0
    
    // memcpy_i2d(dst=r10, src=r11, len=r12)
    CODE_INDEX = r11 | 0x2000000; // AUTO_INC_READ
    for (u32 r14 = 0; r14 < r12; r14 += 4) {
        r10[r14] = CODE;
    }
    0000020b: d9 00 00 00 02     C  mov $r9 0x2000000
    00000210: fd b9 05              or $r11 $r9
    00000213: 49 00 60              mov $r9 0x6000
    00000216: fa 9b 00              iowr I[$r9] $r11                ; CODE_INDEX = r11 | 0x2000000
    00000219: bd e4                 clear b32 $r14                  ; r14 = 0
    0000021b: 4b 00 61              mov $r11 0x6100
    0000021e: bd d4                 clear b32 $r13                  ; r13 = 0
    00000220: 3e 30 02 00           lbra 0x230
    00000224: ff bd ff            B iord $r15 I[$r11+$r13*0x4]      ; r15 = CODE
    00000227: 95 e9 02              shr b32 $r9 $r14 0x2            ; r9 = r14 / 2              
    0000022a: 90 ee 04              add b32 $r14 $r14 0x4           ; r14 += 4                  
    0000022d: bc af 99              st b32 D[$r10+$r9*0x4] $r15     ; [r10 + r9 * 4] = r15
    00000230: a6 ec               B cmp b32 $r14 $r12
    00000232: f4 08 f2              bra b 0x224
    00000235: f8 00                 ret
    
    // memcpy_d2d(dst=r10, src=r11, len=r12)
    00000237: 3e 48 02 00        C  lbra 0x248
    0000023b: bf bf               B ld b32 $r15 D[$r11]
    0000023d: b6 b0 04              add b32 $r11 0x4
    00000240: b6 c2 04              sub b32 $r12 0x4
    00000243: a0 af                 st b32 D[$r10] $r15
    00000245: b6 a0 04              add b32 $r10 0x4
    00000248: b3 c4 00 f3         B bra b32 $r12 0x0 ne 0x23b
    0000024c: f8 00                 ret
    
    ; for some reason there is this extra byte here
    0000024e: 01 
    
    // memcpy_d2i(src=r10, len=r11, dst=r12)
    // caller sets CODE_INDEX to initial page offset
    0000024f: f9 32                 mpush $r3
    00000251: 4d 00 61              mov $r13 0x6100                 ; CODE
    00000254: 4e 00 62              mov $r14 0x6200                 ; CODE_VIRT_ADDR
    00000257: 3e 82 02 00           lbra 0x282
    0000025b: c4 c0 ff            B and $r0 $r12 0xff
    0000025e: f4 0b 2a              bra e 0x288
    00000261: 98 a0 00            B ld b32 $r0 D[$r10]
    00000264: 98 a1 01              ld b32 $r1 D[$r10+0x4]
    00000267: 98 a2 02              ld b32 $r2 D[$r10+0x8]
    0000026a: 98 a3 03              ld b32 $r3 D[$r10+0xc]
    0000026d: f6 d0 00              iowr I[$r13] $r0
    00000270: f6 d1 00              iowr I[$r13] $r1
    00000273: f6 d2 00              iowr I[$r13] $r2
    00000276: f6 d3 00              iowr I[$r13] $r3
    00000279: b6 a0 10              add b32 $r10 0x10
    0000027c: b6 b2 10              sub b32 $r11 0x10
    0000027f: b6 c0 10              add b32 $r12 0x10
    00000282: b3 b4 00 d9         B bra b32 $r11 0x0 ne 0x25b
    00000286: fb 31                 mpopret $r3
    00000288: 95 c0 08            B shr b32 $r0 $r12 0x8
    0000028b: f6 e0 00              iowr I[$r14] $r0                ; write next page base and continue
    0000028e: 3e 61 02 00           lbra 0x261
    
    ; this shit gets copied to 00000019's stack
    struct TSecLoaderInfo {
        u8 derived_key[16];         // written by the secure payload and then written back for bpmp to pass to SE
        u8 field_10[16];            // mac of unauthenticated code (which loads secure_loader). checked by secure_loader
        u8 field_20[16];            // used for auth of secure_loader code pages
        u8 field_30[16];            // used for auth of secure_payload code pages
        u8 field_40[16];            // IV to decrypt secure_payload
        u8 key_name_0[16];          // arg0 for secure_payload(cmd=1)
        u8 key_name_1[16];          // arg0 for secure_payload(cmd=2)
        u32 secure_loader_offset;   // points to this info header (consumes 0x100 bytes). secure_loader relocated here
        u32 secure_loader_len;      // size of secure_loader code after this 0x100 byte header
        u32 secure_payload_len;
    };
    00000300  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
    00000310  f1 40 c7 6e 6c 0c 6d 59  a8 26 44 ca d0 85 2f f1  |.@.nl.mY.&D.../.|
    00000320  9c 8b 75 d3 df 0b f0 6c  95 fc 91 c0 76 1e f0 62  |..u....l....v..b|
    00000330  89 2a 36 22 8d 49 e0 48  4d 48 0c b0 ac da 02 34  |.*6".I.HMH.....4|
    00000340  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
    00000350  48 4f 56 49 5f 45 4b 53  5f 30 31 00 00 00 00 00  |HOVI_EKS_01.....|
    00000360  48 4f 56 49 5f 43 4f 4d  4d 4f 4e 5f 30 31 00 00  |HOVI_COMMON_01..|
    00000370  00 03 00 00 00 06 00 00  00 05 00 00
    
    // u32 secure_loader_thunk(TSecLoaderInfo *info=r10, cmd=r11, skip_load_and_decrypt=r12)
    ; this is just a thunk that (tries to) sanitize state before running secure code
    ; originally @ I:0x400, gets copied twice and winds up executed @ I:0x300
    00000300: f4 32 10              bclr $flags ie0                 ; some re-init code since this can be called by attackers!
    00000303: f4 32 11              bclr $flags ie1
    00000306: f4 32 12              bclr $flags ie2
    00000309: f4 3c 80              cxset 0x80                      ; dma_override(type=0b100, count=0) ; clear overrides?
    0000030c: fe ae 01              mov $r14 $cauth
    0000030f: f0 ea 13              bclr $r14 0x13
    00000312: fe ea 00              mov $cauth $r14                 ; cauth &= ~(1 << 19)
    00000315: 0e 00                 mov $r14 0x0
    00000317: fe eb 00              mov $xtargets $r14              ; xtargets = 0
    0000031a: f8 03                 xdwait
    0000031c: f8 07                 xcwait
    0000031e: f4 3c 02              cxset 0x2                       ; dma_override(type=crypto_reg, count=2)
    00000321: 0e 00                 mov $r14 0x0
    00000323: fa ee 06              xdst $r14 $r14                  ; $c0 = ?
    00000326: f8 03                 xdwait
    00000328: f5 3c 00 ac           cxor $c0 $c0
    0000032c: f5 3c 01 84           cmov $c1 $c0
    00000330: f5 3c 02 84           cmov $c2 $c0
    00000334: f5 3c 03 84           cmov $c3 $c0
    00000338: f5 3c 04 84           cmov $c4 $c0
    0000033c: f5 3c 05 84           cmov $c5 $c0
    00000340: f5 3c 07 84           cmov $c7 $c0
    00000344: 8e 00 0e 02           mov $r14 0x20e00
    00000348: cf ef 00              iord $r15 I[$r14]
    0000034b: f0 fa 10              bclr $r15 0x10
    0000034e: fa ef 00              iowr I[$r14] $r15               ; 0x20e00 &= ~0x10
    00000351: 8e 00 06 01           mov $r14 0x10600
    00000355: cf ef 00              iord $r15 I[$r14]
    00000358: f0 f9 00              bset $r15 0x0
    0000035b: fa ef 00              iowr I[$r14] $r15               ; 0x10600 |= 1
    0000035e: cf ef 00            B iord $r15 I[$r14]
    00000361: f0 f4 02              and $r15 0x2
    00000364: f4 0b fa              bra e 0x35e                     ; while (0x10600 & 2) == 0
    00000367: 4e 00 42              mov $r14 0x4200
    0000036a: cf ee 00              iord $r14 I[$r14]               ; UC_CAPS
    0000036d: b6 e5 09              shr b32 $r14 0x9
    00000370: f1 e4 ff 01           and $r14 0x1ff
    00000374: b6 e4 08              shl b32 $r14 0x8                ; r14 = falcon data segment size
    00000377: fe 4f 01              mov $r15 $sp
    0000037a: a4 fe                 cmpu b32 $r15 $r14
    0000037c: f4 18 51              bra ae 0x3cd                    ; if (sp >= DATA_SEG_SIZE) exit;
    0000037f: b1 f4 00 08           cmpu b32 $r15 0x800
    00000383: f4 08 4a              bra b 0x3cd                     ; if (sp < 0x800) exit;
    00000386: f9 82                 mpush $r8
    00000388: 7e cf 03 00           lcall 0x3cf                     ; call the real entrypoint @ secure_loader
    0000038c: fb 80                 mpop $r8
    0000038e: f5 3c 00 e0           ??? [unknown: 00 00 00 e0] [unknown instruction] ; this is some "cocmd" insn -> "mwk: chmod IIRC, it modifies the ACLs"
    00000392: f5 3c 00 ac           cxor $c0 $c0                    ; we're done... clear some state
    00000396: f5 3c 11 ac           cxor $c1 $c1
    0000039a: f5 3c 22 ac           cxor $c2 $c2
    0000039e: f5 3c 33 ac           cxor $c3 $c3
    000003a2: f5 3c 44 ac           cxor $c4 $c4
    000003a6: f5 3c 55 ac           cxor $c5 $c5
    000003aa: f5 3c 66 ac           cxor $c6 $c6
    000003ae: f5 3c 77 ac           cxor $c7 $c7
    000003b2: 09 00                 mov $r9 0x0
    000003b4: 0b 00                 mov $r11 0x0
    000003b6: 0c 00                 mov $r12 0x0
    000003b8: 0d 00                 mov $r13 0x0
    000003ba: 0e 00                 mov $r14 0x0
    000003bc: 0f 00                 mov $r15 0x0
    000003be: fc f0                 pop $r15                        ; pop THE RETURN ADDRESS!!
    000003c0: 4b 00 03              mov $r11 0x300
    000003c3: f0 b3 01              sethi $r11 0x10000              ; confusing disassembler! this is |= (1 << 16)
    000003c6: 0c 00                 mov $r12 0x0
    000003c8: fa bc 00              iowr I[$r11] $r12               ; 0x10300 = 0
    000003cb: f9 f4                 bra $r15                        ; -> return..?
    000003cd: f8 02               B exit
    
    // u32 secure_loader(TSecLoaderInfo *info=r10, cmd=r11, skip_load_and_decrypt=r12)
    000003cf: f4 30 e0           C  add $sp -0x20
    000003d2: f9 42                 mpush $r4                       ; sp -= 0x14
    000003d4: b2 c4                 mov b32 $r4 $r12
    000003d6: 98 ac 1c              ld b32 $r12 D[$r10+TSecLoaderInfo.secure_loader_offset]
    000003d9: f4 30 fc              add $sp -0x4
    000003dc: b2 a2                 mov b32 $r2 $r10
    000003de: b2 b3                 mov b32 $r3 $r11
    000003e0: bd a4                 clear b32 $r10
    000003e2: bd b4                 clear b32 $r11                  ; copy all insn memory before the secure_loader to D:0
    000003e4: 7e 3f 05 00           lcall 0x53f                     ; memcpy_i2d(dst=0, src=0, len=secure_loader_offset)
    000003e8: bd a4                 clear b32 $r10
    000003ea: bd b4                 clear b32 $r11
    000003ec: 7e 47 06 00           lcall 0x647                     ; key_init(hdr_type=CODE_SIG, key_type=ENCRYPT)
    000003f0: 98 21 1c              ld b32 $r1 D[$r2+TSecLoaderInfo.secure_loader_offset]
    000003f3: 09 f0                 mov $r9 -0x10
    000003f5: fe 40 01              mov $r0 $sp
    000003f8: 90 00 28              add b32 $r0 $r0 0x28
    000003fb: b2 1b                 mov b32 $r11 $r1
    000003fd: fd 09 04              and $r0 $r9
    00000400: b2 0a                 mov b32 $r10 $r0                ; unauth_code_mac = (sp + 0x28) & ~0xf
    00000402: 7e 88 06 00           lcall 0x688                     ; crypto_688(unauth_code_mac{local}, secure_loader_offset)
    00000406: bd 94                 clear b32 $r9
    00000408: b2 1b                 mov b32 $r11 $r1
    0000040a: b2 0c                 mov b32 $r12 $r0
    0000040c: bd a4                 clear b32 $r10
    0000040e: b2 0d                 mov b32 $r13 $r0
    00000410: 0e 02                 mov $r14 0x2
    00000412: b0 91 00              st b32 D[$sp] $r9               ; arg on the stack
    ; crypto_6b9(buf_in=0, buf_in_len=secure_loader_offset, iv=unauth_code_mac, buf_out=unauth_code_mac, mode=2, some_bool=0)
    00000415: 7e b9 06 00           lcall 0x6b9
    00000419: b2 0a                 mov b32 $r10 $r0
    0000041b: 90 2b 10              add b32 $r11 $r2 0x10           ; TSecLoaderInfo.field_10
    0000041e: 0c 10                 mov $r12 0x10
    00000420: 7e 9a 05 00           lcall 0x59a                     ; r10 = memcmp(p1=unauth_code_mac{local}, p2=&info->field_10, len=0x10)
    00000424: b3 a0 00 0d           bra b32 $r10 0x0 e 0x431
    00000428: da ef be ad de        mov $r10 0xdeadbeef
    0000042d: 3e f0 04 00           lbra 0x4f0                      ; if mac failure, return 0xdeadbeef
    00000431: 49 00 42            B mov $r9 0x4200                  ; UC_CAPS
    00000434: cf 99 00              iord $r9 I[$r9]                 ; useless code?
    00000437: 98 2f 1d              ld b32 $r15 D[$r2+TSecLoaderInfo.secure_loader_len]
    0000043a: 98 29 1c              ld b32 $r9 D[$r2+TSecLoaderInfo.secure_loader_offset]
    0000043d: bc f9 10              add b32 $r1 $r15 $r9            ; r1 = 0x600 + 0x300 = 0x900
    00000440: b3 44 00 4c           bra b32 $r4 0x0 ne 0x48c        ; skip load_and_decrypt_payload?
    00000444: 98 20 1e              ld b32 $r0 D[$r2+TSecLoaderInfo.secure_payload_len] ; 0x500
    00000447: fe 49 01              mov $r9 $sp
    0000044a: a6 09                 cmp b32 $r0 $r9
    0000044c: f4 18 40              bra ae 0x48c                    ; if (secure_payload_len >= sp): skip load_and_decrypt_payload ???
    load_and_decrypt_payload:
    ; copy payload to D:0, decrypt it, copy as secret to I:0x900, then clear the copy at D:0
    0000044f: b2 0c                 mov b32 $r12 $r0
    00000451: b8 1b 00 01 00        add b32 $r11 $r1 0x100          ; r11 = 0xa00 (payload_addr)
    00000456: 7e 3f 05 00           lcall 0x53f                     ; memcpy_i2d(dst=0, src=0xa00, len=secure_payload_len)
    0000045a: 0a 01                 mov $r10 0x1
    0000045c: b2 ab                 mov b32 $r11 $r10
    0000045e: 7e 47 06 00           lcall 0x647                     ; key_init(hdr_type=CODE_ENC, key_type=DECRYPT)
    00000462: b2 0b                 mov b32 $r11 $r0
    00000464: 90 2c 40              add b32 $r12 $r2 0x40           ; TSecLoaderInfo.field_40
    00000467: bd d4                 clear b32 $r13
    00000469: bd e4                 clear b32 $r14
    0000046b: bd a4                 clear b32 $r10
    0000046d: b0 41 00              st b32 D[$sp] $r4               ; always zero. arg on the stack
    ; crypto_6b9(buf_in=0, buf_in_len=secure_payload_len, iv=info->field_40, buf_out=0, mode=0, some_bool=0)
    00000470: 7e b9 06 00           lcall 0x6b9
    00000474: b2 1a                 mov b32 $r10 $r1
    00000476: bd b4                 clear b32 $r11
    00000478: b2 0c                 mov b32 $r12 $r0
    0000047a: b2 1d                 mov b32 $r13 $r1
    0000047c: 0e 01                 mov $r14 0x1
    0000047e: 7e f6 04 00           lcall 0x4f6                     ; memcpy_d2i_ex(dst_page_offset=0x900, src=0, len=secure_payload_len, dst=0x900, is_secret=1)
    00000482: b2 0c                 mov b32 $r12 $r0
    00000484: bd a4                 clear b32 $r10
    00000486: bd b4                 clear b32 $r11
    00000488: 7e 6b 05 00           lcall 0x56b                     ; memset(dst=0, val=0, len=secure_payload_len)
    auth_and_exec_payload:
    0000048c: f4 3c 02            B cxset 0x2                       ; dma_override(type=crypto_reg, count=2)
    0000048f: 8f 00 00 06           mov $r15 0x60000
    00000493: 90 29 30              add b32 $r9 $r2 0x30            ; TSecLoaderInfo.field_30
    00000496: fd 9f 05              or $r9 $r15
    00000499: bd f4                 clear b32 $r15
    0000049b: fa f9 06              xdst $r15 $r9                   ; crypto_reg_load(crypto_reg=$c6, local_address=&info->field_30)
    0000049e: f8 03                 xdwait
    000004a0: fe a4 01              mov $r4 $cauth                  ; save cauth
    000004a3: 98 29 1e              ld b32 $r9 D[$r2+TSecLoaderInfo.secure_payload_len]
    000004a6: 95 1f 08              shr b32 $r15 $r1 0x8
    000004a9: b6 94 10              shl b32 $r9 0x10
    000004ac: fd f9 05              or $r15 $r9
    000004af: fe fa 00              mov $cauth $r15                 ; cauth = (secure_payload_len << 16) | (secure_payload_dst >> 8)
    000004b2: b3 34 01 0d           bra b32 $r3 0x1 ne 0x4bf
    handle_cmd_1:
    000004b6: b2 3b                 mov b32 $r11 $r3
    000004b8: 90 2a 50              add b32 $r10 $r2 0x50           ; TSecLoaderInfo.key_name_0
    000004bb: 3e dd 04 00           lbra 0x4dd                      ; status = secure_payload(&info->key_name_0, cmd=1)
    000004bf: b3 34 02 0d         B bra b32 $r3 0x2 ne 0x4cc
    handle_cmd_2:
    000004c3: b2 3b                 mov b32 $r11 $r3
    000004c5: 90 2a 60              add b32 $r10 $r2 0x60           ; TSecLoaderInfo.key_name_1
    000004c8: 3e dd 04 00           lbra 0x4dd                      ; status = secure_payload(&info->key_name_1, cmd=2)
    000004cc: b3 30 03 0d         B bra b32 $r3 0x3 e 0x4d9
    handle_invalid_cmd:
    000004d0: d0 d0 d0 d0 d0        mov $r0 0xd0d0d0d0
    000004d5: 3e e1 04 00           lbra 0x4e1                      ; status = 0xd0d0d0d0;
    handle_cmd_3:
    000004d9: b2 3b               B mov b32 $r11 $r3
    000004db: b2 2a                 mov b32 $r10 $r2
    000004dd: f9 15               B call $r1                        ; status = secure_payload(info, cmd=3)
    000004df: b2 a0                 mov b32 $r0 $r10
    000004e1: b2 2a               B mov b32 $r10 $r2
    000004e3: bd b4                 clear b32 $r11
    000004e5: 0c 7c                 mov $r12 0x7c                   ; clear our copy of the info header
    000004e7: 7e 6b 05 00           lcall 0x56b                     ; memset(dst=info, val=0, len=0x7c)
    000004eb: fe 4a 00              mov $cauth $r4                  ; restore cauth
    000004ee: b2 0a                 mov b32 $r10 $r0                ; return status
    000004f0: f4 30 04            B add $sp 0x4
    000004f3: fb 45 20              mpopaddret $r4 0x20
    
    // memcpy_d2i_ex(dst_page_offset=r10, src=r11, len=r12, dst=r13, is_secret=r14)
    000004f6: f9 02              C  mpush $r0
    000004f8: b2 b0                 mov b32 $r0 $r11
    000004fa: b2 cb                 mov b32 $r11 $r12
    000004fc: b2 dc                 mov b32 $r12 $r13
    000004fe: 33 00 00 0a           bra b8 $r0 0x0 e 0x508
    00000502: f8 02                 exit
    00000504: 3e 04 05 00         B lbra 0x504
    00000508: 33 b0 00 0a         B bra b8 $r11 0x0 e 0x512
    0000050c: f8 02                 exit
    0000050e: 3e 0e 05 00         B lbra 0x50e
    00000512: 33 c0 00 0a         B bra b8 $r12 0x0 e 0x51c
    00000516: f8 02                 exit
    00000518: 3e 18 05 00         B lbra 0x518
    0000051c: b3 e0 00 0d         B bra b32 $r14 0x0 e 0x529
    00000520: d9 00 00 00 11        mov $r9 0x11000000
    00000525: 3e 2e 05 00           lbra 0x52e
    00000529: d9 00 00 00 01      B mov $r9 0x1000000
    0000052e: ff a9 95            B or $r9 $r10 $r9
    00000531: 4f 00 60              mov $r15 0x6000                 ; CODE_INDEX
    00000534: fa f9 00              iowr I[$r15] $r9
    00000537: b2 0a                 mov b32 $r10 $r0
    00000539: 7e 88 08 00           lcall 0x888                     ; memcpy_d2i(src=r10, len=r11, dst=r12)
    0000053d: fb 01                 mpopret $r0
    
    // memcpy_i2d(dst=r10, src=r11, len=r12)
    0000053f: d9 00 00 00 02     C  mov $r9 0x2000000
    00000544: fd b9 05              or $r11 $r9
    00000547: 49 00 60              mov $r9 0x6000                  ; CODE_INDEX
    0000054a: fa 9b 00              iowr I[$r9] $r11
    0000054d: bd e4                 clear b32 $r14
    0000054f: 4b 00 61              mov $r11 0x6100                 ; CODE
    00000552: bd d4                 clear b32 $r13
    00000554: 3e 64 05 00           lbra 0x564
    00000558: ff bd ff            B iord $r15 I[$r11+$r13*0x4]
    0000055b: 95 e9 02              shr b32 $r9 $r14 0x2
    0000055e: 90 ee 04              add b32 $r14 $r14 0x4
    00000561: bc af 99              st b32 D[$r10+$r9*0x4] $r15
    00000564: a6 ec               B cmp b32 $r14 $r12
    00000566: f4 08 f2              bra b 0x558
    00000569: f8 00                 ret
    
    // memset(dst=r10, val=r11, len=r12)
    0000056b: 3e 81 05 00        C  lbra 0x581
    0000056f: b5 ab 00            B st b32 D[$r10] $r11
    00000572: b5 ab 01              st b32 D[$r10+0x4] $r11
    00000575: b5 ab 02              st b32 D[$r10+0x8] $r11
    00000578: b5 ab 03              st b32 D[$r10+0xc] $r11
    0000057b: b6 a0 10              add b32 $r10 0x10
    0000057e: b6 c2 10              sub b32 $r12 0x10
    00000581: b0 c6 10            B cmp b32 $r12 0x10
    00000584: f4 18 eb              bra ae 0x56f
    00000587: 3e 93 05 00           lbra 0x593
    0000058b: a0 ab               B st b32 D[$r10] $r11
    0000058d: b6 a0 04              add b32 $r10 0x4
    00000590: b6 c2 04              sub b32 $r12 0x4
    00000593: b3 c4 00 f8         B bra b32 $r12 0x0 ne 0x58b
    00000597: f8 00                 ret
    
    ; another extra 0x01 byte following a ret
    00000599: 01
    
    // int memcmp(p1=r10, p2=r11, len=r12)
    // NOT TIMING INVARIANT
    0000059a: 3e b0 05 00           lbra 0x5b0
    0000059e: bf ad               B ld b32 $r13 D[$r10]
    000005a0: bf be                 ld b32 $r14 D[$r11]
    000005a2: a6 de                 cmp b32 $r13 $r14
    000005a4: f4 1b 14              bra ne 0x5b8
    000005a7: b6 a0 04              add b32 $r10 0x4
    000005aa: b6 b0 04              add b32 $r11 0x4
    000005ad: b6 c2 04              sub b32 $r12 0x4
    000005b0: b3 c4 00 ee         B bra b32 $r12 0x0 ne 0x59e
    000005b4: 0a 00                 mov $r10 0x0
    000005b6: f8 00                 ret
    000005b8: 0a 01               B mov $r10 0x1
    000005ba: f8 00                 ret
    
    ; again, the floating 0x01 byte...
    000005bc: 01
    
    // these xfers are for crypto stuff. size is in bits!
    
    // crypto_reg_store(crypto_reg=r10, local_addr=r11)
    000005bd: f4 3c 02           C  cxset 0x2                   ; dma_override(type=crypto_reg, count=2)
    000005c0: b6 a4 10              shl b32 $r10 0x10
    000005c3: fd ba 05              or $r11 $r10
    000005c6: fa bb 05              xdld $r11 $r11
    000005c9: f8 03                 xdwait
    000005cb: f8 00                 ret
    
    // crypto_reg_load(crypto_reg=r10, local_addr=r11)
    // read from local_addr into $cX
    000005cd: f4 3c 02           C  cxset 0x2                   ; dma_override(type=crypto_reg, count=2)
    000005d0: b6 a4 10              shl b32 $r10 0x10
    000005d3: fd ba 05              or $r11 $r10
    000005d6: fa bb 06              xdst $r11 $r11
    000005d9: f8 03                 xdwait
    000005db: f8 00                 ret
    
    // get_type_string(buf=r10, type=r11)
    000005dd: c4 a9 0f           C  and $r9 $r10 0xf
    000005e0: f4 0b 09              bra e 0x5e9
    000005e3: f8 02                 exit                        ; assert r10 16byte aligned
    000005e5: 3e e5 05 00         B lbra 0x5e5
    000005e9: b3 b0 00 0c         B bra b32 $r11 0x0 e 0x5f5
    000005ed: b3 b4 01 3e           bra b32 $r11 0x1 ne 0x62b
    000005f1: 3e 10 06 00           lbra 0x610
    ; if (r11 == 0) { "CODE_SIG_01"
    000005f5: d9 43 4f 44 45      B mov $r9 0x45444f43          ; "CODE"
    000005fa: a0 a9                 st b32 D[$r10] $r9
    000005fc: d9 5f 53 49 47        mov $r9 0x4749535f          ; "_SIG"
    00000601: b5 ab 03              st b32 D[$r10+0xc] $r11
    00000604: b5 a9 01              st b32 D[$r10+0x4] $r9
    00000607: 89 5f 30 31           mov $r9 0x31305f            ; "_01"
    0000060b: b5 a9 02              st b32 D[$r10+0x8] $r9
    0000060e: f8 00                 ret
    ; } else if (r11 == 1) { "CODE_ENC_01"
    00000610: d9 43 4f 44 45      B mov $r9 0x45444f43          ; "CODE"
    00000615: a0 a9                 st b32 D[$r10] $r9
    00000617: d9 5f 45 4e 43        mov $r9 0x434e455f          ; "_ENC"
    0000061c: b5 a9 01              st b32 D[$r10+0x4] $r9
    0000061f: 89 5f 30 31           mov $r9 0x31305f            ; "_01"
    00000623: b5 a9 02              st b32 D[$r10+0x8] $r9
    00000626: bd 94                 clear b32 $r9
    00000628: b5 a9 03              st b32 D[$r10+0xc] $r9
    ; }
    0000062b: f8 00               B ret
    
    ; unused function?
    0000062d: f9 02                 mpush $r0
    0000062f: b2 b0                 mov b32 $r0 $r11
    00000631: b2 ab                 mov b32 $r11 $r10
    00000633: 0a 04                 mov $r10 0x4
    00000635: 7e cd 05 00           lcall 0x5cd                 ; crypto_reg_load(crypto_reg=$c4, local_addr=r11)
    00000639: b3 00 00 08           bra b32 $r0 0x0 e 0x641
    0000063d: b3 04 03 08           bra b32 $r0 0x3 ne 0x645
    00000641: f5 3c 44 c8         B ckexp $c4 $c4
    00000645: fb 01               B mpopret $r0
    
    // key_init(hdr_type=r10, key_type=r11)
    // hdr_type 0: CODE_SIG, 1: CODE_ENC
    // key_type 0: ENCRYPT, 1: DECRYPT
    // leaves the key material in c4, then other funcs use that
    00000647: 09 f0                 mov $r9 -0x10
    00000649: f4 30 e0              add $sp -0x20
    0000064c: f9 12                 mpush $r1
    0000064e: b2 b1                 mov b32 $r1 $r11
    00000650: fe 40 01              mov $r0 $sp
    00000653: b2 ab                 mov b32 $r11 $r10           ; r11 = hdr_type
    00000655: 90 00 18              add b32 $r0 $r0 0x18
    00000658: fd 09 04              and $r0 $r9                 ; r0 = (sp + 0x18) & ~0xf
    0000065b: b2 0a                 mov b32 $r10 $r0
    0000065d: 7e dd 05 00           lcall 0x5dd                 ; get_type_string(buf=r0{local}, type=hdr_type)
    00000661: b2 0b                 mov b32 $r11 $r0
    00000663: bd a4                 clear b32 $r10
    00000665: 7e cd 05 00           lcall 0x5cd                 ; crypto_reg_load(crypto_reg=$c0, r0{local})
    00000669: f5 3c 61 c2           csecret $c1 0x26            ; c1 = hw_secrets[0x26]. whatever that means! kfuse data?
    0000066d: f5 3c 01 c4           ckeyreg $c1                 ; ACTIVE_KEY_REG = c1
    00000671: f5 3c 01 d0           cenc $c1 $c0                ; c1 = Aes128EcbEncrypt(key=c1, data=c0)
    00000675: f5 3c 11 dc           csigenc $c1 $c1             ; c1 = EncryptSig(key=c1) this the sig supplied when our code page was auth'd (info.field_20)
    00000679: f5 3c 14 84           cmov $c4 $c1                ; c4 = c1
    0000067d: b3 10 00 08           bra b32 $r1 0x0 e 0x685     ; check key_type
    00000681: f5 3c 44 c8           ckexp $c4 $c4               ; do key expansion if DEC, else skip
    00000685: fb 15 20            B mpopaddret $r1 0x20
    
    // crypto_688(buf=r10, in_word=r11)
    00000688: f9 02                 mpush $r0
    0000068a: bd 94                 clear b32 $r9
    0000068c: b2 a0                 mov b32 $r0 $r10
    0000068e: a0 a9                 st b32 D[$r10] $r9
    00000690: b5 a9 02              st b32 D[$r10+0x8] $r9
    00000693: b5 a9 01              st b32 D[$r10+0x4] $r9
    00000696: 7d b3                 hswap b16 $r11
    00000698: bd b3                 hswap b32 $r11
    0000069a: 7d b3                 hswap b16 $r11
    0000069c: b5 ab 03              st b32 D[$r10+0xc] $r11     ; r10 = 0 || 0 || 0 || bswap32(in_word)
    0000069f: 0a 03                 mov $r10 0x3                ; input num_bytes = 4
    000006a1: b2 0b                 mov b32 $r11 $r0
    000006a3: 7e cd 05 00           lcall 0x5cd                 ; crypto_reg_load(crypto_reg=$c3, local_addr=buf)
    000006a7: f5 3c 04 c4           ckeyreg $c4
    000006ab: f5 3c 35 d0           cenc $c5 $c3                ; c5 = Aes128EcbEncrypt(key=c4, data=c3)
    000006af: 0a 05                 mov $r10 0x5                ; output num_bytes = 16
    000006b1: b2 0b                 mov b32 $r11 $r0
    000006b3: 7e bd 05 00           lcall 0x5bd                 ; crypto_reg_store(crypto_reg=$c5, local_addr=buf)
    000006b7: fb 01                 mpopret $r0
    
    // crypto_6b9(buf_in=r10, buf_in_len=r11, iv=r12, buf_out=r13, mode=r14, some_bool=[sp])
    000006b9: f9 52                 mpush $r5
    000006bb: b2 b3                 mov b32 $r3 $r11
    000006bd: b2 d4                 mov b32 $r4 $r13
    000006bf: b2 cb                 mov b32 $r11 $r12
    000006c1: b2 e2                 mov b32 $r2 $r14
    000006c3: b4 50 07              ld b32 $r5 D[$sp+0x1c]
    000006c6: b2 a1                 mov b32 $r1 $r10
    000006c8: b2 d0                 mov b32 $r0 $r13
    000006ca: b3 34 00 0a           bra b32 $r3 0x0 ne 0x6d4    ; assert buf_in_len != 0
    000006ce: f8 02                 exit
    000006d0: 3e d0 06 00         B lbra 0x6d0
    000006d4: c4 39 0f            B and $r9 $r3 0xf
    000006d7: f4 0b 09              bra e 0x6e0                 ; assert (buf_in_len & 0xf) == 0
    000006da: f8 02                 exit
    000006dc: 3e dc 06 00         B lbra 0x6dc
    000006e0: c4 a9 0f            B and $r9 $r10 0xf
    000006e3: f4 0b 09              bra e 0x6ec                 ; assert (buf_in & 0xf) == 0
    000006e6: f8 02                 exit
    000006e8: 3e e8 06 00         B lbra 0x6e8
    000006ec: c4 49 0f            B and $r9 $r4 0xf
    000006ef: f4 0b 09              bra e 0x6f8                 ; assert (buf_out & 0xf) == 0
    000006f2: f8 02                 exit
    000006f4: 3e f4 06 00         B lbra 0x6f4
    000006f8: b3 b0 00 0e         B bra b32 $r11 0x0 e 0x706    ; if present, use 16byte iv
    set_iv_to_input:
    000006fc: 0a 05                 mov $r10 0x5
    000006fe: 7e cd 05 00           lcall 0x5cd                 ; crypto_reg_load(crypto_reg=$c5, local_addr=iv)
    00000702: 3e 0a 07 00           lbra 0x70a
    set_iv_zero:
    00000706: f5 3c 55 ac         B cxor $c5 $c5
    set_active_key_c4:
    0000070a: f5 3c 04 c4         B ckeyreg $c4
    mode_dispatch:
    0000070e: b3 20 02 50           bra b32 $r2 0x2 e 0x75e
    00000712: b0 26 02              cmp b32 $r2 0x2
    00000715: f4 0c 10              bra a 0x725
    00000718: b3 20 00 2a           bra b32 $r2 0x0 e 0x742
    0000071c: b3 2d 01 6a 01        bra b32 $r2 0x1 ne 0x886
    00000721: 3e 32 07 00           lbra 0x732
    00000725: b3 20 03 5d         B bra b32 $r2 0x3 e 0x782
    00000729: b3 2d 04 5d 01        bra b32 $r2 0x4 ne 0x886
    0000072e: 3e 72 07 00           lbra 0x772
    00000732: f5 3c 40 94         B cs0begin 0x4
    00000736: f5 3c 03 88           cxsin $c3
    0000073a: f5 3c 53 ac           cxor $c3 $c5
    0000073e: 3e 7a 07 00           lbra 0x77a
    00000742: f5 3c 50 94         B cs0begin 0x5
    00000746: f5 3c 03 88           cxsin $c3
    0000074a: f5 3c 32 d4           cdec $c2 $c3
    0000074e: f5 3c 25 ac           cxor $c5 $c2
    00000752: f5 3c 05 8c           cxsout $c5
    00000756: f5 3c 35 84           cmov $c5 $c3
    0000075a: 3e 75 08 00           lbra 0x875
    0000075e: f5 3c 30 94         B cs0begin 0x3
    00000762: f5 3c 03 88           cxsin $c3
    00000766: f5 3c 35 ac           cxor $c5 $c3
    0000076a: f5 3c 55 d0           cenc $c5 $c5
    0000076e: 3e 75 08 00           lbra 0x875
    00000772: f5 3c 30 94         B cs0begin 0x3
    00000776: f5 3c 03 88           cxsin $c3
    0000077a: f5 3c 35 d0         B cenc $c5 $c3
    0000077e: 3e 8e 07 00           lbra 0x78e
    00000782: f5 3c 30 94         B cs0begin 0x3
    00000786: f5 3c 03 88           cxsin $c3
    0000078a: f5 3c 35 d4           cdec $c5 $c3
    0000078e: f5 3c 05 8c         B cxsout $c5
    00000792: 3e 75 08 00           lbra 0x875
    00000796: 95 3f 04            B shr b32 $r15 $r3 0x4
    00000799: b0 f6 10              cmp b32 $r15 0x10
    0000079c: f4 0d 05              bra be 0x7a1
    0000079f: 0f 10                 mov $r15 0x10
    000007a1: 92 f9 01            B sub b32 $r9 $r15 0x1
    000007a4: fd 9f 04              and $r9 $r15
    000007a7: f4 0b 05              bra e 0x7ac
    000007aa: 0f 01                 mov $r15 0x1
    000007ac: 94 fe 04            B shl b32 $r14 $r15 0x4
    000007af: ff 01 f5              or $r15 $r0 $r1
    000007b2: 92 e9 01              sub b32 $r9 $r14 0x1
    000007b5: fd 9f 04              and $r9 $r15
    000007b8: f4 1b 68              bra ne 0x820
    000007bb: b3 e0 40 41           bra b32 $r14 0x40 e 0x7fc
    000007bf: b1 e6 40 00           cmp b32 $r14 0x40
    000007c3: f4 0c 0b              bra a 0x7ce
    000007c6: b3 e4 20 5a           bra b32 $r14 0x20 ne 0x820
    000007ca: 3e 0e 08 00           lbra 0x80e
    000007ce: b3 ea 80 00 1c      B bra b32 $r14 0x80 e 0x7ea
    000007d3: b3 ee 00 01 4d        bra b32 $r14 0x100 ne 0x820
    000007d8: b2 1f                 mov b32 $r15 $r1
    000007da: f0 f3 06              sethi $r15 0x60000
    000007dd: b2 09                 mov b32 $r9 $r0
    000007df: f0 93 06              sethi $r9 0x60000
    000007e2: f5 3c 00 99           cs0exec 0x10
    000007e6: 3e 30 08 00           lbra 0x830
    000007ea: b2 1f               B mov b32 $r15 $r1
    000007ec: f0 f3 05              sethi $r15 0x50000
    000007ef: b2 09                 mov b32 $r9 $r0
    000007f1: f0 93 05              sethi $r9 0x50000
    000007f4: f5 3c 80 98           cs0exec 0x8
    000007f8: 3e 30 08 00           lbra 0x830
    000007fc: b2 1f               B mov b32 $r15 $r1
    000007fe: f0 f3 04              sethi $r15 0x40000
    00000801: b2 09                 mov b32 $r9 $r0
    00000803: f0 93 04              sethi $r9 0x40000
    00000806: f5 3c 40 98           cs0exec 0x4
    0000080a: 3e 30 08 00           lbra 0x830
    0000080e: b2 1f               B mov b32 $r15 $r1
    00000810: f0 f3 03              sethi $r15 0x30000
    00000813: b2 09                 mov b32 $r9 $r0
    00000815: f0 93 03              sethi $r9 0x30000
    00000818: f5 3c 20 98           cs0exec 0x2
    0000081c: 3e 30 08 00           lbra 0x830
    00000820: b2 1f               B mov b32 $r15 $r1
    00000822: f0 f3 02              sethi $r15 0x20000
    00000825: b2 09                 mov b32 $r9 $r0
    00000827: f0 93 02              sethi $r9 0x20000
    0000082a: f5 3c 10 98           cs0exec 0x1
    0000082e: 0e 10                 mov $r14 0x10
    00000830: b3 54 01 0b         B bra b32 $r5 0x1 ne 0x83b
    00000834: f4 3c a1              cxset 0xa1                      ; dma_override(type=0b101, count=1)
    00000837: 3e 3e 08 00           lbra 0x83e
    0000083b: f4 3c 21            B cxset 0x21                      ; dma_override(type=0b001, count=1)
    0000083e: fa ff 06            B xdst $r15 $r15
    00000841: b3 20 02 1e           bra b32 $r2 0x2 e 0x85f
    00000845: b3 54 01 0b           bra b32 $r5 0x1 ne 0x850
    00000849: f4 3c a2              cxset 0xa2                      ; dma_override(type=0b101, count=2)
    0000084c: 3e 53 08 00           lbra 0x853
    00000850: f4 3c 22            B cxset 0x22                      ; dma_override(type=0b001, count=2)
    00000853: fa 99 05            B xdld $r9 $r9
    00000856: f8 03                 xdwait
    00000858: bc 0e 00              add b32 $r0 $r0 $r14
    0000085b: 3e 6f 08 00           lbra 0x86f
    0000085f: b3 54 01 0b         B bra b32 $r5 0x1 ne 0x86a
    00000863: f4 3c a1              cxset 0xa1                      ; dma_override(type=0b101, count=1)
    00000866: 3e 6d 08 00           lbra 0x86d
    0000086a: f4 3c 21            B cxset 0x21                      ; dma_override(type=0b001, count=1)
    0000086d: f8 03               B xdwait
    0000086f: bc 1e 10            B add b32 $r1 $r1 $r14
    00000872: bb 3e 02              sub b32 $r3 $r14
    00000875: b3 3d 00 21 ff      B bra b32 $r3 0x0 ne 0x796
    0000087a: b3 24 02 0c           bra b32 $r2 0x2 ne 0x886
    0000087e: b2 4b                 mov b32 $r11 $r4
    00000880: 0a 05                 mov $r10 0x5
    00000882: 7e bd 05 00           lcall 0x5bd                     ; crypto_reg_store(crypto_reg=$c5, local_addr=r11)
    00000886: fb 51               B mpopret $r5
    
    // memcpy_d2i(src=r10, len=r11, dst=r12)
    00000888: f9 32                 mpush $r3
    0000088a: 4d 00 61              mov $r13 0x6100                 ; CODE
    0000088d: 4e 00 62              mov $r14 0x6200                 ; CODE_VIRT_ADDR
    00000890: 3e bb 08 00           lbra 0x8bb
    00000894: c4 c0 ff            B and $r0 $r12 0xff
    00000897: f4 0b 2a              bra e 0x8c1
    0000089a: 98 a0 00            B ld b32 $r0 D[$r10]
    0000089d: 98 a1 01              ld b32 $r1 D[$r10+0x4]
    000008a0: 98 a2 02              ld b32 $r2 D[$r10+0x8]
    000008a3: 98 a3 03              ld b32 $r3 D[$r10+0xc]
    000008a6: f6 d0 00              iowr I[$r13] $r0
    000008a9: f6 d1 00              iowr I[$r13] $r1
    000008ac: f6 d2 00              iowr I[$r13] $r2
    000008af: f6 d3 00              iowr I[$r13] $r3
    000008b2: b6 a0 10              add b32 $r10 0x10
    000008b5: b6 b2 10              sub b32 $r11 0x10
    000008b8: b6 c0 10              add b32 $r12 0x10
    000008bb: b3 b4 00 d9         B bra b32 $r11 0x0 ne 0x894
    000008bf: fb 31                 mpopret $r3
    000008c1: 95 c0 08            B shr b32 $r0 $r12 0x8
    000008c4: f6 e0 00              iowr I[$r14] $r0
    000008c7: 3e 9a 08 00           lbra 0x89a
    
    
    ; encrypted secure_payload
    00000a00  ca e0 f8 6a d9 72 ba 7b  eb 25 b3 a8 42 98 75 38  |...j.r.{.%..B.u8|
    00000a10  25 ed 0c 3f 80 56 22 01  8a 19 87 8a fe 6d 9e 4f  |%..?.V"......m.O|
    00000a20  dd 80 11 e9 5a 48 40 c4  1a ed c2 7f ed 7f b3 43  |....ZH@........C|
    00000a30  14 bb 58 53 09 2a 45 12  3a b4 b6 44 6a ef 19 1b  |..XS.*E.:..Dj...|
    00000a40  55 2a 99 69 68 06 5c 1b  ab df c2 00 ee a9 e1 b0  |U*.ih.\.........|
    00000a50  c6 aa 5c 54 3a 5d 7d 7d  79 30 50 69 b5 61 be 1d  |..\T:]}}y0Pi.a..|
    00000a60  6f a3 2e ec f1 95 c6 6d  62 22 43 5c 36 a4 0e c4  |o......mb"C\6...|
    00000a70  94 e6 37 4e 41 80 d4 6f  27 80 1c 5e 94 cb d6 d4  |..7NA..o'..^....|
    00000a80  6d f7 0f 26 68 6c fa d7  b4 63 23 f7 19 2f b5 49  |m..&hl...c#../.I|
    00000a90  87 13 59 d0 be 85 00 9e  1e 7e 07 50 1b bc 5c ec  |..Y......~.P..\.|
    00000aa0  2b 1a 81 62 02 f3 83 58  cd 9a b4 7a 1e 11 94 3e  |+..b...X...z...>|
    00000ab0  bf c6 69 fa 41 91 76 c3  4d a4 4e 1a d5 bf 29 37  |..i.A.v.M.N...)7|
    00000ac0  36 74 8d 1c 54 89 ec 47  45 3e 20 f4 69 96 25 fe  |6t..T..GE> .i.%.|
    00000ad0  74 83 64 44 7a 4c 83 a9  b3 c2 1a 1c a9 59 e9 99  |t.dDzL.......Y..|
    00000ae0  89 ba a3 8f ed 26 b6 f7  a2 f4 b2 a7 f0 ab ea 7f  |.....&..........|
    00000af0  ea d2 55 0c 64 36 7b 23  c2 a6 69 86 d4 a3 93 33  |..U.d6{#..i....3|
    00000b00  a3 7e 39 ad 6e a3 72 76  b4 b0 82 b4 67 30 8a 48  |.~9.n.rv....g0.H|
    00000b10  9e dc 94 b3 29 85 22 ca  7b 55 24 33 9c 01 a2 0d  |....).".{U$3....|
    00000b20  10 06 6f f9 01 7a 23 0f  99 37 9f bb 2b a4 3a fc  |..o..z#..7..+.:.|
    00000b30  a4 a0 d5 06 b4 e0 61 44  01 48 b0 75 3f ac a1 25  |......aD.H.u?..%|
    00000b40  4b 85 bf b7 a4 21 f2 82  09 2e 72 61 c7 69 92 11  |K....!....ra.i..|
    00000b50  a6 81 2f e1 c2 e8 aa 41  da 62 a7 a0 6c be 74 a6  |../....A.b..l.t.|
    00000b60  cb 9b 20 c4 65 ed fb 3c  3d d0 9a c8 4e b0 91 f5  |.. .e..<=...N...|
    00000b70  a9 3f e0 9c 7b 6f 21 78  d2 4f 50 a5 b0 61 05 93  |.?..{o!x.OP..a..|
    00000b80  b0 4b 60 98 6d 56 cc 07  a7 d5 61 4c d2 9e 23 0f  |.K`.mV....aL..#.|
    00000b90  cd d9 bf c8 ef 05 a9 24  72 6d 50 7f f7 be fd bf  |.......$rmP.....|
    00000ba0  7c a5 df 4d bb 8d f3 05  2a 48 40 88 34 6d e7 d0  ||..M....*H@.4m..|
    00000bb0  03 b7 4b b1 db df 09 ff  20 94 c0 3b 10 01 ed c8  |..K..... ..;....|
    00000bc0  a9 d2 0f cd 1d 06 92 0f  4c cc 01 c0 e8 d3 d3 5b  |........L......[|
    00000bd0  34 2e 61 20 dd 2c 09 83  6a e3 3b b4 6d d5 34 99  |4.a .,..j.;.m.4.|
    00000be0  7b 22 cd 23 e1 f1 a9 c4  50 07 31 fd 97 18 54 3f  |{".#....P.1...T?|
    00000bf0  ba 88 70 27 89 b4 74 5a  36 bf 73 37 d3 bc 00 86  |..p'..tZ6.s7....|
    00000c00  14 8d 3d e1 30 ac af 6d  72 df 9a 28 b0 98 e7 89  |..=.0..mr..(....|
    00000c10  55 88 60 55 48 a1 ef f9  79 15 6b f0 db 48 4b 9f  |U.`UH...y.k..HK.|
    00000c20  6a ca 6c 29 a2 0c 97 e7  12 05 76 e5 a2 8e ed 15  |j.l)......v.....|
    00000c30  83 14 28 39 fc 98 fa 5d  1d 76 9b ab 3f 06 ea 43  |..(9...].v..?..C|
    00000c40  f8 09 d5 d6 a2 85 ff 5f  5f d0 41 60 68 9a 76 23  |.......__.A`h.v#|
    00000c50  af 18 b8 76 16 3a 8c 83  cd bc 06 5a a7 44 8f 86  |...v.:.....Z.D..|
    00000c60  54 73 e4 11 d0 2b 34 85  34 b2 ee 07 83 a1 57 e8  |Ts...+4.4.....W.|
    00000c70  0b 83 a6 7d bc 4b 2f ca  5e a0 21 ed 82 6a bd 8d  |...}.K/.^.!..j..|
    00000c80  91 a6 79 5b 53 d8 09 0d  6a d8 7d f9 2f 0c a2 71  |..y[S...j.}./..q|
    00000c90  98 37 c7 93 b9 fc 0c af  24 29 66 cc a9 ed 8a 2b  |.7......$)f....+|
    00000ca0  cf e2 5a f1 95 ec 27 95  79 2b b3 e5 7b 14 99 a3  |..Z...'.y+..{...|
    00000cb0  ca be 0f fe 37 c6 04 a4  61 6f 2a 0f 90 d3 f9 88  |....7...ao*.....|
    00000cc0  c3 0c e2 bc 09 20 47 19  53 89 1e e6 18 01 02 51  |..... G.S......Q|
    00000cd0  43 ea b3 c0 04 4f a2 53  74 30 41 2b ec c6 54 4f  |C....O.St0A+..TO|
    00000ce0  65 50 fa 6c f7 d9 bf 45  7c 23 8f 38 3a 89 e0 fd  |eP.l...E|#.8:...|
    00000cf0  d4 48 71 b8 86 65 87 42  01 00 23 22 b6 e7 08 c3  |.Hq..e.B..#"....|
    00000d00  1a c8 c1 4e 69 78 6d 68  c5 9f de 64 85 be 94 52  |...Nixmh...d...R|
    00000d10  fb 7c c5 9e 97 4a e3 aa  2c 6c 49 e6 5d af 1e 2c  |.|...J..,lI.]..,|
    00000d20  a0 29 3c bb f4 94 5f fb  66 49 e7 30 0e 6b e0 9d  |.)<..._.fI.0.k..|
    00000d30  bf 28 25 e8 97 8f 17 c4  87 f3 95 ce be ad 87 b9  |.(%.............|
    00000d40  d1 e4 0c 9e 12 cf f9 9c  ac 8c 6f 77 2a 8a b5 b3  |..........ow*...|
    00000d50  19 7c ea bf b8 c4 0e e0  0f 73 8a 34 8d a9 73 2d  |.|.......s.4..s-|
    00000d60  97 cd 72 51 43 82 e9 bc  af 4c 34 6c b9 3e ec cc  |..rQC....L4l.>..|
    00000d70  e3 e5 7d 06 72 a8 8e ee  2c 11 a1 40 eb 20 0f 77  |..}.r...,..@. .w|
    00000d80  b1 27 b4 3b 82 b6 ec 85  f6 5b 35 48 e4 46 51 e5  |.'.;.....[5H.FQ.|
    00000d90  2a 31 ce e0 e8 04 04 91  d0 db 46 a0 57 19 26 02  |*1........F.W.&.|
    00000da0  d6 c6 dd b9 ce c6 cf bf  55 e5 35 96 71 d3 9c d5  |........U.5.q...|
    00000db0  e0 a7 ec fe e3 8b 7d 9a  28 32 b5 b0 b7 c8 21 38  |......}.(2....!8|
    00000dc0  9e 6e be 08 6f 62 cd ee  b0 a1 79 e2 a0 2b 6e 22  |.n..ob....y..+n"|
    00000dd0  6b 2b 00 7f 49 57 4a 23  28 99 75 b5 40 01 c7 9f  |k+..IWJ#(.u.@...|
    00000de0  2d e7 85 1b 5a 4e 55 3c  ce d6 c7 7b 85 ec 52 ff  |-...ZNU<...{..R.|
    00000df0  23 87 38 cf 44 e1 95 bb  9c e5 44 05 3d f6 f1 85  |#.8.D.....D.=...|
    00000e00  78 a3 7d 19 44 43 3b d4  fa db 9a bd 81 85 34 fd  |x.}.DC;.......4.|
    00000e10  ba c7 9b f5 96 1a 73 c1  46 7c 39 ec 37 56 81 ca  |......s.F|9.7V..|
    00000e20  0e a9 30 7f 82 3c f7 49  85 c7 dc 2e 34 50 78 c1  |..0..<.I....4Px.|
    00000e30  da d5 d2 14 b6 d3 05 5c  be b8 d9 ca 96 bd 52 8b  |.......\......R.|
    00000e40  c1 40 41 56 14 0f 16 aa  3e 07 bb 52 d5 1a 94 0f  |.@AV....>..R....|
    00000e50  5f 53 e5 46 dc 12 b1 74  05 70 6b 16 17 a7 94 ec  |_S.F...t.pk.....|
    00000e60  c0 5f 5e 0e 88 b1 45 e2  08 19 63 e4 b9 12 0d ca  |._^...E...c.....|
    00000e70  05 8d 42 64 39 37 3d fb  5c d1 d3 27 e7 c5 67 1b  |..Bd97=.\..'..g.|
    00000e80  21 61 64 5e a1 5f 6e f6  7b a1 bd 37 35 3a 3a 90  |!ad^._n.{..75::.|
    00000e90  8e 65 78 e9 4b 04 87 6f  fa be 82 63 12 5d 46 b8  |.ex.K..o...c.]F.|
    00000ea0  32 f8 10 67 f9 4b 1f 40  33 f4 b6 50 2d 76 34 bc  |2..g.K.@3..P-v4.|
    00000eb0  e3 49 ee a7 d5 84 31 4e  f3 1e 5b d8 a4 8a f5 12  |.I....1N..[.....|
    00000ec0  80 1a 4b c6 ab 16 31 48  23 ea 1b 72 c4 f6 7c 2d  |..K...1H#..r..|-|
    00000ed0  ef 7a e7 54 65 cc 19 9f  f6 7a fe d7 35 de d7 ab  |.z.Te....z..5...|
    00000ee0  94 7f 7e 5e 47 2a 19 78  95 e2 91 37 bd c9 e9 e9  |..~^G*.x...7....|
    00000ef0  9f 55 b8 00 69 c2 b3 50  ea b4 f9 48 f3 d2 78 c6  |.U..i..P...H..x.|
