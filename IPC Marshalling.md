## IPC Command Structure

This is an array of u32's, usually located in [Thread Local
Storage](Thread%20Local%20Storage.md "wikilink").

| Word | Bits  | Description                                                                                                 |
| ---- | ----- | ----------------------------------------------------------------------------------------------------------- |
| 0    | 15-0  | Type. 4=Request, 5=Control                                                                                  |
| 0    | 19-16 | Number of buf X descriptors (each: 2 words).                                                                |
| 0    | 23-20 | Number of buf A descriptors (each: 3 words).                                                                |
| 0    | 27-24 | Number of buf B descriptors (each: 3 words).                                                                |
| 0    | 31-28 | Number of buf W desciptors (each: 3 words), never observed.                                                 |
| 1    | 9-0   | Size of raw data section in u32s.                                                                           |
| 1    | 13-10 | Flags for buf C descriptor.                                                                                 |
| 1    | 30-20 | ?                                                                                                           |
| 1    | 31    | Enable handle descriptor.                                                                                   |
| ...  |       | [Handle descriptor](#Handle_descriptor "wikilink"), if enabled.                                             |
| ...  |       | [Buf X descriptors](#Buffer_descriptor_X_"Pointer" "wikilink"), each one 2 words.                           |
| ...  |       | [Buf A descriptors](#Buffer_descriptor_A/B/W_"Send"/"Receive"/"Exchange" "wikilink"), each one 3 words.     |
| ...  |       | [Buf B descriptors](#Buffer_descriptor_A/B/W_"Send"/"Receive"/"Exchange" "wikilink"), each one 3 words.     |
| ...  |       | [Type W descriptors](#Buffer_descriptor_A/B/W_"Send"/"Receive"/"Exchange" "wikilink"), each one 3 words.    |
| ...  |       | [Raw data section](#Raw_data_section "wikilink") (including padding before and after aligned data section). |
| ...  |       | [Buf C descriptors](#Buffer_descriptor_C_"ReceiveList" "wikilink"), each one 2 words.                       |

First two header u32's and handle descriptor (if enabled) are copied
as-is from one process to the other.

### Handle descriptor

There can only be one of this descriptor type. It is enabled by bit31 of
the second word.

| Word | Bits | Description               |
| ---- | ---- | ------------------------- |
| 0    | 0    | Send current PID.         |
| 0    | 4-1  | Number of handles to copy |
| 0    | 8-5  | Number of handles to move |
| ...  |      | 8-byte PID if enabled     |
| ...  |      | Handles to copy           |
| ...  |      | Handles to move           |

Sysmodules load the last u64 of rawdata when handling the PID. This is
not written by kernel. For sysmodule handling:

  - In some cases: these commands require a placeholder u64 value passed
    in the input parameters, as mentioned above. In these cases the
    OverwriteClientProcessId method is called to replace the value
    before it is used.
  - In other cases: The rawdata\_u64 is compared with the PID from the
    descriptor. On mismatch and when rawdata\_u64\!=0, error 0x60A is
    returned. The PID value passed to the cmdhandler vtable funcptr is
    the rawdata\_u64.

Handle 0 is allowed, and just means no handle was sent.

### Buffer descriptor X "Pointer"

This one is packed even worse than A, they inserted the bit38-36 of the
address *on top* of the counter field.

Officially, the counter is known as "receive index". This one writes to
the buffer described in the ReceiveList.

| Word | Bits  | Description               |
| ---- | ----- | ------------------------- |
| 0    | 5-0   | Bits 5-0 of counter.      |
| 0    | 8-6   | Bit 38-36 of address.     |
| 0    | 11-9  | Bits 11-9 of counter.     |
| 0    | 15-12 | Bit 35-32 of address.     |
| 0    | 31-16 | Size                      |
| 1    |       | Lower 32-bits of address. |

### Buffer descriptor A/B/W "Send"/"Receive"/"Exchange"

This packing is so unnecessarily complex.

| Word | Bits  | Description                     |
| ---- | ----- | ------------------------------- |
| 0    |       | Lower 32-bits of size.          |
| 1    |       | Lower 32-bits of address.       |
| 2    | 1-0   | Flags. Always set to 0, 1 or 3. |
| 2    | 4-2   | Bit 38-36 of address.           |
| 2    | 27-24 | Bit 35-32 of size.              |
| 2    | 31-28 | Bit 35-32 of address.           |

A reply must not use A/B/W, svcReplyAndReceive will return 0xE801.

[MemoryAttribute](SVC.md "wikilink") IsBorrowed and IsUncached are never
allowed for the source address.

"Send" means buffer is sent from source process into service process.

"Receive" means that data is copied from service process into user
process.

"Exchange" means both "Send" and "Receive".

#### Flags

Determines what [MemoryState](SVC.md "wikilink") to use with the mapped
memory in the sysmodule.

Used to enforce whether or not device mapping is allowed for src and dst
buffers respectively.

  - Flag0: Device mapping \*not\* allowed for src or dst.
  - Flag1: Device mapping allowed for src and dst.
  - Flag3: Device mapping allowed for src but not for dst.

### Buffer descriptor C "ReceiveList"

There's a 4-bit flag in the main header controlling the behavior of C
descriptors.

If it has value 0, the C descriptor functionality is disabled.

If it has value 1, there is an "inlined" C buffer after the raw data.
Received data is copied to ROUND\_UP(cmdbuf+raw\_size+index, 16)

If it has value 2, there is a single C descriptor.

Otherwise it has (flag-2) C descriptors. In this case, index picks which
C descriptor to copy received data to \[instead of picking the offset
into the buffer\].

Data sent with this method must have MemoryState 0x4000000 mask set.

After reply, X descriptors are written to the sender containing the
address, size and index that were copied to.

| Word | Bits  | Description               |
| ---- | ----- | ------------------------- |
| 0    |       | Lower 32-bits of address. |
| 1    | 15-0  | Rest of address.          |
| 1    | 31-16 | Size                      |

### IPC buffers

Buffer descriptor A/B/... map memory into the sysmodule process. For the
mapped memory in the sysmodule the permissions are: desc-A = R--, desc-B
= RW-. The buffer is automatically unmapped while the kernel handles the
cmdreply, the sysmodule doesn't need to specify anything in the cmdreply
to trigger this.

This memory is mapped in the sysmodule to the same vaddr from the
original user-process cmd-request, except with with bits \>=(~28(?))
changed to a different ASLR'd region.

No user-process-\>sysmodule memcpy is done for outbufs, only
sysmodule-\>user-process.

## Raw data section

![An example of an IPC message with a type 0xA buffer in it. Red is
headers/descriptors, yellow is padding, and blue is data/buffer lengths.
Note that the size of the u16 array for type A lengths is padded to fill
up a whole word.](Ipc_msg_buffer_type_a_example.png
"An example of an IPC message with a type 0xA buffer in it. Red is headers/descriptors, yellow is padding, and blue is data/buffer lengths. Note that the size of the u16 array for type A lengths is padded to fill up a whole word.")

| Word | Description                                                                                                                       |
| ---- | --------------------------------------------------------------------------------------------------------------------------------- |
| ...  | Padding to align to 16 bytes.                                                                                                     |
| ...  | If sent to an object domain, a [domain message](#Domain_message "wikilink"), otherwise a [data payload](#Data_payload "wikilink") |
| ...  | Padding                                                                                                                           |
| ...  | Buffer type 0xA lengths (u16 array)                                                                                               |

The total amount of padding within the raw data section is always 0x10
bytes. This means that if no padding is required before the message,
there will be 0x10 bytes of padding after the message (before the buffer
type 0xA lengths).

### Domain message

This header is used to wrap up requests sent to domains instead of
sessions.

| Word | Bits  | Description                                                                                      |
| ---- | ----- | ------------------------------------------------------------------------------------------------ |
| 0    | 7-0   | Command. 1=send message, 2=close virtual handle                                                  |
| 0    | 31-16 | Length of [data payload](IPC%20Marshalling#Data%20payload.md##Data_payload "wikilink") in bytes. |
| 1    |       | Object ID (from cmd 0 in [Control](IPC%20Marshalling#Control.md##Control "wikilink")).           |
| 2    |       | Padding to align to u64                                                                          |
| 3    |       |                                                                                                  |
| 4... |       | [Data payload](#Data_payload "wikilink")                                                         |

### Data payload

This is an array of u32's, but individual parameters are generally
stored as
u64's.

| Word | Description                                                                                     |
| ---- | ----------------------------------------------------------------------------------------------- |
| 0    | Magic ("SFCI" for requests, "SFCO" for responses) as u64.                                       |
| 2    | Command id as u64 for requests, [error code](Error%20codes.md "wikilink") as u64 for responses. |
| 4... | Input parameters or return values                                                               |

## Official marshalling code

The official marshalling function takes an array of (buf\_ptr, size)
pairs and a type-field for each such pair.

Bitmask 0x10 seems to indicate null-terminated strings, but that flag is
ignored by the marshalling
code.

| Type Mask    | Description                                                                 | Direction |
| ------------ | --------------------------------------------------------------------------- | --------- |
| 4 + 1        | Creates a A descriptor with flags=0.                                        | In        |
| 0x40 + 4 + 1 | Creates a A descriptor with flags=1.                                        | In        |
| 0x80 + 4 + 1 | Creates a A descriptor with flags=3.                                        | In        |
| 4 + 2        | Creates a B descriptor with flags=0.                                        | Out       |
| 0x40 + 4 + 2 | Creates a B descriptor with flags=1.                                        | Out       |
| 0x80 + 4 + 2 | Creates a B descriptor with flags=3.                                        | Out       |
| 8 + 1        | Creates an X descriptor                                                     | In        |
| 8 + 2        | Creates a C descriptor, and writes the u16 size to an offset into raw data. | Out       |
| 0x10 + 8 + 2 | Creates a C descriptor                                                      | Out       |
| 0x20 + 1     | Creates both an A and X descriptor                                          | In        |
| 0x20 + 2     | Creates both an B and C descriptor                                          | Out       |

C and X (Pointer and ReceiveList) descriptors are backed by the "pointer
buffer", a buffer in the service process. Its size is a u16, which is
retrieved using the "QueryPointerBufferSize" control message. If the
client code determines all buffers with flag 8 do not fit in the pointer
buffer, it returns error 0x11A0B.

For buffers with flag 0x20 it creates two descriptors (A+X or B+C), but
one descriptor is NULL (zero size and pointer), while the other holds
the expected values. X/C descriptors are used as the non-NULL descriptor
where possible, but if they don't fit in the pointer buffer, A/B
descriptors are used instead. The code defers processing of type 0x20
buffers with sizes that fit in a u16 (and may therefore fit in the
pointer buffer). This ensures all type 8 buffers get pointer-buffer
space before any type 0x20.

(The order in which the deferred type 0x20 buffers are processed is
determined by a convoluted loop.)

## Official IPC Cmd Structure

Official struct that is stored for each IPC command. It contains
precalculated offsets for different portions of the command structure.

All offsets are given is in number of u32 words.

`struct IpcCmdStruct {`  
`  u8  unk0;`  
`  u8  has_handle_descriptor;`  
`  u8  pad0[2];`  
`  u32 cmd0;`  
`  u32 cmd1;`  
`  u32 offset_handle_descriptor;`  
`  u32 pad1;`  
`  u32 offset_handles;          `  
`  u32 pad2;`  
`  u32 offset_x_descriptors;`  
`  u32 offset_a_descriptors;`  
`  u32 offset_b_descriptors;`  
`  u32 offset_w_descriptors; /* this is a guess */`  
`  u32 offset_raw_data;`  
`  u32 offset_c_descriptors;`  
`  u32 unk2;`  
`  u32 unk3;`  
`}`

## Control

When type == 5 you are talking to the IPC manager. These are processed
by the sysmodule.

| Cmd | Name                   | Arguments   | Output          |
| --- | ---------------------- | ----------- | --------------- |
| 0   | ConvertSessionToDomain | None        |                 |
| 1   | ConvertDomainToSession | u32 domain  |                 |
| 2   | DuplicateSession       | None        |                 |
| 3   | QueryPointerBufferSize | None        | u32 as u16-size |
| 4   | DuplicateSessionEx     | u32 unknown |                 |
