# LilyNixie

**LilyNixie** is a small Nixie tube clock housed under a glass dome, in the spirit of the classic glass-dome anniversary clocks with a rotating (torsion) pendulum. Four miniature Nixie tubes show the time, while the electronics sit inside a turned wooden base.

> **Project status:** work in progress. The hardware, schematics and firmware are still being designed. Details in this README may change as the design develops.

## Features

- Four **ITT 5870L** miniature Nixie tubes showing hours and minutes (HH:MM)
- One **SN74141** Nixie driver IC, with the tubes driven in **multiplex mode**
- **Arduino LilyPad** microcontroller board
- **RTC (real-time clock) module** that keeps time when the clock is unplugged
- Custom Nixie driver and high-voltage board designed for this project
- Powered from **5 V USB**
- Time set with **push buttons**
- Fits under a **65 mm × 150 mm glass dome** with a wooden base

### Not included

To keep the clock simple, the following are **currently not planned**:

- alarm function
- DCF77 radio time signal
- GPS time synchronisation
- Wi-Fi or internet time server (NTP) connection

## How it works

### Display and multiplexing

The four Nixie tubes share a single SN74141 BCD-to-decimal driver. All tubes have their matching cathodes (digits 0–9) connected in parallel to the driver outputs, and each tube has its own anode switch.

The microcontroller lights the tubes one at a time:

1. switch off all anodes;
2. send the BCD code of the next digit to the SN74141;
3. switch on the anode of the corresponding tube;
4. wait for a short time, then move to the next tube.

When this cycle is repeated fast enough, the eye sees all four digits lit at once. Multiplexing reduces the number of driver ICs and microcontroller pins needed, which matters in the small space under the dome.

### Power supply

The clock runs from a 5 V USB supply. Nixie tubes need a much higher DC voltage to strike and stay lit (typically around 170 V for this tube family), so the driver board will include a **step-up (boost) converter** that generates the anode voltage from 5 V.

### Timekeeping

The RTC module keeps the time and continues running from its backup battery when USB power is removed. The LilyPad reads the time from the RTC and refreshes the display.

### Setting the time

The time is set with push buttons. The exact button layout and operating sequence will be documented with the firmware.

## Hardware overview

| Part | Description |
|---|---|
| Nixie tubes | 4 × ITT 5870L miniature Nixie tubes |
| Nixie driver | 1 × SN74141 BCD-to-decimal Nixie driver |
| Anode switches | High-voltage transistors, one per tube (to be specified) |
| Microcontroller | Arduino LilyPad |
| Real-time clock | RTC module with backup battery (to be specified) |
| High-voltage supply | 5 V to Nixie anode voltage boost converter |
| Controls | Push buttons for setting the time |
| Power input | 5 V USB |
| Enclosure | 65 mm × 150 mm glass dome with 70 mm wooden base |

The SN74141 has been out of production for decades. New old stock parts are still available from specialist sellers, and the Soviet **K155ID1** is a commonly used functional equivalent. Check the pinout and datasheet of any substitute before use.

## ⚠️ High-voltage warning

Although the clock is powered from 5 V USB, **the driver board generates around 170 V DC** for the Nixie tubes. This voltage can give a painful or dangerous electric shock, and the boost converter's capacitor can stay charged after the power is removed.

- Do not touch the high-voltage board while it is powered.
- Disconnect USB and allow the capacitors to discharge before working on the circuit.
- Build and test the high-voltage section only if you are experienced with such circuits.

## Sourcing the glass dome

The glass dome used for the LilyNixie Nixie clock is sold as a decorative **glass dome with a wooden base**. Look for it in craft shops, florist supply stores and home decoration shops.

### Product identification

The packaging of the dome purchased for this project carries the following details:

| Item | Identification |
|---|---|
| Brand | Decorolla |
| Product code | CRL8478; also listed as 8478 or KB-8478 |
| EAN / barcode | 5998997720146 |
| Hungarian product name | Üvegbúra fa talppal 6,5 × 15 cm |

Retailers specify these nominal dimensions:

| Part | Dimensions |
|---|---|
| Glass dome | 65 mm diameter × 150 mm high |
| Wooden base | 70 mm diameter × 8 mm thick |
| Overall height with base | 158 mm |

These are retail dimensions. The **internal diameter, usable internal height and manufacturing tolerances are not specified**, so check the actual dome against your clock assembly before finalising the enclosure.

### Buying in Hungary

The following Hungarian shops list the matching product:

| Supplier | Product reference | Listed price |
|---|---|---:|
| [Kosárbolt](https://www.kosarbolt.hu/uvegbura_fa_talppal_6515cm) | 8478 | HUF 1,357 |
| [Bloomi](https://bloomi.hu/Uvegbura-fa-talppal-6515cm) | KB-8478; matching EAN | HUF 1,850 |

*Prices include VAT and were checked on 11 November 2026; delivery is additional and prices or stock may change.*

Kosárbolt lists delivery from HUF 1,090, bringing a single dome to **HUF 2,447 delivered**. For a single build, a local craft shop may therefore be cheaper overall, even with a slightly higher shelf price. Search for **“üvegbúra fa talppal 6,5×15 cm”** or use the product code or barcode above.

At Bloomi, check the final delivery charge at checkout: the product page displays conflicting information about free collection-point delivery.

### Buying outside Hungary

First try searching for **Decorolla CRL8478**, **8478 glass dome**, or **5998997720146**. International delivery from the Hungarian shops has not been verified; ask the retailer whether they ship to your country and request a total price.

If the exact product is unavailable, try local craft and florist suppliers or marketplaces such as Amazon, eBay, Etsy and AliExpress. Useful search terms include:

- **glass display dome with wooden base 65 mm × 150 mm**
- **glass cloche 6.5 × 15 cm**
- **mini bell jar wooden base**
- German: **Glasglocke mit Holzsockel 6,5 × 15 cm**

These are search suggestions, not confirmed compatible listings.

Before ordering an alternative, ask for the dome’s **internal opening diameter, usable internal height, external rim diameter and base dimensions**. Check whether the advertised height includes the wooden base. Allow space around the assembled clock, including the curved top of the dome.

A differently sized dome may require changes to the clock base or mounting arrangement. Buy and measure the dome before making the final base.

## Repository contents

The repository will be filled in as the project progresses. Planned contents:

- `hardware/` – schematics and PCB design of the Nixie driver and high-voltage board
- `firmware/` – Arduino sketch for the LilyPad
- `mechanical/` – base and mounting drawings for the glass dome
- `docs/` – photos, datasheets and build notes

## License

This project is licensed under the **GNU General Public License v3.0**. See the [LICENSE](LICENSE) file for details.
