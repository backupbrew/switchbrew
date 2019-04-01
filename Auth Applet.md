This is the Parental Controls authentication applet. See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

## Library Applet Versions

| System Version | Value |
| -------------- | ----- |
| \[1.0.0+\]     | 0x1   |
| \[4.0.0+\]     | 0x2   |

## Arg

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x4  | Always set to 0 by the user-process. |
| 0x4    | 0x4  | Type                                 |
| 0x8    | 0x3  | u8 arg0, arg1, arg2                  |
| 0xB    | 0x1  | Padding                              |

The arg storage is 0xC-bytes.

Types:

  - 0x0 `ShowParentalAuthentication`: With the `(bool)` func, arg0 is
    set to the input bool, with the rest set to zero. false =
    temporarily disable Parental Controls. true = validate the input
    PIN.
      - With the other func available with \[4.0.0+\], 3 u8s from the
        input struct are copied to the u8 arg fields. The
        `ShowAuthenticatorForConfiguration` wrapper func for this passes
        the following arg\* values: 1, 0, 1.
  - 0x1 `RegisterParentalPasscode`: arg\* fields are all-zero. This is
    for registering the Parental Controls PIN.
  - 0x2 `ChangeParentalPasscode`: arg\* fields are all-zero. This is for
    changing the Parental Controls PIN.

If non-Register is used where a PIN is not already registered, the
applet will throw a fatalerr once the user finishes entering the PIN
(unknown for `ShowAuthenticatorForConfiguration`).

## Usage

User-processes should push a common arguments struct as well as the
[\#Arg](#Arg "wikilink") struct. Once the applet finishes running
successfully, it will return an output 4-byte storage containing the
Result (an error is thrown if no storage is available / storage size is
0).

[Category:Library Applets](Category:Library_Applets "wikilink")
