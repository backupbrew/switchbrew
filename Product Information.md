This page details miscellaneous Switch product information (serial
numbers, product models, etc...).

# Product Models

| Device                    | Product Code |
| ------------------------- | ------------ |
| Nintendo Switch           | HAC          |
| Nintendo Switch SDEV/EDEV | HAT          |
| Nintendo Switch Mariko    | HAD          |
| Nintendo Switch Lite      | HDH          |

## Product List

| Product Code | Description                                       |
| ------------ | ------------------------------------------------- |
| HAC-001      | Retail Nintendo Switch console.                   |
| HAC-002      | AC adapter.                                       |
| HAC-003      | Battery.                                          |
| HAC-004      |                                                   |
| HAC-005      |                                                   |
| HAC-006      | Joy-Con battery.                                  |
| HAC-007      | Dock.                                             |
| HAC-008      | Gamecard.                                         |
| HAC-009      | Gamecard case.                                    |
| HAC-010      | USB charging cable.                               |
| HAC-011      | Joy-Con grip.                                     |
| HAC-012      | Joy-Con charge grip.                              |
| HAC-013      | Pro Controller.                                   |
| HAC-014      | Joy-Con strap.                                    |
| HAC-015      | Left Joy-Con.                                     |
| HAC-016      | Right Joy-Con.                                    |
| HAC-017      | Joy-Con handle.                                   |
| HAC-018      | Screen protector.                                 |
| HAC-019      | Left Joy-Con extended battery.                    |
| HAC-020      | Right Joy-Con extended battery.                   |
| HAC-021      | Carrying case.                                    |
| HAC-022      |                                                   |
| HAC-023      |                                                   |
| HAC-024      | Poké Ball Plus controller.                        |
| HAC-025      |                                                   |
| HAC-026      |                                                   |
| HAC-027      |                                                   |
| HAC-028      |                                                   |
| HAC-029      |                                                   |
| HAC-030      | Poké Ball Plus battery.                           |
| HAC-031      | Charging stand.                                   |
| HAC-032      |                                                   |
| HAC-033      | Left NES controller.                              |
| HAC-034      | Right NES controller.                             |
| HAC-035      | Left Famicom controller.                          |
| HAC-036      | Right Famicom controller.                         |
| HAC-037      |                                                   |
| HAC-038      |                                                   |
| HAC-039      |                                                   |
| HAC-040      | Touch Pen.                                        |
| HAC-041      |                                                   |
| HAC-042      | SNES controller.                                  |
| HAC-043      |                                                   |
| HAC-044      |                                                   |
| HAC-045      |                                                   |
| HAC-046      |                                                   |
| HAC-047      |                                                   |
| HAC-048      |                                                   |
| HAC-049      |                                                   |
| HAC-050      |                                                   |
| HAC-051      | Nintendo Labo Toy-Con 1: Variety Kit.             |
| HAC-052      | Nintendo Labo Toy-Con 2: Robot Kit. (To confirm.) |
| HAC-053      | Nintendo Labo Toy-Con 3: Vehicle Kit.             |
| HAC-054      | Nintendo Labo Toy-Con 4: VR Kit.                  |

| Product Code | Description                   |
| ------------ | ----------------------------- |
| HAT-001      | SDEV Nintendo Switch console. |
| HAT-002      | EDEV Nintendo Switch console. |
| HAT-003      | SDEV cradle.                  |
| HAT-004      | Relay Box.                    |

| Product Code       | Description                            |
| ------------------ | -------------------------------------- |
| HAC-001-01/HAD-001 | Retail Nintendo Switch Mariko console. |

| Product Code | Description                          |
| ------------ | ------------------------------------ |
| HDH-001      | Retail Nintendo Switch Lite console. |
| HDH-002      | HDEV Nintendo Switch console.        |

# Product Serial Numbers

## Console

A Switch console serial number is composed of at least [three
letters](#Prefix "wikilink") followed by ten decimal digits. The tenth
digit is a [check digit](#Check_Digit "wikilink"), meaning that it is
derived from the other digits.

### Prefix

Observed prefixes are normally:

  - First letter represents the product line: "X" (NX).
  - Second letter represents the product model: "A" (Old/HAC-001), "J"
    (Lite/HDH-001) or "K" (New/HAC-001-01).
  - Third letter represents the product region: "W" (North America), "J"
    (Japan; and Europe on old models), "E" (Europe) or "K" (Korea).
  - Fourth letter is optional: "F" (factory).

### Check Digit

The check digit is an industry-standard algorithm and is calculated just
like it was on the
[3DS](https://www.3dbrew.org/wiki/Serials#Console_Serial_Numbers).

To calculate the check digit of a Switch console, separate the non-check
digits into "odd" and "even" groups, where the "odd" group is digits in
odd-numbered positions, and the "even" group is digits in even-numbered
positions. (The first digit is "odd", with "first" representing "1".)

After separating the digits, add the digits in each group together.
Multiply the sum of the even digits by 3, then add the sum of the odd
digits. To calculate the check digit, take this value modulo 10, and if
not 0, subtract from 10.

Example: XAW10075273452

The non-check digits are 1007527345. Separating into odd and even
groups, we get the following:

Odds: 1 + 0 + 5 + 7 + 4 = 17 Evens: 0 + 7 + 2 + 3 + 5 = 17

Applying the algorithm, we get ((3 \* 17) + 17) % 10 = 8, which is not
0, thus 10 - 8 = 2, matching the example's check digit.
