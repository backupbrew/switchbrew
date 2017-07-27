The Nintendo Switch's bootloader (called "package1") is the first custom
piece of code running on the Switch. It is loaded in the IRAM and
launched by the Tegra X1 bootROM according to the BCT. It runs on the
boot processor, an ARM7TDMI called "BPMP" by NVidia (Boot and Power
Management Processor). It is split into two parts, one that is in
plaintext, one that is encrypted. The bootROM does not perform any
symmetric cryptographic operations on the bootloader it loads.

## Stage 1

The first stage of the bootloader is the plaintext part of the
bootloader. It has four goals: to power on devices, to look for
incoherencies, to generate keys, and to decrypt and launch the second
stage. The stage 1 bootloader's authors knew that the code was in
plaintext, and thus took extra care to try to protect the bootloader
from side-channel attacks.

### Execution flow

#### Startup

After setting up the stack and branching to main, stage 1 poisons all
the exception vectors to point at the panic function. It then clears the
(empty) bss and calls the functions in the (empty) init array.

#### Main

  - Registers are setup
  - A device (?) is powered on
  - Flags are set on the clock-reset registers
  - \[3.0.0+\] The security engine address is setup
  - \[3.0.0+\] Bit30 of offset 0x800 of the security engine is checked:
    if set, panic.
  - The SKU info is checked. If it doesn't match 0x83, panic.
  - Fuse coherency is checked, potentially panicking.
  - The copy of the BCT left by the bootROM is checked. If the version
    field doesn't match the expected version field, panic.
  - Anti-downgrade fuses are checked, potentially panicking.
  - \[1.0.0-2.3.0\] Fuse programming is disabled until next reboot.
  - The memory controller is powered on and setup to allow GPU DMA to
    the IRAM. This will be needed to interact with the Falcon and with
    the security engine.
  - \[1.0.0-2.3.0\] The security engine address is setup
  - \[1.0.0-2.3.0\] Bit30 of offset 0x800 of the security engine is
    checked: if set, panic.
  - Key generation is performed. If the unit type is equal to 0
    (non-retail) AND if some fuse is clear, the secondary method will be
    used. Else, the main method will be used.
  - Stage 2 is decrypted with keyslot 0xB. Keyslot 0xB is cleared, and
    the second stage's header validity is checked. If any of this fails,
    panic.
  - The entrypoint of stage 2 is computed.
  - The stack is pivoted to a secondary stack, the main stack and the
    key area are cleared, and stage 1 jumps to stage 2's entrypoint.

#### Fuse coherency

Unit type is computed from data from a fuse. It must be either 0
(non-retail) or 1 (retail). If it's neither, 2 will be returned by the
function, and the check will call panic.

#### Downgrade check

The bootloader will check if someone attempted to downgrade it. A fuse
array will be checked, if too many fuses are burnt the bootloader will
panic. If too little are set, the bootloader will program the expected
bitmap and force a reset. The fuse array and the expected number of
burnt fuses is different on unit type 0 (non-retail) and unit type 1
(retail).

| System version | Expected number of burnt fuses (retail) | Expected number of burnt fuses (non-retail) |
| -------------- | --------------------------------------- | ------------------------------------------- |
| 1.0.0          | 1                                       | 0                                           |
| 2.0.0-2.3.0    | 2                                       | 0                                           |
| 3.0.0          | 3                                       | 1                                           |

#### Panic

The panic function does the following things:

  - It clears the stack
  - It disables(?) and clears the security engine
  - It disables fuse programming
  - It clears the key area
  - It clears the data for stage 2
  - It signals over the debug interface that a panic occurred until the
    Switch is reset.

### Key generation

For more detail on the Switch's Cryptosystem, please see [this
page](Cryptosystem.md "wikilink").

In all cases, at the end of the key generation function three keys are
generated: the stage 2 key (stored in keyslot 0xB), the master static
key (stored in keyslot 0xC), and the master device key (stored in
keyslot 0xD). The two keys initialized by the bootROM (the SBK, stored
in keyslot 0xE, and the SSK, stored in keyslot 0xF) are cleared
immediately after the bootloader is finished using them. Keyslots 0xC
and 0xD are marked unreadable. Keyslot 0xB is not, but is is cleared by
stage 1 after stage 2's decryption anyway.

#### Main method

This method is called when the unit type is equal to 1 (retail) OR when
unit type is equal to 0 and some fuse is set.

The master static seed selected depends on whether the unit type is zero
and whether the last byte of the bootloader's RSA modulus is 0x4F.

  - Falcon microcode is loaded, the device keyblob seed generation key
    is obtained from the Falcon.
  - The device keyblob seed generation key is stored in keyslot 0xD.
  - \[3.0.0+\] keyblob key seed 1 is generated by decrypting the keyblob
    seed constant 1 with the device keyblob seed generation key
  - \[3.0.0+\] keyblob key 1 is generated by decrypting keyblob key seed
    1 with the SBK. The result is directly stored in keyslot 0xA without
    leaving the crypto engine.
  - keyblob key seed N is generated by decrypting the keyblob seed
    constant N with the device keyblob seed generation key
  - keyblob key N is generated by decrypting keyblob key seed N with the
    SBK. The result is directly stored in keyslot 0xD without leaving
    the crypto engine.
  - The SBK and the SSK are cleared.
  - The constant MAC key generator block is decrypted with keyblob key N
    to generate keyblob MAC key N. The result is directly stored in
    keyslot 0xB without leaving the crypto engine.
  - With keyblob MAC key N, AES CMAC is performed over the keyblob.
  - With a comparison function which is safe against timing attacks, the
    CMAC is compared with the stored CMAC. If they differ, panic is
    called.
  - The keyblob data is decrypted with AES-CTR, using the keyblob key N
    and the stored CTR.
  - The stage 2 decryption key (the ninth key in the blob) is loaded in
    keyslot 0xB.
  - The master static key encryption key. is loaded in keyslot 0xC.
  - The decrypted keyblob data is erased.
  - The master static key is generated by decrypting the master static
    seed with the master static key encryption key. The result is
    directly stored in keyslot 0xC without leaving the crypto engine.
  - \[1.0.0-2.3.0\] The master device key is generated by decrypting a
    constant block with keyslot 0xD (which contains keyblob N's key 1).
    The result is directly stored in keyslot 0xD without leaving the
    crypto engine.
  - \[3.0.0+\] The master device key is generated by decrypting a
    constant block with keyslot 0xA (which contains keyblob 1's key 1).
    The result is directly stored in keyslot 0xD without leaving the
    crypto engine.
  - \[3.0.0+\] Keyslot 0xA is cleared.

#### Secondary method

The secondary method (which is never launched on retail units) is very
simple. First a master static seed is selected (depending on whether the
bootloader's RSA modulus ends with 0x11). Then, a constant block is
decrypted by the SBK. The result is the stage 2 key and will be stored
in keyslot 0xB. A constant block will be decrypted by the SBK and
temporarily stored in keyslot 0xC. Another constant block will be
decrypted by the SSK and temporarily stored in keyslot 0xD. Both the SBK
and the SSK are cleared. The master static seed is decrypted with
keyslot 0xC and stored in keyslot 0xC. A constant block is decrypted
with keyslot 0xD and stored in keyslot 0xD.

## Stage 2 (package1.1)

The second stage of the bootloader is the encrypted part of the
bootloader. It is much bigger than stage 1, but what it does is
currently unknown due to its being encrypted.

### Header format

| Offset | Size | Description              |
| ------ | ---- | ------------------------ |
| 0x0    | 4    | Magic "PK11"             |
| 0x4    | 4    | Size of section 3        |
| 0x8    | 8    | Unknown                  |
| 0x10   | 4    | Size of section 2        |
| 0x14   | 4    | Entrypoint of section 2  |
| 0x18   | 4    | Size of section 1        |
| 0x1C   | 4    | Entrypoint of section 1? |

Entrypoints are relative to the section. Stage 1 jumps to the entrypoint
of section 2.
