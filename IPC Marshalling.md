## Marshall Portion

This is an array of u32's.

| Word | Description          |
| ---- | -------------------- |
| 0    | Cmd header part 1    |
| 1    | Cmd header part 2    |
| ...  | Marshall descriptors |

### Marshall type A

| Word | Description            |
| ---- | ---------------------- |
| 0    | Word1 is written here. |
| 1    | Word0 is written here. |
| 2    | Weird mix.             |

### Marshall type B

| Word | Description                                     |
| ---- | ----------------------------------------------- |
| 0    | Lower 32-bits of addr?                          |
| 1    | Upper 16bits: Size, Lower 16bits: Rest of addr? |

### Marshall type C

| Word | Description                     |
| ---- | ------------------------------- |
| 0    | Upper 16bits: Size, Lower 16: ? |
| 1    | ?                               |

## Data Portion

This is an array of u64's placed after the marshall header. But it's
always aligned to 16 so sometimes there is padding words inserted
inbetween.

| Word | Description                        |
| ---- | ---------------------------------- |
| 0    | Magic ("SFCI")                     |
| 1    | Cmd id                             |
| ...  | Non-marshalled data is placed here |

## Cmd header

| Cmd header 1 | Cmd header 2 | Description                                    |
| ------------ | ------------ | ---------------------------------------------- |
| 4            | 9            | Data portion size 20.                          |
| 4            | 10           | Data portion size 24.                          |
| 4            | 12           | Data portion size 32.                          |
| 4            | 14           | Data portion size 40.                          |
| 4            | 0x8000000C   | Marshall words: (u32) 1. Data portion size 32. |
