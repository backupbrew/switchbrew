## IPC Command Structure

This is an array of
u32's.

| Word | Bits  | Description                                                  |
| ---- | ----- | ------------------------------------------------------------ |
| 0    | 15-0  | Type. 4=Request, 5=Control                                   |
| 0    | 19-16 | Number of buf X descriptors (each: 2 words).                 |
| 0    | 23-20 | Number of buf A descriptors (each: 3 words).                 |
| 0    | 27-24 | Number of buf B descriptors (each: 3 words).                 |
| 0    | 31-28 | Number of type W desciptors (each: 3 words), never observed. |
| 1    | 9-0   | Total word count (in u32's).                                 |
| 1    | 13-10 | If set to 2, enable buf C descriptor.                        |
| 1    | 31    | Enable handle descriptor.                                    |
| ...  |       | Handle descriptor, if enabled.                               |
| ...  |       | Buf X descriptors, each one 2 words.                         |
| ...  |       | Buf A descriptors, each one 3 words.                         |
| ...  |       | Buf B descriptors, each one 3 words.                         |
| ...  |       | Type W descriptors, each one 3 words.                        |
| ...  |       | Padding                                                      |
| ...  |       | Raw data                                                     |
| ...  |       | Buf C descriptors, each one 2 words.                         |

### Handle descriptor

There can only be one of this descriptor type. It is enabled by bit31 of
the second word.

| Word | Bits | Description                |
| ---- | ---- | -------------------------- |
| 0    | 0    | Send current PID.          |
| 0    | 4-1  | Number of handles to copy  |
| 0    | 8-5  | Number of handles to move? |
| ...  |      | Handles to copy            |
| ...  |      | Handles to move?           |

### Buffer descriptor A/B

This packing is so unnecessarily complex.

| Word | Bits  | Description                 |
| ---- | ----- | --------------------------- |
| 0    |       | Lower 32-bits of size.      |
| 1    |       | Lower 32-bits of address.   |
| 2    | 1-0   | Always set to 1 or 3. R/RW. |
| 2    | 4-2   | Bit 38-36 of address.       |
| 2    | 27-24 | Bit 35-32 of size.          |
| 2    | 31-28 | Bit 35-32 of address.       |

### Buffer descriptor C

| Word | Bits  | Description               |
| ---- | ----- | ------------------------- |
| 0    |       | Lower 32-bits of address. |
| 1    | 15-0  | Rest of address.          |
| 1    | 31-16 | Size                      |

### Buffer descriptor X

This one is packed even worse than A, they inserted the bit38-36 of the
address *on top* of the counter field.

| Word | Bits  | Description               |
| ---- | ----- | ------------------------- |
| 0    | 5-0   | Bits 5-0 of counter.      |
| 0    | 8-6   | Bit 38-36 of address.     |
| 0    | 11-9  | Bits 11-9 of counter.     |
| 0    | 15-12 | Bit 35-32 of address.     |
| 0    | 31-16 | Size                      |
| 1    |       | Lower 32-bits of address. |

## Raw data portion

This is an array of u64's. It's always aligned to 16 so sometimes there
is padding words before it.

| Word | Description                                       |
| ---- | ------------------------------------------------- |
| ...  | Pid is written here if enabled.                   |
| \+0  | Magic ("SFCI" for requests, "SFCO" for responses) |
| \+1  | Cmd id                                            |
| ...  | Rest of raw data.                                 |

## Official marshalling code

The official marshalling function takes an array of (buf\_ptr, size)
pairs and a type-field for each such pair.

Bitmask 0x10 seems to indicate null-terminated strings, but that flag is
ignored by the marshalling code.

| Type Mask | Description                        | Direction |
| --------- | ---------------------------------- | --------- |
| 4 + 1     | Creates an A descriptor            | In        |
| 4 + 2     | Creates a B descriptor             | Out       |
| 8 + 1     | Creates an X descriptor            |           |
| 8 + 2     | Creates a C descriptor             | Out       |
| 0x20 + 1  | Creates both an A and X descriptor |           |

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
`  u32 offset_c_descriptors;`  
`  u32 offset_raw_data;`  
`  u32 unk1;`  
`  u32 unk2;`  
`  u32 unk3;`  
`}`
